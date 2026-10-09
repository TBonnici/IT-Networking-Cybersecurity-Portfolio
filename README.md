# Tommy Bonnici | IT Support & Network Operations

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/tommy-bonnici-1869943b9)
[![Email](https://img.shields.io/badge/Contact-Email-red?style=flat&logo=gmail)](mailto:tbonnici34@gmail.com)

**Location:** Lake Orion, MI | **Open to Relocation:** Metro Detroit (Troy, Royal Oak, Clarkston)

Entry-level IT professional focused on network troubleshooting, Windows Server / Active Directory administration, and security fundamentals. Hands-on with packet analysis (Wireshark, tcpdump), SQL log queries, and incident documentation. Targeting NOC and software/IT support specialist roles, with a long-term path into SOC analyst work.

> **Note:** The projects below are completed lab scenarios from coursework (Google Cybersecurity Certificate), not live production incidents. Each project links to its full write-up as a PDF in this repo.

---

### Related Repositories

| Repo | What it shows |
| ---- | ------------- |
| [Network-Foundation-Homelab](https://github.com/TBonnici/Network-Foundation-Homelab) | 2-site Cisco Packet Tracer network: VLANs, router-on-a-stick, OSPF, and layer-by-layer troubleshooting |
| [Active-Directory-Homelab](https://github.com/TBonnici/Active-Directory-Homelab) | Windows Server 2022 domain controller, OUs and groups, DHCP, domain join, and Group Policy |

---

### Technical Toolset

- **Network Analysis:** Wireshark, tcpdump, TCP/IP three-way handshake, DNS over UDP, ICMP, DoS/DDoS patterns (SYN flood, ICMP flood)
- **Security Operations:** Incident handler's journal, 5 W's documentation, VirusTotal file hash lookup, NIST Cybersecurity Framework, NIST SP 800-30 Rev. 1 risk assessment
- **Systems & Data:** Linux command line, SQL (MariaDB: `WHERE`, `AND`/`OR`/`NOT`, `LIKE`, `%` wildcard)
- **Security Concepts:** Role-based access control, MFA/2FA, TLS, IP allow-listing, firewall rate limiting, IDS/IPS

**Currently working toward (planned):** CCNA, TryHackMe SAL1, CompTIA Security+

---

### Troubleshooting Approach

1. **Define the symptom and scope.** What is failing, for whom, and since when?
2. **Isolate by layer.** Work through the problem from physical to application rather than guessing.
3. **Check the evidence.** Read logs and packet captures to confirm what is actually happening.
4. **Document the findings.** Record what was observed, the likely cause, and the supporting data.
5. **Escalate with context.** Hand off to the next tier with enough detail that they don't start from zero.

---

## Featured Projects

### Network Operations & Traffic Analysis

#### 1. DNS & ICMP Traffic Analysis: UDP Port Unreachable

*Scenario: Customers report that a website cannot be reached and receive an error message.*

- **Objective:** Determine why users could not load a website, using a tcpdump capture of DNS and ICMP traffic.
- **Methodology:** Analyzed tcpdump output showing DNS lookups over UDP answered by ICMP "udp port unreachable" errors. Concluded the DNS service was not reachable on the server, so the website name could not be translated to an IP address. Listed likely causes (DNS server down, firewall blocking, incorrect configuration) and escalated findings to a senior team member.
- **Key Artifacts:** [View Network Traffic Analysis Report](dns-icmp-udp-port-unreachable.pdf)

#### 2. Network Traffic Analysis: SYN Flood DoS Investigation

*Scenario: Website visitors receive connection timeout errors and the web server stops responding.*

- **Objective:** Diagnose a network interruption causing server connection timeouts.
- **Methodology:** Reviewed logs showing the web server overwhelmed by SYN requests. Explained the TCP three-way handshake (SYN, SYN-ACK, ACK) and how a flood of SYN packets exhausts the server's resources, leaving none for legitimate connections.
- **Finding:** Probable SYN flood denial-of-service attack.
- **Key Artifacts:** [View SYN Flood Incident Report](syn-flood-dos-report.pdf)

#### 3. Incident Response: ICMP Flood DDoS (NIST CSF)

*Scenario: All internal network services suddenly stop responding.*

- **Objective:** Document an ICMP flood that took down internal network services, organized by the five NIST Cybersecurity Framework functions.
- **Methodology:** Mapped the incident to Identify, Protect, Detect, Respond, and Recover. Documented the response: firewall rate limiting for incoming ICMP, IDS/IPS filtering, source IP verification to catch spoofed addresses, network monitoring for abnormal traffic, and a recovery order (block external ICMP, stop non-critical services, restore critical services first, then bring the rest back online).
- **Key Artifacts:** [View ICMP Flood Incident Report Analysis](icmp-flood-nist-csf-report.pdf)

---

### Security Operations & Analysis

#### 4. Web Server Compromise: HTTP, Brute Force, and Malicious Download

*Scenario: Visitors to a recipe website are prompted to download a fake browser update, and the site owner is locked out of the admin account.*

- **Objective:** Identify the protocol involved, document the incident, and recommend a remediation.
- **Methodology:** Reviewed a tcpdump capture to identify HTTP at the application layer as the transport for the malicious file. Concluded the attacker likely brute-forced the admin account, changed the password, and injected code that prompted users to download malware.
- **Remediation:** Prevent reuse of default and previous passwords, and require two-factor authentication.
- **Key Artifacts:** [View Security Incident Report](web-server-brute-force-report.pdf)

#### 5. Security Logging: SQL Data Filtering

*Scenario: Suspicious after-hours and out-of-region login activity needs to be investigated.*

- **Objective:** Query security logs to isolate failed and unusual login attempts, and pull employee device information for security updates.
- **Methodology:** Used SQL filters on the `log_in_attempts` and `employees` tables in MariaDB, including `AND`, `OR`, `NOT`, `LIKE`, and the `%` wildcard.

``` sql 
-- Failed login attempts after business hours
SELECT * FROM log_in_attempts
WHERE login_time > '18:00' AND success = FALSE;

-- Login attempts from outside Mexico (data uses both MEX and MEXICO)
SELECT * FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

- **Key Artifacts:** [View SQL Queries & Log Analysis](sql-log-analysis.pdf)

#### 6. Risk Management: Server Vulnerability Assessment

*Scenario: Evaluate access controls on a critical Linux/MySQL database server.*

- **Objective:** Assess the security posture of a database server's access controls.
- **Methodology:** Followed NIST SP 800-30 Rev. 1 to score threat sources by likelihood and severity. Highest-rated risk: an employee disrupting mission-critical operations (likelihood 2 x severity 3 = 6).
- **Remediation:** Authentication, authorization, and auditing mechanisms; role-based access control; MFA; TLS in place of SSL; IP allow-listing to corporate offices.
- **Key Artifacts:** [View Vulnerability Assessment Report](vulnerability-assessment-nist-800-30.pdf)

#### 7. Incident Handler's Journal

- **Objective:** Practice structured incident documentation and hands-on network and threat analysis tools.
- **Entries:**
  - **#1 Ransomware scenario:** Documented a phishing-to-ransomware incident at a healthcare organization using the 5 W's and the detection/analysis and containment/eradication/recovery phases.
  - **#2 Wireshark:** Analyzed a packet capture file in Wireshark.
  - **#3 tcpdump:** Captured and examined network traffic from the command line.
  - **#4 VirusTotal:** Investigated a suspicious SHA-256 file hash from an email attachment alert and confirmed it was reported as malicious.
- **Key Artifacts:** [View Incident Handler's Journal](incident-handlers-journal.pdf)

---

## Contact

Open to NOC, IT support, and software support specialist opportunities. Reach me on [LinkedIn](https://www.linkedin.com/in/tommy-bonnici-1869943b9) or by [email](mailto:tbonnici34@gmail.com).
