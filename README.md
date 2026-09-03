# beFruitbe AI Content Pipeline

**Prototype of an AI-powered content production system for the beFruitbe brand.**

The project explores how LLM agents, a structured brand knowledge base and workflow automation can be combined to automate parts of video content production while keeping a human in control of key decisions.

## Project Overview

In July–August 2026, I worked with the beFruitbe team on the concept and prototype of an AI-powered content factory.

The company wanted to understand how generative AI could be practically integrated into its content-production workflow and whether it made sense to invest in a fully automated system.

The initial task was to:

- understand how different AI tools could be used in the company's workflow;
- design the concept of an AI content factory;
- prepare the brand information for use by AI agents;
- prototype key parts of the system;
- test the concept on real content examples.

The proposed system was designed to take a natural-language content request from a user, retrieve relevant information from the company's knowledge base, develop a creative concept and script, prepare detailed generation instructions and then generate video content after human approval.

## My Role

I worked on the project independently as an **AI consultant and AI automation specialist** and was responsible for the technical exploration and prototype design.

I communicated directly with the CEO, the Marketing Director and other members of the management team to understand the business requirements and translate them into the concept of an AI-powered system.

My work included:

- researching and comparing generative AI tools;
- structuring company and brand information for AI usage;
- preparing a knowledge base;
- creating a custom GPT;
- creating an AI agent prototype;
- designing the logic and architecture of the content pipeline;
- prototyping parts of the workflow in n8n;
- developing prompts and agent instructions;
- testing image and video generation approaches;
- producing 9 complete AI-generated video examples for the brand.

The project took approximately **60 hours** of research, prototyping, testing and content production.
## System Design

The project was designed around the idea that content generation should not start from an empty prompt.

Instead, AI tools should have access to structured information about the brand and use this context at different stages of the content-production process.

The proposed system consisted of several components:

### 1. Brand Knowledge Base

Brand-related information and project materials were organized into several folders to make them easier to use as context for AI tools.

The knowledge base was intended to become the source of verified information for the content-generation workflow.

Its purpose was to reduce the risk of AI models inventing product or brand information and to make generated content more consistent.

### 2. Video Prompt & Script Assistant

I created a custom GPT that worked as a script and prompt preparation assistant for video generation.

The user provided a brief describing what they wanted to see in the final video.

The GPT then transformed this brief into a more structured and detailed prompt suitable for video-generation models.

Its task was to translate a human creative request into generation instructions that included the necessary details for producing the video.

### 3. Content Performance Analysis Agent

### 3. Content Performance Analysis Agent Prototype

I designed a prototype of a content-performance analysis agent in Claude.

The agent was intended to analyze performance metrics of published videos, including:

- views;
- likes;
- engagement indicators;
- differences in performance between content examples.

The purpose of the agent was to identify patterns in audience response and use these insights when planning future content.

At the current project stage, the agent has not yet been tested on production data because the automated video-generation system was not launched and the test content was not published as part of the pipeline.

This component therefore remains a concept / prototype for a future feedback loop:

`Generate → Publish → Measure → Analyze → Improve future content`

### 4. n8n Workflow Prototype

I created a small proof-of-concept workflow in n8n to explore how data could be retrieved from a knowledge base and passed to the next stage of an automated AI workflow.

This was an early technical prototype rather than a complete automation system.

The goal was to test the basic principle:

`Knowledge Base → Retrieve relevant context → Pass context to the next AI stage`

### 5. Human Review

Human approval was an important part of the proposed workflow.

The system was not intended to generate and publish content completely autonomously.

The user should be able to review the concept, source materials and intermediate results, request changes and approve the final direction before continuing to the next generation stage.
## Video Production Process

The automated pipeline was still at the prototype stage, so the 9 demonstration videos were produced through a human-guided AI workflow.

A typical production cycle looked like this:

1. I received a video task from the company.
2. I clarified the idea and discussed what the team expected to see in the final result.
3. We agreed on the source materials and visual direction.
4. I generated multiple image variations and visual concepts.
5. The team reviewed the materials and selected the preferred versions.
6. I created and refined the characters / avatars required for the video.
7. I generated the video using AI tools.
8. The result was reviewed by the team.
9. Based on their feedback, I changed the source materials, prompts or generation approach and created new iterations.
10. The process continued until we reached an approved result.

This process helped me understand which stages could later be automated and which stages still benefited from human creative and quality control.
## Proposed End-to-End Workflow

