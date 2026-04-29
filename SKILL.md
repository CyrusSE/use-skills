---
name: use-skills
description: Helps choose relevant installed skills for complex requests and briefly shows the working set before answering.
---

# Use Skills

Use this skill when the user invokes `$use-skills`, or when a request clearly benefits from combining more than one installed skill.

## Purpose

Choose a small, relevant working set of skills and turn their guidance into one coherent result.

Good fits include requests that combine areas such as:

- planning and implementation
- review and testing
- writing and structure
- design and frontend work
- documentation and code changes

Skip this skill when one domain skill is clearly enough.

## Selection Process

1. Review the visible skill list.
2. Compare each skill with the user request and expected output.
3. Pick the strongest matches as the working set.
4. Use supporting skills only when they materially improve the result.
5. Read only the parts of selected skills that help with the current task.
6. Produce one unified answer, plan, patch, or recommendation.

Keep the working set appropriate to the selected mode. `Recommended` is the usual choice when the user wants balanced quality, but ask for a mode when no reusable prior choice exists.

## Match Labels

Use these labels while choosing:

- `primary`: directly shapes the result
- `support`: adds useful quality, structure, review, wording, or edge-case coverage
- `skip`: not useful for the current request

If no skill is a strong fit, leave this skill unused.

## Modes

Ask the user to choose one mode before the main response when there is no reusable prior choice:

- `All related`: use every available skill that is meaningfully related to the request
- `Recommended`: use the best balanced working set for the request
- `Restricted`: use only the strongest matches, usually one to three skills

Ask with this compact format:

`Choose skill mode: All related, Recommended, or Restricted?`

Do not choose silently unless the user already specified a mode or a previous mode still applies. Reuse the previous mode when the task and expected output are materially the same. Ask again when the task, expected output, or selected skill set changes.

## Response Block

When this skill is used, start with a compact block:

- `Mode: All related | Recommended | Restricted`
- `Using: use-skills, <selected skill>`
- `For: <short purpose>`

List only skills that actually shape the answer. Keep selection details out of the response unless the user asks for them.

## Conflict Handling

When selected skills point in different directions, prefer:

1. the user's current request
2. higher-priority session and project guidance
3. narrower domain skills over broader general skills
4. newer and more specific guidance over older or vague guidance

## Quality Checks

- Keep the answer focused on the user's task.
- Avoid irrelevant skill advice.
- Avoid duplicate guidance.
- Keep the opening block shorter than the answer it introduces.
- Include a support skill in `Using:` only when it materially changes the result.
- Ask for mode when no reusable prior mode exists.
- Do not ask again when the prior mode still fits the task and expected output.
- Ask again when the task, expected output, or selected skill set has changed.

## Example Triggers

- `$use-skills`
- `Turn this feature idea into an implementation plan with testing notes.`
- `Rewrite this README so it is clearer and better structured.`
- `This spans planning, implementation, and review. Use the best combination of skills.`
- `Review this change and give the strongest findings first.`
- `Use restricted mode and only the strongest skills for this request.`
