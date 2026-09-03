# beFruitbe Content Analytics Agent

[Русская версия](README_RU.md)

## Overview

The **beFruitbe Content Analytics Agent** was an AI component I designed in Claude Project to analyze the performance of short-form beFruitbe content.

Its primary purpose was:

> to understand which videos perform better, why they perform better, and which insights should influence future content.

The agent was designed as the second major AI component of the beFruitbe Content Pipeline.

While the Script & Prompt Agent answered:

> What should we create and how?

the Analytics Agent was designed to answer:

> What worked, why did it work, and what should we change next?

---

## Core Concept

A content factory can produce a large number of videos.

However, content volume alone does not guarantee performance.

The system therefore required an additional loop:

```text
Create
    ↓
Publish
    ↓
Collect Data
    ↓
Analyze
    ↓
Detect Patterns
    ↓
Use Insights in Future Content
```

The long-term goal was to move from content based mainly on assumptions toward content informed by actual audience response.

---

## Platforms

The agent was designed to analyze content from:

- TikTok;
- Instagram;
- YouTube.

I worked on connecting social-platform data through APIs.

The full production analytics loop was not validated on a large volume of published content because the project stopped during the prototype stage.

---

## Video-Level Data

The agent was designed to analyze data including:

- views;
- likes;
- comments;
- saves;
- shares;
- average watch time;
- video topic;
- visual style;
- characters;
- storyline;
- format;
- duration.

The analysis was not intended to rely on metrics alone.

The agent was designed to combine:

```text
performance metrics
+
script
+
visual style
+
characters
+
video structure
```

to explain why a specific video may have produced a particular result.

---

## Individual Video Analysis

The intended report structure was:

```text
Result
    ↓
Analysis
    ↓
Why It Worked / Why It Did Not
    ↓
What to Keep
    ↓
What to Change
    ↓
Recommendations for Future Videos
```

The agent could analyze factors such as:

- hook strength;
- speed of the opening;
- characters;
- pacing;
- visual style;
- narrative structure;
- duration;
- differences from previous content.

---

## External Content Research

The agent was also intended to research similar public content.

It should independently discover videos with related topics or creative mechanics and analyze:

- which videos achieved strong results;
- which creative techniques were used;
- which hooks worked;
- visual style;
- character types;
- narrative mechanisms;
- differences between successful and weaker examples.

These external observations would then be compared with:

- beFruitbe's own performance data;
- the brand Knowledge Base;
- product constraints.

The goal was not to copy successful videos, but to identify patterns that could be adapted to the beFruitbe context.

---

## Platform-Specific Analysis

One of the key requirements was to avoid mixing performance across platforms.

TikTok, Instagram and YouTube have different:

- audiences;
- recommendation systems;
- content-consumption behavior;
- typical metrics;
- distribution mechanics.

The agent was therefore intended to analyze:

```text
TikTok separately
Instagram separately
YouTube separately
```

before looking for cross-platform patterns.

---

## Absolute and Relative Performance

The agent was designed to evaluate performance on two levels.

### Absolute

For example:

```text
100,000 views
10,000 views
3,000 views
```

### Relative

A video's performance compared with:

- the account baseline;
- previous publications;
- similar videos;
- the same platform's normal performance.

This prevents the same absolute metric from being interpreted identically in different contexts.

---

## Daily Analytics

After content publication began, the agent was intended to retrieve updated performance metrics every day.

The system would maintain a current daily analytics snapshot.

Each new daily snapshot would replace the previous operational snapshot, while longer-term conclusions would be retained separately.

Daily analysis was intended to help:

- identify early changes;
- detect initial signals;
- identify strong and weak videos;
- monitor audience response.

---

## Monthly Analytics

In addition to operational daily analysis, the system was designed to generate a monthly report.

It could include:

- top-performing videos;
- best-performing creative techniques;
- successful characters;
- strongest topics;
- visual styles;
- ideas;
- story mechanisms;
- effective duration;
- formats;
- recommendations for the next period.

The monthly report was intended to identify repeated patterns rather than overreact to one isolated video.

---

## Analytics Output

The central question was:

> Which videos work, and why?

The expected output therefore went beyond a metrics table.

```text
DATA
Publication Metrics

    ↓

OBSERVATIONS
What Happened

    ↓

ANALYSIS
Why It May Have Happened

    ↓

PATTERNS
What Repeats

    ↓

RECOMMENDATIONS
What to Keep / Change / Test
```

---

## Human-in-the-Loop

During the initial stage, all important analytics conclusions were intended to be reviewed by a human.

```text
AI Analysis
      ↓
Human Review
      ↓
Insight Valid?
   ↙          ↘
 No           Yes
 ↓             ↓
Discard      Store as Insight
```

This was important because correlation alone does not prove causation.

Once sufficient data and confidence in agent quality were accumulated, more of the process could potentially be automated.

---

## Writing Insights Back to the Knowledge Base

Human-validated conclusions were intended to be stored in a dedicated analytics section of the Knowledge Base.

For example:

```text
Audience Insights

- visual styles that perform better;
- character types that attract attention;
- dialogue patterns that work;
- effective story mechanisms;
- successful video duration;
- stronger hooks;
- platform-specific formats.
```

The Script & Prompt Agent could then use these validated insights when preparing future content.

---

## Integration with the Script Agent

The complete feedback loop was designed as:

```text
Script & Prompt Agent
        ↓
New Script
        ↓
Video
        ↓
Publication
        ↓
TikTok / Instagram / YouTube
        ↓
Metrics
        ↓
Content Analytics Agent
        ↓
Analysis
        ↓
Human Review
        ↓
Validated Insights
        ↓
Knowledge Base
        ↓
Script & Prompt Agent
        ↓
Next Script
```

The system was therefore intended to gradually incorporate real audience behavior into future content decisions.

---

## Implementation Status

**Status: prototype / not production validated**

I independently:

- proposed the agent concept;
- designed its logic;
- created the Claude Project;
- designed the analysis structure;
- worked on API access to social-platform data;
- designed daily and monthly analytics cycles;
- designed the mechanism for returning validated insights to the Knowledge Base.

The complete production feedback loop was not launched because the project stopped before large-scale content publication began.

The original Claude Project is currently unavailable, so this repository contains a reconstruction of the architecture based on my project design rather than an export of the original agent instruction.
