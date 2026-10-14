# Day 4: OSI Model, TCP Flags and Wireshark

Author: Qasim Mujahid

---

## OSI Model: SOC Analyst View

A SOC analyst uses the OSI model as a map during an investigation. It helps decide which layer a problem belongs to, and which logs and tools to check.

| Layer | What the analyst checks | Typical logs and tools | Example attacks |
|---|---|---|---|
| 7 Application | Web requests, DNS queries, emails, logins | Web server, proxy and DNS logs, WAF | SQL injection, XSS, phishing, DNS tunneling |
| 4 Transport | Ports, TCP flags, connection counts | Firewall logs, IDS/IPS, Wireshark | Port scans, SYN flood |
| 3 Network | Source and destination IPs, routes | Firewall and router logs, threat intelligence | IP spoofing, traffic to known malicious IPs |
| 2 Data Link | MAC addresses, devices on the local network | Switch and DHCP logs, ARP tables | ARP spoofing, rogue devices |
| 1 Physical | Cables, devices, physical access | Physical security records | Cable tapping, unauthorized device plugged in |
| 6 and 5 | Encryption, certificates, sessions | TLS and authentication logs | Session hijacking, fake certificates |

### How I would use it

- **Troubleshooting from the bottom up:** if a user has no network access, check the cable or Wi-Fi (layer 1), then the IP address and gateway with `ipconfig` (layer 3), then DNS with `nslookup` (layer 7), then whether a firewall blocks the port (layer 4).
- **Different tools see different layers:** a switch sees MAC addresses, a firewall sees IPs and ports, and a web proxy sees the actual requests. An analyst combines them to build the full story.
- **Encapsulation helps here:** one packet carries a MAC address, an IP address, a port and the application data, so a single packet can give evidence at several layers.

---

## TCP Flags

Flags are small on/off bits in the TCP header. They tell the receiver what a packet is for.

| Flag | Meaning | Simple explanation |
|---|---|---|
| **SYN** | Synchronize | Starts a connection and shares the starting sequence number |
| **ACK** | Acknowledge | Confirms that data (or a SYN or FIN) was received |
| **URG** | Urgent | Marks data as urgent so it is handled before the normal data. Rarely used today |
| **PSH** | Push | Tells the receiver to pass the data to the application right away, instead of waiting for the buffer to fill |
| **FIN** | Finish | A polite way to close the connection: "I have no more data to send" |
| **RST** | Reset | Ends the connection immediately. It is also the reply when a port is closed |

### Common flag combinations

| In Wireshark | What it means |
|---|---|
| `[SYN]` | Client asks to connect |
| `[SYN, ACK]` | Server accepts and answers |
| `[ACK]` | Client confirms. The connection is established |
| `[PSH, ACK]` | Data is being sent and acknowledged |
| `[FIN, ACK]` | One side is closing the connection |
| `[RST]` or `[RST, ACK]` | Connection refused or forcibly ended |

### Security view

- **Port scan:** many SYN packets from one source to many ports. Closed ports answer with RST-ACK, and open ports answer with SYN-ACK.
- **SYN flood:** a huge number of SYN packets with no final ACK, which overloads the server.
- **Unusual flag combinations:** a packet with no flags (NULL scan) or with FIN, PSH and URG together (Xmas scan) is not normal and is often used by scanning tools.
- **Many RST packets:** can mean closed ports being probed, or a connection being forced to end.

---

## Wireshark

Wireshark is a free tool that captures network traffic and shows every packet in detail. I installed it on my Windows PC (it also installs Npcap, which does the actual capturing) and used it on my own network to capture DNS and TCP traffic and look for simple issues.

### Filters I learned

| Filter | What it shows |
|---|---|
| `dns` | Only DNS traffic |
| `tcp` | Only TCP traffic |
| `icmp` | Ping traffic |
| `arp` | ARP traffic |
| `http` | Unencrypted web traffic |
| `ip.addr == 192.168.1.5` | All traffic to or from one IP address |
| `tcp.port == 443` | Traffic using port 443 |
| `tcp.dstport == 22` | Traffic going to port 22 |
| `tcp.flags.syn == 1` | Packets with the SYN flag set |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Only the first SYN packets (useful for spotting scans) |

### Other things I learned

- A filter is typed in the bar at the top, and it turns green when the syntax is valid.
- Clicking a packet shows its layers in the middle pane: Ethernet (layer 2), IP (layer 3), TCP or UDP (layer 4), and the application data such as DNS or HTTP (layer 7).
- **Follow, then TCP Stream** shows a whole conversation in one window.
- **Statistics, then Conversations** shows which hosts talk the most.

---

## What I Learned Today

- How a SOC analyst uses the OSI layers to decide where to look.
- What each TCP flag does, and how flag patterns can reveal scans and floods.
- How to install Wireshark, capture my own traffic, and use filters to find what I need.
