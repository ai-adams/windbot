# Phase 1 Runtime Flow

## Startup

1. Program.Main loads configuration.
2. Program.InitDatas initializes deck executors and cards.cdb.
3. Program creates GameClient.
4. GameClient connects to the YGOPro host.
5. GameClient forwards incoming packets to GameBehavior.

## Duel Processing

1. GameBehavior decodes network and game messages.
2. GameBehavior updates Room, Duel, Deck, and field state.
3. GameBehavior calls GameAI for decisions.
4. GameAI evaluates the active Executor.
5. The Executor applies deck-specific rules.
6. GameAI returns an action.
7. GameBehavior writes the corresponding response packet.
8. GameClient sends the response to the host.

## Decision Path

GameBehavior
    -> GameAI
        -> ordered Executor rules
            -> ShouldExecute
                -> selected action

## Extension Points

- DeckAttribute registers a deck executor.
- DecksManager discovers executor classes through reflection.
- AddExecutor registers ordered behavioral rules.
- Executor virtual methods allow deck-specific selection behavior.
- DefaultExecutor provides shared fallback behavior.

## Architectural Risks

- Rule priority is implicit in registration order.
- Reordering AddExecutor calls can change behavior silently.
- Decision logic and duel-state mutation are closely coupled.
- Most validation currently depends on compilation or live duel behavior.
- Full duel execution is not yet verified locally.
