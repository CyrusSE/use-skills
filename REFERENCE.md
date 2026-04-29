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

## Response Block

When used, begin with:

- `Mode: All related | Recommended | Restricted`
- `Using: use-skills, <selected skills>`
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
