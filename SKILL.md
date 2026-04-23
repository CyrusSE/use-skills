---
name: use-skills
description: Reviews every visible installed skill, extracts the guidance that can improve the current request, and synthesizes one stronger final output.
---

# Use Skills

Use this skill when the user wants the strongest possible result and it would help to combine guidance from more than one installed skill instead of relying on a single obvious match.

## Core Idea

Do not stop at the first matching skill.

Treat the installed skill catalog as a review surface:

1. Inspect all visible installed skills.
2. Compare the current user request against every skill.
3. Decide how each skill should influence the work.
4. Synthesize the useful guidance into one coherent output.

The objective is breadth of review with disciplined synthesis.

## When To Use This Skill

Activate when the user:

- explicitly asks to use all skills, combine skills, or improve the result with every available skill
- asks for the best possible output and the task spans multiple domains like planning, coding, review, docs, UX, testing, or research
- wants a stronger answer than simple one-skill routing would provide

## Required Workflow

### Step 1: Inventory The Skill Catalog

List the installed skills visible in the current environment.

For each skill, capture:

- skill name
- short description
- likely strengths
- obvious non-matches for the current request

Never stop early because one skill looks good enough.

### Step 2: Evaluate Every Skill

For each visible skill, assign one of these labels:

- `apply`: directly improves the current request and should shape the result
- `support`: not the main driver, but has guidance worth borrowing
- `skip`: reviewed, but not useful for this specific request

Do not silently ignore skills. Review all of them, even if most end up as `skip`.

### Step 3: Read Only What Helps

Read only enough from `apply` and `support` skills to improve the answer.

Do not bloat the context window by loading full skill libraries when a short targeted read is enough.

### Step 4: Synthesize, Do Not Dump

Combine the useful guidance into one answer, artifact, or execution plan.

Your output should feel deliberate, not like stitched-together fragments.

Rules:

- lead with the improved answer or action
- briefly name the skills that materially influenced the result
- remove duplicated advice
- resolve contradictions before responding
- keep the final output shaped around the user request, not around the skill catalog

### Step 5: Resolve Conflicts

When multiple skills disagree, use this order:

1. Direct user instructions
2. System, developer, or repository instructions
3. Narrower domain skills over broader generic skills
4. Newer or more explicit skill instructions over vague ones

If two skills cannot be reconciled, say which one you followed and why.

## Output Template

Use a compact structure like this:

1. improved answer, plan, patch, or recommendation
2. brief note on which skills influenced the result
3. fallback note if most skills were reviewed and skipped

## Guardrails

- Do not force irrelevant domain advice into the result.
- Do not claim a skill was used if you only saw its name.
- Do not replace direct execution with analysis-only output when the user clearly wants implementation.
- Do not turn this into a popularity contest. The best result matters more than the biggest or most famous skill.

## Example Triggers

- `Use all available skills to improve this feature spec before implementation.`
- `Run this request through every helpful installed skill and give me the strongest final answer.`
- `I do not want one router pick. I want the combined benefit of the skills I already installed.`
