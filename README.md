# SISKI ALIFE (System for Intelligent Squad Kinesis & Intellect)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/qkff99/siski)

# [English](README_EN.md)
## [Changelog RU](changelog_ru.md)
## [Changelog EN](changelog_en.md)

## Описание
SISKI — модульная ALife-надстройка для Anomaly 1.5.3, которая управляет sim_squads через децентрализованную модель.

Текущая архитектура:
- engine callbacks -> `siski.bus` -> subscribers -> локальные keyed timers;
- без центрального poll-runtime и steady-state world scans;
- stalker и mutant логика разделены;
- vanilla jobs, smart logic и `axr_trade_manager` по возможности сохраняются.

С точки зрения геймплея SISKI:
- назначает отрядам задачи и цели;
- ведёт отдельный stalker task FSM и отдельный mutant FSM;
- старается сохранить ванильную совместимость и nil-safe fallback поведение.

## Настройки
Настройки доступны через `gamedata/configs/siski_settings.ltx` и MCM -> `SISKI`.

Актуальные группы настроек:
- общие переключатели;
- stalker tasks и targeting;
- mutant behavior;
- trade и fast trading;
- base/dynamic/service fillers;
- loot;
- cache/debug/logging knobs, которые реально используются текущим runtime.

Если вы ставите SISKI поверх старых версий SISKI/REZNYA, сбросьте настройки мода в MCM.

## Совместимость
- Anomaly 1.5.3 + Modded Exes.
- Целевая модель: vanilla ALife + modpacks, которые не ломают базовые engine callbacks и `SIMBOARD`.
- Боевые AI-моды уровня Redone AI / Enhanced Combat AI обычно не конфликтуют напрямую, потому что SISKI работает на уровне симулятивных отрядов, а не переписывает боевое поведение online NPC целиком.

## Важно
- Текущий runtime рассчитан на локальную decentralized-модель, а не на широкие world scans.
- SISKI пишет логи как обычные текстовые файлы. Это не “ломает игру”; логи нужны для диагностики.
- В репозитории нет отдельной build-системы. Базовая проверка — это syntax check `.script` файлов и in-game smoke/QA.
- Код открыт для использования и модификации, но это не обещание бесконечных микропатчей под каждую сборку.

## Репозиторий
- Основной bootstrap: [`gamedata/scripts/siski.script`](gamedata/scripts/siski.script)
- Runtime callback hub: [`gamedata/scripts/siski_core.script`](gamedata/scripts/siski_core.script)
- Основной config: [`gamedata/configs/siski_settings.ltx`](gamedata/configs/siski_settings.ltx)
- MCM schema: [`gamedata/scripts/siski_mcm_schema.script`](gamedata/scripts/siski_mcm_schema.script)
- Дизайн-документ: [`docs/siski_0.7_design_document.md`](docs/siski_0.7_design_document.md)
