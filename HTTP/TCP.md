# Transmission Control Protocol TCP

- web communications standard that enables application programs and computing devices to exchange messages over a network
- designed to send packets across the internet and ensure the successful delivery of data and messages
- organizes data so that it can be transmitted between a server and a client
  - guarantees the integrity of the data being communicated over a network
  - before it transmits data, TCP `establishes a connection` between a source and its destination, which remains live until communication begins
  - breaks large amounts of data into smaller packets
- alternative is User Datagram Protocol (UDP)

## UDP vs TCP

- UDP
  - used to establish `low-latency` connections
  - does not provide error connection or packet sequeincing nor does it signal a destination before it delivers data
  - less reliable
  - less expensive
  - good for time-sensitive situations
    - DNS lookup
    - streaming
    - Voice over Internet Protocol (VoIP)

## TCP vs IP

- separate protocols that work together to ensure that data is delivered to its intended destination within a network
  - IP (Internet Protocol) obtains and defines the address - the IP address - of the application or device the data must be sent to
    - low-level protocol
    - limited by the amount of data it can send. max size of a single IP data packet which contains both the header and data is 20-24 bytes
    - operates at Layer 3, `network layer` of the `Open Systems Interconnection (OSI model)`
    - connection-less protocol, does not provide error checking and correction
  - TCP is then responsible for transporting and routing data through the network athitecture and ensuring it gets delivered to the destination application or device that IP has defined
    - higher level smart communcations protocol
    - operates at Layer 4, `transport layer` of the `Open Systems Interconnection (OSI model)`
    - connection-oriented protocol
    - controls the size and flow rate of data

### How does TCP/IP work

- client-side model
- data is broken into smaller packets and automatically reassembled once they reach their destination
- For source and destination device IP address TCP uses `three-way handshake` to establish a reliable connection
  - connection is `full duplex`
  - both sides `synchronize (SYN)` and `acknowledge (ACK)` each other
  - exchange of these four flags is performed in three steps
    1. client sends SYN, chooses initial sequence number set in first SYN packet
    2. server sends SYN-ACK, chooses its own initial sequence number and acknowledges client with incrementing sequence number, set in SYN/ACK packet
    3. client sends ACK, acknowledges server with incrementing sequence number, set in ACK packet
    4. `CONNECTION ESTABLISHED`
  - the use of sequence and acknowledgment numbers allows both sides to detect missong or out-of-order segments
  - connection will end with `RST flag (reset or tear down the connection)` or `FIN (gracefully end the connetion)`

![TCP handshake](https://ars.els-cdn.com/content/image/3-s2.0-B9781597499613000030-f03-08-9781597499613.jpg)

### The 4 layers of TCP/IP model

1. Application layer, top layer provides applications with standardized data exchange, HTTPS, HTTP, FTP, SSH, SMPT
2. Transport layer, TCP, UDP
3. Internet layer, network layer, IP
4. Network link layer, network interface layer or data link layer, lowest layer include `Ethernet` for local area networks and `ARP (Address Resolution Protocol)`, `MAC`. The network component that interconnects nodes or hosts in the network

![Layers of the TCP/IP model](https://cdn.ttgtmedia.com/rms/onlineimages/tcp_ip_model_with_protocols_and_addresses-h.png)
