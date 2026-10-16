# Experiment 6: Self-Signed X.509 Certificate

| Detail | Information |
|---|---|
| Student | P Ganesh |
| Course | Cryptography — CSL0509 |
| Programme | B.Tech AIML, V Semester |
| Faculty | Mr. Hirendra Singh Sengar |
| Academic year | 2026–27 |

**Evidence status:** Certificate generated, inspected and verified with OpenSSL. Actual terminal screenshots are pending.

## Aim

Create a self-signed X.509 certificate and analyze identity, public key, validity, extensions and trust.

## Run and procedure

```powershell
openssl version
python Exp06_X509_Certificate/run.py
```

The script generates an RSA-3072 key and a certificate signed with SHA-256, requests 365 days of validity, then inspects it with `openssl x509`. It verifies the certificate with an explicitly trusted copy, checks the correct hostname, and tests rejection of both a wrong hostname and an untrusted self-signed certificate.

## Attributes

| Attribute | Meaning / configured value |
|---|---|
| Subject | `C=IN, O=Cryptography Lab, CN=localhost` |
| Issuer | Same as subject: the certificate is self-signed |
| SAN | DNS `localhost`, IP `127.0.0.1` |
| Public key | RSA, 3072 bits |
| Signature | SHA-256 with RSA |
| Basic constraints | CA:FALSE; this is a leaf certificate |
| Key usage | Digital signature and key encipherment |
| Extended key usage | Server authentication |
| Validity | Concrete notBefore/notAfter dates appear in the saved output |
| Serial and fingerprint | Identify this generated certificate; regenerated certificates differ |

Read [certificate_details.txt](results/certificate_details.txt) for the actual serial, validity dates and extensions. The public [certificate.pem](results/certificate.pem) is included; its private key is not retained.

## Result and interpretation

Explicit-trust verification for `localhost` passed. A different hostname failed. Verification with no trusted CA source failed for the self-signed certificate. Its signature protects the certificate contents, but self-signing does not establish third-party identity trust. Valid dates and an intact signature alone are insufficient for public trust.

## Required screenshots to finish the submission

These are the captures still needed from the specified tool. Do not rename a rendered log image as a tool screenshot.

- [ ] `01_Certificate_Generation.png` — OpenSSL version and generation command
- [ ] `02_Certificate_Attributes.png` — subject, issuer, validity, SAN and extensions
- [ ] `03_Certificate_Verification.png` — trusted verification and rejection checks

Store the captures in a `screenshots` subfolder and add relative image links after the actual files exist.

## Recorded execution evidence

[Full execution log](results/execution.txt) · [Machine-readable results](results/summary.json)

The image below is a **rendered extract of the actual execution log**, not a screenshot of CrypTool, VS Code, Kali or Wireshark.

![Rendered execution log](results/execution_log.png)

## References

- [OpenSSL x509](https://docs.openssl.org/3.0/man1/openssl-x509/)
- [OpenSSL verify](https://docs.openssl.org/3.0/man1/openssl-verify/)
