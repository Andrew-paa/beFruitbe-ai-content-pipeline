# Example 01 — Tony Pineapple

[Русская версия](README_RU.md)

## Status

**Real beFruitbe production case**

**Final version:** accepted by the company  
**Published:** TikTok / Instagram / YouTube  
**Result:** approximately 3,000 cumulative views across the three platforms

---

## Original Task

The team provided a short creative brief:

> Create a short video using the mechanics of a cinematic press-conference edit followed by a dynamic sequence focused on the main character.

A recognizable superhero press-conference scene was used as a creative reference for pacing and dramatic structure.

The goal was not to reproduce the original footage but to adapt its storytelling and editing mechanics to original beFruitbe characters.

---

## Concept

The main character became:

### Tony Pineapple

An anthropomorphic pineapple designed as a confident central character.

Other characters included:

### Strawberry Reporter

An anthropomorphic strawberry acting as the reporter.

### Press Room

The room was populated by other anthropomorphic fruit characters acting as journalists and interviewers.

---

## Video Structure

The concept consisted of two main sections.

### Part 1 — Press Conference

The main character faces the press.

The reporter asks a question.

Tony Pineapple delivers the central reveal, which triggers the transition to the second part of the video.

### Part 2 — Character Edit

A dynamic music-driven sequence presents Tony Pineapple through multiple short cinematic scenes.

The purpose of this section was to establish a memorable character identity and a recognizable content style.

---

## Production Workflow

The actual production process was:

```text
Creative Brief
        ↓
Adapt Concept for beFruitbe
        ↓
Character Design
        ↓
Generate Character References
        ↓
Validate Character Appearance
        ↓
Prepare Prompts
        ↓
Generate Video Scenes in Kling
        ↓
Check Continuity
        ↓
Adjust Prompts
        ↓
Regenerate
        ↓
Generate Voice Separately
        ↓
Lip Sync
        ↓
Editing
        ↓
Final Version
        ↓
Company Approval
```

---

## Character Reference Pipeline

Before generating video, I first established the visual appearance of the key characters.

Each main character was generated from several angles.

For two main characters, the workflow was approximately:

```text
Character
    ↓
Front View
Side View
Alternative View
    ↓
Multiple generations per angle
    ↓
Select the strongest references
```

Approximately **18 character/reference images** were generated during this stage.

The purpose was to improve character consistency across separate video scenes.

---

## Tools

### Script & Prompt Preparation

**Custom GPT Script & Prompt Agent**

Used for script development and generation-prompt preparation.

### Character Generation

**Kling AI**

Used to create visual character concepts and reference images.

### Video Generation

**Kling AI**

Used for the main generated video scenes.

### Voice

**ElevenLabs**

Voice was generated separately from the video.

### Lip Sync

Speech was synchronized with the generated video during a separate stage.

### Editing

I assembled and edited the final video myself.

---

## Generation Volume

The final result required approximately:

```text
≈18 character/reference images
+
≈4–5 video generations
+
voice generation
+
lip sync
+
final editing
```

This illustrates that even a short AI-generated video can require several production and review stages.

---

## Main Technical Challenge

The main challenge was maintaining a consistent environment between generations.

In some early versions, the background changed between scenes.

This reduced visual continuity.

---

## Solution

I refined the prompts by specifying the environment more precisely, including:

- scene context;
- spatial characteristics;
- object placement;
- visual properties of the background.

After several prompt iterations, the environment became significantly more stable.

---

## Why Character References Were Created First

One of the common problems in generative video is character inconsistency between scenes.

Instead of independently generating each scene from a fresh textual description, I first created reusable character-reference sets.

The approach became:

```text
First:
lock the character identity

Then:
generate scenes using that identity
```

rather than:

```text
describe the character from scratch every time
```

This helped preserve:

- character shape;
- major visual features;
- overall visual style;
- recognizability across scenes.

---

## Human-in-the-Loop

Although AI was used throughout the production process, final decisions remained human-controlled.

I reviewed:

- character appearance;
- continuity;
- environment;
- movement;
- generation quality;
- alignment with the creative concept.

The completed result was then reviewed and accepted by the beFruitbe team.

---

## Result

The final version was accepted by the company.

The video was published on:

```text
TikTok
Instagram
YouTube
```

Based on the data available to me, it received approximately **3,000 cumulative views** across the three platforms.

The exact platform-level breakdown was not retained.

This was the first published test of AI-generated content produced during the project.

---

## Key Learning

This case demonstrated the importance of preparing character references before video generation.

Instead of:

```text
Prompt → Video
```

a more reliable process became:

```text
Character Design
      ↓
Reference Set
      ↓
Scene Prompt
      ↓
Video Generation
      ↓
Continuity Check
      ↓
Iteration
```

It also demonstrated how strongly environmental detail in a prompt can affect scene consistency across separate generations.

---

## Media

### Final Video

`final-video.mp4`

### Character References

See:

[`assets/`](assets/)

---

## Copyright Note

The original movie scene was used only as a creative reference for pacing and storytelling mechanics.

Original copyrighted movie footage and protected music are not included in this public repository unless appropriate usage rights are available.
