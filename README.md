# use-skills

`use-skills` helps Codex choose a small set of relevant installed skills for complex work.

It is useful when a request spans more than one area, such as planning plus coding, review plus testing, or writing plus structure.

## At A Glance

- reviews the available skill list
- chooses a small working set
- supports three modes: `All related`, `Recommended`, and `Restricted`
- starts with a short working-set block when used
- combines selected guidance into one coherent result
- stays unused when no skill is a strong match

## Install

```bash
npx skills add https://github.com/CyrusSE/use-skills --global
```

## Basic Use

```text
$use-skills
Turn this feature request into an implementation plan with testing notes.
```

The skill can also be selected automatically when the request is clearly multi-domain.

## Modes

### All related

Uses every available skill that is meaningfully related to the request.

This is best when the user explicitly wants broad skill coverage.

### Recommended

Uses the best balanced working set for the request.

This is the default for broad quality improvement.

### Restricted

Uses only the strongest matches, usually one to three skills.

This is best when the user asks for focus or fewer skills.

## Output Shape

When used, the response begins with:

- `Mode: All related | Recommended | Restricted`
- `Using: use-skills, <selected skill>`
- `For: <short purpose>`

Then Codex continues with the answer, plan, patch, or recommendation.

## Good Fits

- planning a feature before implementation
- combining coding, testing, and review guidance
- improving a README or product spec
- reviewing a change with stronger structure
- choosing fewer skills for a focused answer

## Poor Fits

- narrow tasks where one skill is enough
- requests that only need a direct command
- work where no installed skill adds clear value

## Documentation Map

- [SKILL.md](./SKILL.md): runtime behavior
- [REFERENCE.md](./REFERENCE.md): selection model
- [examples/prompts.md](./examples/prompts.md): example prompts
