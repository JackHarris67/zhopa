# ZHOPA ALIFE
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/qkff99/zhopa)

# [English](README_EN.md)
## [Changelog RU](changelog_ru.md)
## [Changelog EN](changelog_en.md)

## Описание
ZHOPA — модульная ALife-надстройка для Anomaly 1.5.3, которая управляет sim_squads через децентрализованную модель.

Текущая архитектура:
- engine callbacks -> `zhopa.bus` -> subscribers -> локальные keyed timers;
- без центрального poll-runtime и steady-state world scans;
- stalker и mutant логика разделены;
- vanilla jobs, smart logic и `axr_trade_manager` по возможности сохраняются.

С точки зрения геймплея ZHOPA:
- назначает отрядам задачи и цели;
- ведёт отдельный stalker task FSM и отдельный mutant FSM;
- старается сохранить ванильную совместимость и nil-safe fallback поведение.

## Настройки
Настройки доступны через `gamedata/configs/zhopa_settings.ltx` и MCM -> `ZHOPA`.

Актуальные группы настроек:
- общие переключатели;
- stalker tasks и targeting;
- mutant behavior;
- trade и fast trading;
- base/dynamic/service fillers;
- loot;
- cache/debug/logging knobs, которые реально используются текущим runtime.

Если вы ставите ZHOPA поверх старых версий ZHOPA/REZNYA, сбросьте настройки мода в MCM.

## Совместимость
- Anomaly 1.5.3 + Modded Exes.
- Целевая модель: vanilla ALife + modpacks, которые не ломают базовые engine callbacks и `SIMBOARD`.
- Боевые AI-моды уровня Redone AI / Enhanced Combat AI обычно не конфликтуют напрямую, потому что ZHOPA работает на уровне симулятивных отрядов, а не переписывает боевое поведение online NPC целиком.

## Важно
- Текущий runtime рассчитан на локальную decentralized-модель, а не на широкие world scans.
- ZHOPA пишет логи как обычные текстовые файлы. Это не “ломает игру”; логи нужны для диагностики.
- В репозитории нет отдельной build-системы. Базовая проверка — это syntax check `.script` файлов и in-game smoke/QA.
- Код открыт для использования и модификации, но это не обещание бесконечных микропатчей под каждую сборку.

## Репозиторий
- Основной bootstrap: [`gamedata/scripts/zhopa.script`](gamedata/scripts/zhopa.script)
- Runtime callback hub: [`gamedata/scripts/zhopa_core.script`](gamedata/scripts/zhopa_core.script)
- Основной config: [`gamedata/configs/zhopa_settings.ltx`](gamedata/configs/zhopa_settings.ltx)
- MCM schema: [`gamedata/scripts/zhopa_mcm_schema.script`](gamedata/scripts/zhopa_mcm_schema.script)
- Дизайн-документ: [`docs/zhopa_0.7_design_document.md`](docs/zhopa_0.7_design_document.md)
