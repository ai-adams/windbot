# APG WindBot

Roles: AJ=Executive; ChatGPT=Architect; Claude=Sr. Engineer.

For each approved phase:
1. Inspect first.
2. Report plan, files, risks, assumptions, checks.
3. Wait for approval.
4. Make the smallest scoped change.
5. Run checks and report exact results.

Do not change architecture, scope, dependencies, upstream behavior, or unrelated code without approval. Never commit secrets, binaries, databases, generated files, or local config.

Stop on ambiguity, failed validation, unexpected behavior, or security/licensing risk.

Baseline: `xbuild WindBot.sln /p:Configuration=Release`; 0 errors, 90 warnings; 62 decks loaded; full duel unverified.
