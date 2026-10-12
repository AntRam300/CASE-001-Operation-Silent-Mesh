# Lab 03 — Heltec Hardware Identification and Flash Acquisition

**Case:** CASE-001 | **Status:** Flash image acquired and its recorded SHA-256 successfully checked.

## Hardware identification
Examiner identifies manufacturer as **Heltec**; exact board revision pending. `esptool 5.5.0` queried `/dev/ttyACM0` and returned ESP32-S3 (QFN56), revision v0.2, 40 MHz crystal, USB-Serial/JTAG, embedded 2 MB PSRAM and 16 MB SPI flash. These specifications are consistent with a WiFi LoRa 32 V4 configuration, but are not definitive proof of board revision. Unique MAC excluded from public records.

## Acquisition
```bash
python -m esptool --port /dev/ttyACM0 chip-id
python -m esptool --port /dev/ttyACM0 flash-id
python -m esptool --port /dev/ttyACM0 read-flash 0 ALL Evidence/CASE-001-E004-original-flash.bin
sha256sum Evidence/CASE-001-E004-original-flash.bin > Notes/CASE-001-E004-original-flash.sha256
sha256sum -c Notes/CASE-001-E004-original-flash.sha256
cp Evidence/CASE-001-E004-original-flash.bin Working/CASE-001-E004-analysis.bin
```

The saved image size was **16,777,216 bytes** (16 MiB), and the checksum comparison returned `OK`. Analysis and original image hashes later matched as reported by the examiner. Actual image SHA-256 value is stored in the local private manifest; no value is invented here.

## Important limitations
Esptool entered downloader mode and performed hard resets via RTS, so the collection was not zero-impact on volatile state. A verified SHA-256 binds the saved bytes to the manifest; it cannot prove all source flash was recovered error-free. Preserve original raw image privately; do not upload flash image to GitHub.
