---
name: intent-handoff
description: Keep AGENTS.md, PLAN.md, DECISIONS.md and HANDOFF.md at the repository root current. Write AGENTS.md and PLAN.md right after requirements are agreed, record each major decision, check off finished plan units, and prepare HANDOFF.md before handing off to a new session; in a new session, resume work from these files. Use for requests to record intent, plan the implementation, record a decision, hand off, or resume.
---

# Intent and Handoff Records

A decision or plan that lives only in chat does not exist for the next session or for the evaluator. Keep four files at the repository root current.

## When to use

- Right after requirements are agreed: write AGENTS.md and PLAN.md for the first time.
- Right after a major decision: add an entry to DECISIONS.md.
- After a PLAN unit passes its Verify command: mark it done in PLAN.md and commit it with the code.
- Right before handing off: follow "Handing off" below.
- When starting a new session: follow "Resuming" below.

## Language

- Write AGENTS.md, PLAN.md, DECISIONS.md and HANDOFF.md in English.
- Talk to the user in Korean.
- Write stakeholder questions and the task's deliverables in the task's language, unless the task says otherwise.

## What each file contains

1. `AGENTS.md`, 50 lines or fewer: a one-sentence goal, completion criteria as a checkable list, constraints and things not to do, verification commands that can be copied and run as is, verification scope, security rules (secrets and personal data), and language. Put this sentence in the verification scope verbatim: "Verify with the commands and completion criteria above. Before building a new verification tool, such as a fuzzer, mutation testing or reruns across versions, ask the user." Copy the three lines under "Language" above into the language section verbatim. AGENTS.md describes the whole task and what the finished deliverable must satisfy, not the current request: leave completion criteria unchecked until the deliverable meets them, and do not add constraints that apply only to the current request.
2. `PLAN.md`, 40 lines or fewer: the implementation units in build order, each small enough to build and verify in about 20 to 30 minutes. The first unit is the thinnest slice that works end to end. Write each unit in this format:
   ```
   - [ ] U<n>. <what works when this unit is done>
     - Files: <files to create or change>
     - Verify: <command that shows it works>
     - Covers: <numbers of the AGENTS.md completion criteria it satisfies>
   ```
   Mark a unit `[x]` only after its Verify command passed and the unit was committed. When the plan changes, edit PLAN.md in place and add a DECISIONS.md entry with the reason.
3. `DECISIONS.md`: add four lines per decision in the format below. Never delete earlier entries; when a decision is reversed, add a new entry that names the old number.
   ```
   ## D<n>. <decision in one line>
   - Why: <reason; if a stakeholder answer is the reason, say which answer>
   - Rejected: <alternative>: <why it was rejected>
   - Source: stakeholder / user / AI suggestion (for an AI suggestion, say who accepted it and how it was checked)
   ```
   If the stakeholder must make a decision and has not answered yet, end its heading with `(UNCONFIRMED)`. When it is fully confirmed later, replace `(UNCONFIRMED)` with `(confirmed in D<n>)`, where D<n> is the entry that records the confirmation. If only part of it is confirmed, keep `(UNCONFIRMED)` and record the confirmed part in a new entry.
4. `HANDOFF.md`: rewrite it whole each time, in 40 lines or fewer, with these sections:
   - Current unit: the PLAN unit in progress and how far it got. Refer to PLAN units by number instead of restating the plan.
   - Uncommitted changes: the files `git status` lists, and what each change is for.
   - How to run: start commands, ports, and dependencies installed during the session.
   - Last verification: the command and its numbers.
   - Fixed failures: symptom → cause → fix → same check passed again.
   - First action: the one concrete thing the next session does first.
   - Open questions.

## Handing off

1. Run the Verify command of the current unit. If it passes, mark the unit done and commit it. If the unit is half done, do not rush to finish it; leave it uncommitted and describe it in HANDOFF.md.
2. Rewrite HANDOFF.md from `git status` and the work so far, and check that AGENTS.md, PLAN.md and DECISIONS.md match the current state.
3. Commit the documents only, so a half-done unit stays visible as uncommitted changes.
4. Tell the user to type `/new` and then ask `$intent-handoff` to resume.

## Rules

- Never write that a check passed unless it was run.
- An instruction that limits only the current request, such as "do not commit yet" or "tests only for now", is not a decision. Do not record it in DECISIONS.md or pass it to the next session as a restriction; HANDOFF.md describes only the state it left.
- When listing unconfirmed decisions in HANDOFF.md's open questions or in a summary such as a README, do not write from memory. Run `grep '^## D.*[(]UNCONFIRMED[)]' DECISIONS.md` and copy the entry numbers it prints; if it prints nothing, say there are none.
- Each line of PLAN.md, DECISIONS.md and HANDOFF.md holds at most two sentences, so a person can read and explain them without AI.
- Do not repeat what the code or git log already shows.
- Commit after each update of these files; when a code change goes with them, commit both together.

## Resuming

1. Read AGENTS.md, PLAN.md, HANDOFF.md, then DECISIONS.md.
2. Run `git status` and `git log --oneline -3`, then the verification commands in AGENTS.md. Check that the actual state matches HANDOFF.md and PLAN.md; if it does not, fix those files first.
3. Restart anything HANDOFF.md says must be running, such as a dev server.
4. Do not ask the stakeholder again about anything they already answered.
5. Continue from the first action in HANDOFF.md.
