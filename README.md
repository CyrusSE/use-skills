# use-skills

`use-skills` is a meta-skill for agents that want more than one obvious match.

Instead of picking a single installed skill and stopping there, `use-skills` tells the agent to inspect the full visible skill catalog, review every skill against the current request, and synthesize the useful guidance into one stronger result.

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

1. inspect all visible installed skills
2. review every skill against the current prompt
3. classify each skill as `apply`, `support`, or `skip`
4. read only the helpful skills deeply enough to improve the work
5. return one coherent output instead of a pile of disconnected advice

## Install

Install from GitHub:

```bash
npx skills add https://github.com/CyrusSE/use-skills --global
```

## Example Prompts

```text
Use use-skills on this request: turn this rough product idea into a clean implementation plan.
```

```text
Use use-skills to improve this README draft with every helpful installed skill.
```

```text
Use use-skills to review this feature request with all available installed skills before you code.
```

## How The Skill Thinks

`use-skills` does not blindly paste every skill into the answer.

It reviews all visible skills, then merges only the guidance that actually improves the current request. That keeps the output stronger without turning it into noise.

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

## Poor Use Cases

- forcing irrelevant skills into a narrow task
- replacing direct execution with endless analysis
- loading huge skill libraries when one targeted read is enough

## Repository Structure

```text
use-skills/
├── SKILL.md
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
