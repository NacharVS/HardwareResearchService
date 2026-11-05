# DigitalWater PLC Research Standalone

Отдельная Windows-утилита для инженерного READ ONLY исследования PLC/OPC.

## Текущая версия

**v3.0**

Поддерживаемые режимы:

- **OPC UA** — прямое подключение к opc.tcp://..., Browse/Read, метаданные и текущие значения, экспорт JSON.
- **OPC DA Classic** — Windows COM/DCOM, поиск серверов через OPCEnum, выбор ProgID/CLSID, Browse ItemID, чтение стандартных свойств и при возможности Value/Quality/Timestamp, экспорт JSON.

Утилита автономна и не требует LocalApp, GlobalHub или Docker для исследования оборудования.

## Статус

| Компонент | Статус |
|---|---|
| OPC UA direct research | Реализован |
| OPC UA JSON export | Реализован |
| Автопересоздание собственного UA client certificate | Реализовано |
| OPC DA OPCEnum discovery | Реализован |
| OPC DA classic Browse | Реализован |
| OPC DA properties / Value / Quality / Timestamp | Реализован |
| OPC DA реальный E2E-тест на промышленном сервере | **Требуется** |
| DA3-only IOPCBrowse adapter | Пока не реализован |
| Файловое логирование | Пока не реализовано |

## READ ONLY

В standalone research utility не реализованы OPC UA Write, OPC DA Write и управляющие команды.

## Хранение исходника

Точная зафиксированная поставка v3.0 находится в:

source/DigitalWater_PLC_Research_Standalone_v3_0.zip

SHA-256 указан в source/SHA256SUMS.txt.

Архив содержит исходный C# проект, bootstrap/build scripts, README, OPC DA requirements и provenance.

Архив используется как immutable snapshot текущего standalone-проекта. Это позволяет не смешивать его с основным Researcher API.

## Сборка

GitHub Actions workflow:

.github/workflows/plc-research-standalone.yml

Собирает Windows x64 self-contained artifact независимо от ResearcherApiPrototype_1.

Локально можно использовать START_STANDALONE.bat из source archive.

## Архитектурное размещение

Этот проект специально хранится как отдельный tool/subproject внутри HardwareResearchService:

tools/PLCResearchStandalone/

Он не является частью runtime API Research Service и не должен влиять на его миграции, БД или deployment.
