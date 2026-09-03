# Knowledge Base Structure

[Русская версия](structure-ru.md)

> Public reconstruction of the architecture.  
> Real company documents and internal data are not published.

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

## Architecture Logic

### Facts

```text
Brand
Technology
SKU
Claims
```

answer:

> What is the AI allowed to treat as fact?

### Communication

```text
Tone
Messaging
Examples
```

answer:

> How should the AI communicate those facts?

### Visual System

```text
Visual Rules
Media
Packaging
Product Truth
```

answer:

> What may the AI show and which verified assets should it use?

### Governance

```text
Rights
Statuses
Metadata
```

answer:

> Is the system allowed to use this asset or information?

### Learning Loop

```text
Content Registry
Analytics
```

answer:

> What can the system learn from previously produced content?
