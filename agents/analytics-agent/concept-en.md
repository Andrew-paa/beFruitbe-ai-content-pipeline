# Analytics Agent Architecture Concept

[Русская версия](concept-ru.md)

## Main Pipeline

```text
TikTok API ─────┐
Instagram API ──┼──→ Data Collection
YouTube API ────┘
                       ↓
                Platform Separation
                       ↓
                Video-Level Analysis
                       ↓
                Cross-Video Analysis
                       ↓
                External Research
                       ↓
                 Pattern Detection
                       ↓
                 Recommendations
                       ↓
                   Human Review
                       ↓
              Validated Audience Insights
                       ↓
                beFruitbe Knowledge Base
                       ↓
                Script & Prompt Agent
```

## Analysis Layers

### 1. Individual Video

```text
Metrics
+
Script
+
Visual Style
+
Characters
+
Format
+
Duration
```

Output:

```text
What happened?
Why?
What should remain?
What should change?
```

### 2. Platform

Separate analysis for:

```text
TikTok
Instagram
YouTube
```

Metrics from different platforms should not be directly mixed.

### 3. Time Period

Daily:

- current performance updates;
- early signals;
- monitoring new publications.

Monthly:

- repeated patterns;
- strongest formats;
- topics;
- characters;
- visual styles;
- duration;
- story mechanisms.

### 4. External Market

Discover similar public content:

```text
Find
 ↓
Compare
 ↓
Understand
 ↓
Adapt, not copy
```

### 5. Feedback Loop

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
Store Insight
 ↓
Create Better
```

## Key Constraint

The agent should not interpret identical metrics as identical performance across different platforms.

Platform context and account-level baselines must be considered separately.

## Status

The concept and Claude Project were created, but the system did not reach full production validation on a large volume of published content.
