# Knowledge Base Structure Examples

[Русская версия](README_RU.md)

This directory contains synthetic examples of records similar to those used in the **beFruitbe AI Content Pipeline** Knowledge Base.

## Important

These files:

- do not contain real confidential beFruitbe data;
- do not disclose actual product compositions;
- do not contain internal company claims;
- do not contain real SKUs;
- do not contain confidential interviews or internal documents.

Their purpose is to demonstrate the **data structure and Knowledge Base design principles** without exposing proprietary company information.

---

## Included Examples

### SKU Example

[`sample-sku-en.md`](sample-sku-en.md)

Demonstrates how information about a specific product could be structured:

- identification;
- verified facts;
- composition;
- data status;
- claims;
- related assets;
- usage permissions.

### Claim Example

[`sample-claim-en.md`](sample-claim-en.md)

Demonstrates how product statements were separated from ordinary text and assigned explicit statuses such as:

- APPROVED;
- DRAFT;
- CONFIRMATION REQUIRED;
- NOT ALLOWED.

### Document Metadata Example

[`sample-document-metadata-en.md`](sample-document-metadata-en.md)

Demonstrates how the Knowledge Base could manage:

- document versions;
- information owners;
- statuses;
- scope;
- AI usage permissions;
- publication permissions;
- archived versions.

---

## Core Principle

The Knowledge Base was designed so that AI components worked with structured context rather than a random collection of files.

Simplified flow:

```text
User Request
       ↓
Identify Relevant Product / Context
       ↓
Retrieve Verified Facts
       ↓
Check Claims & Restrictions
       ↓
Retrieve Approved Assets
       ↓
Generate AI Output
       ↓
Human Verification where required
```

---

## Why This Matters

In a commercial AI system, uploading documents to an LLM is not enough.

The system also needs to understand:

```text
What is a verified fact?
What is still a draft?
Which product is being discussed?
Which source is current?
Can this information be published?
Can it be used by AI?
Does it require human confirmation?
```

The Knowledge Base architecture was designed to solve these problems.
