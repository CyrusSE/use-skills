# use-skills

`use-skills` is a meta-skill for agents that want more than one obvious match.

Instead of picking a single installed skill and stopping there, `use-skills` tells the agent to inspect the full visible skill catalog, review every skill against the current request, and synthesize the useful guidance into one stronger result.

## At A Glance

- scans all visible skills before deciding
- analyzes the current session, prompt, and expected output
- recommends one of three modes: `Recommended`, `Restricted`, or `Strict`
- keeps a small `primary` set of strong matches
- allows weaker matches to help only as `support`
- optimizes for best output quality, not just speed
- fails closed if no skill is a strong enough fit
- announces the selected skill set at the start in a short bullet block
- activates on explicit mention or obvious fit

## Why It Exists

Single-skill routing is fast, but it often misses additive improvements.

One request can benefit from:

- planning structure from a planning skill
- implementation discipline from a coding skill
- sharper wording from a writing skill
- QA pressure from a review or testing skill

`use-skills` is built for that overlap.

## What It Does

When activated, the skill tells the agent to:

1. analyze the current session, prompt, expected output, and project context
2. inspect all visible installed skills
3. score every skill against the current prompt
4. recommend a skill-use mode
5. promote the right skills for that mode
6. fail closed if no skill is strong enough
7. return one coherent output instead of a pile of disconnected advice

## Quick Start

Install from GitHub:

```bash
npx skills add https://github.com/CyrusSE/use-skills --global
```

Then use a prompt like:

```text
Turn this feature request into the strongest possible implementation plan with testing and review discipline.
```

## Activation Model

`use-skills` is not meant to run on every prompt.

It should activate when:

- the user explicitly asks for `$use-skills`
- the request is obviously multi-domain and would benefit from cross-skill synthesis
- the user asks for stronger output quality and the request clearly spans multiple kinds of work
- the prompt would obviously benefit from planning, implementation, review, documentation, or testing guidance working together

It should not become a broad default router for every non-trivial task.

The user should not need to know the skill exists for it to help, but explicit invocation should also work.

## Restriction Model

This skill is intentionally gated:

- optimize for best output quality over speed
- keep the `primary` set small, usually `1` to `3` skills
- allow weak matches to help only as `support`
- show a short upfront bullet block when the skill activates
- fail closed if nothing is a strong match

That restriction model is what keeps the skill useful instead of noisy.

## Recommendation Modes

`use-skills` gives the agent three choices before it starts:

### 1. Recommended

Use every skill that meaningfully improves the result.

Best for broad, high-quality work where several skill domains can help. This is the default when the user does not specify a mode.

### 2. Restricted

Use only the strongest primary skills, usually `1` to `3`.

Best when the user wants focus, concision, lower noise, or fewer skills. Support skills may still quietly inform the result when they materially improve quality.

### 3. Strict

Use only essential skills.

Best when the user wants minimalism or high precision. Usually this means `use-skills` plus one strongest domain skill, or no activation if nothing is clearly necessary.

## Session Context Analysis

Before recommending a mode or skill set, `use-skills` should inspect the current session:

- current prompt
- recent user preferences and corrections
- last accepted mode and working set, if this skill already ran in the session
- previous output issues or quality gaps
- current repo, files, and task context
- expected deliverable
- whether the task needs planning, coding, review, docs, testing, design, research, or safety guidance
- whether the prompt, expected output, or recommendation has materially changed

This keeps recommendations grounded in what is happening now, not just generic keyword matching.

## Reuse Behavior

If the user mentions the skill again and the context has not materially changed, reuse the same mode and working set.

Do not ask the user to choose again just because the skill was mentioned again.

Ask again only when something important changes:

- the prompt means something different
- the expected output changes
- the session context changes
- the recommended mode or skill set changes

## Upfront Announcement

When `use-skills` activates, it should announce the selected working set before the main answer:

- `Mode: Recommended | Restricted | Strict`
- `Using: use-skills, <skill 1>, <skill 2>`
- `For: <purpose 1>, <purpose 2>`

This block should be:

- short
- honest
- limited to the skills that materially shape the answer
- shown only when the skill actually activates

## Example Prompts

```text
Turn this rough product idea into a clean implementation plan.
```

```text
Rewrite this README draft so it is clearer, more structured, and more actionable.
```

```text
Review this feature request before coding and make the result stronger if multiple skill domains clearly apply.
```

```text
$use-skills
```

```text
Use restricted skills for this. Keep only the strongest recommendations.
```

```text
Use strict mode and only include skills that are clearly necessary.
```

## How The Skill Thinks

`use-skills` does not blindly paste every skill into the answer.

It reviews all visible skills, then merges only the guidance that actually improves the current request. Strong matches drive the result. Weaker matches can refine it, but they do not take ownership.

Conflict resolution order:

1. direct user instructions
2. system, developer, or repo instructions
3. narrower domain skills over generic skills
4. explicit instructions over vague guidance

## Good Use Cases

- turning a rough request into a stronger plan before implementation
- combining coding, testing, review, and documentation guidance in one pass
- improving deliverables when multiple installed skills are clearly relevant
- getting a more disciplined answer than a single-skill pick would give
- protecting quality by refusing to force synthesis when no strong skill fit exists

## Poor Use Cases

- forcing irrelevant skills into a narrow task
- replacing direct execution with endless analysis
- loading huge skill libraries when one targeted read is enough
- running it as a universal default on every non-trivial prompt

## What Counts As A Strong Match

A skill is strong enough for the `primary` set when it materially helps with:

- the domain of the task
- the type of work being requested
- the exact deliverable the user wants
- the most important constraints, such as quality, testing, structure, clarity, or safety

If nothing meets that bar, `use-skills` should fail closed rather than force a weak synthesis.

## Automatic By Design

`use-skills` should feel natural, not ceremonial.

That means:

- the user does not need to say `use-skills`
- but explicitly saying `$use-skills` should always work
- the skill should activate when the fit is obvious
- the skill should stay out of the way when the fit is weak
- the safety gate remains the same: at least one strong primary match or no activation

## Documentation Map

- [SKILL.md](./SKILL.md): the runtime instructions
- [REFERENCE.md](./REFERENCE.md): the decision model, gating rules, and anti-patterns
- [examples/prompts.md](./examples/prompts.md): ready-to-use prompts
- [CONTRIBUTING.md](./CONTRIBUTING.md): contribution rules

## Repository Structure

```text
use-skills/
├── SKILL.md
├── REFERENCE.md
├── README.md
├── CONTRIBUTING.md
├── LICENSE
├── examples/
│   └── prompts.md
└── .gitignore
```

## Design Position

This repo is intentionally small.

It is not a plugin, a package manager, or a runtime framework. It is a clean skill that improves output quality by forcing broad skill review before synthesis.

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md).
