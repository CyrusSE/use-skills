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

0. Resolve the skill mode using the hard gate below.
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

Ask the user to choose one mode before any workspace exploration, tool calls, file reads, skill selection, or main response when there is no reusable prior choice:

- `All related`: use every available skill that is meaningfully related to the request
- `Recommended`: use the best balanced working set for the request
- `Restricted`: use only the strongest matches, usually one to three skills

Ask with this compact Markdown format. Use uppercase option and label text so terminal clients still show clear emphasis even when they do not render Markdown styling:

**1. ALL RELATED** - use every available skill that is meaningfully related.

**USING:** $use-skills, $<all-related-skill-candidate>
**FOR:** broad coverage across <purposes>

**2. RECOMMENDED** - use the best balanced working set.

**USING:** $use-skills, $<recommended-skill-candidate>
**FOR:** strong output without unnecessary noise

**3. RESTRICTED** - use only the strongest matches.

**USING:** $use-skills, $<one-to-three-strongest-skill-candidates>
**FOR:** focused output with minimal skill involvement

**Choose skill mode. Reply with 1, 2, or 3.**

## Mode Choice Hard Gate

If `$use-skills` is invoked and the prompt does not explicitly name `All related`, `Recommended`, or `Restricted`, the next assistant response must be only:

the numbered mode menu above.

Do not inspect files, search the workspace, read skill files, or infer a final mode before asking.

The menu should still mention likely skills for each option. Use only the current prompt and visible/provided skill names/descriptions to draft those candidate lists. Do not use tools to discover more context before the user chooses.

Candidate sources allowed before mode choice:

- installed skill metadata already visible in the current session
- skill blocks pasted or provided by the user in the current conversation, such as `<skill><name>enhance-prompt</name>...`
- skills explicitly named by the user with `$skill-name`, when a visible/provided description exists in the session

Replace the placeholder skill candidates with actual visible/provided skill names whenever they are available. Prefix skill names with `$`, such as `$use-skills`, `$enhance-prompt`, and `$writing-plans`. If the visible skill list is unavailable, say `skills selected after mode choice` instead of inventing names.

For `All related`, include every candidate with a meaningful primary or support role. If the user explicitly names or provides a skill and it has any plausible support role, include it in `All related` even when it is too broad or weak for `Recommended`. Example: include `$enhance-prompt` when the task involves improving prompts, examples, mode menus, docs, UI prompts, or prompt-facing wording.

Keep each mode separated by a blank line. Use Markdown bold for the option title, `USING:`, `FOR:`, and final choose line. Use uppercase labels because some terminal transcripts do not visually render Markdown bold. Put `Choose skill mode. Reply with 1, 2, or 3.` after the three options, not before them.

Phrases like `best`, `most relevant`, `strongest`, `helpful`, or `best combination` do not count as explicit mode choices.

Do not choose silently unless the user already specified one of the three modes or a previous mode still applies. Reuse the previous mode only when the task and expected output are materially the same. Ask again when the task, expected output, or selected skill set changes.

## Response Block

When this skill is used, start with a compact block:

- `Mode: All related | Recommended | Restricted`
- `Using: $use-skills, $<selected-skill>`
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
- Ask for mode before doing anything else when no reusable prior mode exists.
- Do not ask again when the prior mode still fits the task and expected output.
- Ask again when the task, expected output, or selected skill set has changed.

## Example Triggers

- `$use-skills`
- `Turn this feature idea into an implementation plan with testing notes.`
- `Rewrite this README so it is clearer and better structured.`
- `This spans planning, implementation, and review. Use the best combination of skills.`
- `Review this change and give the strongest findings first.`
- `Use restricted mode and only the strongest skills for this request.`
