---
name: intent-handoff
description: Update AGENTS.md, DECISIONS.md and HANDOFF.md at the repository root right after requirements are agreed, right after a major decision, and right before handing off to a new session; in a new session, resume work from these files. Use for requests to record intent, record a decision, hand off, or resume.
---

# Intent and Handoff Records

A decision that lives only in chat does not exist for the next session or for the evaluator. Keep three files at the repository root current.

## When to use

- Right after requirements are agreed: write AGENTS.md for the first time.
- Right after a major decision: add an entry to DECISIONS.md.
- Right before handing off: rewrite HANDOFF.md and check that the other files are current.
- When starting a new session: follow "Resuming" below.

## Language

- Write AGENTS.md, DECISIONS.md and HANDOFF.md in English.
- Talk to the user in Korean.
- Write stakeholder questions and the task's deliverables in the task's language, unless the task says otherwise.

## What each file contains

1. `AGENTS.md`, 50 lines or fewer: a one-sentence goal, completion criteria as a checkable list, constraints and things not to do, verification commands that can be copied and run as is, verification scope, security rules (secrets and personal data), and language. Put this sentence in the verification scope verbatim: "Verify with the commands and completion criteria above. Before building a new verification tool, such as a fuzzer, mutation testing or reruns across versions, ask the user." Copy the three lines under "Language" above into the language section verbatim.
2. `DECISIONS.md`: add four lines per decision in the format below. Never delete earlier entries; when a decision is reversed, add a new entry that names the old number.
   ```
   ## D<n>. <decision in one line>
   - Why: <reason; if a stakeholder answer is the reason, say which answer>
   - Rejected: <alternative>: <why it was rejected>
   - Source: stakeholder / user / AI suggestion (for an AI suggestion, say who accepted it and how it was checked)
   ```
   If the stakeholder must make a decision and has not answered yet, end its heading with `(UNCONFIRMED)`. When it is fully confirmed later, replace `(UNCONFIRMED)` with `(confirmed in D<n>)`, where D<n> is the entry that records the confirmation. If only part of it is confirmed, keep `(UNCONFIRMED)` and record the confirmed part in a new entry.
3. `HANDOFF.md`: rewrite it whole each time, in 40 lines or fewer. Include the current state (done and not done), the last verification (command and numbers), failures that were fixed (symptom → cause → fix → same check passed again), next steps in priority order, and open questions.

## Rules

- Never write that a check passed unless it was run.
- When listing unconfirmed decisions in HANDOFF.md's open questions or in a summary such as a README, do not write from memory. Run `grep '^## D.*[(]UNCONFIRMED[)]' DECISIONS.md` and copy the entry numbers it prints; if it prints nothing, say there are none.
- Each line of DECISIONS.md and HANDOFF.md holds at most two sentences, so a person can read and explain them without AI.
- Do not repeat what the code or git log already shows.
- Commit document updates together with the related code.

## Resuming

1. Read AGENTS.md, HANDOFF.md, then DECISIONS.md.
2. Run the verification commands in AGENTS.md and check that the actual state matches HANDOFF.md. If it does not, fix HANDOFF.md first.
3. Do not ask the stakeholder again about anything they already answered.
4. Continue from the first next step in HANDOFF.md.
