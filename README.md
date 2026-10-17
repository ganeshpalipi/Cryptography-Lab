# Cryptography Laboratory — CSL0509

**P Ganesh · B.Tech AIML, V Semester · Academic year 2026–27**

Faculty: Mr. Hirendra Singh Sengar

This repository contains 16 separately documented experiments. **The record is not yet submission-complete.** The table below separates executed work from the remaining tool-specific practical work and screenshots.

## Start here

- [Windows setup and run guide](START_HERE.md)
- [Remaining practical work](REMAINING_WORK.md)
- [Evidence provenance and validation](EVIDENCE.md)

## Experiment index and actual status

| No. | Experiment | Prepared / verified | Still required |
|---:|---|---|---|
| 1 | [Caesar, Vigenère, Rail Fence](Exp01_Classical_Ciphers/README.md) | Existing practical screenshots and README retained | None identified in existing image links |
| 2 | [Frequency analysis](Exp02_Frequency_Analysis/README.md) | Existing Caesar practical retained; four image filenames fixed | Image paths corrected and validated |
| 3 | [DES vs AES](Exp03_DES_AES/README.md) | CrypTool AES/DES round trips verified; five actual screenshots and both .cwm workspaces; supplemental OpenSSL benchmark | Controlled CrypTool timing |
| 4 | [RSA file encryption](Exp04_OpenSSL_RSA/README.md) | Windows PowerShell RSA-OAEP run and rejection checks passed; two actual screenshots recorded | None for the documented practical |
| 5 | [SHA-256 and signatures](Exp05_OpenSSL_Signatures/README.md) | OpenSSL signature and tamper tests passed | Actual terminal screenshots |
| 6 | [X.509 certificate](Exp06_X509_Certificate/README.md) | Certificate and trust/hostname tests passed | Actual terminal screenshots |
| 7 | [RSA and Diffie–Hellman](Exp07_RSA_Diffie_Hellman/README.md) | Python execution passed | Run/capture in required VS Code environment |
| 8 | [AES text application](Exp08_AES_Text_App/README.md) | CLI application and negative checks passed | VS Code screenshots |
| 9 | [Password hashing and salt](Exp09_Password_Hashing/README.md) | Python comparison executed | VS Code screenshots |
| 10 | [TLS capture](Exp10_TLS_Wireshark/README.md) | Local HTTP/TLS fixture executed | Wireshark capture and packet analysis |
| 11 | [VPN vs plaintext](Exp11_VPN_Traffic_Analysis/README.md) | Detailed controlled procedure prepared | Experiment 15 tunnel and Wireshark captures |
| 12 | [Secure/insecure protocols](Exp12_Protocol_Security/README.md) | Local fixture and procedure prepared | Wireshark HTTP/HTTPS capture |
| 13 | [John password audit](Exp13_John_Password_Audit/README.md) | Actual John dictionary and bounded PIN audit passed | Kali execution/environment screenshots |
| 14 | [SSH/RSA authentication](Exp14_SSH_Key_Authentication/README.md) | Key generation checked; two-host procedure prepared | Two-system public-key login and screenshots |
| 15 | [OpenVPN](Exp15_OpenVPN/README.md) | Private config/certificate generator prepared | Two-VM connection, tunnel verification and screenshots |
| 16 | [WPA2-AES WLAN](Exp16_WPA2_Packet_Tracer/README.md) | Topology and validation procedure prepared | Packet Tracer execution, .pkt and screenshots |

## Quick run

With Python 3.11+ and OpenSSL on PATH, install `requirements.txt` into a virtual environment, then run:

```powershell
python tools/run_supported.py
python tools/check_repository.py
```

The first command executes Experiments 4–9 and refreshes text/JSON evidence. It does not execute CrypTool, Wireshark, Kali or Packet Tracer. Other supplementary runners are described in their own README files.

## Evidence policy

Experiments 1–4 contain supplied tool screenshots. Newly prepared `results/execution_log.png` files are explicitly labeled **rendered execution log extracts**, not application screenshots. Full text logs and JSON summaries are alongside them. No failed/unexecuted practical has been represented as completed. Private keys and VPN profiles stay out of version control.

All new code and documentation were prepared with AI assistance, with command-line experiments executed in a Linux preparation environment. Review, understand and reproduce the required practicals in the assigned tools before submission, following the course's rules for assisted work.
