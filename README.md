
## How to Reproduce
1. Open Wireshark and select your active network interface.
2. Start a capture.
3. Perform the action for the capture (see below).
4. Stop the capture and apply the filter listed.
5. Compare your results with the screenshots.

## Practical Steps

### 1. Capture Setup
Start Wireshark, select your active interface, and confirm packets are appearing.

![Wireshark capture](screenshots/01-wireshark-capture.png)

### 2. DNS and TCP (`captures/dns-tcp-analysis.pcapng`)
- Clear the DNS cache, then visit `https://example.com`.
- Filter `dns` to find the query and response.
- Filter `tcp.flags.syn == 1` to find the handshake (SYN, SYN-ACK, ACK).

![DNS analysis](screenshots/02-dns-analysis.png)
![TCP handshake](screenshots/03-tcp-handshake.png)

### 3. TLS and HTTPS (`captures/tls-handshake.pcapng`)
- Visit `https://example.com`.
- Filter `tls.handshake.type == 1` to find the Client Hello.

![TLS and HTTPS traffic](screenshots/04-tls-https-traffic.png)

### 4. UDP (`captures/dns-tcp-analysis.pcapng`)
- Filter `udp` to see DNS and QUIC traffic, which do not use a handshake.

![UDP analysis](screenshots/05-udp-analysis.png)

### 5. Following a TCP Stream
- Right-click a TCP packet and choose **Follow → TCP Stream**.

![Follow TCP stream](screenshots/06-follow-tcp-stream.png)

### 6. TCP Teardown
- Filter `tcp.flags.fin == 1 || tcp.flags.reset == 1` to find connection closes and resets.

![TCP FIN and RST](screenshots/07-tcp-fin-reset.png)

### 7. ICMP Ping (`captures/icmp-ping.pcapng`)
- Run `ping 8.8.8.8` for about 5 packets.
- Filter `icmp` to find the Echo Request and Echo Reply pairs.

![ICMP echo](screenshots/08-icmp-echo.png)

### 8. Clear-Text HTTP (`captures/http-clear-text.pcapng`)
- Visit `http://neverssl.com`.
- Filter `http` and expand the request.

![HTTP request](screenshots/09-http-request.png)

## Analysis
DNS translates domain names into IP addresses. A browser needs that IP before it can start a connection.

TCP provides reliable communication. The three-way handshake (SYN, SYN-ACK, ACK) sets up the connection, and FIN or RST packets close it.

UDP is connectionless and has no handshake. DNS and QUIC use it for fast, lightweight exchanges.

TLS encrypts HTTPS traffic. The Client Hello shows the server name (SNI) in clear text, but the page content stays encrypted.

HTTP sends requests in clear text. Comparing it with HTTPS shows why encryption matters.

## Results

**DNS:** [Query name, the IP returned, and the time between the DNS response and the first SYN.]

**TCP:** [Server IP and port, and whether all three handshake packets were seen.]

**UDP:** [The protocols and ports you observed, and what they were used for.]

**TLS:** [The SNI value from the Client Hello and the cipher suite from the Server Hello.]

**ICMP:** [Number of requests and replies, and the round-trip times.]

**HTTP:** [The host and request line you could read, and what this shows compared with HTTPS.]

**Traffic overview:** [Top protocols from Protocol Hierarchy and the busiest conversation.]

## Conclusion
This project builds practical packet analysis skills and shows how DNS, TCP, UDP, TLS, ICMP, and HTTP work together during a normal web request.

## Author
Laxmikant Siddaram Poojari
B.E. Computer Science and Engineering
Moodlakatte Institute of Technology