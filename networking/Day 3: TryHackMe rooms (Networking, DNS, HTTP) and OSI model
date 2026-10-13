# Day 3: TryHackMe Rooms and the OSI Model

## TryHackMe rooms I completed today

- Networking
- DNS
- HTTP

I did these rooms first, then moved on to the OSI model.

---

## OSI Model (Open Systems Interconnection)

The OSI model splits network communication into 7 layers. Each layer has its own job and hands the data to the next one.

The main use of it is troubleshooting. If I can tell which layer a problem is in, I don't waste time checking the other layers.

| # | Layer | What it does | Examples |
|---|---|---|---|
| 7 | Application | Gives applications access to network services | HTTP, DNS, SMTP |
| 6 | Presentation | Keeps data in a usable format and handles encryption | TLS/SSL, JPEG |
| 5 | Session | Starts, maintains and ends the connection between two systems | Login sessions |
| 4 | Transport | Delivers data to the right program using ports | TCP, UDP |
| 3 | Network | Chooses the route the data takes, using IP addresses | IP, routers |
| 2 | Data Link | Delivers data inside the local network using MAC addresses | Switches, Ethernet, Wi-Fi |
| 1 | Physical | Sends the raw bits (0s and 1s) over the medium | Cables, Wi-Fi signals |

### How I understand each layer

- **Application:** the layer closest to the user. It is not the app itself, but the network services the app uses, like HTTP for websites.
- **Presentation:** makes sure the data can be read by the receiver. Encryption happens here.
- **Session:** keeps the conversation between two systems open until it is finished.
- **Transport:** uses TCP or UDP to send the data, and uses port numbers to reach the correct program.
- **Network:** decides which path the data takes to reach another network. Routers work here.
- **Data Link:** moves data between devices on the same local network using MAC addresses. Switches work here.
- **Physical:** the actual cables and signals that carry the bits.

### Connecting it to what I learned earlier

- DNS and HTTP are at layer 7.
- TCP, UDP and port numbers are at layer 4.
- IP addresses and routers are at layer 3.
- MAC addresses and switches are at layer 2.

### Encapsulation

When data is sent, each layer adds its own information around it. For example, the transport layer adds the ports, the network layer adds the IP addresses, and the data link layer adds the MAC addresses. The receiver removes this information layer by layer in reverse order.
