# Contributing

`use-skills` works only if it stays narrow and predictable.

## Contribution Rules

- Keep the repository focused on cross-skill discovery, classification, and synthesis.
- Prefer examples that show how multiple skills improve one realistic request.
- Avoid adding runtime-specific behavior unless it is clearly marked as optional.
- Keep the instructions readable in one pass. This repo should stay lightweight.
- When you change the behavior, update the README and examples in the same pull request.
- Keep `README.md`, `REFERENCE.md`, and `SKILL.md` aligned. The public docs should never describe a different model from the runtime instructions.
- Preserve the gating model: small primary set, support-only weak matches, fail closed when no strong fit exists.

## Good Contributions

- Better examples for planning, coding, design, review, or documentation tasks
- Clearer conflict-resolution rules when multiple skills disagree
- Small documentation improvements that make installation or usage easier
- Sharper matching rules that improve quality without increasing noise

## Changes To Avoid

- Turning the repo into a CLI, plugin, or framework
- Adding long catalogs of unrelated advice
- Forcing irrelevant skills into every output
- Expanding the primary set so far that the skill becomes a noisy default router

## Review Checklist

- The change improves the quality of the synthesized output.
- The change does not make the skill harder to understand.
- The public documentation still matches the `SKILL.md` behavior.
- The change does not weaken the fail-closed gate or the support-only restriction for weak matches.
