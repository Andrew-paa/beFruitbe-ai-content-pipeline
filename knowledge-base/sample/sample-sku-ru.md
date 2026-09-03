# Синтетический пример карточки SKU

[English version](sample-sku-en.md)

> Этот файл создан исключительно для демонстрации структуры.  
> Все данные ниже являются вымышленными и не описывают реальные продукты beFruitbe.

---

## Identification

**SKU ID:** `SKU-EXAMPLE-001`

**Product Name:** Example Product

**Category:** Product for brewing

**Status:** `APPROVED`

**Knowledge Version:** `v1.0`

---

## Product Data

**Flavour:** Example Fruit

**Product Form:** Dry product for brewing

**Preparation:** Use verified preparation instructions from the approved product specification.

---

## Composition

### Verified

- Example Ingredient A
- Example Ingredient B

### Restrictions

AI не должен добавлять или предполагать ингредиенты, которых нет в подтверждённых данных продукта.

Если информации о составе недостаточно:

```text
[НУЖНО ПОДТВЕРДИТЬ]
```

---

## Product Facts

### APPROVED

- Example verified product fact.
- Example verified preparation fact.

### CONFIRMATION REQUIRED

- Example statement that has not yet been fully approved.

### NOT ALLOWED

- Unsupported medical benefit.
- Unsupported comparison with another product category.
- Any invented product property.

---

## Tone of Voice

При описании этого SKU:

- использовать понятный язык;
- избегать преувеличенных обещаний;
- не придумывать свойства продукта;
- использовать утверждённую терминологию бренда.

---

## Visual Assets

Примеры Asset ID:

```text
SKU_EXAMPLE_PKG_FRONT_001.jpg
SKU_EXAMPLE_PKG_45DEG_001.jpg
SKU_EXAMPLE_DRY_MACRO_001.jpg
SKU_EXAMPLE_BREW_001.mov
```

---

## Asset Rules

При показе:

- упаковки;
- логотипов;
- этикеток;
- внешнего вида продукта

приоритет должен отдаваться реальным утверждённым assets.

Если существует реальный asset, критически важные элементы упаковки не следует генерировать с нуля.

---

## Claims

Связанные claims:

```text
CLAIM-EXAMPLE-001
CLAIM-EXAMPLE-002
```

Перед использованием claim необходимо проверить его актуальный статус.

---

## Usage Permissions

**Use in Knowledge Base:** YES

**Use by Script Agent:** YES

**AI Reference:** YES, if permitted by asset rights

**Public Publication:** depends on the specific asset

---

## Source

Синтетический пример на основе структуры Knowledge Base проекта beFruitbe.

Этот файл не описывает реальный SKU компании.
