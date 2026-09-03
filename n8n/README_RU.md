# n8n Automation — beFruitbe AI Content Pipeline

[English version](README.md)

## О проекте

В этой папке находится техническая часть **beFruitbe AI Content Pipeline**, связанная с автоматизацией процесса производства AI-контента в n8n.

Я проектировал систему как набор независимых workflow, которыми управляет центральный оркестратор.

Главный компонент:

`BF_00_DAILY_ORCHESTRATOR`

Он был собран в n8n, подключён к реальной Google Sheets базе и протестирован на проектных данных.

Полный end-to-end pipeline до автоматической генерации и публикации видео завершён не был: разработка остановилась на этапе реализации внутренних AI-модулей.

---

## Что было реализовано

Основной оркестратор содержит около **37 узлов** и отвечает за:

- автоматический и ручной запуск задач;
- чтение данных из Google Sheets;
- выбор готовых к обработке Daily Tasks;
- проверку обязательных полей;
- перевод некорректной задачи в `HOLD`;
- генерацию уникального `Run_ID`;
- защиту от повторного запуска одной и той же версии задачи;
- журналирование выполнения;
- получение данных о бренде, SKU, claims, аудитории и media assets;
- фильтрацию Knowledge Base;
- проверку статусов и разрешений;
- разделение внутреннего и публичного контекста;
- передачу задачи в downstream AI-workflows.

---

## Основная архитектура

```text
Daily Task
    ↓
Validation
    ↓
Duplicate Check
    ↓
Run Logging
    ↓
Knowledge Retrieval
    ↓
Context Filtering
    ↓
┌───────────────────────────────┐
│ PUBLIC_RESEARCH_BRIEF         │
│              ↓                │
│       External Research       │
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

## Источники данных

Оркестратор работал с центральной Google Sheets базой.

В ней были отдельные разделы для:

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

Это позволяло хранить данные отдельно от automation logic и получать только необходимый контекст для конкретной задачи.

---

## Task Validation

Перед запуском pipeline система проверяла обязательные поля задачи, включая:

```text
Task_ID
Task_Date
Brand_ID
SKU_ID
Content_Type
```

Для автоматического запуска выбирались только задачи:

```text
Task_Date = today
Task_Status = READY
```

Если данных было недостаточно:

```text
Task
 ↓
Validation Failed
 ↓
HOLD
 ↓
Runs Log
```

---

## Deduplication

Для предотвращения повторной обработки одинаковой задачи использовалась отдельная логика.

Система формировала `Input_Hash` и проверяла комбинацию:

```text
Task_ID + Input_Hash
```

по предыдущим запускам.

Если такая версия задачи уже существовала:

```text
DUPLICATE_SKIPPED
```

Если нет:

```text
Generate Run_ID
        ↓
RUN_STARTED
```

---

## Run Logging

Для каждого запуска создавался уникальный `Run_ID`.

Система записывала в журнал статусы, включая:

```text
RUN_STARTED
HOLD
DUPLICATE_SKIPPED
```

Это позволяло отслеживать историю выполнения и понимать, почему конкретная задача была обработана, остановлена или пропущена.

---

## Knowledge Filtering

Наличие информации в базе ещё не означало, что её можно автоматически передавать AI.

Перед использованием Knowledge записи проходили фильтрацию по параметрам вроде:

```text
Status
Readiness
Approved_for_Knowledge
Confidentiality
Usage permissions
```

Цель — использовать только подходящий и разрешённый контекст.

---

## Public и Internal Context

Одна из ключевых идей архитектуры — разделение данных.

### INTERNAL_BRAND_CONTEXT

Внутри системы могли использоваться:

- брендовые данные;
- SKU;
- claims;
- Knowledge;
- аудитория;
- media assets;
- предыдущий контент;
- внутренние сообщения.

### PUBLIC_RESEARCH_BRIEF

Для внешнего research создавался отдельный очищенный пакет.

Из него исключались потенциально чувствительные данные:

- внутренняя экономика;
- цены и margin;
- данные поставщиков;
- персональные данные;
- email и телефоны;
- rights documents;
- secrets и API-related information;
- confidential records.

Идея заключалась в том, чтобы внешний research-агент получил **взгляд из интернета**, но не получил внутреннюю базу компании.

После research внешний контекст можно было объединить с закрытым контекстом бренда уже внутри pipeline.

---

## Workflow Modules

| Workflow | Назначение | Статус |
|---|---|---|
| `BF_00_DAILY_ORCHESTRATOR` | Orchestration, validation, database access, deduplication, logging, routing | **Implemented prototype / tested** |
| `BF_01_RESEARCH_GEMINI` | External research | Workflow skeleton |
| `BF_02_SCRIPT_OPENAI` | Script & prompt generation | Workflow skeleton |
| `BF_03_IMAGE_GENERATION` | Image generation | Workflow skeleton |
| `BF_04_VEO_VIDEO_GENERATION_AND_ASSEMBLY` | Video generation & assembly | Workflow skeleton |
| `BF_05_FINAL_GEMINI_QA` | Final quality check | Workflow skeleton |
| `BF_06_ANALYTICS` | Content analytics | Workflow skeleton |

На момент остановки проекта центральный orchestrator был реализован значительно глубже, чем downstream-модули.

---

## Workflow Preview

![BF_00 Daily Orchestrator](diagrams/orchestrator-overview.png)

Скриншот показывает общий масштаб основного workflow.

Для технического просмотра доступны очищенные JSON exports:

→ [`workflows/`](workflows/)

---

## Public-safe exports

В репозитории опубликованы специально очищенные версии workflow.

Из публичных JSON удалены или заменены:

- Google Sheets IDs;
- credential IDs;
- credential names;
- внутренние workflow IDs;
- приватный webhook path;
- другие данные, которые не требуются для демонстрации архитектуры.

Логика основного orchestrator сохранена.

Оригинальные production/project credentials в репозитории не публикуются.

---

## Что я использовал в n8n

В процессе работы я получил практический опыт с:

- Google Sheets nodes;
- Schedule Trigger;
- Webhook;
- Filter;
- IF / Switch;
- Merge;
- Set;
- Execute Workflow;
- JavaScript Code nodes;
- task validation;
- deduplication;
- execution logging;
- context filtering;
- modular workflows.

---

## Что я понял в процессе

До этого проекта автоматизация AI-задачи могла выглядеть для меня примерно так:

```text
Input → AI → Result
```

На практике оказалось, что большая часть надёжной системы находится вокруг модели:

```text
Какая задача должна запуститься?
        ↓
Все ли данные есть?
        ↓
Не выполняли ли её раньше?
        ↓
Какая версия информации актуальна?
        ↓
Что AI разрешено использовать?
        ↓
Какие данные можно отправить наружу?
        ↓
Что должно остаться внутри системы?
        ↓
Как сохранить результат и статус выполнения?
```

Для меня n8n-часть проекта стала первым большим практическим опытом проектирования автоматизации между данными, AI-компонентами и несколькими этапами бизнес-процесса.

---

## Статус проекта

**Implemented orchestration prototype / incomplete end-to-end pipeline**

Реализовано и протестировано:

```text
Google Sheets
→ Task Selection
→ Validation
→ Deduplication
→ Run Logging
→ Knowledge Retrieval
→ Context Filtering
→ Public / Internal Context Separation
→ Downstream Routing
```

Следующим этапом должна была стать полноценная реализация:

```text
Research
→ Script Generation
→ Image Generation
→ Video Generation
→ QA
→ Analytics
```

До production-развёртывания этой части проект не дошёл.
