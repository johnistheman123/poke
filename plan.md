# Work Plan

## Goal
Align singleplayer behavior with multiplayer behavior in the Pokémon guessing game.

## Tasks
1. Review current singleplayer and multiplayer flow in `poke.html`.
2. Identify any host-only guards or singleplayer special cases that diverge from multiplayer.
3. Update `checkAnswer()` so singleplayer shows the success screen instead of auto-advancing.
4. Verify `generateNewQuestion()` and navigation functions work for singleplayer.
5. Test singleplayer gameplay manually:
   - start singleplayer
   - answer correctly and verify success screen
   - answer incorrectly and verify fail screen
   - press "Next Pokémon" and continue
6. Confirm multiplayer remains unchanged.

## Validation
- Play one singleplayer round to success.
- Play one singleplayer round to failure.
- Ensure the win condition still appears when score threshold is reached.

## Notes
- Keep documentation in root for easy reference.
- Use `spec.md` for requirements and `plan.md` for implementation steps.
