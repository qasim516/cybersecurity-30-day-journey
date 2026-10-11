# Day 2: DNS, TCP vs UDP, and Network Commands

Author: Qasim Mujahid

Topics covered: DNS, TCP vs UDP, and the commands I ran on my own PC (`ipconfig`, `ipconfig /all`, `ping`, `nslookup`).

---

## DNS (Domain Name System)

DNS translates human-readable domain names into IP addresses, so users can type `google.com` instead of remembering an IP address.

**Example:** I save a phone number in my contacts under the name "Qasim". Now I do not have to remember the number `03XX-XXXXXXX`. When I tap "Qasim", the phone looks up the number and calls it. DNS works the same way: the domain name is the contact name, and the IP address is the phone number.

### Common DNS record types

| Record | What it does | Example |
|---|---|---|
| **A** | Name to IPv4 address | `google.com` to `142.250.180.14` |
| **AAAA** | Name to IPv6 address | `google.com` to `2a00:1450:...` |
| **CNAME** | A name that points to another name | `www.example.com` to `example.com` |
| **MX** | Mail server for the domain | Where emails for the domain are delivered |
| **TXT** | Extra text, used for email security and verification | SPF and DKIM records |

### DNS port and protocol

DNS uses **port 53**. It usually uses **UDP** (fast, for small questions) and uses **TCP** when answers are large.

### Security view

- **DNS logs:** show which websites a device tried to reach. If a computer contacts strange or random-looking domains, it can be a sign of malware.
- **DNS spoofing (poisoning):** an attacker feeds a fake answer, so the user goes to a fake website instead of the real one.
- **DNS tunneling:** attackers hide stolen data inside DNS requests.
- SOC analysts check DNS logs to find infected machines.

---

## TCP vs UDP

**TCP (Transmission Control Protocol)** is connection-oriented and reliable. It uses a three-way handshake and acknowledgements.
**UDP (User Datagram Protocol)** is connectionless and faster, but it does not guarantee delivery.

TCP suits web and email. UDP suits streaming, gaming, and DNS.

**Example:** TCP is like a phone call: if I miss something, I can ask the other person to repeat it. UDP is like a live radio broadcast: if I miss a part, it is gone.

### TCP three-way handshake

1. **SYN:** the client says, "I want to connect."
2. **SYN-ACK:** the server says, "OK, I am ready. Are you ready?"
3. **ACK:** the client says, "Yes, let's start."

After that, data flows. TCP stays reliable in these ways:

- Data is split into numbered pieces (**sequence numbers**).
- The receiver sends **acknowledgements** (ACKs), for example "I got pieces 1 to 5."
- If an ACK does not arrive, the sender **resends** that piece.
- At the end, the connection is closed properly using **FIN** packets.

### UDP details

UDP just sends the data. It has:

- No handshake
- No acknowledgement
- No resending
- No guarantee of order

Because of this, it is lighter and faster.

### Comparison table

| | TCP | UDP |
|---|---|---|
| Connection | Handshake first | No connection |
| Reliable? | Yes, resends lost data | No |
| Order | Arrives in order | May arrive out of order |
| Speed | Slower | Faster |
| Overhead | Higher | Lower |
| Used for | Websites (HTTP/HTTPS), email, SSH, file transfer | DNS lookups, video calls, live streaming, online games |

### Security view

- **SYN scan:** tools like Nmap send SYN packets to many ports and watch the replies to find open ports.
- **SYN flood:** an attacker sends huge numbers of SYN packets and never completes the handshake, which overloads the server.
- **UDP floods and amplification attacks:** these abuse UDP's lack of a handshake.
- In Wireshark, I can see the SYN, SYN-ACK, and ACK packets of a real connection.

---

## Commands I Ran

All commands were run on my own Windows PC in Command Prompt. Private details (MAC address, last parts of local IP addresses) are hidden.

### 1. `ipconfig`

**Purpose:** shows my network settings.

| Item | Result |
|---|---|
| IPv4 address | `192.168.x.x` (hidden) |
| Subnet mask | `255.255.255.0` |
| Default gateway (router) | `192.168.x.x` (hidden) |

**What it means:** the IPv4 address is my device's address on the local network, and the default gateway is my router.

### 2. `ipconfig /all`

**Purpose:** shows more details, including the MAC address and DNS servers.

| Item | Result |
|---|---|
| Physical address (MAC) | `XX-XX-XX-XX-XX-XX` (hidden) |
| DHCP enabled | Yes |
| DNS server | My router |

**What it means:** DHCP enabled = Yes means my router gave me the IP address automatically. The DNS server is the one my PC asks to translate names into IP addresses.

### 3. `ping google.com`

**Purpose:** tests whether I can reach Google and measures the delay.

| Item | Result |
|---|---|
| Reply from | `2a00:1450:4018:80e::200e` (an IPv6 address) |
| Time | 42 ms |
| Packets sent / received / lost | 4 / 4 / 0 |
| Average time | 42 ms |

**What it means:** 0% packet loss means my connection is stable. The time is the round-trip delay. The reply came from an IPv6 address, so my PC reached Google over IPv6.

### 4. `nslookup google.com`

**Purpose:** asks DNS for the IP address of a website.

| Item | Result |
|---|---|
| DNS server that answered | My router (`192.168.x.x`) |
| IP address of google.com | `142.250.187.14` (IPv4) |
| Non-authoritative answer | Yes |

**What it means:** "Non-authoritative" means the answer came from a resolver or cache, not directly from Google's own DNS server. `nslookup` listed an IPv4 address (A record), while `ping` used an IPv6 address (AAAA record). Both belong to google.com.

---

## What I Learned

- DNS turns names into IP addresses, and it uses port 53.
- TCP is reliable and uses a three-way handshake. UDP is faster but does not guarantee delivery.
- `ipconfig`, `ping`, and `nslookup` show my IP settings, my connection quality, and how DNS answers.
