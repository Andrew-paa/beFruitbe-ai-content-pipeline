# n8n Automation Prototype

[English version](README.md)

## Описание

В рамках проекта **beFruitbe AI Content Pipeline** я спроектировал в n8n модульную архитектуру для автоматизации полного цикла производства AI-контента.

Основной компонент — `BF_00_DAILY_ORCHESTRATOR`.

Он отвечает за:

- получение задач;
- валидацию входных данных;
- работу с центральной базой Google Sheets;
- защиту от повторных запусков;
- сбор брендового контекста;
- разделение публичных и внутренних данных;
- запуск последующих AI-модулей;
- журналирование статусов выполнения.

Основной оркестратор был реализован и тестировался на реальных данных Google Sheets.

Полный end-to-end pipeline с генерацией изображений, видео, QA и аналитикой до production-версии доведён не был.

---

## Основной оркестратор

`BF_00_DAILY_ORCHESTRATOR`

**37 n8n nodes**

Оркестратор поддерживал два способа запуска:

```text
Automatic Schedule
каждый день в 06:00 Europe/Moscow

или

Manual Webhook
запуск конкретной задачи по Task_ID
```

---

## Центральная база данных

Оркестратор получал контекст из центральной Google Sheets базы.

Он работал с отдельными разделами данных:

```text
Daily Tasks
Runs Log
Brands
SKUs
Claims
Audiences
Media Library
Previous Content
Messages
Knowledge
```

Таким образом, данные о продукте, аудитории, claims, media assets и предыдущем контенте не хранились непосредственно внутри workflow.

n8n получал необходимый контекст из структурированной базы.

---

## Валидация задач

Перед запуском AI-этапов оркестратор проверял наличие обязательных параметров:

```text
Task_ID
Task_Date
Brand_ID
SKU_ID
Content_Type
```

Для автоматического запуска выбирались задачи:

```text
Task_Date = today
+
Task_Status = READY
```

Если обязательных данных не хватало:

```text
PROCESS → запрещён
HOLD → записывается в журнал
```

В Runs Log сохранялась информация о причине остановки.

---

## Защита от повторного запуска

Я добавил отдельную deduplication-логику.

Из данных задачи формировался `Input_Hash`.

Затем система проверяла:

```text
Task_ID
+
Input_Hash
```

по истории запусков.

Если такая версия задачи уже обрабатывалась:

```text
DUPLICATE
    ↓
DUPLICATE_SKIPPED
```

Новый запуск не создавался.

Если задача новая:

```text
NEW
 ↓
Generate Run_ID
 ↓
RUN_STARTED
```

---

## Run Logging

Для каждого выполнения формировался уникальный `Run_ID`.

В отдельном Runs Log сохранялись статусы, включая:

```text
RUN_STARTED
HOLD
DUPLICATE_SKIPPED
```

Это позволяло отслеживать историю выполнения задач и причины остановки pipeline.

---

## Knowledge Filtering

Перед передачей данных AI система отдельно фильтровала Knowledge.

Например, Knowledge record должен был соответствовать требованиям:

```text
Status = APPROVED
Approved_for_Knowledge = YES
Readiness = READY
Confidentiality != CONFIDENTIAL
```

Похожая проверка выполнялась для сообщений и других элементов Knowledge Base.

Таким образом, наличие информации в таблице ещё не означало автоматического разрешения использовать её в AI.

---

## Internal и Public Context

Одной из ключевых архитектурных идей стало разделение данных на два контекста.

### INTERNAL_BRAND_CONTEXT

Внутренний контекст мог содержать:

```text
Brand Data
Messages
Knowledge
SKU
Allowed Claims
Forbidden Claims
Audience
Media Assets
Previous Content
```

Этот контекст предназначался для внутренних этапов системы и сценариста.

### PUBLIC_RESEARCH_BRIEF

Для внешнего research-агента создавался отдельный очищенный context.

Из него исключались потенциально закрытые данные, например:

```text
внутренние цены;
себестоимость и margin;
данные поставщиков;
персональные данные;
email и phone;
rights documents;
API keys / secrets;
неопубликованные промо-данные;
confidential fields.
```

Кроме того, материал должен был иметь подходящий статус и права использования.

---

## Почему research был отделён

Research Agent должен был смотреть на задачу **снаружи**:

