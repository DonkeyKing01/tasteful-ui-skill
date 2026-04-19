# Design Context UI

**English** | [中文](./README.zh-CN.md)

![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Type: Skill](https://img.shields.io/badge/Type-Skill-blue)
![Focus: UI Design](https://img.shields.io/badge/Focus-UI%20Design-orange)

A UI design skill for AI coding agents.

It turns real project context, design-reference routing, and code-level implementation constraints into a workflow that is `reference-led, context-anchored`. The goal is not to blindly preserve the existing product UI, and it is also not to let references steamroll the product. The goal is to let references lead design direction while letting real project context anchor what the result must stay true to.

This project is mainly inspired by:

- [Claude Design Sys Prompt](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/Claude-Design-Sys-Prompt.txt)
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md)

## What This Project Does

**Design Context UI** helps an agent follow a UI workflow that is closer to real design collaboration:

- read project context carefully
- use mature design references to lead visual direction
- translate design language into implementation decisions

The workflow is:

1. Understand the request and target surface
2. Read project context to understand product truth, information architecture, reusable components, technical constraints, and useful existing signals
3. Route through `catalog.md`
4. Read only the closest 1 to 3 design references
5. Produce a design readout
6. Translate the references into implementation decisions in context
7. If the task enters exploration mode, show multiple directions first and then converge on one
8. Return to code and implement
9. Check both code quality and visual quality

## Problems It Solves

Many agents run into the same issues when doing UI work:

- They overfit to the current UI and never produce a stronger result
- They rely on vague words like "premium," "minimal," or "techy" without turning them into concrete design choices
- They read too many references and end up with style collage
- They mechanically preserve weak old design decisions just because they already exist in the product
- They produce something usable, but it still does not feel like a product that was intentionally designed

This skill is mainly designed to address those failures.

## Core Characteristics

- **Context anchoring**
  Read the real project carefully to understand product truth, information structure, constraints, implementation conditions, and the signals worth preserving.

- **Design references**
  Use the reference library to select and absorb the most suitable mature design languages.

- **Explicit design readout**
  Before touching code, state what is being borrowed, what is not being copied, and what the task is optimizing for.

- **Small routing set**
  Narrow through `catalog.md` and read only the closest 1 to 3 references.

- **Reference-to-implementation translation**
  Do not stop at style description. Turn color, typography, density, hierarchy, rhythm, and component character into implementation decisions.

- **Explore first, implement second**
  In exploration mode, directions must come before implementation.

- **Avoid product-safe mediocrity**
  The aim is not to stay close to old UI by default. The aim is to produce a stronger, clearer, more intentional result.

- **Visual and technical verification**
  Check not just whether it runs, but whether it has collapsed back into generic UI.

## Quick Start

### Install Into Codex

```bash
git clone https://github.com/DonkeyKing01/design-context-ui-skill.git
cp -r design-context-ui-skill/design-context-ui ~/.codex/skills/design-context-ui
```

### Install Into Claude Code

```bash
git clone https://github.com/DonkeyKing01/design-context-ui-skill.git
cp -r design-context-ui-skill/design-context-ui ~/.claude/skills/design-context-ui
```

### Manual Install

You only need to preserve this structure:

```text
design-context-ui/
  SKILL.md
  references/
    catalog.md
    designs/
      ...
```

The key files are [design-context-ui/SKILL.md](./design-context-ui/SKILL.md) and the full `references/` directory.

## How To Use It

### Design A New Page

```text
/design-context-ui

Create a landing page for our product
```

In that case, the skill will:

1. Read the project first to understand what the product is doing
2. Route through `references/catalog.md`
3. Read the closest 1 to 3 references
4. Produce a compact design readout
5. Implement a stronger direction in code

### Reconstruct An Existing Surface

```text
/design-context-ui

This is our current frontend page. Rebuild it with a Claude-like direction.
```

In that case, the skill will:

1. Read the project context first
2. Select the closest references
3. Extract transferable traits and brand details that should not be copied directly
4. Map the reference language onto the current technical stack
5. Implement a stronger direction

### Explore Multiple Design Directions

```text
/design-context-ui

For this new page, show me 2 to 3 directions first, then implement the best one.
```

In that case, the skill will:

1. Enter `design exploration`
2. Produce 2 to 3 directions with clear differences
3. Explain the rationale for each direction
4. Converge on one direction based on user feedback or context
5. Implement the chosen direction

## How The Skill Works

It follows one main path:

`Understand user needs -> Read real project context -> Route through catalog.md -> Read the closest design references -> Choose delivery mode -> Externalize the design readout -> Extract implementation decisions from references in context -> If exploring, present directions and choose one -> Implement in the existing stack -> Verify code and visual quality -> Handoff briefly`

Compared with "just give the agent a design reference," design-context-ui emphasizes:

- **Read the product first, but do not get trapped by the old UI**
- **Let references lead design judgment**
- **Write the design readout before writing code**
- **Explore before implementing**
- **Make the final output implementation-ready code, not a moodboard**

## Reference Library

The current reference library covers multiple common product families, including:

- AI / LLM Platform
- Developer Tools / IDE
- Backend / Database / DevOps
- Productivity / SaaS
- Design / Creative Tools
- Fintech / Crypto
- E-commerce / Retail
- Media / Consumer Tech
- Automotive

The routing index lives in [catalog.md](./design-context-ui/references/catalog.md).

Each detailed design reference typically includes:

- overall mood and visual character
- color system and semantic roles
- typography hierarchy and practical substitutes
- component styling for buttons, cards, inputs, navigation, and more
- grid, whitespace, radius, and density rhythm
- shadows, elevation, and surface treatment
- style boundaries and transferable principles

## Project Structure

```text
design-context-ui-skill/
  design-context-ui/
    SKILL.md
    references/
      catalog.md
      designs/
        ai_llm_platforms/
        productivity _ saas/
        developer tools _ ides/
        ...
  ref/
    Claude-Design-Sys-Prompt.txt
    ...
```

- `design-context-ui/SKILL.md`
  The main workflow and behavior rules for the skill
- `design-context-ui/references/catalog.md`
  The routing index used to choose the most relevant references first
- `design-context-ui/references/designs/*`
  The detailed design reference files, each describing one branded visual language
- `ref/Claude-Design-Sys-Prompt.txt`
  Source material that influenced the writing style, pacing, and design-director tone of this skill

## Project Intent

The starting point of this project is simple:

I wanted to preserve the value of "read the real project context first," but stop letting the current UI automatically become the default aesthetic source.

design-context-ui is not a full design system, and it is not a magic aesthetic prompt.
It is closer to a reusable workflow shell that emphasizes three things:

- understand product truth first
- let references lead design
- translate the design into code

## License

MIT
