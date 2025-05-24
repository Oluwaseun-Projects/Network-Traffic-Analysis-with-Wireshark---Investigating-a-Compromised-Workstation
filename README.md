# 🕵️ Network Traffic Analysis with Wireshark: Investigating a Compromised Workstation

## 📌 Project Overview

This project simulates a real-world network forensics case where a workstation within an organization accesses a compromised website. Using Wireshark, I demonstrate how to perform packet capture, filter and analyze protocols, identify security anomalies, and trace potential compromise paths.

The goal is to showcase practical skills in network traffic analysis and incident investigation using industry-standard tools and methodologies.

---

## 🎯 Objectives

By the end of this investigation, you will:

* Understand the concept and importance of network traffic analysis.
* Use Wireshark to capture and analyze network communication across various protocols.
* Determine the root cause of network issues using packet analysis.
* Navigate and utilize Wireshark panes, capture filters, and display filters.
* Identify common protocols (TCP, UDP, ICMP, DNS, HTTP) and how to isolate traffic by ports and IPs.
* Extract forensic evidence such as User-Agent headers and follow TCP streams.

---

## 🛠️ Tools & Technologies

| Tool           | Purpose                               |
| -------------- | ------------------------------------- |
| **Wireshark**  | Packet capture and protocol analysis  |
| **PCAP file**  | Provided network capture for analysis |

---

## 🧠 Skills Demonstrated

* Network protocol analysis (TCP, UDP, DNS, HTTP)
* Wireshark filtering and stream following
* Root cause analysis and incident reconstruction
* Threat investigation methodology
* Communication and documentation of technical findings

---

## 🗂️ Lab Scenario

A workstation (IP: `192.168.248.171`) within TechnoCorp accesses a local website which has been compromised. The IT team captures traffic during this time using Wireshark. My job is to investigate the captured packets and determine what happened.

---

## 🔍 Step-by-Step Investigation

### Step 1: Load and Navigate Wireshark

* Open the provided `.pcap` file in Wireshark.

* <img width="1077" alt="01-Open Pcap File in WireShark" src="https://github.com/user-attachments/assets/cc210f18-d9ca-4d44-9f7a-28be1fbbf7a8" />


 
* Explore the **Packet List Pane**, **Packet Details Pane**, and **Packet Bytes Pane**.

**Packets List Pane**
* <img width="1241" alt="02-Packet List Pane" src="https://github.com/user-attachments/assets/6bffe9da-fb86-4e03-83fc-4abe6e6f4c59" />

**Packets Details Pane**
<img width="989" alt="03-Packet Details Pane" src="https://github.com/user-attachments/assets/a58190d9-dbdf-4897-acfa-242d3f52b777" />

**Packets Bytes Pane**

<img width="859" alt="04-Packet Bytes Pane" src="https://github.com/user-attachments/assets/97861b9a-3de3-4156-8abe-ee6f12b866ac" />


### Step 2: Apply Protocol Filters

| Filter                               | Purpose                             |
| ----------------                     | ----------------------------------- |
| `tcp`                                | Display TCP traffic                 |
| `udp`                                | Display UDP traffic                 |
| `icmp`                               | Display ICMP traffic                |
| `tcp.port == 80`                     | Filters for all TCP traffic on port 80, typically HTTP traffic.     |
| `ip.addr==192.168.248.171`           | Isolate all traffic from the investiagted system.      |

**Filter all TCP traffic**
<img width="1241" alt="05-TCP Packets" src="https://github.com/user-attachments/assets/9af71fb3-3553-4e44-a544-26fc7a946c0f" />

**Filter all UDP traffic**
<img width="1085" alt="06-UDP  Packets" src="https://github.com/user-attachments/assets/506216fc-4dfd-43d3-9a48-e6120d6a51e7" />

**Filter all ICMP traffic**
<img width="1250" alt="07-ICMP Packets" src="https://github.com/user-attachments/assets/bf139876-33ab-494e-b393-1e1e0eed3e1d" />

**Filter all TCP traffic pn port 80 only (HTTP traffic)**
<img width="1205" alt="08-Isolate TCP traffic" src="https://github.com/user-attachments/assets/c67f3d7b-44dc-4943-96f0-98b250523bde" />

**Isolate all traffic from the investiagted system 192.168.248.171**
<img width="1232" alt="10-All traffic from the investigated Machine - source and destination " src="https://github.com/user-attachments/assets/b829c225-0ded-4300-b1ae-3468461ce590" />


### Step 3: Investigate HTTP Headers

* Filter: `http.request`to determine the compromised employee’s operating system and the version of Chrome used during the compromise.

**HTTP Request to get more information about the investigated system**
<img width="1238" alt="11 - Http Request" src="https://github.com/user-attachments/assets/77b00f59-c834-4a2b-9ab1-b79dd2aaada3" />

* Drill down to inspect the **User-Agent** header

**Use User-Agent to extract more information**
<img width="1250" alt="12-User Agent " src="https://github.com/user-attachments/assets/01a700af-eeee-4cb6-8b78-31a7b4166152" />


* Extract OS and browser version used by the compromised machine

**User-Agent Information**
![13-OS and Chrome](https://github.com/user-attachments/assets/03368155-103f-4aaa-968e-2dc734f1635c)


### Step 4: Follow TCP Streams

* Use `tcp.stream eq 1` (where 1 is the stream number)

* Right-click → Follow → TCP Stream to reconstruct conversations

**TCP Stream to follow the full conversation of the investigated machine with any specific server**
<img width="1255" alt="14-TCP Stream" src="https://github.com/user-attachments/assets/751477e1-d802-4844-a2c9-b47458afd4b4" />



* Identify suspicious payloads, login attempts, or data exfiltration

**Check to see any suspicious activities from the conversations**
![15- TCP Stream in YAML](https://github.com/user-attachments/assets/aceb4a41-ef77-4140-8b66-f8a6cb3e630b)



### Step 5: Advanced Filtering

* Combine filters: `ip.addr == 192.168.248.171 && tcp.port == 80`

**Use of logical operators to combine more than one filter**
<img width="1240" alt="16 - Advanced Filtering" src="https://github.com/user-attachments/assets/203e23f7-43b3-45db-afd7-9ef9c9904fbd" />


* Use `tcp.analysis.flags` to identify retransmissions or anomalies

**Check for retransmission anomalies**
![17- TCP Flags](https://github.com/user-attachments/assets/5e9ff4ca-01c5-4449-9893-58d2c5e116e3)

---

## 📚 Takeaways

This investigation demonstrates how forensic analysis using Wireshark can uncover the digital trail of a security breach. From protocol inspection to stream reconstruction, the insights gathered are critical for incident response and security posture improvement.

> ✅ *This project strengthens core cybersecurity skills needed for SOC analysts, IT support engineers, and network defenders.*


