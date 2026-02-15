---
name: compound-knowledge
description: Save team knowledge notes into ./knowledge/ with date-prefixed filenames. Implements the Compound step from compound engineering — every solved problem, discovered pattern, or key decision becomes searchable knowledge that makes future work easier. Use when the user wants to capture gotchas, errors, build issues, solutions, patterns, or decisions for future reference.
---

# Save Knowledge

This skill implements the **Compound step** from compound engineering: the
practice of making each unit of work teach the system something so subsequent
work gets easier, not harder. Bug fixes eliminate future bug categories.
Patterns become tools. Decisions become searchable context.

## Quick Start

1. Determine the knowledge type from context (see heuristics below).
2. If the type is not clear, ask the user which type to use.
3. Choose a short slug and date prefix for the filename.
4. Create `./knowledge/<type>/` in the repo root if it does not exist.
5. Verify the target file does not already exist. If it does, change the slug
   or add a numeric suffix before copying.
6. Copy the type template into the target file:
   - `cp resources/<type>.md ./knowledge/<type>/YYYY-MM-DD-<short-slug>.md`
7. Fill in the placeholders in the new file.
8. **System update check** — after saving, ask: should any learning be
   promoted to `AGENTS.md` or a cursor rule so the agent catches this
   automatically next time? If yes, propose the update.

## Knowledge Types

| Type        | When to use                                                                                                           |
| ----------- | --------------------------------------------------------------------------------------------------------------------- |
| `error-fix` | Something broke or surprised you — errors, gotchas, build failures, incidents. What happened and how to fix/avoid it. |
| `pattern`   | A recurring approach worth codifying — code patterns, workflow patterns, architectural conventions.                   |
| `decision`  | An architecture or design decision with rationale, alternatives, and tradeoffs.                                       |

## Type Selection Heuristics

- "error", "exception", "bug", "broke", "incident", "stack trace" → `error-fix`
- "build", "CI", "pipeline", "compile", "npm install", "webpack" → `error-fix`
- "gotcha", "unexpected", "pitfall", "surprising behavior" → `error-fix`
- "pattern", "convention", "standard", "we always do X", "reusable" → `pattern`
- "how we solved", "approach", "what worked" → `pattern`
- "decided", "tradeoff", "chose X over Y", "ADR", "why we" → `decision`
- If uncertain, ask the user to choose a type.

## Templates

Use the type-specific template from `resources/` and copy it to the target.
Then fill in the placeholders.

- Error fix: `resources/error-fix.md`
- Pattern: `resources/pattern.md`
- Decision: `resources/decision.md`

## When to Compound

Trigger this skill after any of these events:

- **Bug fix** — capture root cause so the category is prevented, not just this instance.
- **Feature completion** — capture what the plan missed, what surprised you, reusable patterns.
- **Debugging session** — if it took significant effort to find, it's worth documenting.
- **Architecture decision** — before you forget the alternatives you rejected and why.
- **Review finding** — if a reviewer (human or agent) caught something non-obvious.
- **Repeated question** — if someone asks how X works more than once, write it down.

Ask yourself: _"Would the system catch this automatically next time?"_
If no, save the knowledge and consider promoting it to `AGENTS.md`.

## The Compound Checklist

After saving knowledge, verify:

- [ ] **Captured the insight** — not just what happened, but the reusable takeaway.
- [ ] **Made it findable** — tags and scope are accurate.
- [ ] **Considered system update** — should `AGENTS.md` or a cursor rule be updated?
- [ ] **Prevention over cure** — does the note help prevent recurrence, not just fix it?

## Notes

- If the user wants a type outside the list, pick the closest type and proceed.
- Keep notes concise and factual; avoid large log dumps.
- Prefer concrete examples over abstract descriptions.
- Each note should be self-contained — a future reader (human or agent) should understand it without extra context.
