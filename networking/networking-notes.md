# Day 1: Networking Basics

Topics covered: IP address, router, MAC address, ports.

---

## IP Address

An **IP address** is a unique identifier that lets a device communicate over a network, including the internet. IP stands for **Internet Protocol**.

There are two versions in use:

- **IPv4**
  - Introduced in 1983 and still widely used.
  - Four numbers separated by dots, for example `192.168.8.1`.
  - It supports about 4.3 billion unique addresses, which is not enough for the number of devices that are now online.
- **IPv6**
  - Uses a longer format of numbers and letters (hexadecimal) separated by colons, for example `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.
  - A double colon (`::`) can be used to shorten groups of zeros.
  - It supports about 340 undecillion unique addresses, which solves the shortage.

**Why is there no IPv5?**
IPv5 was an experimental protocol for streaming data and was never widely deployed. It used the same 32-bit addresses as IPv4, so it would not have solved the address shortage.

### Static vs Dynamic IP

- **Static IP:** stays the same and does not change on its own. It is useful for hosting websites and running home servers.
- **Dynamic IP:** changes automatically over time. The address is assigned automatically (usually by DHCP), and this is still very common.

### Security view

In logs, the IP address tells a SOC analyst where traffic came from. Repeated failed logins from one IP address are a classic sign of a brute-force attack.

---

## Router

A router guides and directs network data. Data travels in **packets**, which carry files, messages, and other online activity.

- A home router connects our private network (local IPs) to the internet (public IP).
- It uses **NAT (Network Address Translation)** so many devices can share one public IP address.

---

## MAC Address

A **MAC address** is the permanent ID of a device's network card. It is like a serial number assigned to the hardware when it is made. A comparison: it is like a CNIC number, which stays with the person.

Example: `A4:5E:60:B1:23:CF`

- The first half identifies the manufacturer of the card.
- The second half is the unique number given to that card.

Our home network (all devices connected to the same router) is a small local area network. Inside it, devices need to know exactly which device to send data to, so they use MAC addresses.

Note: a MAC address is normally fixed by the manufacturer, but it can be changed (spoofed) by software, and many phones use random MAC addresses on Wi-Fi for privacy.

---

## Ports

A **port** is a numbered door on a computer. Each port is used by one program or service to send and receive data.

Example: the IP address is the location of a hotel, and the port is the room number inside it.

### Why are ports needed?

Our system runs many network programs at the same time, such as browsers, WhatsApp, YouTube, and Gmail. They all share the same IP address. Ports let the system know which data belongs to which program.

An IP address and a port are written together:

```
142.250.180.14:443
```

Here `142.250.180.14` is the IP address and `443` is the port number.

### Port ranges

There are 65,536 port numbers in total (0 to 65535).

| Range | Type | Use |
|---|---|---|
| 0 - 1023 | Well-known ports | Standard services (for example HTTP, HTTPS, SSH) |
| 1024 - 49151 | Registered ports | Specific applications |
| 49152 - 65535 | Dynamic ports | Our computer picks one at random when the browser opens a connection |

### Important ports

| Port | Name | What it is used for | Easy memory | Security note |
|---|---|---|---|---|
| **21** | FTP | Sending files between computers | "File Transfer" | Sends passwords in plain text, so it is unsafe |
| **22** | SSH | Secure remote login to a server's command line | "Secure Shell" | Attackers often try to guess passwords here |
| **53** | DNS | Turns names (google.com) into IP addresses | The phone book | Used constantly. Strange DNS traffic can mean malware |
| **80** | HTTP | Websites without encryption | Normal web | Anyone on the path can read the data |
| **443** | HTTPS | Websites with encryption | Secure web (the padlock) | The standard for safe web traffic |
| **3389** | RDP | Remote Desktop on Windows | Remote screen | Often attacked. Never expose it directly to the internet |
