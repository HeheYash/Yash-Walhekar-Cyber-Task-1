# Yash-Walhekar-Cyber-Task-1
Network scan and analysis for Elevate Labs internship task 1

# Cyber Security Internship: Task 1 - Network Port Scan

## 1. Objective

The objective of this task was to perform network reconnaissance on a local network using Nmap[cite: 10]. [cite_start]The goal was to discover active hosts, identify open ports, and analyze the potential security risks associated with the running services

## 2. Methodology and Execution

The task was completed by following a systematic process:
1. **Tool Installation:** Nmap was installed as the primary tool for port scanning.
2. **Network Identification:** The local IP range was identified for the scan target.
3. **Scan Execution:** A TCP SYN Scan (`-sS`) was performed using Nmap. This "stealth" scan is efficient as it doesn't complete the full TCP handshake. The command used was:
    ```bash
    nmap -sS -oN nmap_results.txt LOCAL_NETWORK_RANGE
    ```
4. **Analysis:** The output was analyzed to identify services and assess risks.

## 3. Sanitized Scan Results

The scan identified two active hosts. For privacy and security, all IP addresses have been anonymized. The findings are summarized below:

| Anonymized Host | Open Ports                               | Inferred OS / Device Type | Notes                                      |
| --------------- | ---------------------------------------- | ------------------------- | ------------------------------------------ |
| `Host 1`     | `53/tcp` (DNS)                           | Router or DNS Server      | Standard port for network DNS resolution.  |
| `Host 2`    | `135/tcp` (msrpc) <br> `139/tcp` (netbios-ssn) <br> `445/tcp` (microsoft-ds) | Windows Machine           | Ports indicate active file/printer sharing services (SMB). |

---

## 4. Security Analysis and Recommendations

The analysis focused on the services running on **`Host 2`**, which present a potential attack surface.

* **Identified Risk:** The Server Message Block (SMB) service on port `445/tcp` is a primary vector for network attacks if not properly secured. Historically, vulnerabilities in SMB have been exploited by widespread ransomware like WannaCry.

* **Recommendations to Secure the Open Ports:**
    * **Implement a Firewall:** A host-based firewall should be configured to restrict access to ports `135`, `139`, and `445`. Only trusted IP addresses on the local network should be allowed to connect.
    * **Apply Security Patches:** Ensure the Windows operating system is always updated with the latest security patches to mitigate known vulnerabilities.
    * **Disable Legacy Protocols:** If not required, disable NetBIOS over TCP/IP to reduce the attack surface.
