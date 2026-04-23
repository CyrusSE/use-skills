# use-skills Reference

`use-skills` is a quality-first meta-skill. It reviews the full visible skill catalog, but it does not treat every skill as equally useful.

## Operating Model

The skill works in four layers:

1. `scan`
   Review all visible installed skills. Do not stop after the first plausible match.

2. `score`
   Evaluate each skill for:
   - domain fit
   - task fit
   - deliverable fit
   - constraint fit

3. `select`
   Place each skill into one of three buckets:
   - `primary`
   - `support`
   - `skip`

4. `synthesize`
   Let the `primary` set drive the result. Let `support` skills refine it without taking ownership.

## Activation Rules

Activate `use-skills` when:

- the user explicitly asks for `use-skills`
- the user asks to combine skills or use all helpful skills
- the request is obviously multi-domain and would benefit from cross-skill synthesis

Do not activate it as a broad default for every prompt.

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

## Fail-Closed Gate

If no skill is strong enough to enter the `primary` set, `use-skills` should fail closed.

That means:

- do not force synthesis
- do not pretend broad review helped
- do not add a low-signal trace to the output

## Default Output Behavior

The default output stays clean and invisible.

That means:

- return the improved answer, plan, patch, or recommendation
- do not append a skill trace unless the user asks for one
- keep the result centered on the request, not on the routing process

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
- exposing noisy internal reasoning when the user only wants the result

## Prompting Tips

These prompts usually work well:

- `Use use-skills on this request and optimize for the strongest final output.`
- `Use use-skills if this prompt is an obvious multi-domain fit.`
- `Scan all visible skills, but keep weak matches support-only.`
- `Fail closed if there is no strong primary skill set.`
