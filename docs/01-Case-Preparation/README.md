# CASE-001: Operation Silent Mesh

## Phase 01 — Case Preparation

**Investigation:** Meshtastic Radio Communications Forensics

**Case Identifier:** CASE-001

**Investigation Type:** Simulated Digital Forensics and Incident Response (DFIR)

**Current Status:** Planning

### 1. Case Background

Operation Silent Mesh is a simulated digital-forensics investigation involving a Meshtastic radio potentially associated with unauthorized communications.

The purpose is to identify, preserve, collect, and analyze available digital artifacts from the radio and associated network infrastructure.

All investigative activities will occur in an authorized laboratory environment.

### 2. Investigative Objectives

1. Identify the Meshtastic device and its firmware.
2. Document the laboratory environment.
3. Establish evidence acquisition and preservation procedures.
4. Examine accessible radio communication artifacts.
5. Integrate network analysis using GNS3 and Wireshark.
6. Reconstruct a timeline from available evidence.
7. Produce a professional forensic investigation report.

### 3. Laboratory Equipment

| Equipment | Purpose |
|---|---|
| Meshtastic LoRa Node | Primary device under examination |
| Arch Linux Workstation | Evidence collection and analysis |
| Meshtastic CLI | Logical device acquisition |
| Wireshark | Network traffic analysis |
| GNS3 | Simulated network infrastructure |
| SHA-256 Utility | Evidence integrity verification |

### 4. Evidence Preservation

Evidence collection will prioritize minimal alteration of the original device.

Each acquired artifact will be documented using an evidence identifier, acquisition timestamp, tool version, source, and SHA-256 hash.

Original evidence will be preserved separately from analysis copies.

### 5. Investigative Limitations

The investigation currently involves one physical Meshtastic node.

Logical acquisition may not recover all historical messages, deleted records, or internal flash artifacts.

Conclusions will distinguish confirmed observations from investigative assumptions.

### 6. Project Status

- [x] Create GitHub repository.
- [x] Establish initial documentation directory.
- [ ] Record device inventory.
- [ ] Establish acquisition procedures.
- [ ] Conduct initial device identification.
- [ ] Verify collected evidence integrity.

### 7. Next Phase

Proceed to Phase 02: Evidence Acquisition and Preservation.
