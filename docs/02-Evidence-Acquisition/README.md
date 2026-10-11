# Phase 02 — Evidence Acquisition and Preservation

**Case ID:** CASE-001

**Case Name:** Operation Silent Mesh

**Status:** Planning — Acquisition not yet performed

## 1. Objective

Identify and acquire accessible forensic artifacts from a personally owned Meshtastic LoRa radio while documenting the source device, collection method, and potential evidence alterations.

## 2. Evidence Sources

| Evidence ID | Artifact | Status |
|---|---|---|
| E-001 | Device hardware inventory | Planned |
| E-002 | USB identification output | Planned |
| E-003 | Meshtastic device information | Planned |
| E-004 | Node database information, if available | Planned |
| E-005 | Host acquisition logs | Planned |

## 3. Acquisition Environment

- Operating System: Arch Linux
- Primary Evidence Device: One Meshtastic LoRa node
- Interface: USB serial, pending verification
- Tools: Meshtastic CLI, lsusb, sha256sum
- Device Model: To be determined
- Firmware Version: To be determined

## 4. Acquisition Procedure

1. Photograph and identify the physical device.
2. Record acquisition date, time, timezone, and examiner.
3. Record workstation operating system and tool versions.
4. Document the device's initial power and connection state.
5. Identify the device using available USB information.
6. Perform a documented logical device-information acquisition.
7. Record any changes caused by interacting with the device.
8. Generate SHA-256 hashes for acquired files.
9. Preserve originals separately from analysis copies.
10. Update the evidence register and acquisition log.

## 5. Evidence Integrity

Each collected artifact will receive a unique evidence identifier and SHA-256 hash.

Hashes will be verified against preserved copies to detect subsequent changes.

A hash establishes file integrity relative to a known reference; it does not independently prove that acquisition was complete or that the original device was unaltered.

## 6. Limitations

Meshtastic CLI acquisition is a logical collection method and not a complete physical image of device flash memory.

Connecting, powering, or querying the radio may change certain device states or records. These potential alterations must be documented.

## 7. Completion Checklist

- [ ] Physical device inventory completed
- [ ] USB connection identified
- [ ] Acquisition logs preserved
- [ ] Device information collected
- [ ] Available artifacts inventoried
- [ ] SHA-256 hashes generated and verified
- [ ] Sanitized documentation prepared for GitHub

## 8. Next Phase

Phase 03 — Forensic Analysis.
