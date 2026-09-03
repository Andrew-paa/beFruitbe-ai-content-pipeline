# Архитектурная концепция Analytics Agent

[English version](concept-en.md)

## Главный pipeline

```text
TikTok API ─────┐
Instagram API ──┼──→ Data Collection
YouTube API ────┘
                       ↓
                Platform Separation
                       ↓
                Video-Level Analysis
                       ↓
                Cross-Video Analysis
                       ↓
                External Research
                       ↓
                 Pattern Detection
                       ↓
                 Recommendations
                       ↓
                   Human Review
                       ↓
              Validated Audience Insights
                       ↓
                beFruitbe Knowledge Base
                       ↓
                Script & Prompt Agent
```

## Уровни анализа

### 1. Видео

```text
Метрики
+
сценарий
+
визуал
+
персонажи
+
формат
+
длительность
```

Результат:

```text
Что произошло?
Почему?
Что оставить?
Что изменить?
```

### 2. Площадка

Отдельный анализ:

```text
TikTok
Instagram
YouTube
```

Без прямого смешивания метрик разных платформ.

### 3. Период

Ежедневно:

- обновление текущих результатов;
- ранние сигналы;
- наблюдение за новыми публикациями.

Ежемесячно:

- устойчивые закономерности;
- топовые форматы;
- темы;
- персонажи;
- стилистика;
- длительность;
- сюжетные механики.

### 4. Внешний рынок

Поиск похожего публичного контента:

```text
Find
 ↓
Compare
 ↓
Understand
 ↓
Adapt, not copy
```

### 5. Feedback Loop

```text
Create
 ↓
Publish
 ↓
Measure
 ↓
Analyze
 ↓
Human Validate
 ↓
Store Insight
 ↓
Create Better
```

## Главное ограничение

Агент не должен считать одинаковые показатели одинаковым результатом на разных площадках.

Контекст платформы и базовые показатели аккаунта должны учитываться отдельно.

## Статус

Концепция и Claude Project были созданы, однако система не дошла до полноценного production-тестирования на большом массиве опубликованного контента.
