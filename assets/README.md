# Architecture Assets

[Русская версия](README_RU.md)

This directory contains visual materials explaining the architecture of the **beFruitbe AI Content Pipeline**.

## System Architecture

→ [Open the architecture diagram](architecture-diagram.md)

The diagram presents the proposed end-to-end flow:

`task → data → orchestration → research → scripting → generation → human review → publishing → analytics → knowledge update`

## Component Status

The diagram intentionally distinguishes between:

- implemented components;
- prototypes;
- designed but incomplete components;
- human-in-the-loop checkpoints.

This distinction is important because the complete end-to-end pipeline was not deployed to production.

## Detailed Documentation

### System Architecture

[`../docs/en/architecture.md`](../docs/en/architecture.md)

### Workflow

[`../docs/en/workflow.md`](../docs/en/workflow.md)

### n8n Orchestrator

[`../n8n/architecture.md`](../n8n/architecture.md)

### AI Agents

[`../agents/`](../agents/)

### Knowledge Base

[`../knowledge-base/`](../knowledge-base/)
