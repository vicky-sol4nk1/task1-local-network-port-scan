# task1-local-network-port-scan
Task 1 - Scan Your Local Network for Open Ports using Nmap







---

#  Local Network Port Scanning – Cyber Security Internship Task

##  Objective

Discover open ports and services in my local network using Nmap and analyze potential security risks.

---

## 🛠 Tools Used

* Nmap:
* Wireshark 
* Kali Linux / Ubuntu

---

## bfrief descriptio
* nmap: Nmap (Network Mapper) is a free and open-source network scanning tool used for network discovery and security auditing.

It helps identify:

Active hosts on a network

Open and closed ports

Running services and their versions

Operating system information

## 🌐 Step 1: Identify Local IP Range

```
ip a
```

Detected network range: `192.168.1.0/24`

---

## 🚀 Step 2: Perform TCP SYN Scan

```
nmap -sS -sV 192.168.1.0/24 -oN nmap-scan.txt
```

Scan results saved in:

```
nmap-scan.txt
```

---

## 📊 Scan Results Summary

| IP Address   | Open Port | Service | Risk                |
| ------------ | --------- | ------- | ------------------- |
| 192.168.1.1  | 80        | HTTP    | Web vulnerabilities |
| 192.168.1.5  | 22        | SSH     | Brute force risk    |
| 192.168.1.10 | 445       | SMB     | SMB exploits        |

---

## ⚠️ Security Risks Identified

* Open SSH port → password brute force
* Open SMB → lateral movement risk
* Web service → possible misconfiguration

---

## 🔐 How to Secure Open Ports

* Enable firewall
* Close unused ports
* Disable unnecessary services
* Use strong passwords
* Regular patching

---

## 📡 Wireshark Analysis

Captured SYN packets to observe TCP handshake behavior.

Screenshot included in `/screenshots`.

---

## 🎓 Interview Questions & Answers

(Add all 8 answers here neatly)

---

## 📚 Key Concepts Learned

* TCP SYN Scan
* Network Reconnaissance
* Port Exposure
* Basic Security Hardening

---

# 💡 Important

Yes, everything in one file is fine —
but make sure:

✔ Headings clear ho
✔ Commands properly formatted ho
✔ Table use karo
✔ Professional language use karo

---

# 🚨 Mistake Mat Karna

❌ Sirf nmap output paste mat kar dena
❌ Explanation bina submit mat karna
❌ Screenshot ke bina mat bhejna

---

Agar chaho toh main tumhara current README review kar du aur usko internship-ready bana du 🔥

