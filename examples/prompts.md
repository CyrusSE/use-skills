# Example Prompts

These examples are written to reinforce the intended behavior:

- full scan of visible skills
- small primary set
- support-only use of weaker matches
- fail-closed behavior when nothing is strong enough
- no requirement for the user to name the skill explicitly

## Planning

```text
Turn this feature request into a clear implementation plan with strong testing and review discipline.
```

## Coding

```text
Patch this bug report with strong implementation discipline and only the most relevant skill guidance driving the fix.
```

## Documentation

```text
Rewrite this README for maximum quality. Use weaker guidance only as background support.
```

## Review

```text
Review this change. If no skill is a strong match, fail closed instead of forcing synthesis.
```

## Product Spec

```text
This request spans planning, implementation, and review. Improve it if cross-skill synthesis is an obvious fit and keep the final output clean.
```

## Strong Gate

```text
Only activate broad synthesis here if at least one skill is a strong primary match. If not, fail closed.
```

## Support-Only Reminder

```text
Keep loosely relevant skills in support mode only. Do not let them steer the answer.
```
