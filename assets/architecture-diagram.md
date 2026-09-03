# beFruitbe AI Content Pipeline — Architecture

This diagram shows the overall architecture of the project and distinguishes between implemented, prototyped and planned components.

```mermaid
flowchart TD

    %% USER LAYER
    U[Content Manager / Employee]
    TG[Telegram Bot<br/>Planned Interface]

    U --> TG

    %% TASK / ORCHESTRATION
    TG --> TASK[Daily Task]
    TASK --> ORCH[BF_00_DAILY_ORCHESTRATOR<br/>n8n<br/>Implemented Prototype]

    %% DATA LAYER
    DB[(Google Sheets<br/>Structured Data Layer)]
    KB[(beFruitbe Knowledge Base<br/>Implemented)]

    DB --> ORCH
    KB --> ORCH

    %% VALIDATION
    ORCH --> VAL[Task Validation]
    VAL --> DEDUP[Deduplication<br/>Task_ID + Input_Hash]
    DEDUP --> LOG[Run Logging<br/>Run_ID / HOLD / DUPLICATE]

    %% CONTEXT
    LOG --> CTX[Context Builder]

    CTX --> PUB[PUBLIC_RESEARCH_BRIEF]
    CTX --> INT[INTERNAL_BRAND_CONTEXT]

    %% RESEARCH
    PUB --> RES[External Research<br/>Gemini Module<br/>Workflow Skeleton]

    RES --> MERGE[Merge Research + Internal Context]
    INT --> MERGE

    %% SCRIPT AGENT
    MERGE --> SCRIPT[Script & Prompt Agent<br/>Custom GPT<br/>Implemented & Tested]

    %% PRODUCTION
    SCRIPT --> IMG[Image Generation<br/>Planned Automation]
    IMG --> H1{Human Approval}

    H1 -->|Revise| SCRIPT
    H1 -->|Approved| VIDEO[Video Generation<br/>Kling / Veo / HeyGen]

    VIDEO --> H2{Human Review}

    H2 -->|Revise| SCRIPT
    H2 -->|Approved| QA[Final QA<br/>Planned Module]

    %% PUBLISHING
    QA --> PUBLI[Automatic Publishing<br/>Planned]

    PUBLI --> TT[TikTok]
    PUBLI --> IG[Instagram]
    PUBLI --> YT[YouTube Shorts]

    %% ANALYTICS
    TT --> ANALYTICS[Content Analytics Agent<br/>Claude Prototype]
    IG --> ANALYTICS
    YT --> ANALYTICS

    ANALYTICS --> HR{Human Validation}

    HR -->|Validated Insights| INSIGHTS[Audience Insights]
    INSIGHTS --> KB

    %% CLASSES

    classDef implemented fill:#d9ead3,stroke:#38761d,stroke-width:2px;
    classDef prototype fill:#fff2cc,stroke:#bf9000,stroke-width:2px;
    classDef planned fill:#eeeeee,stroke:#777777,stroke-width:1px,stroke-dasharray:5 5;
    classDef human fill:#d9eaf7,stroke:#3d85c6,stroke-width:2px;

    class ORCH,DB,KB,SCRIPT implemented;
    class RES,ANALYTICS prototype;
    class TG,IMG,QA,PUBLI planned;
    class U,H1,H2,HR human;
```

## Status Legend

- **Green** — implemented / tested during the project
- **Yellow** — prototype or partially implemented
- **Grey dashed** — designed but not completed
- **Blue** — human decision / human-in-the-loop

## Core Architecture Principle

The system was designed around three ideas:

```text
Structured Data
      +
Specialized AI Components
      +
Human Approval
```

rather than a single:

```text
Prompt → AI → Video
```

## Feedback Loop

The long-term architecture was designed to create the following cycle:

```text
Create
  ↓
Publish
  ↓
Measure
  ↓
Analyze
  ↓
Human Validate
  ↓
Store Insights
  ↓
Create Better Content
```

This allows future content decisions to use both:

- verified brand knowledge;
- actual audience-performance data.
