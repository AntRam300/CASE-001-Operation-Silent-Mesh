# Evidence Register — Public Sanitized Summary

| Reference | Artifact | Status / location |
|---|---|---|
| E-001 | Device inventory/photograph | Device observed; full inventory privately maintained; formal inventory not shown complete |
| E-002 | USB enumeration export | Local `Evidence/E-002-usb-identification.txt` listed |
| E-003 | Serial identification export | Local `Evidence/E-003-serial-identification.txt` listed |
| E-004 | Full flash acquisition | Local `Evidence/CASE-001-E004-original-flash.bin`, 16 MiB, SHA-256 verified |
| Working | Flash analysis copy | Local `Working/CASE-001-E004-analysis.bin`, matching original hash reported |
| Working | SPIFFS / NVS / OTA / core dump | Extracted partition binaries in local `Working/`, manifests in `Notes/`, reported checksum checks passed |
| Host log | `kernal_usb_log.txt` | Original SHA-256 and decrypted-copy SHA-256 match; encrypted GPG copy retained locally |

The USB export labels and E-004 flash acquisition are taken from actual filenames; earlier planning templates used inconsistent labels. This register is authoritative only for the observed artifacts described here. Exact collector, chain-of-custody events and acquisition timestamps should be transcribed from local originals before submitting a formal case report.
