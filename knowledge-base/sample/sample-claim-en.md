# Synthetic Claim Example

[Русская версия](sample-claim-ru.md)

> Demonstration example only.  
> The statement below is fictional and does not refer to any real beFruitbe product.

---

## Claim ID

```text
CLAIM-EXAMPLE-001
```

## Statement

> “Example product statement.”

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

Possible system statuses:

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

The statement applies only to a specific SKU.

It must not automatically be transferred to other products.

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

The agent may use the statement as a working hypothesis during script development while preserving its verification status.

### Publication

**HOLD**

Publication is blocked until human verification.

---

## Expected Agent Behaviour

If a script requires this claim:

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

The agent must not silently convert an unverified statement into a fact.

---

## Example Agent Warning

```text
[CONFIRMATION REQUIRED: product statement before publication]
```

---

## Why Claims Are Stored Separately

A structured claims layer makes it possible to distinguish:

```text
Creative Copy
from
Product Fact
```

and:

```text
Draft
from
Approved Statement
```

This helps reduce hallucinations and unsupported statements in commercial content.
