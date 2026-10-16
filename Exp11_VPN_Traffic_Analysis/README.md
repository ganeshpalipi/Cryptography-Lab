# Experiment 11: VPN Traffic vs Plaintext Traffic

| Detail | Information |
|---|---|
| Student | P Ganesh |
| Course | Cryptography — CSL0509 |
| Programme | B.Tech AIML, V Semester |
| Faculty | Mr. Hirendra Singh Sengar |
| Academic year | 2026–27 |

**Evidence status:** Procedure prepared. Requires the two-VM OpenVPN lab from Experiment 15; no capture/results yet.

## Aim

Compare a controlled HTTP request sent directly across a lab network with the same request carried inside an encrypted OpenVPN tunnel.

## Prerequisites

Complete [Experiment 15](../Exp15_OpenVPN/README.md) first. Use your two host-only lab VMs. Example physical server IP: `192.168.56.10`; VPN server IP: `10.8.0.1`. Substitute your actual physical IP. The capture interface matters: observe the host-only physical interface for the outer encrypted packets, and the TUN interface for decrypted inner traffic.

## Procedure

1. On the server VM, create an otherwise empty directory containing only `marker.txt` with the content `CSL0509_VPN_LAB_ONLY`.
2. In that directory start the lab web server:

   ```bash
   python3 -m http.server 8000 --bind 0.0.0.0
   ```

   Use only the isolated lab VM network. Do not serve a directory containing private keys.
3. Start Wireshark on the physical host-only interface. From the client request the direct server address:

   ```bash
   curl http://192.168.56.10:8000/marker.txt
   ```

4. Stop and save `baseline_http.pcapng`. Filter `tcp.port == 8000`, then **Follow TCP Stream**. Verify whether the request and marker are readable.
5. Start a fresh physical-interface capture, with OpenVPN connected. From the client request the tunnel address:

   ```bash
   curl http://10.8.0.1:8000/marker.txt
   ```

6. Stop and save `vpn_outer.pcapng`. Filter `udp.port == 1194`. Inspect the OpenVPN/UDP stream and search for the test marker. Record the negotiated data cipher from the OpenVPN log; unreadable bytes alone are not proof of a secure configuration.
7. Optionally capture on `tun0` during a new tunnel request. The decrypted HTTP marker should be visible there. Save `vpn_inner.pcapng` separately and explain why this is expected at an endpoint.
8. Compare response content and record the actual interface names and IPs used.

## Observation table — fill from actual captures

| Capture | Interface | Request/marker readable? | Protocol/port observed | Evidence packet number |
|---|---|---|---|---|
| Direct HTTP | Physical host-only | Pending | Pending | Pending |
| VPN outer | Physical host-only | Pending | Pending | Pending |
| VPN inner (optional) | TUN | Pending | Pending | Pending |

## Analysis

A VPN protects traffic between its tunnel endpoints, while outer addresses, packet sizes and timing remain observable. It does not turn HTTP into end-to-end HTTPS beyond the VPN endpoint. Visibility of HTTP on the local TUN interface is expected after decryption. Compare separate captures to avoid confusing baseline traffic with tunneled traffic.

## Pending result

The configuration, successful request and captures must be obtained on the actual two-VM lab before adding a result statement.

## Required screenshots to finish the submission

These are the captures still needed from the specified tool. Do not rename a rendered log image as a tool screenshot.

- [ ] `01_Capture_Setup.png` — VM interface and capture filter
- [ ] `02_Direct_HTTP.png` — readable synthetic marker
- [ ] `03_VPN_Outer.png` — outer UDP packets and no readable marker in that stream
- [ ] `04_VPN_Connection.png` — negotiated data cipher and successful tunneled response

Store the captures in a `screenshots` subfolder and add relative image links after the actual files exist.

## References

- [OpenVPN manual](https://openvpn.net/community-docs/community-articles/openvpn-2-6-manual.html)
- [Wireshark documentation](https://www.wireshark.org/docs/)
