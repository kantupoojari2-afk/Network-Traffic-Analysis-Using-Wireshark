# Network Traffic Analysis Using Wireshark

## Project Overview
This project analyzes network traffic with Wireshark to understand how computers communicate. It covers DNS resolution, TCP connection setup and teardown, UDP traffic, TLS encryption, ICMP, and clear-text HTTP.

## Objectives
- Understand DNS resolution.
- Analyze the TCP three-way handshake and connection teardown.
- Observe TLS handshake and encrypted HTTPS traffic.
- Compare encrypted (HTTPS) and clear-text (HTTP) traffic.
- Identify UDP traffic and its role in DNS and QUIC.
- Identify source and destination IP addresses.
- Learn basic network protocols.

## Tools Used
- Wireshark [version]
- [Windows / Linux / macOS] [version]
- Web browser

## Protocol Filters
| Filter | Purpose |
|--------|---------|
| `dns` | Analyze DNS queries and responses |
| `tcp` | Examine TCP handshake, data, and teardown |
| `udp` | Examine UDP traffic such as DNS and QUIC |
| `tls.handshake.type == 1` | Find the TLS Client Hello and server name (SNI) |
| `tls.handshake.type == 2` | Find the TLS Server Hello and chosen cipher suite |
| `icmp` | Analyze ping request and reply traffic |
| `http` | View clear-text HTTP requests and responses |

## Repository Structure
