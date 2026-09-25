# network-traffic-analysis-ICMP-DNS
Wireshark-based network traffic analysis lab focused on detecting ICMP and DNS tunneling, anomalous payloads, and potential C2 communication.
[README.md](https://github.com/user-attachments/files/32648816/README.md)
# Network Traffic Analysis: ICMP & DNS Tunneling

![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7)
![Focus](https://img.shields.io/badge/Focus-Network%20Traffic%20Analysis-informational)
![SOC](https://img.shields.io/badge/Role-SOC%20Analyst%20Practice-success)

## 📌 Overview

This project documents a practical **Network Traffic Analysis** lab performed with **Wireshark**, focused on identifying suspicious traffic patterns associated with **ICMP tunneling** and **DNS tunneling**.

The objective was to analyze packet captures, apply Wireshark display filters, identify anomalous traffic characteristics, and document indicators that could be relevant to a SOC investigation.

---

## 🎯 Objectives

- Analyze ICMP traffic for anomalous packet sizes and payloads.
- Identify indicators associated with possible **ICMP tunneling**.
- Analyze DNS queries for unusual or encoded-looking subdomains.
- Identify indicators associated with possible **DNS tunneling**.
- Practice Wireshark filtering and packet inspection.
- Document findings using a SOC-style investigation workflow.

---

## 🛠️ Tools

- **Wireshark**
- Packet capture files supplied by the lab
- Wireshark display filters

---

# 🔴 ICMP Tunneling Analysis

### Filter used

```text
data.len > 64 and icmp
```

### What was observed

The capture contains ICMP Echo Request and Echo Reply traffic.

Several packets show unusually large payloads. One highlighted packet has a packet length of approximately **1075 bytes**, with a **Data** field of approximately **1033 bytes**.

Large or anomalous ICMP payloads can be an indicator that ICMP is being used to transport additional data.

### Evidence

![ICMP tunneling analysis](images/icmp-tunneling.png)

---

# 🔵 DNS Tunneling Analysis

### Filters used

```text
dns
```

```text
dns contains "dnscat"
```

### What was observed

The capture contains repeated DNS queries involving patterns associated with **dnscat**.

The packet details show unusual query structures and encoded-looking subdomain data. Query length, anomalous DNS names, encoded subdomains, and unusual DNS request volumes are useful indicators when investigating possible DNS tunneling.

### Evidence

![DNS tunneling analysis](images/dns-tunneling.png)

---

## 🔎 Indicators Reviewed

| Protocol | Indicator | Wireshark filter |
|---|---|---|
| ICMP | Large payloads | `data.len > 64 and icmp` |
| ICMP | Abnormal packet sizes | `icmp` |
| DNS | `dnscat` pattern | `dns contains "dnscat"` |
| DNS | Long DNS queries | `dns.qry.name.len > 15 and !mdns` |
| DNS | Unusual DNS activity | `dns` |

---

## 🧠 SOC Analyst Takeaways

During network traffic analysis, protocol names alone are not enough to determine whether traffic is suspicious.

Useful indicators include:

- Packet size
- Payload size
- Query length
- Destination addresses
- Repeated requests
- Unusual or encoded subdomains
- Traffic volume
- Protocol behavior that differs from the expected baseline

ICMP and DNS are legitimate protocols, but their characteristics can also be abused for covert communication, data exfiltration, or command-and-control activity.

---

## 📊 Investigation Workflow

```text
Packet Capture
      ↓
Protocol Identification
      ↓
Wireshark Filtering
      ↓
Anomaly Detection
      ↓
Packet Inspection
      ↓
Indicator Identification
      ↓
Further Investigation
```

---

## 📄 Detailed Report

For the complete investigation notes, filters, observations, and evidence:

👉 [ICMP & DNS Tunneling Wireshark Report](ICMP_DNS_Tunneling_Wireshark_Report.md)

---

## 💻 Skills Demonstrated

- Wireshark
- Network Traffic Analysis
- Packet Analysis
- ICMP Analysis
- DNS Analysis
- Detection of tunneling indicators
- C2 traffic investigation
- Display filters
- SOC investigation methodology
- Technical documentation

---

## ⚠️ Disclaimer

This project was performed in a controlled lab environment for cybersecurity training and educational purposes.

The indicators documented here should be treated as **investigation indicators**, not as standalone proof of malicious activity in a real environment.

---

## 👤 Portfolio

**Aldo**  
SOC Analyst / Cybersecurity Portfolio

[GitHub](https://github.com/aldorock1987-sketch)

[LinkedIn](https://www.linkedin.com/in/aldo-sadia-50053a134/)
