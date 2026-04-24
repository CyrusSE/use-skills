# use-skills Reference

`use-skills` is a quality-first meta-skill. It reviews the full visible skill catalog, but it does not treat every skill as equally useful.

## Operating Model

The skill works in six layers:

1. `context`
   Analyze the current prompt, recent session behavior, expected output, user preferences, and project context.

2. `scan`
   Review all visible installed skills. Do not stop after the first plausible match.

3. `score`
   Evaluate each skill for:
   - domain fit
   - task fit
   - deliverable fit
   - constraint fit

4. `mode`
   Choose one of three skill-use modes:
   - `Recommended`
   - `Restricted`
   - `Strict`

5. `select`
   Place each skill into one of three buckets:
   - `primary`
   - `support`
   - `skip`

6. `synthesize`
   Let the `primary` set drive the result. Let `support` skills refine it without taking ownership.

## Activation Rules

Activate `use-skills` when:

- the user explicitly asks for `$use-skills`
- the request is obviously multi-domain and would benefit from cross-skill synthesis
- the prompt clearly benefits from several kinds of guidance working together
- stronger output quality depends on combining more than one relevant skill domain

Do not activate it as a broad default for every prompt.

The user does not need to mention the skill by name, but explicit invocation must also work.

## Matching Rules

### Primary

A skill belongs in `primary` when it is a strong match for the request and should directly shape the result.

Signals:

- it matches the core task
- it helps produce the exact deliverable the user wants
- it aligns with the strongest stated constraints

Keep the primary set small. Prefer `1` to `3` primary skills.

### Support

A skill belongs in `support` when it can improve the result but should not steer it.

Typical support contributions:

- clearer structure
- sharper wording
- stronger testing pressure
- better edge-case awareness
- tighter review discipline

Support skills can refine the result, but they do not own it.

### Skip

A skill belongs in `skip` when it is weak, irrelevant, or only superficially related.

Skipping is normal. `use-skills` is useful because it is selective, not because it forces broad coverage.

## Recommendation Modes

### Recommended

Use every skill that meaningfully improves the result.

This is the default mode when the user does not specify a restriction level.

Use it when:

- the task is broad or high stakes
- several skill domains clearly improve quality
- the user asks for the strongest output
- session context suggests previous answers need more structure, review, or precision

### Restricted

Use only the strongest primary skills, usually `1` to `3`.

Use it when:

- the user asks for focus or concision
- too many skills would create noise
- the task benefits from support guidance but should be driven by a small set

Support skills may quietly inform the result, but should not appear in `Using:` unless they materially shape the answer.

### Strict

Use only essential skills.

Use it when:

- the user asks for minimal skill involvement
- the prompt needs high precision
- only one domain skill is clearly necessary

If no skill is clearly necessary, fail closed.

## Session Context Signals

Use session context to improve skill recommendations.

Check:

- current prompt and requested deliverable
- recent user corrections or preferences
- last accepted mode and working set, when available
- previous output quality issues
- current repo, files, and task context
- whether the task needs planning, coding, review, docs, testing, design, research, or safety guidance
- whether the user asked for broad, restricted, or strict behavior
- whether the prompt meaning, expected output, or recommendation has materially changed

Do not rely only on skill names or keyword matches.

## Reuse And Reconfirmation

When `use-skills` has already run in the current session, reuse the last accepted mode and working set if the context is materially the same.

Do not ask the user to choose again when:

- the current prompt has the same meaning
- the expected output is the same type
- the selected mode still fits
- the selected skill set would not materially change

Ask again when:

- the prompt meaning changes
- the expected output changes
- session context changes the recommendation
- the selected mode or skill set should materially change

## Fail-Closed Gate

If no skill is strong enough to enter the `primary` set, `use-skills` should fail closed.

That means:

- do not force synthesis
- do not pretend broad review helped
- do not add a low-signal trace to the output

## Default Output Behavior

The default output starts with a short, visible working-set block when the skill activates.

That means:

- begin with:
  - `Mode: Recommended | Restricted | Strict`
  - `Using: use-skills, <selected skills>`
  - `For: <purposes>`
- return the improved answer, plan, patch, or recommendation immediately after
- keep the result centered on the request, not on the routing process
- do not show the block if the skill fails closed

## Conflict Resolution

When guidance conflicts, prefer:

1. direct user instructions
2. system, developer, or repository instructions
3. narrower domain skills over broader generic skills
4. explicit guidance over vague guidance

## Anti-Patterns

Avoid these failure modes:

- turning `use-skills` into a universal default router
- allowing support skills to dominate the answer
- reading loosely relevant skills too deeply
- forcing “something” from every visible skill
- exposing a long routing trace instead of a short working-set declaration

## Prompting Tips

These prompts usually work well:

- `$use-skills`
- `Turn this rough feature request into a clean implementation plan with testing and review discipline.`
- `Rewrite this README so it is clearer, more structured, and more actionable.`
- `Review this change and give me the strongest findings first.`
- `Fail closed if there is no strong primary skill set.`
- `Use restricted mode and recommend only the strongest skills.`
- `Use strict mode and only include skills that are clearly necessary.`
