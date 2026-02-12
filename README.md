The repo at https://github.com/Drive/task1-local-network-port-scan appears to **not exist publicly** (or might be private, misspelled, or not yet created/pushed properly — GitHub returns 404). I couldn't access or "travel" to it to view actual files/screenshots.  

However, you've shared the **current README content** (which looks like a good start but is incomplete — especially the interview questions section is just a placeholder).

I've completed and polished the entire report for you below.  
- Filled in **all 8 interview questions** with clear, accurate, professional answers (standard for cybersecurity interviews).  
- Fixed grammar, formatting, consistency, and flow.  
- Made tables cleaner and added logical improvements.  
- Added placeholders for your screenshots (update filenames/paths as needed).  
- Kept your structure but made it more internship-report ready.

Just **copy-paste** this full content into your `README.md` file, commit + push to your repo, then submit the GitHub link.

```markdown
# Task 1: Scan Your Local Network for Open Ports using Nmap  
**Cyber Security Internship Task**

## Objective
Perform network reconnaissance to discover open ports and running services on devices in my local network (and on a deliberately vulnerable target like Metasploitable 3), understand exposure, and identify potential security risks.

## 🛠 Tools Used

| Tool Name       | Description                                                                 | Purpose in Task                                                                 |
|-----------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **Nmap**        | Open-source network exploration & security auditing tool                    | Host discovery, port scanning, service detection                                |
| **Wireshark**   | Network protocol analyzer for capturing and inspecting packets              | Observe TCP SYN packets and responses during scanning                           |
| **Kali Linux**  | Penetration testing focused Linux distribution with pre-installed tools     | Execution environment for Nmap and Wireshark                                    |
| **Metasploitable 3** | Intentionally vulnerable VM (Ubuntu-based) for safe practice             | Target machine to demonstrate real-world open ports and services                |

## 🌐 Step 1: Identify Local IP Range & Active Hosts

Checked my network interface configuration:

```bash
ip a    # or ifconfig (older systems)
# or on Windows: ipconfig
```

My local subnet: **192.168.1.0/24**

![Local IP Range](Screenshot/ip_range.png)  
*(Screenshot: Output of `ip a` showing interface and CIDR range)*

Performed host discovery (ping scan) to find live hosts:

```bash
sudo nmap -sn 192.168.1.0/24 -oN live_hosts_report.txt
```

![Live Hosts Scan](Screenshot/live_hosts.png)  
*(Screenshot: Nmap -sn output showing discovered active IPs)*

## 🚀 Step 2: Perform TCP SYN Scan

**TCP SYN Scan explanation**:  
Also called "half-open" scan (`-sS`). Nmap sends SYN packets.  
- Open port → target replies SYN-ACK → Nmap sends RST (never completes handshake)  
- Closed port → target sends RST  
- Filtered → no response or ICMP unreachable  

This method is fast and relatively stealthy (doesn't log full connections on many systems).

Targeted my Metasploitable 3 VM (IP: 192.168.1.86) with full port scan:

```bash
sudo nmap -sS -p- -T4 192.168.1.86 -oN target-192.168.1.86-full-scan.txt
# -p- = all 65,535 ports, -T4 = faster timing
```

Also ran a quicker version on the whole subnet (common ports):

```bash
sudo nmap -sS 192.168.1.0/24 -oN local-network-scan.txt
```

Scan results saved as:  
- `live_hosts_report.txt`  
- `target-192.168.1.86-full-scan.txt`  
- `local-network-scan.txt`

![Nmap SYN Scan Output](Screenshot/nmap_syn_scan.png)  
*(Screenshot: Example Nmap -sS output on Metasploitable 3 showing open ports)*

## 📊 Scan Results Summary (from Metasploitable 3 + local devices)

| IP Address     | Open Ports (examples)      | Service / Version                  | Potential Risk                              |
|----------------|----------------------------|------------------------------------|---------------------------------------------|
| 192.168.1.86 (Metasploitable 3) | 21, 22, 23, 80, 445, 3306, etc. | FTP, SSH, Telnet, HTTP, SMB, MySQL | Very high – many known vulnerable services |
| 192.168.1.1   | 80, 443                    | HTTP/HTTPS (router admin page)     | Default creds / web vulnerabilities         |
| 192.168.1.5   | 22                         | SSH                                | Weak passwords → brute-force risk           |
| 192.168.1.10  | 445                        | Microsoft SMB                      | EternalBlue / WannaCry style exploits       |

(Actual ports/services may vary — update based on your real scan output)

## ⚠️ Security Risks Identified

- **Open SSH (22)** → Exposed to brute-force or credential stuffing attacks  
- **Telnet (23)** → Clear-text credentials — never use in production  
- **SMB (445)** → Vulnerable to ransomware/worms if unpatched  
- **HTTP (80) admin panels** → Default credentials, XSS, CSRF, command injection  
- **Multiple services on Metasploitable** → Designed to be vulnerable (learning only — never expose to internet)

## 🔐 Recommendations to Secure Open Ports

- Enable and configure a firewall (ufw / iptables / Windows Firewall) to restrict access  
- Close / disable unnecessary services (`systemctl disable ssh` if not needed)  
- Use strong, unique passwords + key-based auth for SSH  
- Keep systems patched (`apt update && apt upgrade`)  
- Avoid running vulnerable/test VMs on production networks  
- Place public-facing services behind reverse proxy / VPN  

## 📡 Wireshark Analysis

Captured traffic while running Nmap scan:

- Observed large number of outgoing SYN packets to many ports/IPs  
- Saw SYN-ACK from open ports on target → confirms open status  
- RST packets from closed ports  

![Wireshark Capture](Screenshot/wireshark_syn.png)  
*(Screenshot: Wireshark showing TCP SYN → SYN-ACK sequence during scan)*

## 🎓 Interview Questions & Answers

1. **What is an open port?**  
   A port is open when a service/application is actively listening for incoming connections on that TCP/UDP port number. It indicates the device is ready to accept traffic for that service (e.g., port 80 = web server listening).

2. **How does Nmap perform a TCP SYN scan?**  
   Nmap sends a TCP SYN packet to initiate connection. If target replies SYN-ACK → port open (Nmap sends RST to abort). If RST → closed. No full 3-way handshake occurs, making it stealthier and faster than connect scan (-sT).

3. **What risks are associated with open ports?**  
   Open ports expand the attack surface. Attackers can fingerprint services, exploit vulnerabilities, brute-force credentials, or use known exploits (e.g., EternalBlue on SMB 445) to gain access, steal data, or pivot inside the network.

4. **Explain the difference between TCP and UDP scanning.**  
   TCP scans use connection-oriented handshake (clear open/closed/filtered responses). UDP scans are connectionless — open ports often send no reply, closed ports send ICMP port unreachable. UDP scans are slower, less accurate, require more timeouts.

5. **How can open ports be secured?**  
   - Close unnecessary services/ports  
   - Use host-based firewall to allow only trusted sources  
   - Apply patches and secure configurations  
   - Use strong authentication (keys, MFA)  
   - Monitor with IDS/IPS  
   - Segment network (e.g., DMZ for public services)

6. **What is a firewall's role regarding ports?**  
   A firewall enforces rules to allow/deny traffic based on port, protocol, IP, direction. It blocks unwanted inbound connections to open ports and can hide internal services from external scans.

7. **What is a port scan and why do attackers perform it?**  
   Port scanning is probing a target to identify open ports, running services, OS version, etc. Attackers do it during reconnaissance phase to map the network, find weak services, and plan exploitation.

8. **How does Wireshark complement port scanning?**  
   Wireshark captures raw packets, allowing verification of scan behavior (SYN/SYN-ACK/RST), timing analysis, service banner grabbing, detection of scan evasion attempts, and deeper protocol inspection beyond Nmap summaries.

## 📚 Key Concepts Learned

- Network reconnaissance basics  
- Difference between host discovery (-sn) and port scanning (-sS)  
- Stealth scanning techniques (SYN scan)  
- Interpreting Nmap output (open/filtered/closed)  
- Risks of exposed services in home/lab networks  
- Importance of Wireshark for packet-level understanding  
- Hardening principles (least privilege, patching)

## Files in this Repository

- `README.md` → This report  
- `live_hosts_report.txt` → Ping scan results  
- `local-network-scan.txt` → Subnet SYN scan  
- `target-192.168.1.86-full-scan.txt` → Detailed target scan  
- `Screenshot/` → All images (ip_range.png, live_hosts.png, nmap_syn_scan.png, wireshark_syn.png, etc.)

**Note:** All scans performed in a controlled lab environment (own network + legal vulnerable VM). No unauthorized scanning was done.

Feel free to explore and suggest improvements!
```

**Next steps for you:**
1. Create/update the repo (if name is wrong, maybe it's `Drive/cybersecurity-internship-task1` or similar — double-check spelling/case).
2. Create `Screenshot/` folder and upload your actual images.
3. Add the scan `.txt` files if you have them.
4. Paste the above into README.md → commit → push.
5. Submit the correct repo URL.

If you share the **real working GitHub link** (or correct username/repo), I can review it again and suggest specific fixes. Good job starting strong — this will look great for the internship! 🚀
