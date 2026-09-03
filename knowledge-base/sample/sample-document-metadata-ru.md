# Синтетический пример метаданных документа

[English version](sample-document-metadata-en.md)

> Демонстрационный пример структуры.  
> Не содержит данных внутренних документов beFruitbe.

---

## Document

**Name:** Example Product Specification

**Document ID:** `DOC-EXAMPLE-001`

**Version:** `v1.2`

**Date:** `2026-08-20`

---

## Owner

```text
Product Team
```

Человек или подразделение, ответственное за достоверность документа.

---

## Status

```text
APPROVED
```

Возможные статусы:

```text
APPROVED
DRAFT
CONFIDENTIAL
ARCHIVED
```

---

## Scope

```text
SKU-EXAMPLE-001
```

Документ относится только к указанному продукту.

---

## Knowledge Base Usage

**Can be used in Knowledge Base:** YES

**Can be used by AI agents:** YES

**Can be quoted publicly:** NO

**Can be used for internal script development:** YES

---

## AI Asset Permission

```text
AI_REFERENCE_ALLOWED = YES
```

Если значение `NO`, материал нельзя загружать или использовать как reference в сторонних AI-сервисах.

---

## Replaces

```text
DOC-EXAMPLE-001 v1.1
```

Предыдущая версия должна считаться архивной.

---

## Notes

```text
Current verified version.
Do not use older product descriptions.
Public citation is not permitted.
```

---

## Expected Retrieval Logic

```text
Agent finds document
       ↓
Check status
       ↓
APPROVED?
       ↓
Check version
       ↓
Latest version?
       ↓
Check scope
       ↓
Correct SKU?
       ↓
Check permissions
       ↓
Use information
```

---

## Почему метаданные важны

Без метаданных AI может случайно использовать:

- старую версию документа;
- данные другого продукта;
- черновик;
- конфиденциальную информацию;
- материал, который нельзя загружать в AI;
- asset без права на публикацию.

Поэтому метаданные были частью архитектуры Knowledge Base, а не дополнительной бюрократией.
