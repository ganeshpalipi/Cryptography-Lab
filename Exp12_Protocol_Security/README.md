# Experiment 12: Secure and Insecure Protocols

| Detail | Information |
|---|---|
| Student | P Ganesh |
| Course | Cryptography — CSL0509 |
| Programme | B.Tech AIML, V Semester |
| Faculty | Mr. Hirendra Singh Sengar |
| Academic year | 2026–27 |

**Evidence status:** Capture procedure and local traffic fixture prepared. Wireshark evidence is pending.

## Aim

Identify protocols in captured traffic and compare their confidentiality, integrity and metadata exposure. The controlled practical compares HTTP and HTTPS; other protocols are discussed theoretically.

## Procedure

1. Run `python tools/local_web_lab.py` from the repository root. Use the same local fixture described in Experiment 10.
2. In Wireshark choose the loopback capture interface. Capture filter: `tcp port 8000 or tcp port 8443`.
3. In a second terminal make both requests, using the printed temporary certificate path:

   ```powershell
   curl.exe http://127.0.0.1:8000/CSL0509_LOCAL_LAB_ONLY
   curl.exe --cacert "C:\actual\temporary\cert.pem" https://127.0.0.1:8443/CSL0509_LOCAL_LAB_ONLY
   ```

4. Stop the capture and save `http_https_comparison.pcapng`.
5. Filter `tcp.port == 8000` and inspect **Follow TCP Stream**. Identify the method, URI, response and marker.
6. Filter `tcp.port == 8443` or `tls` and inspect TLS records. Without session keys, the HTTP request/response should not be readable in the captured stream.
7. Record endpoint addresses, TCP ports, packet sizes and timing that remain visible in both cases.
8. Capture the selected packet's protocol tree and both streams. Add actual packet numbers to your observations.

## Comparison

| Protocol | Protection / limitation | Evidence scope |
|---|---|---|
| HTTP | Application headers/body travel without TLS protection | Planned controlled capture |
| HTTPS | TLS protects application content, subject to correct certificate validation | Planned controlled capture |
| FTP / Telnet | Common plain variants expose application data/credentials | Theory only; not captured in this record |
| SFTP / SSH | SSH protects application traffic; host-key validation matters | Theory only; not captured in this record |
| Traditional DNS | Ordinary UDP/TCP DNS exposes queries | Theory only; not captured in this record |

Port numbers are clues, not proof: a protocol may use a non-default port. Confirm using the decoded protocol and handshake. HTTPS does not conceal all traffic metadata. Avoid drawing conclusions about FTP, Telnet or DNS captures that were not actually made.

## Pending result

The HTTP/TLS fixture was tested in [Experiment 10](../Exp10_TLS_Wireshark/results/execution.txt), but no Wireshark capture was possible in the preparation environment. Add the capture and observed packet-level findings to complete this experiment.

## Required screenshots to finish the submission

These are the captures still needed from the specified tool. Do not rename a rendered log image as a tool screenshot.

- [ ] `01_Protocol_Capture_Setup.png` — loopback interface and filter
- [ ] `02_HTTP_Stream.png` — readable request and marker
- [ ] `03_HTTPS_Stream.png` — TLS records and protected payload
- [ ] `04_Protocol_Comparison.png` — selected packets with protocol details

Store the captures in a `screenshots` subfolder and add relative image links after the actual files exist.

## References

- [Wireshark TLS](https://wiki.wireshark.org/TLS)
- [Wireshark loopback capture](https://wiki.wireshark.org/CaptureSetup/Loopback)
