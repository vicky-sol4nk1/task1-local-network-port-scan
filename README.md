Perfect 👍
Main tumhara content **professional polish version** bana raha hoon — grammar improve, tone thoda security-analyst level, lekin **screenshots links bilkul same rahenge** (`Screenshot/...` unchanged).

Tum direct replace kar sakte ho.

---

```md
# task1-local-network-port-scan  
Task 1 - Scan Your Local Network for Open Ports using Nmap

---

# 🔎 Local Network Port Scanning – Cyber Security Internship Task

## 🎯 Objective

The objective of this task is to perform network reconnaissance on my local network using Nmap in order to identify active hosts, discover open ports, enumerate running services, and analyze potential security risks associated with exposed services.

---

## 🛠 Tools Used

| Tool Name            | Description                                                                          | Purpose in Task                                                                 |
|----------------------|--------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **Nmap**             | Open-source network scanning tool used for discovering hosts and open ports.        | Used to scan the local network and identify open ports and running services.    |
| **Wireshark**        | Network protocol analyzer that captures and analyzes network traffic in real time.  | Used to observe and analyze packets generated during the Nmap scan.             |
| **Kali Linux**       | Security-focused Linux distribution with pre-installed penetration testing tools.   | Used as the operating system to perform network scanning and analysis.          |
| **Metasploitable 3** | Intentionally vulnerable virtual machine designed for security testing and learning.| Used as a target machine to practice scanning and identify open ports/services. |

---

## 🌐 Step 1: Identify Local IP Range

To determine my local IP configuration and network range, I used the following commands:

```

ip a        (Linux)
ifconfig    (Linux)
ipconfig    (Windows)

```

### 📸 Screenshot
![IP Range](Screenshot/ip_range.png)

From the output, the detected network range was:

```

192.168.1.0/24

```

This indicates a Class C private network containing 254 usable host addresses.

---

## 🔍 Step 2: Identify Live Hosts (Host Discovery)

To identify active systems within the network, I performed a ping scan:

```

nmap -sn 192.168.1.0/24 -oN live_hosts_report.txt

```

- `-sn` → Host discovery only (no port scanning)
- `-oN` → Save output in normal format

This helped identify which systems were online before performing detailed scans.

### 📸 Screenshot
![Live Hosts](Screenshot/ip_range.png)

---

## 🚀 Step 3: Perform TCP SYN Scan on Target Machine (Metasploitable 3)

Target IP: `192.168.1.86`

### 🔎 Understanding TCP SYN Scan

A TCP SYN scan works by:

1. Sending a SYN packet to the target port  
2. Receiving a SYN-ACK response if the port is open  
3. Sending a RST packet instead of completing the handshake  

Because it does not complete the full TCP three-way handshake, it is:

- Faster  
- Less noisy  
- More stealthy than a full connect scan  

---

### 🔥 Scan All Ports (Full Port Scan)

```

nmap -sS -p- 192.168.1.86 -oN target-192.168.1.86-open-port-report.txt

```

- `-sS` → TCP SYN scan  
- `-p-` → Scan all 65535 ports  
- `-oN` → Save results  

### 📸 Screenshot
![Open Ports](Screenshot/port-scan.png)

---

## 🔎 Step 4: Service Version Detection

To identify versions of running services:

```

nmap -sS -sV 192.168.1.86 -oN service-version-report.txt

```

- `-sV` → Enables service version detection  

This helps determine if outdated or vulnerable services are running.

### 📸 Screenshot
![Service Version](Screenshot/service-version.png)

---

## 📡 Wireshark Analysis

During the scan, network traffic was captured using Wireshark to analyze:

- SYN packets sent by Nmap  
- SYN-ACK responses from the target  
- RST packets sent by the scanner  

This packet-level analysis provided deeper insight into how TCP SYN scanning works internally.

---

# 📊 Scan Result Summary

| Port | Service | Potential Risk |
|------|---------|---------------|
| 22   | SSH     | Brute-force attack risk |
| 80   | HTTP    | Web vulnerabilities / misconfiguration |
| 445  | SMB     | Exploitable SMB vulnerabilities |
| 3306 | MySQL   | Unauthorized database access |

---

## ⚠️ Security Risks Identified

- SSH exposed to network → susceptible to brute force attacks  
- SMB service exposed → risk of exploitation if outdated  
- Web server exposed → potential web application vulnerabilities  
- Database service exposed → possible unauthorized data access  

---

## 🔐 Recommended Security Measures

- Configure firewall to restrict unnecessary ports  
- Disable unused services  
- Implement strong authentication mechanisms  
- Regularly patch and update services  
- Restrict sensitive services to internal access only  
- Apply network segmentation if possible  

---

# 🎓 Interview Questions & Answers

### 1. What is an open port?
An open port is a network port that is actively accepting connections from external systems.

### 2. How does Nmap perform a TCP SYN scan?
Nmap sends a SYN packet and analyzes the response. If a SYN-ACK is received, the port is considered open. It then sends a RST packet instead of completing the handshake.

### 3. What risks are associated with open ports?
Open ports may expose vulnerable services that attackers can exploit for unauthorized access, data theft, or lateral movement.

### 4. Explain the difference between TCP and UDP scanning.
TCP scanning targets connection-oriented protocols, while UDP scanning targets connectionless protocols and is typically slower and less reliable.

### 5. How can open ports be secured?
By implementing firewalls, disabling unused services, restricting access, and applying regular updates and patches.

### 6. What is a firewall's role regarding ports?
A firewall filters incoming and outgoing traffic and blocks unauthorized access to network ports.

### 7. What is a port scan and why do attackers perform it?
A port scan is a reconnaissance technique used to identify open ports and running services. Attackers use it to find potential entry points into a system.

### 8. How does Wireshark complement port scanning?
Wireshark enables packet-level traffic analysis, allowing deeper understanding of how scanning techniques work.

---

## 📚 Key Concepts Learned

- Network Reconnaissance  
- Host Discovery  
- TCP SYN Scanning  
- Service Enumeration  
- Network Exposure Analysis  
- Basic Security Hardening  

---
```

---

🔥 Ab ye version:

* Professional lagta hai
* Internship level se thoda upar hai
* Clear, structured, confident tone me hai
* Screenshot links bilkul unchanged hain

Agar chaho to main tumhe bata sakta hoon recruiter isme kya notice karega 😉
