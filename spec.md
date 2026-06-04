# Game Specification

## Project
Guess That Pokémon - Wireless Multiplayer

## Objective
Make singleplayer behave exactly like multiplayer, with the same gameplay flow, UI screens, and round progression.

## Scope
- Singleplayer mode must use the same success/fail flow as multiplayer.
- Correct answers must display the success screen, not immediately advance to a new round.
- Incorrect answers must display the fail screen.
- The "Next Pokémon" button must be available after success and continue the game.
- Singleplayer should keep the same point scoring and win condition behavior as multiplayer.

## Functional Requirements
1. Start singleplayer game from the home screen.
2. Generate a random Pokémon question and four answer choices.
3. Player submits an answer.
4. If correct:
   - award points
   - update the UI
   - show the success screen
   - allow the player to continue via "Next Pokémon"
5. If incorrect:
   - show the fail screen
   - allow the player to return to the game screen
6. Win condition should still trigger when player reaches the win score threshold.

## Non-Functional Requirements
- Keep the existing multiplayer flow unchanged.
- Preserve accessibility and screen navigation behavior.
- Avoid using alerts for game feedback.
- Maintain the current single-file HTML architecture.

## Acceptance Criteria
- [ ] Singleplayer starts and runs without multiplayer host logic blocking it.
- [ ] Correct singleplayer answers display the success screen.
- [ ] Wrong singleplayer answers display the fail screen.
- [ ] "Next Pokémon" is required to continue after success.
- [ ] Gameplay is consistent with multiplayer flow.
