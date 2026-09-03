# Синтетический пример Claim

[English version](sample-claim-en.md)

> Демонстрационный пример.  
> Утверждение ниже является вымышленным и не относится к реальным продуктам beFruitbe.

---

## Claim ID

```text
CLAIM-EXAMPLE-001
```

## Statement

> «Пример продуктового утверждения.»

---

## Type

```text
PRODUCT FACT
```

---

## Status

```text
CONFIRMATION REQUIRED
```

Возможные статусы:

```text
APPROVED
DRAFT
CONFIRMATION REQUIRED
NOT ALLOWED
```

---

## Scope

```text
SKU-EXAMPLE-001
```

Утверждение относится только к конкретному SKU.

Оно не должно автоматически переноситься на другие продукты.

---

## Source

```text
Example Product Specification
```

---

## Verification Owner

```text
Product / Brand Owner
```

---

## AI Usage

### Script Development

**ALLOWED**

Агент может использовать утверждение как рабочую гипотезу при разработке сценария, сохраняя статус проверки.

### Publication

**HOLD**

Публикация невозможна до подтверждения человеком.

---

## Expected Agent Behaviour

Если сценарий требует этот claim:

```text
Script Agent
      ↓
Find Claim
      ↓
Check Status
      ↓
CONFIRMATION REQUIRED
      ↓
Continue Drafting
      ↓
Flag Claim
      ↓
Human Verification
```

Агент не должен незаметно превращать неподтверждённое утверждение в факт.

---

## Example Agent Warning

```text
[НУЖНО ПОДТВЕРДИТЬ: продуктовое утверждение перед публикацией]
```

---

## Почему claims хранятся отдельно

Отдельный структурированный слой позволяет различать:

```text
Creative Text
от
Product Fact
```

и:

```text
Draft
от
Approved Statement
```

Это снижает риск hallucinations и некорректных продуктовых утверждений в коммерческом контенте.
