# Architecture

## Layers

1. **Content schema** — `stp-game-package-1.2` (JSON)
   - Node types: dialogue, choice, router, quran_card, reflection, ending
   - Variables: boolean, integer, enum
   - Effects: `set` operations on variables
   - Validation: PHP + JavaScript parity

2. **Runtime** — `stp-game-runtime.js`
   - Executes any 1.2 package
   - Self-contained (no external assets at runtime)
   - Optional "juice" layer for timers, audio, portraits (all additive)

3. **Authoring** — two interfaces
   - Story Workshop: for coaches, no technical terms
   - Graph Editor: for advanced branching (router, variables)

4. **Persistence** — WordPress integration
   - Session payload: scores, decisions, reflections, events
   - Idempotency keys for safe retry
   - Pure functions extracted for testability

## Design rules

- Producer never sees JSON or `steps[]`
- Simple by default, full control on demand
- 1.2 never replaced; only extended
- Tests must be able to fail (mutation testing)
