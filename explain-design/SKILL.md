---
name: explain-design
description: Explain the whole implementation at the concept level, its core idea, main algorithm, structure and the decisions behind them, so the user can understand it and explain it without AI. Read-only; it never edits files. Use when the user asks to understand or explain the implementation, its concept, algorithm, architecture or structure.
---

# Explain the Design

The user must be able to explain this implementation in their own words, without AI and without reading code. Explain the whole implementation at the concept level, not line by line and not one unit at a time.

## Rules

- Read AGENTS.md, PLAN.md, DECISIONS.md and HANDOFF.md if they exist, then the code. Do not edit any file and do not run commands that change state.
- Explain what the files show now. When PLAN.md has unfinished units, mark which parts are built and which are only planned.
- Talk in Korean. Do not show code; name a file or module only to say where a concept lives.
- Define each technical term in one plain sentence the first time it appears.
- Keep the answer to one screen. When the user asks about one part, go deeper on that part in the same format instead of repeating the whole answer.

## Format

1. **In one sentence**: what goes in, what comes out, and for whom.
2. **Core idea**: the one to three ideas the rest depends on, in plain words.
3. **Algorithm**: the main procedure in three to seven numbered steps, then one concrete example from the task's own data carried through those steps.
4. **Structure**: the main parts, what each is responsible for, and how data moves between them, as a short list or a small text diagram.
5. **Why this way**: the two to four decisions that shaped the design, each with its DECISIONS.md entry number and the alternative it rejected.
6. **Limits**: what is not built yet, what rests on an assumption, and the open decisions printed by `grep '^## D.*[(]UNCONFIRMED[)]' DECISIONS.md`.
7. **Check yourself**: three questions an evaluator could ask about this design. Do not answer them unless the user asks; when the user answers, say what was missing or wrong.
