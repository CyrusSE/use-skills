---
name: use-skills
description: Recommends the right installed skills for complex requests, chooses a useful restriction level, and shows the selected skill set before working.
---

# Use Skills

Use this skill when the user explicitly invokes `$use-skills` or when the request is an obvious multi-domain fit and it would help to combine guidance from more than one installed skill instead of relying on a single obvious match.

## Core Idea

Do not stop at the first matching skill.

Treat the installed skill catalog as a review surface:

1. Analyze the current session, prompt, expected output, and available project context.
2. Inspect all visible installed skills.
3. Compare the current request against every skill.
4. Choose one of three skill-use modes.
5. Promote the right skills for that mode.
6. Synthesize the useful guidance into one coherent output.

The objective is breadth of review with disciplined synthesis, not blind coverage.

## When To Use This Skill

Activate when the user:

- explicitly invokes `$use-skills`
- asks for the best possible output and the task is obviously multi-domain, such as planning plus coding, review plus testing, or documentation plus structure
- wants a stronger answer than simple one-skill selection would provide
- presents a request where cross-skill synthesis is clearly useful even without naming this skill

The user does not need to name `use-skills` for it to activate, but explicit mention must also work.

Do not activate as a broad default for every non-trivial prompt. Activate only when the fit is obvious and strong enough to justify broad skill review.

## Operating Rules

- Optimize for best output quality, even if that means reading more than one relevant skill.
- Require at least one strong match to proceed.
- Keep the primary set small: prefer `1` to `3` primary skills.
- Allow weaker matches to contribute only as support.
- When the skill activates, announce the selected working set before the main answer.
- Keep that announcement short: one `Mode:` bullet, one `Using:` bullet, and one `For:` bullet.
- Stay inactive when no skill clears the strong-match threshold.
- Do not require an explicit invocation phrase from the user.
- Do not announce anything if this skill stays inactive.

## Required Workflow

### Step 1: Analyze The Current Session

Before selecting skills, inspect the current session context.

Consider:

- the current user prompt
- recent user preferences and corrections
- the last accepted mode and working set, if this skill already ran in the session
- previous assistant output issues or quality gaps
- current repo, task, and file context
- whether the task needs planning, coding, review, docs, testing, design, research, or safety guidance
- whether the user asked for more or less restriction
- whether the current prompt, expected output, or recommendation has materially changed

Use this analysis to recommend the right skill-use mode and working set.

### Step 2: Inventory The Skill Catalog

List the installed skills visible in the current environment.

For each skill, capture:

- skill name
- short description
- likely strengths
- obvious non-matches for the current request

Never stop early because one skill looks good enough.

### Step 3: Evaluate Every Skill

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
- if no skill qualifies as `primary`, leave this meta-skill inactive

Review each visible skill during evaluation, even if most end up as `skip`.

### Step 4: Choose A Skill-Use Mode

Choose one of these modes before announcing the working set:

1. `Recommended`
   Use every skill that meaningfully improves the result. Include primary skills and useful support skills. This is the default when the user does not specify a mode.

2. `Restricted`
   Use only the strongest primary skills, usually `1` to `3`. Support skills may inform the result, but should not appear in `Using:` unless they materially shape the output.

3. `Strict`
   Use only essential skills. Usually this means `use-skills` plus the single strongest domain skill. If no skill is clearly necessary, leave this meta-skill inactive.

Mode selection rules:

- default to `Recommended` for broad quality improvement
- use `Restricted` when the user asks for focus, concision, lower noise, or fewer skills
- use `Strict` when the user asks for minimalism, high precision, or only necessary skills
- reuse the last accepted mode and working set when the current context is materially the same
- ask again only when the context, prompt meaning, expected output, or recommended working set materially changes
- never use a mode to justify irrelevant skills

### Step 5: Read Only What Helps

Read only enough from `primary` and `support` skills to improve the answer.

Do not bloat the context window by loading full skill libraries when a short targeted read is enough.

### Step 6: Synthesize, Do Not Dump

Combine the useful guidance into one answer, artifact, or execution plan.

Your output should feel deliberate, not like stitched-together fragments.

Before the main answer, emit a short bullet block:

- `Mode: Recommended | Restricted | Strict`
- `Using: use-skills, <primary skill 1>, <primary skill 2>`
- `For: <purpose 1>, <purpose 2>`

Rules for the block:

- always include the selected mode
- always include `use-skills` itself when activated
- list only the selected working set, not the full scanned catalog
- include support skills only if they materially shape the result
- describe purposes in `For:` as functions, not repeated skill names
- do not include skipped skills
- do not include confidence scores or lengthy selection notes

Rules:

- lead with the improved answer or action
- remove duplicated advice
- resolve contradictions before responding
- keep the final output shaped around the user request, not around the skill catalog
- let primary skills drive the result
- let support skills sharpen quality, wording, structure, testing pressure, or edge-case coverage without taking ownership
- show detailed selection notes, scores, and skipped skills only when the user explicitly asks for them

### Step 7: Resolve Conflicts

When multiple skills disagree, use this order:

1. Direct user instructions
2. Higher-priority session and project-level instructions
3. Narrower domain skills over broader generic skills
4. Newer or more explicit skill instructions over vague ones

If two skills cannot be reconciled, follow the higher-priority guidance and keep the result consistent.

## Output Template

Use a compact structure like this:

1. `Mode:` bullet
2. `Using:` bullet
3. `For:` bullet
4. improved answer, plan, patch, or recommendation

If no skill earns a strong enough match, stay inactive and do not force synthesis.

## Quality Checks

- Do not force irrelevant domain advice into the result.
- Do not claim a skill was used if you only saw its name.
- Do not replace direct execution with analysis-only output when the user clearly wants implementation.
- Do not turn this into a popularity contest. The best result matters more than the biggest or most famous skill.
- Do not let support-level skills hijack the final answer.
- Do not keep reading loosely relevant skills deeply once they are clearly only background support.
- Leave this skill inactive when everything is weak, vague, or speculative.
- Do not let the upfront block become longer than the answer it introduces.
- Do not recommend a mode without considering the current session context.
- Do not include a support skill in `Using:` unless it materially changes the output.
- Do not repeatedly ask the user to choose a mode when the same recommendation still applies.
- Do ask again when the recommendation changes because the prompt, context, or expected output changed.

## Example Triggers

- `$use-skills`
- `Turn this rough feature spec into a clean implementation plan with strong testing and review discipline.`
- `Rewrite this README so it is clearer, more structured, and better documented.`
- `This request spans planning, implementation, and review. Improve the result if cross-skill synthesis is clearly useful.`
- `Review this change and give me the strongest findings first, but stay precise and well structured.`
- `Use fewer skills and keep this focused.`
- `Use only the essential skills for this request.`
