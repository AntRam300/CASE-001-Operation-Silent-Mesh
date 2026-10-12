# Lab 04 — ESP32-S3 Firmware, Partition and Crash Dump Examination

**Case:** CASE-001 | **Status:** Static analysis completed through core-dump structural examination; crash cause and running firmware identity unresolved.

## Method
Offline analysis of `Working/CASE-001-E004-analysis.bin` using `xxd`, `file`, `dd`, `readelf`, Python and `esptool image-info`. Original full-flash image preserved and verified. The `file` tool called the complete flash a DOS COM executable; manual header and esptool analysis showed the more relevant ESP32 image structure. An attempted unsupported `esptool image-info --version 2` option produced a CLI error, not an invalid firmware image.

## Bootloader and application
At `0x000000`, magic `E9`; `esptool 5.5.0` identified ESP32-S3 image, four segments, DIO, 80 MHz, 16MB declared flash, valid checksum `0x4B`, valid internal validation digest. At `0x010000`, `app0` begins with `E9 07` and was extracted in full (1,310,720 bytes). Esptool reported seven segments, valid checksum `0xBC`, valid internal validation digest; project `arduino-lib-builder`, app version `6683a0d`, build timestamp `2024-06-24 13:24:30` (timezone not established), ESP-IDF `v5.1.4-358-gbd2b9390ef-dirty`. This is not a definitive user-facing firmware name. The first 64 bytes of `app1` were FF, not proof the entire slot is erased.

## Partition table
The table at `0x8000` had six entries and a terminator (`EB EB` at `0x80C0`):

| Partition | Offset | Size |
|---|---|---|
| nvs | `0x9000` | 20,480 bytes |
| otadata | `0xE000` | 8,192 bytes |
| app0 | `0x10000` | 1,310,720 bytes |
| app1 | `0x150000` | 1,310,720 bytes |
| spiffs | `0x290000` | 1,441,792 bytes |
| coredump | `0x3F0000` | 65,536 bytes |

## Partition findings
**SPIFFS:** All 1,441,792 bytes were `FF` (non-FF count 0). Consistent with erased flash at acquisition, not evidence it was never used.

**NVS:** 20,480 bytes, 3,607 non-FF and 16,873 FF. Five 4 KiB pages had non-FF counts of `[3117, 490, 0, 0, 0]`. Strings `misc` and `nvs.net80211` are consistent with NVS/networking-related metadata; no confirmed historical Wi-Fi association or user communications. The partition's recorded SHA-256 verified `OK`.

**OTA:** 8,192 bytes, 12 non-FF bytes. Sector 0: sequence `1`, state `0xFFFFFFFF` (undefined), recorded CRC `0x4743989A`; sector 1: sequence `0`, state and CRC all FF. The available fields are consistent with selection of `app0`, but do not prove successful execution or historical update activity. Recorded OTA hash verified `OK`.

**Core dump:** 65,536 bytes, 28,893 non-FF, 36,643 FF. ESP-IDF-style wrapper followed by ELF magic at partition offset `0x14`. Extracted file 65,516 bytes classified by `file` as ELF32 little-endian Tensilica Xtensa `CORE`. `readelf` listed eight program headers (three NOTE and five LOAD) and three `NT_PRSTATUS` notes, with `ESP_CORE_DUMP_INFO` and `ESP_EXTRA_INFO` notes. Record starts `64 73 00 00`; last non-FF byte at `0x737F`; four-byte field `1D 92 25 23` at `0x7360` remains unidentified. No proven crash date, cause, or connection to the displayed LoRa error. The partition hash verified `OK`.

## Crash-tool limitations
`esp-coredump 1.17.2` installed, supports `info_corefile`; matching firmware ELF with debug symbols unavailable, `xtensa-esp32s3-elf-gdb` not found on PATH, host `/usr/bin/gdb` present. Detailed symbolic crash attribution deferred.

## Integrity, claims, and scope
All reported partition SHA-256 checks passed against locally saved manifests. CRC and embedded image digest checks are firmware-structure checks, not independent authentication of the 16 MiB collection. No radio transmissions or Meshtastic application-protocol session were established. Raw flash, dumps, credentials, persistent hardware identifiers and unredacted logs are not published.

## Next steps
Confirm exact board revision, identify/backup current firmware as far as practical, prepare correct Meshtastic firmware, explicitly record changes introduced by flashing, configure an authorized test node and then examine controlled communications.
