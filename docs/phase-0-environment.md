# Phase 0 Environment

## System

- OS: Linux Mint
- Mono: 6.8.0.105
- Build tool: xbuild 14.0
- Git remote: git@github.com:ai-adams/windbot.git
- Branch: phase-0-foundation

## Installed Dependencies

- Git
- Mono
- xbuild
- curl
- VS Code

## Build

Command:

    xbuild WindBot.sln /p:Configuration=Release

Result:

- Build succeeded
- 0 errors
- 90 warnings
- Output created at bin/Release/WindBot.exe

## Build Warnings

- xbuild is deprecated
- xbuild reports limited .NET Framework 4.8 toolset support
- Existing upstream compiler warnings remain unchanged

## Runtime Dependency

WindBot requires cards.cdb.

Download command:

    curl -L https://raw.githubusercontent.com/ProjectIgnis/BabelCDB/master/cards.cdb \
      -o bin/Release/cards.cdb

For the smoke test, cards.cdb was copied to the repository root:

    cp bin/Release/cards.cdb .

## Runtime Smoke Test

Command:

    mono bin/Release/WindBot.exe

Result:

- WindBot started successfully
- 62 decks initialized
- cards.cdb loaded successfully
- WindBot attempted its default localhost YGOPro connection
- No host was running, so WindBot exited normally

## Current Limitations

- No local YGOPro host is installed or running
- A complete duel smoke test has not yet been performed
