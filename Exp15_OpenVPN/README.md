# Experiment 15: OpenVPN Configuration and Verification

| Detail | Information |
|---|---|
| Student | P Ganesh |
| Course | Cryptography — CSL0509 |
| Programme | B.Tech AIML, V Semester |
| Faculty | Mr. Hirendra Singh Sengar |
| Academic year | 2026–27 |

**Evidence status:** Configuration generator prepared. OpenVPN service, TUN device and two-VM connectivity have not been executed here.

## Aim

Configure a certificate-authenticated encrypted VPN between two owned Linux lab VMs and verify communication through the tunnel.

## Topology and requirements

- Server and client: Kali/Linux VMs on an isolated host-only network.
- Example physical addresses: server `192.168.56.10`, client `192.168.56.11`; substitute your real lab IPs.
- Tunnel subnet: `10.8.0.0/24`, with server `10.8.0.1`.
- OpenVPN 2.6-compatible options, OpenSSL, Python 3 and a working TUN device.

No full-internet routing, NAT or DNS changes are needed for this lab. The preparation environment had no TUN device or OpenVPN executable, so a working tunnel cannot be claimed.

## Configuration procedure

1. In the server VM check `openvpn --version`, `openssl version` and the presence of `/dev/net/tun`.
2. From the repository root run:

   ```bash
   python3 Exp15_OpenVPN/setup_lab.py --server-ip 192.168.56.10
   ```

3. The generator refuses to replace an existing `.private` directory. It creates a lab CA, separate server/client certificates, private keys, a shared `tls-crypt` key and configurations. Certificates have appropriate serverAuth/clientAuth extensions and are checked against the CA.
4. Transfer only `.private/client` to the client VM using a trusted lab transfer method. Keep the CA private key and server private key on the server side; do not commit any `.private` content.
5. In the server's generated directory run:

   ```bash
   cd Exp15_OpenVPN/.private/server
   sudo openvpn --config server.conf
   ```

6. In the transferred client directory on the second VM run:

   ```bash
   sudo openvpn --config client.conf
   ```

7. If a firewall blocks the connection, allow UDP 1194 only from the client VM's lab IP; do not disable the entire firewall. Record both sides' actual log output.
8. After connection, inspect `ip -brief address` and the OpenVPN negotiated data cipher. From the client run `ping -c 4 10.8.0.1`. If ICMP is filtered, check the lab firewall before interpreting the result.
9. Use the HTTP marker and captures in Experiment 11 for a second verification of tunnel traffic.
10. Stop the foreground VPN processes with Ctrl+C after the lab. Retain only safe evidence, not private keys, in GitHub.

## Security design

The configurations require TLS 1.2 or newer, verify certificate roles, pin the expected server certificate name, and offer AES-GCM data ciphers. `tls-crypt` protects the control-channel packets. `dh none` permits ephemeral ECDH negotiation rather than requiring a custom finite-field DH parameter file. Compression is not enabled.

## Evidence to collect

Record client/server physical IPs, tunnel IPs, certificate verification result, negotiated cipher, successful ping/HTTP response and the exact version. A configuration file alone does not prove that a VPN connected or that traffic took the tunnel. The generator has been syntax-checked, but full OpenVPN execution remains pending.

## Required screenshots to finish the submission

These are the captures still needed from the specified tool. Do not rename a rendered log image as a tool screenshot.

- [ ] `01_Kali_OpenVPN_Setup.png` — versions and two-host network setup
- [ ] `02_Server_Connected.png` — server connection and negotiated cipher
- [ ] `03_Client_Connected.png` — client connection and tunnel IP
- [ ] `04_Tunnel_Verification.png` — successful traffic through 10.8.0.1

Store the captures in a `screenshots` subfolder and add relative image links after the actual files exist.

## References

- [OpenVPN 2.6 manual](https://openvpn.net/community-docs/community-articles/openvpn-2-6-manual.html)
