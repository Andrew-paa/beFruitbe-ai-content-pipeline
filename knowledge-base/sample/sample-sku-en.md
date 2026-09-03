# Synthetic SKU Record Example

[Русская версия](sample-sku-ru.md)

> This file exists only to demonstrate the Knowledge Base structure.  
> All information below is fictional and does not describe real beFruitbe products.

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

The AI must not add or infer ingredients that are not explicitly listed in verified product data.

If composition information is missing:

```text
[CONFIRMATION REQUIRED]
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

When describing this SKU:

- use clear language;
- avoid exaggerated promises;
- do not invent product properties;
- use approved brand terminology.

---

## Visual Assets

Example asset references:

```text
SKU_EXAMPLE_PKG_FRONT_001.jpg
SKU_EXAMPLE_PKG_45DEG_001.jpg
SKU_EXAMPLE_DRY_MACRO_001.jpg
SKU_EXAMPLE_BREW_001.mov
```

---

## Asset Rules

Prefer real approved assets when showing:

- packaging;
- logos;
- labels;
- product appearance.

Do not regenerate critical packaging details when an approved original asset exists.

---

## Claims

Related claims:

```text
CLAIM-EXAMPLE-001
CLAIM-EXAMPLE-002
```

Always check the current status of a claim before using it.

---

## Usage Permissions

**Use in Knowledge Base:** YES

**Use by Script Agent:** YES

**AI Reference:** YES, subject to asset rights

**Public Publication:** depends on the specific asset

---

## Source

Synthetic example based on the architecture used in the beFruitbe Knowledge Base.

This record does not represent an actual company SKU.
