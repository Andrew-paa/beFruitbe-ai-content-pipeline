# Synthetic Document Metadata Example

[Русская версия](sample-document-metadata-ru.md)

> Demonstration of the metadata structure only.  
> This file does not contain data from internal beFruitbe documents.

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

The person or department responsible for verifying the document.

---

## Status

```text
APPROVED
```

Possible statuses:

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

The document applies only to the specified product.

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

If the value is `NO`, the material must not be uploaded to or used as a reference in third-party AI services.

---

## Replaces

```text
DOC-EXAMPLE-001 v1.1
```

The previous version should be treated as archived.

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
Agent Finds Document
       ↓
Check Status
       ↓
APPROVED?
       ↓
Check Version
       ↓
Latest Version?
       ↓
Check Scope
       ↓
Correct SKU?
       ↓
Check Permissions
       ↓
Use Information
```

---

## Why Metadata Matters

Without metadata, an AI system could accidentally use:

- an outdated document;
- information from another SKU;
- a draft;
- confidential information;
- data that cannot be uploaded to AI;
- an asset without publication rights.

For this reason, metadata was treated as part of the Knowledge Base architecture rather than administrative overhead.
