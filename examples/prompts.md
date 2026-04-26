# Example Prompts

These prompts show the intended use of `use-skills`.

## Direct Request

```text
$use-skills
```

## Planning

```text
Turn this feature request into a clear implementation plan with testing notes.
```

## Coding

```text
Patch this bug report with the most relevant skill guidance driving the fix.
```

## Documentation

```text
Rewrite this README for clarity, structure, and actionability.
```

## Review

```text
Review this change and give me the strongest findings first.
```

## Product Spec

```text
This spans planning, implementation, and review. Use the best combination of skills and keep the final output clean.
```

## Focused Use

```text
Use restricted mode. Recommend only the strongest skills.
```

## Essential Use

```text
Use strict mode. Include only essential skills.
```

## Reuse Previous Choice

```text
$use-skills again
```

Expected behavior: reuse the previous mode and working set if the task has not materially changed.
