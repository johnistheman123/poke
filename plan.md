# Work Plan

## Goal
Align singleplayer behavior with multiplayer behavior in the Pokémon guessing game. Scope: this is an alignment fix only (no feature additions or multiplayer networking work).

## Scope
- In scope: change singleplayer flow so it mirrors multiplayer navigation and success/fail handling; ensure deterministic client-side behavior for singleplayer.
- Out of scope: matchmaking, network protocol, multiplayer infrastructure, UI redesign.

## Task Breakdown (scoped to alignment fix)
1. Inspect singleplayer flow in `poke.html` and map divergences from multiplayer (owner: dev).
2. Modify `checkAnswer()` to show the success/fail modal in singleplayer and stop automatic advancement (owner: dev).
3. Ensure `generateNewQuestion()` and navigation handlers call the same shared APIs used by multiplayer (owner: dev).
4. Add a minimal, explicit singleplayer flag or shared adapter to avoid host-only branching in game logic (owner: dev).
5. Write and run manual test cases and small automated sanity checks where available (owner: dev + reviewer).
6. Create PR with description, link to `spec.md`, and request reviewer for merge (owner: dev).

## Dependency Mapping
- Blockers:
   - Acceptance of this alignment change against `spec.md` (blocks task 2).
   - Missing UI templates/assets for modals (blocks task 3).
- Parallelizable:
   - Task 1 (inspection) and Task 3 (API alignment) can be worked in parallel by two engineers.
   - Writing tests (Task 5) can begin after Task 2 or run in parallel against a local stub.
- Sequencing rules:
   - Do not merge test/validation changes before behavior change (merge order: 2 -> 3 -> 5 -> 6).

## Data Inventory
- Inputs required for this alignment fix:
   - Runtime state: current question object, player score, UI state (modals), singleplayer/multiplayer flag.
   - Files to inspect: `poke.html`, `spec.md`.
- Outputs produced:
   - Success/fail modal state and navigation events; updated `checkAnswer()` behavior.

## Data Flow (concise)
User answer -> `checkAnswer()` -> correctness decision -> update score & emit navigation event -> render success/fail modal -> user action (Next) -> `generateNewQuestion()` -> render new question.

Notes: in multiplayer the server may advance turns; in singleplayer the client must wait for user action before advancing.

## Build-Readiness & Validation Checklist
- Pre-merge checks:
   - [ ] Code compiles / no lint errors
   - [ ] Unit/smoke tests (if present) pass
   - [ ] PR includes `spec.md` reference and validation steps
- Validation steps to confirm done:
   - [ ] Singleplayer shows success modal on correct answer
   - [ ] Singleplayer does not auto-advance without user action
   - [ ] `generateNewQuestion()` updates UI and state correctly after Next
   - [ ] Multiplayer smoke test confirms no regressions

## Sequencing Insight & Ownership
- Ownership:
   - Implementation owner: developer who edits `poke.html` (assign in PR)
   - Reviewer: different team member for regression checks
- Sequence reminder: inspect -> implement -> test -> review -> merge

## Validation (detailed)
1. Start singleplayer, answer correctly -> confirm success modal visible.
2. Click Next -> confirm a new question appears and internal state updates.
3. Repeat with incorrect answer -> confirm fail modal.
4. Run a quick multiplayer smoke test to ensure no behavioral regressions.

## Notes
- Keep changes minimal and easily revertible; prefer small commits and a focused PR.
- Reference `spec.md` for acceptance criteria.
