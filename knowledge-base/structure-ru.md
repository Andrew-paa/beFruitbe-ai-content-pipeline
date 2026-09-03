# Структура Knowledge Base

[English version](structure-en.md)

> Публичная реконструкция структуры.  
> Реальные документы и данные компании не опубликованы.

```text
BF_KNOWLEDGE_AND_MEDIA/
│
├── 01_BRAND_AND_CATEGORY/
│   ├── Brand History
│   ├── Category Definition
│   ├── Audience
│   ├── Positioning
│   └── Founder Interviews
│
├── 02_TECHNOLOGY/
│   ├── Product Technology
│   ├── Verified Process Facts
│   ├── Allowed Descriptions
│   └── Visualization Restrictions
│
├── 03_SKU_MASTER/
│   └── SKU-XXX/
│       ├── Product Data
│       ├── Composition
│       ├── Flavour
│       ├── Preparation
│       ├── Packaging
│       └── Status
│
├── 04_CLAIMS/
│   ├── Approved
│   ├── Draft
│   ├── Confirmation Required
│   └── Not Allowed
│
├── 05_TONE_AND_EXAMPLES/
│   ├── Tone of Voice
│   ├── Messaging Rules
│   ├── Good Examples
│   ├── Bad Examples
│   └── CTA Rules
│
├── 06_VISUAL_SYSTEM/
│   ├── Visual Rules
│   ├── AI Generation Rules
│   ├── Continuity
│   ├── Packaging Rules
│   └── Production Requirements
│
├── 07_MEDIA_LIBRARY/
│   ├── Photos/
│   ├── Video/
│   ├── Audio/
│   └── Graphics/
│
├── 08_PACKAGING/
│   └── SKU-XXX/
│       └── Package Version/
│
├── 09_PRODUCT_TRUTH/
│   └── SKU-XXX/
│
├── 10_RIGHTS/
│   ├── Brand
│   ├── Packaging
│   ├── People
│   ├── Music
│   └── AI Usage
│
├── 11_CONTENT_REGISTRY/
│   ├── Published Content
│   ├── Scripts
│   └── Content Metadata
│
└── 12_ANALYTICS/
    ├── Daily
    ├── Monthly
    └── Validated Audience Insights
```

---

## Логика

### Facts

```text
Brand
Technology
SKU
Claims
```

отвечают на вопрос:

> Что AI имеет право считать фактом?

### Communication

```text
Tone
Messaging
Examples
```

отвечают:

> Как AI должен об этом говорить?

### Visual System

```text
Visual Rules
Media
Packaging
Product Truth
```

отвечают:

> Что AI имеет право показывать и какие реальные assets использовать?

### Governance

```text
Rights
Statuses
Metadata
```

отвечают:

> Можно ли этот материал использовать?

### Learning Loop

```text
Content Registry
Analytics
```

отвечают:

> Что система может узнать из уже созданного контента?
