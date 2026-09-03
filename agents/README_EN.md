# AI Agents

This directory contains documentation and artifacts for the AI agents designed as part of the **beFruitbe AI Content Pipeline**.

Two specialized AI components were designed during the project:

### 1. Script & Prompt Agent

A Custom GPT responsible for transforming short creative tasks into detailed video scripts, scene descriptions and generation prompts using the beFruitbe Knowledge Base.

→ [`script-agent/`](./script-agent/)

### 2. Content Performance Analysis Agent

A Claude-based prototype designed to analyze published content performance, identify patterns in audience response and generate recommendations for future videos.

→ [`analytics-agent/`](./analytics-agent/)

## Proposed Feedback Loop

```text
Script Agent
     ↓
Video
     ↓
Publication
     ↓
Performance Metrics
     ↓
Analytics Agent
     ↓
Human Validation
     ↓
Validated Insights
     ↓
Knowledge Base
     ↓
Script Agent
