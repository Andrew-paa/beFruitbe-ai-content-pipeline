# Архитектурные материалы

[English version](README.md)

В этой папке находятся визуальные материалы, объясняющие архитектуру проекта **beFruitbe AI Content Pipeline**.

## Общая архитектура

→ [Открыть архитектурную схему](architecture-diagram.md)

Схема показывает полный предполагаемый цикл:

`задача → данные → orchestration → research → сценарий → генерация → human review → публикация → аналитика → обновление знаний`

## Статусы компонентов

На диаграмме специально разделены:

- реализованные компоненты;
- прототипы;
- спроектированные, но незавершённые компоненты;
- human-in-the-loop checkpoints.

Это важно, поскольку полный end-to-end pipeline не был запущен в production.

## Более подробная документация

### Общая архитектура

[`../docs/ru/architecture.md`](../docs/ru/architecture.md)

### Workflow

[`../docs/ru/workflow.md`](../docs/ru/workflow.md)

### n8n Orchestrator

[`../n8n/architecture_RU.md`](../n8n/architecture_RU.md)

### AI Agents

[`../agents/`](../agents/)

### Knowledge Base

[`../knowledge-base/`](../knowledge-base/)
