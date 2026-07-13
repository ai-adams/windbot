# Phase 1 Repository Inspection

```text
./App.config
./BotWrapper/app.config
./BotWrapper/bot.conf
./BotWrapper/BotWrapper.cs
./BotWrapper/BotWrapper.csproj
./BotWrapper/BotWrapper.sh
./BotWrapper/load-once.conf
./BotWrapper/WindBot.ico
./CLAUDE.md
./Config.cs
./Decks/AI_Albaz.ydk
./Decks/AI_Altergeist.ydk
./Decks/AI_Apophis.ydk
./Decks/AI_BE2025.ydk
./Decks/AI_Blackwing.ydk
./Decks/AI_BlueEyesMaxDragon.ydk
./Decks/AI_BlueEyes.ydk
./Decks/AI_Brave.ydk
./Decks/AI_Burn.ydk
./Decks/AI_ChainBurn.ydk
./Decks/AI_CyberDragon.ydk
./Decks/AI_DarkMagician.ydk
./Decks/AI_Dogmatika.ydk
./Decks/AI_Dragunity.ydk
./Decks/AI_Dragun.ydk
./Decks/AI_Evilswarm.ydk
./Decks/AI_Exosister.ydk
./Decks/AI_FamiliarPossessed.ydk
./Decks/AI_Frog.ydk
./Decks/AI_Gravekeeper.ydk
./Decks/AI_Graydle.ydk
./Decks/AI_GrenMajuThunderBoarder.ydk
./Decks/AI_Horus.ydk
./Decks/AI_Kashtira.ydk
./Decks/AI_Labrynth.ydk
./Decks/AI_Level8.ydk
./Decks/AI_LightswornShaddoldinosour.ydk
./Decks/AI_Lightsworn.ydk
./Decks/AI_MalissOCG.ydk
./Decks/AI_Maliss.ydk
./Decks/AI_Mathmech.ydk
./Decks/AI_MokeyMokeyKing.ydk
./Decks/AI_MokeyMokey.ydk
./Decks/AI_Neko.ydk
./Decks/AI_Nekroz.ydk
./Decks/AI_OldSchool.ydk
./Decks/AI_Orcust.ydk
./Decks/AI_Phantasm.ydk
./Decks/AI_PureWinds.ydk
./Decks/AI_Qliphort.ydk
./Decks/AI_Rainbow.ydk
./Decks/AI_Rank5.ydk
./Decks/AI_Ryzeal.ydk
./Decks/AI_SacredBeast.ydk
./Decks/AI_Salamangreat.ydk
./Decks/AI_SkyStriker.ydk
./Decks/AI_ST1732.ydk
./Decks/AI_SuperheavySamurai.ydk
./Decks/AI_Swordsoul.ydk
./Decks/AI_Tearlaments.ydk
./Decks/AI_ThunderDragon.ydk
./Decks/AI_Timethief.ydk
./Decks/AI_ToadallyAwesome.ydk
./Decks/AI_Trickstar.ydk
./Decks/AI_Witchcraft.ydk
./Decks/AI_Yosenju.ydk
./Decks/AI_Yubel.ydk
./Decks/AI_Zefra.ydk
./Decks/AI_ZexalWeapons.ydk
./Decks/AI_Zoodiac.ydk
./Dialogs/anothercopy.zh-CN.json
./Dialogs/BA.zh-TW.json
./Dialogs/cirno.zh-CN.json
./Dialogs/copy.zh-CN.json
./Dialogs/default.json
./Dialogs/ecclesia.zh-CN.json
./Dialogs/gugugu.zh-CN.json
./Dialogs/kiwi.zh-TW.json
./Dialogs/mokey.zh-CN.json
./Dialogs/near.zh-CN.json
./Dialogs/smart.zh-CN.json
./Dialogs/soul.zh-CN.json
./Dialogs/superheavysamurai.zh-CN.json
./Dialogs/swordsman.zh-CN.json
./Dialogs/verre.zh-CN.json
./Dialogs/VI-1911.zh-CN.json
./Dialogs/Xiaoye.zh-CN.json
./Dialogs/Zefra.zh-CN.json
./Dialogs/zh-CN.json
./docs/phase-0-environment.md
./docs/phase-1-repository-inspection.md
./Game/BattlePhaseAction.cs
./Game/BattlePhase.cs
./Game/ChainInfo.cs
./Game/ClientCard.cs
./Game/ClientField.cs
./Game/Deck.cs
./Game/Duel.cs
./Game/GameAI.cs
./Game/GameBehavior.cs
./Game/GameClient.cs
./Game/GamePacketFactory.cs
./Game/MainPhaseAction.cs
./Game/MainPhase.cs
./Game/Room.cs
./.gitignore
./LICENSE
./Logger.cs
./Mono.Data.Sqlite.dll
./Program.cs
./Properties/AssemblyInfo.cs
./README.md
./sqlite3.dll
./WindBot.csproj
./WindBot.ico
./WindBotInfo.cs
./WindBot.sln
./YGOSharp.Network/BinaryClient.cs
./YGOSharp.Network/NetworkClient.cs
./YGOSharp.Network/YGOClient.cs
./YGOSharp.OCGWrapper/Card.cs
./YGOSharp.OCGWrapper/CardsManager.cs
./YGOSharp.OCGWrapper.Enums/CardAttribute.cs
./YGOSharp.OCGWrapper.Enums/CardLinkMarker.cs
./YGOSharp.OCGWrapper.Enums/CardLocation.cs
./YGOSharp.OCGWrapper.Enums/CardPosition.cs
./YGOSharp.OCGWrapper.Enums/CardRace.cs
./YGOSharp.OCGWrapper.Enums/CardType.cs
./YGOSharp.OCGWrapper.Enums/DuelPhase.cs
./YGOSharp.OCGWrapper.Enums/GameMessage.cs
./YGOSharp.OCGWrapper.Enums/PlayerHintType.cs
./YGOSharp.OCGWrapper.Enums/Query.cs
./YGOSharp.OCGWrapper/NamedCard.cs
./YGOSharp.OCGWrapper/NamedCardsManager.cs
```

## Decision Engine

WindBot uses an ordered rule list.

Each deck executor registers candidate actions through AddExecutor.

Each candidate contains:

- action type
- optional card ID
- optional boolean predicate

GameAI evaluates candidates through ShouldExecute.

A candidate succeeds when:

- the current card exists
- the action type matches
- the card ID matches, or the rule is generic
- the optional predicate returns true
- activation safety checks pass

Registration order therefore acts as action priority.

Initial APG interpretation:

- AddExecutor = register behavioral rule
- ExecutorType = action category
- CardId = target or trigger identity
- Func<bool> = contextual eligibility test
- ShouldExecute = constitutional decision gate
- ordered executor list = priority policy

## Priority Confirmation

Executor.AddExecutor appends rules to the Executors list.

GameAI iterates that list in order when evaluating available actions.

The first matching rule that passes ShouldExecute is returned as the selected action.

Therefore:

- registration order is executable priority
- deck behavior is encoded as ordered rules
- broad fallback rules should appear after specific rules
- changing constructor order can change gameplay without changing predicates
