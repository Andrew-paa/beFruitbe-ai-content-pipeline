# n8n Automation — beFruitbe AI Content Pipeline

[Русская версия](README_RU.md)

## Overview

This directory contains the automation layer of the **beFruitbe AI Content Pipeline**, designed in n8n.

The system was designed as a set of modular workflows controlled by a central orchestrator.

The main component:

`BF_00_DAILY_ORCHESTRATOR`

was implemented in n8n, connected to the real Google Sheets data layer, and tested on project data.

The complete end-to-end video generation and publishing pipeline was not finished. Development stopped while the internal downstream AI modules were still being implemented.

---

## What Was Implemented

The main orchestrator contains approximately **37 nodes** and handles:

- scheduled and manual task execution;
- Google Sheets data retrieval;
- Daily Task selection;
- required-field validation;
- HOLD handling;
- unique `Run_ID` generation;
- duplicate-run prevention;
- execution logging;
- retrieval of brand, SKU, claims, audience and media data;
- Knowledge Base filtering;
- status and permission checks;
- public/private context separation;
- routing to downstream AI workflows.

---

## High-Level Architecture

```text
Daily Task
    ↓
Validation
    ↓
Duplicate Check
    ↓
Run Logging
    ↓
Knowledge Retrieval
    ↓
Context Filtering
    ↓
┌───────────────────────────────┐
│ PUBLIC_RESEARCH_BRIEF         │
│              ↓                │
│       External Research       │
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

## Data Layer

The orchestrator used a central Google Sheets data layer containing separate sections for:

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

This allowed structured project data to remain separate from automation logic.

---

## Task Validation

Before starting the AI pipeline, the orchestrator validated required task fields such as:

```text
Task_ID
Task_Date
Brand_ID
SKU_ID
Content_Type
```

Scheduled execution selected tasks matching:

```text
Task_Date = today
Task_Status = READY
```

If required information was missing:

```text
Task
 ↓
Validation Failed
 ↓
HOLD
 ↓
Runs Log
```

---

## Deduplication

The system implemented duplicate-run protection.

An `Input_Hash` was created and the combination:

```text
Task_ID + Input_Hash
```

was checked against previous executions.

If the same task version had already been processed:

```text
DUPLICATE_SKIPPED
```

Otherwise:

```text
Generate Run_ID
        ↓
RUN_STARTED
```

---

## Execution Logging

Each execution received a unique `Run_ID`.

The Runs Log stored states including:

```text
RUN_STARTED
HOLD
DUPLICATE_SKIPPED
```

This created an execution history and made it possible to understand why a task was processed, blocked or skipped.

---

## Knowledge Filtering

A record existing in the Knowledge Base did not automatically mean it could be passed to AI.

Knowledge records were filtered using properties such as:

```text
Status
Readiness
Approved_for_Knowledge
Confidentiality
Usage permissions
```

The purpose was to use only valid and permitted project context.

---

## Public and Internal Context

A key architecture decision was separating project context into two layers.

### INTERNAL_BRAND_CONTEXT

Internal processing could include:

- brand data;
- SKU data;
- claims;
- Knowledge;
- audience context;
- media assets;
- previous content;
- internal messages.

### PUBLIC_RESEARCH_BRIEF

External research received a separate sanitized context.

Potentially sensitive information was removed, including:

- internal economics;
- pricing and margins;
- supplier information;
- personal information;
- email and phone data;
- rights documentation;
- secrets and API-related information;
- confidential records.

The Research Agent was intended to provide an **outside perspective** without receiving the company's complete internal database.

External research could then be combined with private brand context inside the pipeline before script generation.

---

## Workflow Modules

| Workflow | Responsibility | Status |
|---|---|---|
| `BF_00_DAILY_ORCHESTRATOR` | Orchestration, validation, database access, deduplication, logging and routing | **Implemented prototype / tested** |
| `BF_01_RESEARCH_GEMINI` | External research | Workflow skeleton |
| `BF_02_SCRIPT_OPENAI` | Script & prompt generation | Workflow skeleton |
| `BF_03_IMAGE_GENERATION` | Image generation | Workflow skeleton |
| `BF_04_VEO_VIDEO_GENERATION_AND_ASSEMBLY` | Video generation & assembly | Workflow skeleton |
| `BF_05_FINAL_GEMINI_QA` | Final quality assurance | Workflow skeleton |
| `BF_06_ANALYTICS` | Content analytics | Workflow skeleton |

At the point development stopped, the central orchestrator had been implemented much more deeply than the downstream modules.

---

## Workflow Preview

![BF_00 Daily Orchestrator](diagrams/orchestrator-overview.png)

The screenshot provides a high-level view of the main workflow.

Sanitized JSON exports are available for technical inspection:

→ [`workflows/`](workflows/)

---

## Public-Safe Exports

The JSON workflows in this repository are sanitized portfolio versions.

The public exports have sensitive project references removed or replaced, including:

- Google Sheets IDs;
- credential IDs;
- credential names;
- internal workflow IDs;
- private webhook paths;
- other environment-specific references.

The orchestration logic itself remains available for inspection.

Real project credentials are not published.

---

## n8n Experience

During the project I worked with:

- Google Sheets nodes;
- Schedule Trigger;
- Webhooks;
- Filter;
- IF / Switch;
- Merge;
- Set;
- Execute Workflow;
- JavaScript Code nodes;
- task validation;
- deduplication;
- execution logging;
- context filtering;
- modular workflows.

---

## Key Learning

Before this project, AI automation could appear as simple as:

```text
Input → AI → Result
```

In practice, a reliable system requires significant logic around the model:

```text
Which task should run?
        ↓
Is all required data available?
        ↓
Has this task already been processed?
        ↓
Which version of the information is current?
        ↓
What is AI allowed to use?
        ↓
What may be sent to an external model?
        ↓
What must remain internal?
        ↓
How should execution status be recorded?
```

The n8n part of this project became my first substantial practical experience designing automation between structured data, AI components and multiple stages of a business workflow.

---

## Project Status

**Implemented orchestration prototype / incomplete end-to-end pipeline**

Implemented and tested:

```text
Google Sheets
→ Task Selection
→ Validation
→ Deduplication
→ Run Logging
→ Knowledge Retrieval
→ Context Filtering
→ Public / Internal Context Separation
→ Downstream Routing
```

The planned next stage was:

```text
Research
→ Script Generation
→ Image Generation
→ Video Generation
→ QA
→ Analytics
```

This part did not reach full production deployment.
