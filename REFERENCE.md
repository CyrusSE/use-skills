# use-skills Reference

`use-skills` is a small selection layer for combining installed skills when a task spans multiple areas.

## Selection Model

1. Review the visible skill list.
2. Compare each skill with the current request.
3. Choose the strongest matches.
4. Add supporting skills only when they improve quality.
5. Read only the selected material needed for the task.
6. Return one unified answer or artifact.

## Match Labels

### Primary

Primary skills directly shape the result.

Good signals:

- strong domain match
- strong task match
- clear help with the requested output
- clear help with quality, testing, clarity, structure, or review

### Support

Support skills refine the result without leading it.

Common uses:

- clearer structure
- sharper wording
- better edge-case coverage
- stronger testing notes
- tighter review framing

### Skip

Skipped skills are weak matches for the current request.

Skipping is expected. The point is to choose well, not to use everything.

## Modes

When there is no reusable prior mode, ask the user to choose before any workspace exploration, tool calls, file reads, or skill selection:

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

Do not choose silently unless:

- the user already specified a mode
- the previous mode still applies to the current task and expected output
- session context makes the same choice clearly reusable

Phrases like `best`, `most relevant`, `strongest`, `helpful`, or `best combination` do not count as explicit mode choices.

If `$use-skills` is invoked and no mode is explicit, the mode question must be the next assistant response.

The mode question may include likely skills for each option, but those candidates must come only from visible/provided skill metadata and the current prompt. Do not use tools, inspect files, or read skill bodies before the user chooses.

Allowed candidate sources before mode choice:

- installed skill metadata already visible in the current session
- skill blocks pasted or provided by the user in the current conversation
- skills explicitly named by the user with `$skill-name`, when a visible/provided description exists in the session

Use real visible/provided skill names when available and prefix them with `$`. If no visible skill list is available, use `skills selected after mode choice` rather than invented names.

For `All related`, include every candidate with a meaningful primary or support role. If the user explicitly names or provides a skill and it has any plausible support role, include it in `All related` even when it is too broad or weak for `Recommended`. Example: include `$enhance-prompt` when the task involves improving prompts, examples, mode menus, docs, UI prompts, or prompt-facing wording.

Keep each mode separated by a blank line. Use Markdown bold for the option title, `USING:`, `FOR:`, and final choose line. Use uppercase labels because some terminal transcripts do not visually render Markdown bold. Put `Choose skill mode. Reply with 1, 2, or 3.` after the three options, not before them.

### All related

Use every available skill that is meaningfully related to the request.

This is the broadest mode.

### Recommended

Use the best balanced working set for the request.

### Restricted

Use only the strongest selected skills, usually one to three.

## Reuse

If the user asks for `use-skills` again and the task is materially the same, reuse the previous mode and working set.

Choose again when:

- the requested output changes
- the task changes
- the selected skill set would change
- the user asks for a different mode
- there is no previous mode to reuse

## Response Block

When used, begin with:

- `Mode: All related | Recommended | Restricted`
- `Using: $use-skills, $<selected-skill>, $<selected-skill>`
- `For: <purposes>`

Keep the block brief and continue directly into the work.

## Selection Priorities

When guidance differs, prefer:

1. the user's current request
2. active session and project guidance
3. narrower domain skills over broader general skills
4. clearer, newer guidance over vague guidance

## Common Mistakes

- using too many skills
- adding skills that do not change the result
- making the opening block longer than the answer
- rereading large files when a targeted read is enough
- asking the user to choose a mode again when the prior choice still fits
