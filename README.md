# Yash-Walhekar-Cyber-Task-1
Network scan and analysis for Elevate Labs internship task 1

# Cyber Security Internship: Task 1 - Network Port Scan

![Nmap](https://img.shields.io/badge/Tool-Nmap-brightgreen) ![Status](https://img.shields.io/badge/Status-Completed-blue)

## 1. Objective

[cite_start]The objective of this task was to perform network reconnaissance on a local network using Nmap[cite: 10]. [cite_start]The goal was to discover active hosts, identify open ports, and analyze the potential security risks associated with the running services[cite: 9, 18].

---

## 2. Methodology and Execution

The task was completed by following a systematic process:
1.  [cite_start]**Tool Installation:** Nmap was installed as the primary tool for port scanning[cite: 12].
2.  [cite_start]**Network Identification:** The local IP range was identified for the scan target[cite: 13].
3.  **Scan Execution:** A TCP SYN Scan (`-sS`) was performed using Nmap. [cite_start]This "stealth" scan is efficient as it doesn't complete the full TCP handshake[cite: 14]. The command used was:
    ```bash
    nmap -sS -oN nmap_results.txt LOCAL_NETWORK_RANGE
    ```
4.  [cite_start]**Analysis:** The output was analyzed to identify services and assess risks[cite: 18].

---

## 3. Sanitized Scan Results

The scan identified two active hosts. For privacy and security, all IP addresses have been anonymized. The findings are summarized below:

| Anonymized Host | Open Ports                               | Inferred OS / Device Type | Notes                                      |
| --------------- | ---------------------------------------- | ------------------------- | ------------------------------------------ |
| `ROUTER_IP`     | `53/tcp` (DNS)                           | Router or DNS Server      | Standard port for network DNS resolution.  |
| `YOUR_PC_IP`    | `135/tcp` (msrpc) <br> `139/tcp` (netbios-ssn) <br> `445/tcp` (microsoft-ds) | Windows Machine           | Ports indicate active file/printer sharing services (SMB). |

---

## 4. Security Analysis and Recommendations

The analysis focused on the services running on **`YOUR_PC_IP`**, which present a potential attack surface.

* **Identified Risk:** The Server Message Block (SMB) service on port `445/tcp` is a primary vector for network attacks if not properly secured. Historically, vulnerabilities in SMB have been exploited by widespread ransomware like WannaCry.

* **Recommendations to Secure the Open Ports:**
    * **Implement a Firewall:** A host-based firewall should be configured to restrict access to ports `135`, `139`, and `445`. Only trusted IP addresses on the local network should be allowed to connect.
    * **Apply Security Patches:** Ensure the Windows operating system is always updated with the latest security patches to mitigate known vulnerabilities.
    * **Disable Legacy Protocols:** If not required, disable NetBIOS over TCP/IP to reduce the attack surface.
