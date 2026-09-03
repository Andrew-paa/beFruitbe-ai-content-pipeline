# Project Workflow

[Русская версия](../ru/workflow.md)

## beFruitbe AI Content Pipeline

This document describes two different processes:

1. the actual workflow I used to produce demonstration videos for beFruitbe;
2. the proposed automated workflow for the future AI Content Pipeline.

The distinction is important: during the Proof-of-Concept stage, video production remained human-guided, while the experience gained from this process was used to design the future automation.

---

## 1. How Tasks Were Received

I usually received new video requests through Telegram from the Deputy CEO.

The request could be:

- a short text message;
- a voice message.

Usually, it described the general idea rather than providing a detailed technical specification.

The team could describe the desired story, product or characters, while I was responsible for translating that idea into a more detailed AI-production process.

The initial workflow therefore looked approximately like this:

```text
Short Business Idea
        ↓
Requirements Clarification
        ↓
Transform the Idea into an AI Production Specification
```

---

## 2. Actual Video Production Workflow

A typical production process for one video looked like this:

```text
Task from the Team
        ↓
Clarify the Idea
        ↓
Create Prompts for Video and Avatars
        ↓
Generate 3–4 Avatar Variations
        ↓
Select 2–3 Best References
        ↓
Team Approval
        ↓
Revisions
        ↓
Generate Part of the Video
        ↓
Team Approval
        ↓
Revisions
        ↓
Generate the Complete Video
        ↓
Final Review
        ↓
Revisions
        ↓
Editing
        ↓
Final Video
```

Both brand owners and the marketing team generally participated in the approval process.

---

## 3. Character and Avatar Workflow

After receiving the task, I prepared prompts for the required characters.

I initially generated several visual alternatives, usually 3–4 variations.

After an initial selection, I presented 2–3 of the strongest options to the team.

The team could:

- select an option;
- request changes to the character;
- change the visual direction;
- modify individual details.

Only after the characters were approved did I proceed to the next stage of video generation.

This became one of the first human-in-the-loop checkpoints in the production workflow.

---

## 4. Video Generation

I used several tools for video generation:

- Kling AI;
- HeyGen;
- Google Veo.

Different tools required different production workflows.

### Kling AI

When using Kling, a one-minute video had to be assembled from separate segments of approximately 15 seconds.

One one-minute video therefore required four primary segments.

In practice, each segment usually required at least one additional iteration after review.

A typical production cycle could therefore involve approximately:

```text
4 Required Segments
+
4 Revised Versions
=
Approximately 8 × 15-second Generations
```

before enough material was available for a final one-minute video.

The individual segments then had to be combined into a single video.

### HeyGen and Google Veo

With these tools, I experimented with longer generations and full video versions.

This reduced the number of individual scenes that had to be generated separately, although the complete result still required review and usually another 1–2 iterations.

---

## 5. Voice and Lip Sync

Voice generation became a separate part of the production workflow.

I used ElevenLabs to generate speech.

The audio was created separately from the video.

After obtaining an acceptable voice result, I synchronized the speech with the video using lip sync.

The simplified process was:

```text
Text / Dialogue
       ↓
ElevenLabs
       ↓
Audio
       +
Video
       ↓
Lip Sync
       ↓
Synchronized Scene
```

This approach emerged after early generations showed problems with voice quality and synchronization.

---

## 6. Iteration and Feedback

Almost none of the videos were produced successfully in a single generation.

The most common feedback from the team concerned:

- dynamics;
- text;
- movement of characters and objects.

The working cycle became:

```text
Generate
    ↓
Send to the Team
    ↓
Receive Feedback
    ↓
Adjust Prompt / Source Materials
    ↓
Regenerate
    ↓
Review Again
```

With Kling, this process happened separately for multiple 15-second segments.

With HeyGen or Veo, revisions could be applied to longer video versions.

---

## 7. Editing

After generating the required materials, I edited the final video myself.

My work therefore did not end when the AI model returned a generation.

The final production stage included:

- selecting usable generations;
- combining separate video segments;
- synchronizing video and voice;
- checking scene sequence;
- applying final revisions;
- preparing the finished video file.

---

## 8. Results of the Actual Workflow

Using this workflow, I produced 9 completed videos during the Proof-of-Concept stage.

All 9 were reviewed and accepted by the beFruitbe team.

One test video was published on:

- TikTok;
- Instagram;
- YouTube.

Based on the information available to me during the project, the video received approximately **3,000 cumulative views** across the three platforms.

The exact distribution of views between the platforms was not retained.

Publishing a single video was not a full test of the planned content strategy, but it provided an initial example of using the AI-generated content in real social-media channels.

---

## 9. What the Manual Workflow Revealed

Producing the 9 videos manually helped reveal the real structure of the process before attempting full automation.

Initially, the task could appear as simple as:

```text
Idea → AI → Video
```

In practice, many additional stages emerged:

```text
Idea
 ↓
Requirements Clarification
 ↓
Script
 ↓
Prompt
 ↓
Avatars
 ↓
Approval
 ↓
Scene Generation
 ↓
Additional Approval
 ↓
Voice
 ↓
Lip Sync
 ↓
Editing
 ↓
Revisions
 ↓
Final Approval
```

This experience directly influenced the architecture of the proposed automated workflow.

---

## 10. Proposed Automated Workflow

The future system was designed to reduce the amount of manual work required from the employee.

The proposed interaction was:

```text
Employee Sends a Request in Telegram
        ↓
System Receives the Request
        ↓
GPT Script Agent Analyzes the Request
        +
Uses the beFruitbe Knowledge Base
        ↓
Script and Generation Prompts Are Created
        ↓
Several Avatar / Reference Options Are Generated
        ↓
Telegram
        ↓
Human Approves an Option
        ↓
System Starts Video Generation
        ↓
Preview Video
        ↓
Telegram
        ↓
Human Reviews the Result
        ↓
[Changes Required?]
      ↙       ↘
    Yes        No
     ↓          ↓
New             Final
Iteration       Approval
                    ↓
             Automatic Publishing
                    ↓
       TikTok / Instagram / YouTube
```

---

## 11. What Was Intended to Be Automated

The future system was intended to handle most repetitive technical operations:

```text
Receive Request
→ Retrieve Brand Context
→ Prepare Script
→ Prompt Engineering
→ Generate References
→ Send Inputs to Generation Tools
→ Prepare Video
→ Process User Revisions
→ Publish
```

The employee would no longer need to manually switch between multiple AI services and transfer information from one tool to another.

---

## 12. What Was Intentionally Kept Human

The most important stage that I do not consider suitable for complete automation is the final review and approval.

Even if the technical pipeline could run fully autonomously, the resulting content still has to match:

- the real product;
- the brand;
- visual requirements;
- Tone of Voice;
- the current marketing objective.

During the Proof-of-Concept stage, I encountered model failures including:

- incorrect movement;
- visual artifacts;
- text problems;
- distorted packaging;
- voice-generation issues.

For this reason, human-in-the-loop checkpoints were intentionally included in the architecture.

The core principle became:

> Automate content production, but do not give AI the final decision about what the brand is ready to publish.

---

## 13. Target Workflow

The proposed workflow can therefore be summarized in three layers:

```text
AI
performs generation and repetitive technical work
        ↓
Human
approves key decisions
        ↓
System
continues the automated process
```

This approach was intended to increase content-production capacity while preserving human control over quality.
