---
name: use-skills
description: Scans all visible installed skills, promotes only the strongest matches into a small primary set, uses weaker matches as support only, and fails closed when no strong fit exists.
---

# Use Skills

Use this skill when the user wants the strongest possible result and it would help to combine guidance from more than one installed skill instead of relying on a single obvious match.

## Core Idea

Do not stop at the first matching skill.

Treat the installed skill catalog as a review surface:

1. Inspect all visible installed skills.
2. Compare the current user request against every skill.
3. Promote only the strongest matches into a small primary set.
4. Allow weaker but still useful matches to contribute as support only.
5. Synthesize the useful guidance into one coherent output.

The objective is breadth of review with disciplined synthesis, not blind coverage.

## When To Use This Skill

Activate when the user:

- explicitly asks to use `use-skills`, use all skills, combine skills, or improve the result with every available skill
- asks for the best possible output and the task is obviously multi-domain, such as planning plus coding, review plus testing, or documentation plus structure
- wants a stronger answer than simple one-skill routing would provide

Do not activate as a broad default for every non-trivial prompt.

## Hard Restrictions

- Optimize for best output quality, even if that means reading more than one relevant skill.
- Require at least one strong match to proceed.
- Keep the primary set small: prefer `1` to `3` primary skills.
- Allow weaker matches to contribute only as support.
- Keep the final output invisible by default: do not append a skill trace unless the user asks for one.
- Fail closed when no skill clears the strong-match threshold.

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

For each visible skill, score it on these dimensions:

- `domain fit`: does it match the subject area?
- `task fit`: does it match what the user is trying to do?
- `deliverable fit`: does it help produce the exact output type?
- `constraint fit`: does it help with priorities like quality, clarity, testing, safety, or structure?

Then assign one of these labels:

- `primary`: a strong match that should directly shape the result
- `support`: useful but not strong enough to steer the result
- `skip`: reviewed, but not useful for this specific request

Rules:

- promote only the strongest matches into the primary set
- cap the primary set at `1` to `3` skills
- if two strong skills overlap heavily, prefer the narrower one and downgrade the broader one to support
- if no skill qualifies as `primary`, fail closed and do not apply this meta-skill

Do not silently ignore skills during evaluation, even if most end up as `skip`.

### Step 3: Read Only What Helps

Read only enough from `primary` and `support` skills to improve the answer.

Do not bloat the context window by loading full skill libraries when a short targeted read is enough.

### Step 4: Synthesize, Do Not Dump

Combine the useful guidance into one answer, artifact, or execution plan.

Your output should feel deliberate, not like stitched-together fragments.

Rules:

- lead with the improved answer or action
- remove duplicated advice
- resolve contradictions before responding
- keep the final output shaped around the user request, not around the skill catalog
- let primary skills drive the result
- let support skills sharpen quality, wording, structure, testing pressure, or edge-case coverage without taking ownership
- stay invisible by default unless the user explicitly asks which skills were used

### Step 5: Resolve Conflicts

When multiple skills disagree, use this order:

1. Direct user instructions
2. System, developer, or repository instructions
3. Narrower domain skills over broader generic skills
4. Newer or more explicit skill instructions over vague ones

If two skills cannot be reconciled, follow the higher-priority guidance and keep the result consistent.

## Output Template

Use a compact structure like this:

1. improved answer, plan, patch, or recommendation
2. nothing extra unless the user asked for a trace

If no skill earns a strong enough match, fail closed and do not force synthesis.

## Guardrails

- Do not force irrelevant domain advice into the result.
- Do not claim a skill was used if you only saw its name.
- Do not replace direct execution with analysis-only output when the user clearly wants implementation.
- Do not turn this into a popularity contest. The best result matters more than the biggest or most famous skill.
- Do not let support-level skills hijack the final answer.
- Do not keep reading loosely relevant skills deeply once they are clearly only background support.
- Do not proceed under this skill when everything is weak, vague, or speculative.

## Example Triggers

- `Use all available skills to improve this feature spec before implementation.`
- `Run this request through every helpful installed skill and give me the strongest final answer.`
- `I do not want one router pick. I want the combined benefit of the skills I already installed.`
- `This request spans planning, implementation, and review. Use use-skills if that will improve the result.`
