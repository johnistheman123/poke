# Project Plan: Guess That Pokémon! 🗺️

## 1. Development Phases

### Phase 1: Core Mechanics & Layout (The Foundation)
*   Build the structural HTML5 layout using a mobile-first card design.
*   Implement the baseline CSS styling, focusing on centering the gameplay zone.
*   Write the JavaScript logic to load a random Pokémon and successfully apply the CSS silhouette filter (`brightness(0)`).

### Phase 2: State Engine & Economy (The Twist)
*   Create a central global state object to track current score, wallet cash, unlocked items, and game status.
*   Implement input validation for user guesses (handling capitalization and spaces defensively).
*   Code the scoring logic: add +$10 for wins, trigger the failure/retry screen for losses.

### Phase 3: The Arcade Shop & Interface
*   Build the Arcade Shop overlay panel.
*   Write buy-functions that deduct currency correctly and push unlocked badges into the player's profile state.
*   Disable shop items once purchased to prevent accidental double-spending.

### Phase 4: Polish, Testing & Deployment
*   Add smooth CSS transition animations for screen switches and reveals.
*   Run cross-browser testing (Chrome, Safari, iOS Safari, Android Chrome).
*   Deploy the production-ready code to GitHub Pages.

---

## 2. Definition of "Done"
The project is considered complete when it satisfies the following gates:

1. **Gate 1 (Gameplay):** A player can endlessly loop through random Pokémon silhouettes, input a guess, and see the correct visual reveal.
2. **Gate 2 (Economy):** Wallet totals accurately increment by $10 on success, display immediately in the UI, and allow purchases in the shop.
3. **Gate 3 (Resiliency):** The game handles unexpected typos gracefully without crashing the UI loop.
4. **Gate 4 (Deployment):** The game is fully accessible via a public live URL on GitHub Pages with no console errors on load.

---

## 3. Verification & Metrics
*   **Visual Check:** Confirmed layout bounds remain perfectly centered and scaled across mobile screens (iPhone/Android templates) and desktop browsers.
*   **State Integrity Check:** Verified through console logging that currency values never drop below $0, even when a user attempts to buy a shop item they cannot afford.
