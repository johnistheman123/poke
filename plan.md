# Work Plan

## Goal
Align singleplayer behavior with multiplayer behavior in the Pokémon guessing game. This change is intentionally limited to client-side flow alignment and does not add multiplayer networking or new gameplay features.

## Scope
- In scope:
  - Make singleplayer use the same round-resolution flow as multiplayer.
  - Show the correct success/fail feedback screen in singleplayer.
  - Require an explicit user action to continue to the next question after a correct answer.
  - Keep the existing single-file HTML architecture and avoid introducing new networking logic.
- Out of scope:
  - Matchmaking and server/client networking.
  - New UI redesign.
  - New game modes or score rules.

## Task Breakdown
Each task below is written so it can be executed and checked without re-explaining the build order.

1. Inspect the existing game flow in poke.html and create a short divergence list for singleplayer vs multiplayer.
   - Deliverable: a written map of the current functions involved in question generation, answer handling, modal display, and round progression.
   - Acceptance check: the list identifies where singleplayer currently differs from multiplayer.

2. Introduce a minimal mode switch for the client-side flow.
   - Deliverable: one explicit singleplayer flag or a small adapter that lets the game choose the correct round-resolution path without branching across the whole file.
   - Acceptance check: the code path can be selected explicitly for singleplayer and leaves multiplayer behavior intact.

3. Update checkAnswer() so singleplayer follows the same round outcome flow as multiplayer.
   - Deliverable: correct answers update score, show the success modal, and stop auto-advancing; incorrect answers show the fail modal.
   - Acceptance check: a correct answer in singleplayer does not immediately generate the next question, and an incorrect answer shows the fail screen.

4. Update the continue/Next handler and the question-generation path so they use the same shared logic.
   - Deliverable: the Next button, question reset, and UI refresh all route through the same function or shared API used by the existing multiplayer flow.
   - Acceptance check: after clicking Next, a new question appears and the game state is reset for the next round.

5. Add focused manual or lightweight automated smoke checks for the alignment fix.
   - Deliverable: a short test checklist or small browser-based smoke script covering correct answer, incorrect answer, Next behavior, and a multiplayer sanity check.
   - Acceptance check: the checklist can be run quickly and confirms the intended behavior without broad regression work.

6. Prepare the change for review.
   - Deliverable: a concise PR description, a reference to spec.md, and a short validation summary.
   - Acceptance check: the PR explains what changed, why it changed, and how the behavior was verified.

## Dependency Mapping
- Blockers:
  - The acceptance criteria in spec.md must be clear before the implementation change is finalized, because they define the expected singleplayer success/fail flow.
  - The existing modal markup and round-navigation hooks in poke.html must be available before the flow can be wired correctly.
- Parallel work:
  - The inspection work in Task 1 and the drafting of the small mode adapter in Task 2 can happen in parallel if two engineers are available.
  - The smoke-test checklist in Task 5 can start once the behavior change is implemented, even if the final PR text is still being drafted.
- Sequencing rules:
  - Implement the mode switch first, then the answer-resolution logic, then the continue/Next flow, then validation.
  - Do not merge the validation work before the behavior change itself.
  - Keep the change set narrow so it remains easy to review and revert.

## Data Inventory
The plan explicitly tracks the data that moves through one round so the implementation order is clear.

- Current question object
  - Source: generated from the Pokémon question data at round start.
  - Location: a JavaScript variable or state object in poke.html.
- Answer choices
  - Source: derived from the current question object.
  - Location: a JavaScript variable or DOM-rendered list in poke.html.
- Player answer
  - Source: user input from the answer selection UI.
  - Location: event-handler variable or state field in poke.html.
- Correctness result
  - Source: calculated by comparing the player answer to the correct answer.
  - Location: local variable returned from checkAnswer() or a small state field.
- Round outcome
  - Source: determined from the correctness result.
  - Location: a local variable or UI-state field that drives the success/fail modal.
- Score
  - Source: incremented when the answer is correct.
  - Location: a JavaScript variable or state object used by the UI.
- Win condition flag
  - Source: calculated from the score against the win threshold.
  - Location: a JavaScript variable or state field used by the gameplay UI.
- Modal state
  - Source: set by the outcome handler.
  - Location: DOM visibility state or a small UI-state variable.
- Continue/Next state
  - Source: user action after the outcome screen.
  - Location: a click-handler variable or state field that triggers the next question.

## Data Flow
This is the full round path the implementation must preserve.

1. The game creates a question and answer choices.
2. The player submits an answer through the UI.
3. checkAnswer() compares the answer to the correct answer.
4. The result sets the round outcome and updates the score if needed.
5. The UI switches to the success or fail modal and stops automatic advancement in singleplayer.
6. The player clicks Next to continue.
7. The same shared generation path creates the next question and refreshes the UI.
8. The loop repeats until the win condition is reached.

## Build-Readiness & Required Scope
This plan is buildable as written because it breaks the work into ordered, testable steps and keeps the scope tight. It explicitly preserves the existing multiplayer behavior and limits the change to the singleplayer client-side flow required by spec.md.

## Reflection
- Highest-leverage task: the mode switch in Task 2, because it prevents the rest of the work from turning into a maze of host-only branches.
- Riskiest task: the answer-resolution path in Task 3, because a small mistake there can break both the modal behavior and round progression. The backup plan is to keep the original logic intact and wrap only the singleplayer branch behind the new explicit mode switch.
- Sequencing insight: the round outcome and Next flow must be aligned before any validation work begins; otherwise the tests will be checking inconsistent behavior.
- Ownership: the implementation owner should be the developer editing poke.html, and a second reviewer should verify the singleplayer and multiplayer paths before merge.

## Validation Checklist
1. Start a singleplayer round and answer correctly; confirm the success modal appears.
2. Verify that the game does not advance automatically until the player clicks Next.
3. Click Next and confirm a new question is generated and the UI refreshes correctly.
4. Answer incorrectly and confirm the fail modal appears.
5. Run a quick multiplayer smoke test to confirm no regression in the existing flow.
