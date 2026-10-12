# Lab 02 — SHA-256 and AES-256 Evidence Protection

**Case:** CASE-001 | **Status:** Original/decrypted content match verified.

## Artifact
Local file `kernal_usb_log.txt` (spelling as actually saved). A previous attempt to hash `kernal _usb_log.txt` failed because of an unintended space.

## Procedure
```bash
sha256sum kernal_usb_log.txt > ../Notes/kernal_usb_log.sha256
sha256sum -c ../Notes/kernal_usb_log.sha256
gpg --symmetric --cipher-algo AES256 --output kernal_usb_log.txt.gpg kernal_usb_log.txt
gpg --output ../Working/kernal_usb_log_verified.txt --decrypt kernal_usb_log.txt.gpg
sha256sum kernal_usb_log.txt ../Working/kernal_usb_log_verified.txt
sha256sum kernal_usb_log.txt.gpg > ../Notes/kernal_usb_log_encrypted.sha256
```

## Findings
- Original SHA-256 and decrypted working-copy SHA-256 matched: `dc30ac698e8ff3b6c86294827b6eaa3433ba031455b87d775ea0a86065d4c15f`.
- GPG reported AES256.CFB encryption; successful recovery with passphrase.
- First encryption attempt failed on passphrase-agent timeout; second succeeded.
- Recorded displayed file sizes: original 140K, encrypted 25K (text can compress before encryption).

## Limits
This establishes an encryption/decryption round-trip with matching bytes, not independent authenticity of source logs. GPG symmetric encryption is **not** AES-GCM and does not imply a separate GCM authentication tag. Local plaintext originals remain outside the encrypted artifact. An encrypted-file checksum was created; subsequent `-c` verification was requested but its result was not shown in the conversation. Do not present that check as completed.
