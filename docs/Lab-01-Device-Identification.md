# Lab 01 — USB and Serial Interface Identification

**Case:** CASE-001 | **Status:** Host-side identification complete; Meshtastic query unsuccessful.

## Environment and method
Arch Linux workstation `Mujine`; commands: `lsusb`, `ls -l /dev/serial/by-id/`, `ls -l /dev/ttyACM0`, `id -nG`, `fuser`, and `journalctl -k -b`. The device had an active display showing `WiFi Scan`, `RSSI -255` and `LoRa Error` (as observed by the examiner).

## Results
- USB VID:PID `303a:1001`, Espressif USB JTAG/serial debug interface.
- USB enumeration log recorded manufacturer Espressif and device revision `1.01`.
- `cdc_acm` created `/dev/ttyACM0`.
- Serial permissions `crw-rw---- root:uucp`; examiner subsequently verified membership in `uucp`.
- `fuser -v /dev/ttyACM0` reported no process at check time.
- Meshtastic Python CLI **2.7.11** installed but `meshtastic --port /dev/ttyACM0 --info` timed out.
- A mistyped `/dev/ttyACMO` path (letter O) returned file not found; a command with a trailing backslash was interrupted.

## Interpretation
USB enumeration and serial device registration were verified. This does **not** establish successful Meshtastic protocol exchange, LoRa transmitter function, or successful over-the-air communication. Actual firmware identity remains unverified. Line numbers 1059 (USB) and 1423 (serial) referred to a particular local log view, not permanent system-wide identifiers; use timestamps and original export for provenance.

## Handling
Raw journal exports and persistent device identifiers remain local. Reproduce with the commands above; preserve timestamp, tool versions and a SHA-256 of each exported record.
