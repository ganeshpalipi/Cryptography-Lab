# Evidence provenance and validation

## Source and scope

- Base repository: https://github.com/ganeshpalipi/Cryptography-Lab
- Starting commit: 67a9c1b (the full commit is retained in Git history).
- Requirements: supplied Cryptography CSL0509 activity document, academic year 2026–27.
- Existing Experiments 1–2 were preserved; only Experiment 2's doubled PNG extensions were corrected.
- Preparation execution: Linux x86_64, Python 3.12.14, OpenSSL 3.0.13, cryptography 50.0.2. Per-run timestamps and versions are in execution logs.
- John was built from official source commit `5184bc0b8c105f8c5978b112e723d65b2de3e63e` and run against only locally generated synthetic hashes.

## What was executed

| Work | Verification |
|---|---|
| CrypTool DES/AES practical | Five user-supplied Windows CrypTool 2.1 Build 9778.2 screenshots dated 17 October 2026; AES-256-CBC and DES-ECB recover the original 21-character message |
| DES/AES supplement | 1 MiB round trips, five timed trials per cipher |
| RSA/OAEP | Exact file round trip, oversized input and modified ciphertext rejection |
| RSA-PSS signature | Saved signature verifies; changed message rejected |
| X.509 | Explicit trust and hostname pass; wrong hostname/untrusted certificate rejected |
| RSA/DH | Toy arithmetic, RSA-OAEP, shared-secret equality, HKDF and AES-GCM round trip |
| AES app | Unicode/empty input, wrong-key/tamper rejection, CLI file round trip |
| Password hashing | Equal unsalted hashes, distinct salted hashes, small dictionary/scrypt comparison |
| HTTP/TLS fixture | Actual localhost HTTP, TLS 1.2 and TLS 1.3 exchanges |
| John | Dictionary weak-password recovery and bounded three-digit PIN recovery |
| SSH supplement | RSA key generation and public-key fingerprint only |

OpenSSL signatures and certificate files were also independently verified after the scripts finished. The AES CLI was tested through its keygen/encrypt/decrypt commands, including verification that a wrong key writes no plaintext output.

## What was not executed

CrypTool was not executed in the Linux preparation environment; Experiment 3 was subsequently verified from the user's Windows screenshots. Controlled CrypTool timing and saved workspace uploads remain pending. Wireshark captures, two-system SSH authentication, an OpenVPN tunnel and Cisco Packet Tracer were not executed here. Raw capture permission was unavailable, and a TUN device and the required GUI tools were unavailable. The OpenVPN generator was syntax-checked only. Linux command-line execution is not evidence of using VS Code or Kali.

## Image provenance

New `results/execution_log.png` images render actual saved log extracts with a clear label. They may omit middle lines from long logs and lines with non-portable fonts; the full UTF-8 text is retained separately. They do not imitate application windows and do not substitute for the course's required screenshots. Re-running a script changes random keys, certificates, timings and some outputs; regenerate log images if you want them to match a new run.

## Reproduction

Run each listed script from the repository root following its README. Python assertions enforce the stated comparisons. Do not run with Python's `-O` option because it disables assertions. `tools/check_repository.py` validates local image references and the 16 README folders, not practical completion.

Public lab test keys/passwords in examples are teaching inputs. Actual generated private keys are temporary or kept under ignored `.private` paths; no reusable private key is included in the deliverable.