```text
PUBLIC_RESEARCH_BRIEF
        ↓
External Research
        ↓
Trends / Audience Context / Public Information
```

При этом он не должен был получать внутреннюю базу компании.

После завершения research результаты снова объединялись с:

```text
INTERNAL_BRAND_CONTEXT
```

и только затем передавались сценаристу.

Это позволяло сочетать:

```text
Внешний взгляд
+
Закрытая брендовая база
```

не раскрывая внутренние данные внешнему research-этапу.

---

## Модульная архитектура

Полный pipeline был разбит на независимые workflow.

| Workflow | Назначение | Статус |
|---|---|---|
| `BF_00_DAILY_ORCHESTRATOR` | Оркестрация, данные, validation, deduplication, logging и routing | **Implemented prototype / tested** |
| `BF_01_RESEARCH_GEMINI` | Внешний research | Interface / skeleton |
| `BF_02_SCRIPT_OPENAI` | Сценарий и prompt engineering | Interface / skeleton |
| `BF_03_IMAGE_GENERATION` | Генерация визуальных материалов | Interface / skeleton |
| `BF_04_VEO_VIDEO_GENERATION_AND_ASSEMBLY` | Видеогенерация и сборка | Interface / skeleton |
| `BF_05_FINAL_GEMINI_QA` | Финальная AI-проверка | Interface / skeleton |
| `BF_06_ANALYTICS` | Аналитика опубликованного контента | Interface / skeleton |

Также в оркестраторе была предусмотрена точка передачи ошибок в отдельный `BF_99_ERROR_HANDLER`, однако отдельный workflow этого обработчика в сохранившийся экспорт не вошёл.

---

## Планируемый pipeline

```text
Daily Task
    ↓
Validation
    ↓
Deduplication
    ↓
Run Logging
    ↓
Knowledge Retrieval
    ↓
Context Filtering
    ↓
┌───────────────────────────────┐
│ PUBLIC_RESEARCH_BRIEF         │
│             ↓                 │
│        Research Agent         │
└───────────────────────────────┘
              +
┌───────────────────────────────┐
│ INTERNAL_BRAND_CONTEXT        │
└───────────────────────────────┘
              ↓
      Script & Prompt Agent
              ↓
       Image Generation
              ↓
       Video Generation
              ↓
            QA
              ↓
         Analytics
```

---

## Реализованный и планируемый scope

Важно разделять архитектуру и фактическую реализацию.

### Реально реализовано и протестировано

Основной orchestrator:

```text
Google Sheets
→ task selection
→ validation
→ deduplication
→ Run_ID
→ logging
→ Knowledge retrieval
→ filtering
→ internal/public context separation
→ downstream workflow routing
```

### Подготовлено как следующая стадия

В export были созданы отдельные workflow interfaces для:

```text
Research
Script Generation
Image Generation
Video Generation
QA
Analytics
```

На момент остановки проекта их внутренняя автоматизация ещё не была завершена.

---

## Что дал мне этот этап

Работа с n8n стала для меня практическим опытом проектирования automation workflow между несколькими системами.

Я работал с:

- Google Sheets nodes;
- Schedule Trigger;
- Webhook;
- Switch / IF / Filter;
- Execute Workflow;
- Merge;
- Set;
- JavaScript Code nodes;
- task validation;
- deduplication;
- run logging;
- context filtering;
- modular workflow architecture.

Главный вывод: автоматизация AI-системы — это не только вызов модели.

Большая часть надёжности находится вокруг неё:

```text
какие данные взять
→ можно ли их использовать
→ какую задачу запускать
→ запускалась ли она раньше
→ что передать внешней модели
→ что оставить внутри системы
→ что делать при ошибке
→ как сохранить статус выполнения
```

---

## Project Status

**Status: implemented orchestration prototype / incomplete end-to-end pipeline**

Основной orchestrator был собран и тестировался с реальной Google Sheets базой.

Разработка остановилась на этапе реализации внутренней логики downstream AI workflows.

Полный автоматизированный production pipeline запущен не был.

---

## Workflow Preview

![BF_00 Daily Orchestrator](diagrams/orchestrator-overview.png)

Изображение показывает общий масштаб основного workflow. Для детального изучения структуры в репозитории также опубликованы очищенные JSON exports.

→ [`workflows/`](workflows/)