```text
User Request
     ↓
Request Analysis
     ↓
Brand Knowledge Base
     ↓
Creative / Script Stage
     ↓
Video Prompt Preparation
     ↓
Concept & Source Materials
     ↓
Human Review
     ↓
Video Generation
     ↓
Human Feedback
     ↓
Iteration / Final Result
     ↓
Performance Analysis
     ↓
Insights for Future Content
## Building the Brand Knowledge Base

Before designing the AI workflow, I needed to prepare structured brand context that could later be used by AI agents.

I first created a set of questions and requirements describing what information would be needed for the knowledge base and sent them to the company.

After receiving the initial materials, I conducted interviews with both brand owners to collect additional context and clarify the information.

The knowledge base was organized into several folders and included:

- brand history;
- information from interviews with the founders;
- product information;
- flavours;
- product and brand photos;
- logos;
- Tone of Voice;
- other materials required to provide AI systems with brand-specific context.

The goal was to make the AI workflow rely on actual company information instead of generating content only from a generic user prompt.
## Tools & Technologies

### LLMs and AI Assistants

- **ChatGPT / Custom GPTs** — prompt development and creation of a custom video prompt assistant
- **Claude** — agent prototyping, analysis and development of AI workflow logic
- **Gemini** — research and experimentation
- **Perplexity** — research and information discovery

### Generative Video

- **Kling AI** — AI video generation
- **Google Veo** — AI video generation and experimentation
- **HeyGen** — avatar-based video generation

### Automation

- **n8n** — early proof-of-concept workflow for passing information from the knowledge base to subsequent AI stages

### Project Design

- brand knowledge-base design;
- prompt engineering;
- LLM agent design;
- human-in-the-loop workflow design;
- AI content workflow prototyping;
- iterative testing of generative video.
## Challenges and Iterations

One of the most useful parts of the project was discovering the practical limitations of generative video models.

The first generations were significantly less predictable than I expected.

### Video dynamics

Some of the early results looked more like animated slideshows than natural videos.

I had to experiment with the generation approach and prompts to achieve more dynamic scenes and more natural movement.

### Voice generation

Some generations had problems with voice and speech quality.

This required additional iterations and adjustments before the result was suitable for the project.

### Visual artifacts

Generative video models occasionally produced visual artifacts, including:

- incorrect or unnatural limbs;
- inconsistent character details;
- distorted objects;
- other generation errors.

These problems required reviewing the output, changing the source materials or generation instructions and generating new versions.

### Product packaging and text

One of the most noticeable problems was the generation of product packaging.

AI models could distort:

- text on cans;
- typography;
- labels;
- visual details of the product.

In some generations, text became incorrect or unreadable.

This required additional control of source materials and multiple iterations to reach acceptable results.

### Iterative workflow

In practice, producing a usable AI-generated video was rarely a one-prompt process.

A typical workflow became:

`Generate → Review → Identify problems → Adjust inputs/prompts → Regenerate → Review again`

This experience became one of the reasons why human review remained an important part of the proposed automated pipeline.
## What I Learned

Before starting this project, I expected AI-based content production to be significantly easier.

In practice, I learned that getting a useful result from generative AI requires much more than choosing a model and writing a prompt.

The project taught me the importance of:

- clearly understanding the business task before choosing AI tools;
- collecting and structuring the right context for AI systems;
- breaking a complex process into separate stages;
- testing different tools instead of relying on a single model;
- reviewing generated results critically;
- iterating on prompts and source materials;
- keeping human approval in parts of the workflow where quality and accuracy matter.

The project also gave me experience working directly with a management team.

I learned to clarify requirements, present technical ideas in understandable language, discuss results, receive critical feedback and make changes based on that feedback.

Working on unfamiliar problems under time pressure also taught me to stay focused when the first solution did not work and continue experimenting until I found a better approach.
## Results and Deliverables

The proof-of-concept stage resulted in a set of practical deliverables rather than only a theoretical system design.

During the project, I delivered:

- a structured brand knowledge base based on company materials and interviews with both founders;
- a custom GPT for transforming creative briefs into detailed prompts for video-generation models;
- a prototype of a content-performance analysis agent in Claude;
- an initial n8n proof of concept for passing brand context into an AI workflow;
- the proposed architecture of an AI-powered content production pipeline;
- prompt-engineering approaches for generative video;
- multiple visual concepts, characters and avatars for video production;
- 9 complete AI-generated videos created through an iterative production process.

All 9 demonstration videos were reviewed and accepted by the company.

The results were then used as practical reference material while refining the brand's visual direction and Tone of Voice for future AI-generated content.

The video examples also helped identify which parts of the workflow could potentially be automated and where human review remained important.
## Project Status

The project reached the prototype / proof-of-concept stage.

The main concepts were researched, the proposed workflow was designed, key AI components were prototyped, and 9 demonstration videos were successfully produced and accepted by the company.

A complete end-to-end automated content pipeline was not deployed to production.

After the proof-of-concept stage, the company decided to reconsider which parts of the content-production process should be automated and how the system should fit into its existing workflow.

Further technical implementation was therefore paused while the business requirements were being refined.

The content-performance analysis agent also remains untested on real publication data because the automated publishing and analytics loop has not yet been launched.
## Demo

The repository will include all 9 video examples produced during the proof-of-concept stage.

For each example, I plan to document:

- the original task;
- the creative approach;
- AI tools used;
- generation process;
- problems found during generation;
- iterations and corrections;
- final accepted result.

This makes it possible to compare the initial task with the final output and see how the workflow evolved through experimentation.
