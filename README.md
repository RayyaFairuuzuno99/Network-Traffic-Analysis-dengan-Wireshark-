# Network-Traffic-Analysis-dengan-Wireshark

# Network Traffic Analysis with Wireshark

## Overview

This project is a beginner-level cybersecurity lab focused on analyzing network traffic using **Wireshark**.

The traffic was generated from an Ubuntu virtual machine by accessing a website through a web browser. Wireshark was then used to capture and analyze the packets involved in the communication.

The analysis focuses on:

* DNS request and response
* Source and destination IP addresses
* TCP three-way handshake
* Source and destination ports
* TLS handshake
* HTTPS encrypted traffic

---

## Objectives

The objectives of this project are:

1. Understand how DNS resolution works.
2. Identify source and destination IP addresses.
3. Analyze the TCP three-way handshake.
4. Identify source and destination ports.
5. Observe TLS/HTTPS traffic.
6. Understand what information can and cannot be observed from encrypted traffic.

---

## Lab Environment

| Component        | Details             |
| ---------------- | ------------------- |
| Operating System | Ubuntu Linux        |
| Environment      | Virtual Machine     |
| Tool             | Wireshark           |
| Browser          | Mozilla Firefox     |
| Network          | Internet connection |

---

## Network Flow

The captured traffic can be summarized as:

```text
Ubuntu VM
    |
    | DNS Query
    v
DNS Server
    |
    | DNS Response
    v
Ubuntu VM
    |
    | TCP Three-Way Handshake
    v
Web Server
    |
    | TLS Handshake
    v
HTTPS Encrypted Traffic
```

---

# Analysis

## 1. DNS Analysis

When a website is accessed, the system first needs to resolve the domain name into an IP address.

Wireshark was used to identify the DNS request and response.

### Wireshark Filter

```text
dns
```

### Observed Information

```text
Domain:
DNS Server:
Resolved IP:
Protocol: DNS
```

### Screenshot

![DNS Query](images/Capture.png)



---

## 2. TCP Three-Way Handshake

After DNS resolution, the client establishes a TCP connection with the destination server.

The TCP connection begins with a three-way handshake:

```text
Client                         Server
  |                              |
  | -------- SYN -------------> |
  | <------- SYN, ACK ----------|
  | -------- ACK -------------> |
  |                              |
        Connection Established
```

### Wireshark Filter

```text
tcp
```

The packets were identified by the TCP flags:

```text
[SYN]
[SYN, ACK]
[ACK]
```

### Screenshot

![TCP Three-Way Handshake](images/Capture2.png)

---

## 3. IP Address Analysis

Each packet contains source and destination IP addresses.

Example:

```text
Source IP:
Destination IP:
```

The source IP represents the sender of the packet, while the destination IP represents the intended receiver.

The IP addresses were identified directly from the captured packets.

---

## 4. Port Analysis

TCP communication also uses ports to identify services and connections.

For HTTPS traffic, the destination service commonly uses:

```text
Destination Port: 443
```

The client may use a temporary **ephemeral source port**, for example:

```text
Source Port: 57192
Destination Port: 443
```

The exact values depend on the captured packet.

---

## 5. TLS / HTTPS Analysis

After the TCP connection is established, the browser can perform a TLS handshake before exchanging HTTPS data.

### Wireshark Filter

```text
tls
```

The TLS traffic demonstrates that the communication is encrypted.

### What can be observed

Wireshark can still provide information such as:

* Source IP
* Destination IP
* Source port
* Destination port
* Packet length
* Timing
* TCP information
* TLS handshake information

### What cannot normally be observed directly

Because HTTPS uses encryption, the actual HTTP content is not available as readable plaintext in a normal capture.

For example, the following type of information is not directly visible:

```text
GET /login
username=example
password=example
```

Instead, the application data appears as encrypted TLS traffic.

### Screenshot

![TLS / HTTPS Traffic](images/Capture3.png)

---

# Key Findings

From the packet capture, the following communication process was observed:

```text
1. DNS
   Domain name is resolved to an IP address.

2. TCP
   A TCP three-way handshake establishes the connection.

3. TLS
   TLS handshake is performed.

4. HTTPS
   Application traffic is transmitted in encrypted form.
```

This demonstrates how a typical web connection is established and how Wireshark can be used to inspect network traffic at the packet level.

---

# What I Learned

Through this lab, I learned:

* How to capture network traffic using Wireshark.
* How DNS queries and responses work.
* How to identify source and destination IP addresses.
* How TCP three-way handshake works.
* How source and destination ports are used.
* How TLS/HTTPS traffic appears in Wireshark.
* The difference between observable network metadata and encrypted application data.
* How packet analysis can be used as a basic cybersecurity investigation technique.

---

# Tools Used

* Ubuntu Linux
* Wireshark
* Mozilla Firefox

---

# Future Improvements

Possible extensions for this project:

* Analyze HTTP traffic.
* Analyze DNS traffic in more detail.
* Investigate suspicious network traffic.
* Analyze ICMP traffic.
* Compare HTTP and HTTPS.
* Perform basic packet-based threat investigation.

---

## Disclaimer

This project was performed in a controlled environment using traffic generated by my own system for educational purposes.
