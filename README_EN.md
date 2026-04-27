# SISKI ALIFE (System for Intelligent Squad Kinesis & Intellect)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/qkff99/siski)

# [Русский](README.md)
## [Changelog RU](changelog_ru.md)
## [Changelog EN](changelog_en.md)

## Description
SISKI is a modular ALife layer for Anomaly 1.5.3 that drives simulation squads through a decentralized runtime model.

Current architecture:
- engine callbacks -> `siski.bus` -> subscribers -> local keyed timers;
- no central poll runtime and no steady-state world scans;
- separate stalker and mutant control paths;
- vanilla jobs, smart logic and `axr_trade_manager` are preserved where practical.

Gameplay-wise SISKI:
- assigns squad tasks and targets;
- runs a stalker task FSM and a separate mutant FSM;
- tries to preserve vanilla compatibility and nil-safe fallback behavior.

## Settings
Settings are available through `gamedata/configs/siski_settings.ltx` and MCM -> `SISKI`.

Current user-facing groups:
- general toggles;
- stalker tasks and targeting;
- mutant behavior;
- trade and fast trading;
- base/dynamic/service fillers;
- loot;
- cache/debug/logging knobs that are still used by the current runtime.

If you install SISKI over older SISKI/REZNYA versions, reset the mod settings in MCM.

## Compatibility
- Anomaly 1.5.3 + Modded Exes.
- Target environment: vanilla ALife + modpacks that keep the core engine callbacks and `SIMBOARD` intact.
- Combat AI mods such as Redone AI / Enhanced Combat AI usually do not conflict directly, because SISKI operates at the simulation-squad layer rather than replacing all online combat behavior.

## Important
- The current runtime is local and decentralized rather than based on broad world scans.
- SISKI writes plain text logs. That does not “break the game”; the logs exist for diagnostics.
- There is no standalone build pipeline in this repo. Normal verification is syntax checking `.script` files plus in-game smoke/QA.
- The code is open to use and modify, but that is not a promise of endless micro-patches for every individual modpack.

## Repository
- Main bootstrap: [`gamedata/scripts/siski.script`](gamedata/scripts/siski.script)
- Runtime callback hub: [`gamedata/scripts/siski_core.script`](gamedata/scripts/siski_core.script)
- Main config: [`gamedata/configs/siski_settings.ltx`](gamedata/configs/siski_settings.ltx)
- MCM schema: [`gamedata/scripts/siski_mcm_schema.script`](gamedata/scripts/siski_mcm_schema.script)
- Design document: [`docs/siski_0.7_design_document_en.md`](docs/siski_0.7_design_document_en.md)
