# Example Prompts

These examples are written to reinforce the intended behavior:

- full scan of visible skills
- small primary set
- support-only use of weaker matches
- fail-closed behavior when nothing is strong enough

## Planning

```text
Use use-skills on this feature request and improve it with the strongest relevant installed skills before you write the implementation plan.
```

## Coding

```text
Use use-skills on this bug report, scan all visible skills, and let only the strongest matches shape the patch.
```

## Documentation

```text
Use use-skills to rewrite this README for maximum quality. Use weaker matches only as support.
```

## Review

```text
Use use-skills to review this change. If no skill is a strong match, fail closed instead of forcing synthesis.
```

## Product Spec

```text
This request spans planning, implementation, and review. Use use-skills if it is an obvious fit and keep the final output clean.
```

## Strong Gate

```text
Use use-skills here only if at least one skill is a strong primary match. If not, fail closed.
```

## Support-Only Reminder

```text
Use use-skills, but keep loosely relevant skills in support mode only. Do not let them steer the answer.
```
