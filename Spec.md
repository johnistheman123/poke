# Project Specification: Guess That Pokémon! 🎮

## 1. Overview & Problem Statement
Standard trivia games often lack replay value because they only tally correct answers without giving the player a sense of progression. *Guess That Pokémon!* solves this by turning a classic nostalgia-driven mechanic ("Who's That Pokémon?") into a competitive, state-driven arcade game featuring an active in-game economy.

## 2. Target Audience
*   **Classic Fans:** Nostalgic players looking for Gen-1 to Gen-4 Pokémon content.
*   **Casual Gamers:** Web users looking for an unblocked, instantly loading mobile/desktop minigame.
*   **Aspiring Developers:** Anyone looking for a clean, vanilla JavaScript blueprint featuring robust state management.

## 3. Core Features & Scope

### A. The Core Trivia Loop
*   **Silhouette Generation:** Uses CSS brightness filters (`brightness(0)`) to hide the Pokémon's identity until guessed.
*   **Data Retrieval:** Fetches official character artwork and names dynamically (or via a clean local data object for speed).
*   **Win/Loss States:** 
    *   **Correct:** Shows the unmasked Pokémon, plays a success state, and awards cash.
    *   **Incorrect:** Takes the player to a failure screen with a choice to skip or spend resources to retry.

### B. The Game Economy & Arcade Shop
*   **Currency System:** Players earn +$10 in pocket cash per correct answer.
*   **The Arcade Shop:** A dedicated UI panel where players can spend accumulated earnings on collectible badges (e.g., "Novice Trainer", "Master Trainer") and passive utility items.

### C. UI/UX Design
*   **Mobile-First Card Layout:** A layout-locked, responsive container optimized for single-hand mobile play or centered desktop play.
*   **Minimal Clicks:** Streamlined transitions between the quiz, the failure screen, and the shop to maximize player engagement.

## 4. Technical Stack
*   **Frontend:** Semantic HTML5, responsive CSS3 (Flexbox/Grid), and Vanilla JavaScript (ES6+).
*   **Styling:** Native CSS filters for silhouettes; custom utility variables for theme colors.
*   **Deployment:** Hosted completely via GitHub Pages for zero-install, instant web delivery.
