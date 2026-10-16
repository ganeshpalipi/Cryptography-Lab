# Experiment 16: WPA2-AES Wireless Network

| Detail | Information |
|---|---|
| Student | P Ganesh |
| Course | Cryptography — CSL0509 |
| Programme | B.Tech AIML, V Semester |
| Faculty | Mr. Hirendra Singh Sengar |
| Academic year | 2026–27 |

**Evidence status:** Topology plan and procedure prepared. Packet Tracer execution, .pkt file and screenshots are pending.

## Aim

Build a small WLAN using WPA2-Personal with AES, connect authorized clients, and verify that a client with an incorrect key cannot associate successfully.

## Proposed topology

Use one wireless router (for example WRT300N) and two laptops with compatible wireless adapters. Device labels and exact menus depend on the Packet Tracer version.

| Setting | Lab value |
|---|---|
| SSID | `CSL0509-LAB` |
| Router LAN address | `192.168.10.1/24` |
| DHCP | Enabled; pool begins at `192.168.10.100` |
| Security mode | WPA2-Personal |
| Encryption | AES |
| Example lab-only passphrase | `LabOnly-BlueRiver-4827!` |
| Router administration | Change the default admin password; disable remote management |

The published passphrase is only a lab fixture. Use a separate private passphrase on a real WLAN. SSID hiding and MAC filtering are not substitutes for encryption and authentication.

## Packet Tracer procedure

1. Add a compatible wireless router and two laptops to the workspace.
2. If a laptop has no wireless adapter, power it off in its Physical tab, replace the network module with a compatible wireless module such as WPC300N, then power it on.
3. Open the router GUI. Set its LAN address/subnet and DHCP pool. Save changes.
4. Under Wireless settings, set SSID `CSL0509-LAB`. Under Wireless Security, choose **WPA2 Personal** and **AES**, enter the lab passphrase and save.
5. On each laptop open Desktop → PC Wireless (or the equivalent Wireless interface settings). Select the SSID and configure the same WPA2 passphrase. Use DHCP for IP configuration.
6. Check each client has an address in `192.168.10.0/24` and the gateway `192.168.10.1`. Record the actual assigned addresses rather than assuming the first lease.
7. From one laptop's command prompt ping the router and then the other laptop. Initial packets may be consumed by ARP resolution; repeat and record the observed result.
8. Disconnect the second laptop and remove/update its saved wireless profile. Try an incorrect passphrase and confirm a fresh association fails. A cached old connection is not a valid negative test.
9. Restore the correct key, reconnect and verify reachability again.
10. Save the actual topology as `Exp16_WPA2_Lab.pkt` in this folder and capture the evidence below.

## Analysis and pending result

WPA2-Personal authenticates clients using the shared secret and uses AES-CCMP for link protection when configured for AES. A weak shared passphrase can still be guessed. This protects the wireless link, not every subsequent network hop. Packet Tracer simulates device behavior; successful pings alone do not prove a cryptographic implementation, so document the security settings and negative association test as well.

No `.pkt` file or successful network result is claimed until this procedure is executed in Packet Tracer.

## Required screenshots to finish the submission

These are the captures still needed from the specified tool. Do not rename a rendered log image as a tool screenshot.

- [ ] `01_PacketTracer_Topology.png` — router, two laptops and tool environment
- [ ] `02_WPA2_AES_Settings.png` — SSID and WPA2/AES settings
- [ ] `03_Client_IP_Association.png` — successful associations and actual DHCP addresses
- [ ] `04_Connectivity_Test.png` — router/client pings
- [ ] `05_Wrong_Key_Test.png` — failed fresh association with the wrong passphrase

Store the captures in a `screenshots` subfolder and add relative image links after the actual files exist.

## References

- [Cisco Packet Tracer wireless security lab](https://contenthub.netacad.com/legacy/I2IoT/2.0/en/course/files/5.1.2.6%20Packet%20Tracer%20-%20Configure%20Wireless%20Security.pdf)
