# Example Prompts

These examples are written to reinforce the intended behavior:

- full scan of visible skills
- small primary set
- support-only use of weaker matches
- fail-closed behavior when nothing is strong enough
- no requirement for the user to name the skill explicitly
- explicit `$use-skills` invocation also works
- when activated, the skill announces the working set first
- mode choice between `Recommended`, `Restricted`, and `Strict`
- session context analysis before recommending skills

## Explicit Invocation

```text
$use-skills
```

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

## Recommended Mode

```text
Use the recommended skill set for this request. Prioritize the strongest final output.
```

## Restricted Mode

```text
Use restricted mode. Recommend only the strongest skills and keep support guidance quiet unless it materially improves the result.
```

## Strict Mode

```text
Use strict mode. Include only essential skills, and fail closed if nothing is clearly necessary.
```

## Session-Aware Recommendation

```text
Analyze the current session, my latest prompt, and the expected output before recommending which skills to use.
```

## Reuse Previous Choice

```text
$use-skills again
```

Expected behavior: reuse the previous mode and working set if the context has not materially changed.

## Ask Again When Changed

```text
Now use this for a different kind of output: turn the same idea into launch documentation instead of an implementation plan.
```

Expected behavior: ask again or update the recommendation because the expected output changed.
