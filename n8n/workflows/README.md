# n8n Automation Prototype

[Русская версия](README_RU.md)

## Overview

As part of the **beFruitbe AI Content Pipeline**, I designed a modular n8n architecture for automating an AI-assisted content production workflow.

The main component was:

`BF_00_DAILY_ORCHESTRATOR`

It was responsible for:

- task retrieval;
- input validation;
- accessing the central Google Sheets database;
- duplicate-run protection;
- brand-context assembly;
- separation of public and internal data;
- routing tasks to downstream AI workflows;
- run-status logging.

The main orchestrator was implemented and tested with real Google Sheets data.

The complete end-to-end image, video, QA and analytics pipeline was not completed as a production system.

---

## Main Orchestrator

`BF_00_DAILY_ORCHESTRATOR`

**37 n8n nodes**

The orchestrator supported two execution modes:

```text
Automatic Schedule
daily at 06:00 Europe/Moscow

or

Manual Webhook
run a specific Task_ID
```

---

## Central Data Source

The orchestrator retrieved context from a central Google Sheets database.

The workflow accessed separate data areas for:

```text
Daily Tasks
Runs Log
Brands
SKUs
Claims
Audiences
Media Library
Previous Content
Messages
Knowledge
```

Product, audience, claims, media and previous-content information therefore remained in a structured external data layer rather than being hard-coded into the workflow.

---

## Task Validation

Before starting AI stages, the orchestrator checked required fields:

```text
Task_ID
Task_Date
Brand_ID
SKU_ID
Content_Type
```

For scheduled runs, it selected tasks matching:

```text
Task_Date = today
+
Task_Status = READY
```

If required information was missing:

```text
PROCESS → blocked
HOLD → written to Runs Log
```

---

## Duplicate Protection

I implemented a deduplication mechanism.

An `Input_Hash` was generated from task inputs.

The system then checked:

```text
Task_ID
+
Input_Hash
```

against previous runs.

If the same task version had already been processed:

```text
DUPLICATE
    ↓
DUPLICATE_SKIPPED
```

Otherwise:

```text
NEW
 ↓
Generate Run_ID
 ↓
RUN_STARTED
```

---

## Run Logging

Each execution received a unique `Run_ID`.

The Runs Log recorded states including:

```text
RUN_STARTED
HOLD
DUPLICATE_SKIPPED
```

This created a basic execution history and made it possible to understand why a pipeline run was started, skipped or blocked.

---

## Knowledge Filtering

Knowledge records were filtered before being passed to AI components.

For example, a Knowledge record was expected to satisfy conditions such as:

```text
Status = APPROVED
Approved_for_Knowledge = YES
Readiness = READY
Confidentiality != CONFIDENTIAL
```

This meant that simply existing in the database did not automatically make information available to AI.

---

## Internal and Public Context

A key architecture decision was separating the context into two layers.

### INTERNAL_BRAND_CONTEXT

The internal context could contain:

```text
Brand Data
Messages
Knowledge
SKU
Allowed Claims
Forbidden Claims
Audience
Media Assets
Previous Content
```

This context was intended for internal system stages and the Script Agent.

### PUBLIC_RESEARCH_BRIEF

A separate sanitized context was created for external research.

Potentially sensitive information was removed, including fields related to:

```text
internal pricing;
cost and margin;
suppliers;
personal information;
email and phone;
rights documentation;
API keys / secrets;
unpublished promotions;
confidential information.
```

Public eligibility also depended on record status and usage rights.

---

## Why Research Was Separated

The Research Agent was intended to provide an **external perspective**:

```text
PUBLIC_RESEARCH_BRIEF
        ↓
External Research
        ↓
Trends / Audience Context / Public Information
```

It was intentionally prevented from receiving the company's full internal database.

The resulting research packet could later be combined with:

```text
INTERNAL_BRAND_CONTEXT
```

before being passed to the Script Agent.

This allowed the pipeline to combine:

```text
External Perspective
+
Private Brand Knowledge
```

without unnecessarily exposing internal information to the research stage.

---

## Modular Architecture

| Workflow | Responsibility | Status |
|---|---|---|
| `BF_00_DAILY_ORCHESTRATOR` | Orchestration, data access, validation, deduplication, logging and routing | **Implemented prototype / tested** |
| `BF_01_RESEARCH_GEMINI` | External research | Interface / skeleton |
| `BF_02_SCRIPT_OPENAI` | Script and prompt generation | Interface / skeleton |
| `BF_03_IMAGE_GENERATION` | Image generation | Interface / skeleton |
| `BF_04_VEO_VIDEO_GENERATION_AND_ASSEMBLY` | Video generation and assembly | Interface / skeleton |
| `BF_05_FINAL_GEMINI_QA` | Final AI quality check | Interface / skeleton |
| `BF_06_ANALYTICS` | Content analytics | Interface / skeleton |

The orchestrator also referenced a planned `BF_99_ERROR_HANDLER`; however, that separate workflow was not included in the preserved export.

---

## Proposed Pipeline

```text
Daily Task
    ↓
Validation
    ↓
Deduplication
    ↓
Run Logging
    ↓
Knowledge Retrieval
    ↓
Context Filtering
    ↓
┌───────────────────────────────┐
│ PUBLIC_RESEARCH_BRIEF         │
│             ↓                 │
│        Research Agent         │
└───────────────────────────────┘
              +
┌───────────────────────────────┐
│ INTERNAL_BRAND_CONTEXT        │
└───────────────────────────────┘
              ↓
      Script & Prompt Agent
              ↓
       Image Generation
              ↓
       Video Generation
              ↓
            QA
              ↓
         Analytics
```

---

## Implemented vs Planned Scope

### Implemented and Tested

The main orchestrator included:

```text
Google Sheets
→ task selection
→ validation
→ deduplication
→ Run_ID generation
→ logging
→ Knowledge retrieval
→ filtering
→ internal/public context separation
→ downstream workflow routing
```

### Prepared as the Next Stage

Separate workflow interfaces existed for:

```text
Research
Script Generation
Image Generation
Video Generation
QA
Analytics
```

Their internal automation logic had not yet been completed when development stopped.

---

## Technical Experience

The n8n prototype gave me practical experience with:

- Google Sheets nodes;
- Schedule Trigger;
- Webhooks;
- Switch / IF / Filter nodes;
- Execute Workflow;
- Merge;
- Set;
- JavaScript Code nodes;
- task validation;
- deduplication;
- run logging;
- context filtering;
- modular workflow architecture.

One of the main lessons was that a reliable AI automation system requires much more than calling an AI model.

A significant part of the architecture is responsible for:

```text
selecting the right data
→ checking whether it may be used
→ validating the task
→ preventing duplicate execution
→ controlling what external AI receives
→ preserving private context
→ handling execution status
```

---

## Project Status

**Status: implemented orchestration prototype / incomplete end-to-end pipeline**

The main orchestrator was built and tested against the real Google Sheets data layer.

Development stopped while the internal logic of downstream AI workflows was still being implemented.

A complete automated production pipeline was therefore not deployed.

---

## Workflow Preview

![BF_00 Daily Orchestrator](diagrams/orchestrator-overview.png)

The image provides a high-level view of the workflow scale. Sanitized JSON exports are also available for technical inspection.

→ [`workflows/`](workflows/)
