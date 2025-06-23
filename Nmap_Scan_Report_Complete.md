
# 🔍 Local Network Port Scan Report using Nmap

**Date:** June 23, 2025  
**Scanner Tool Used:** Nmap  
**Scan Command Used:**  
```bash
nmap -sS 192.168.1.0/24
```

---

## ✅ Network Information (From `ipconfig`)
- **IPv4 Address:** 192.168.1.10
- **Subnet Mask:** 255.255.255.0
- **Default Gateway:** 192.168.1.1
- **Network Range Scanned:** 192.168.1.0/24

---

## 📋 Scan Results Summary

| IP Address     | Open Ports            | Services                        |
|----------------|-----------------------|----------------------------------|
| 192.168.1.1    | 443                   | HTTPS                           |
| 192.168.1.2    | None                  | All ports closed                |
| 192.168.1.3    | None                  | All ports closed                |
| 192.168.1.5    | 8008, 8009, 8443, 9000| HTTP, AJP13, HTTPS-ALT, CSLISTENER|
| 192.168.1.8    | 49152, 62078          | Unknown, iPhone-sync            |
| 192.168.1.10   | 135, 139, 445, 6464   | MSRPC, NetBIOS-SSN, Microsoft-DS, Unknown |
| 192.168.1.11   | 7                     | Echo (Filtered)                 |

---

## 🔎 Common Services and Their Meaning

| Port | Service         | Description                                                                 |
|------|------------------|-----------------------------------------------------------------------------|
| 443  | HTTPS            | Secure web traffic                                                          |
| 8008 | HTTP (Alt)       | Alternate HTTP, often used for web UIs of devices                           |
| 8009 | AJP13            | Apache JServ Protocol - used to connect web servers to application servers  |
| 8443 | HTTPS-ALT        | Alternate HTTPS port for secure web access                                  |
| 9000 | CSLISTENER       | May be a custom server listener; often used for debugging or monitoring     |
| 62078| iPhone-sync      | Used by Apple devices for syncing                                           |
| 135  | MSRPC            | Microsoft Remote Procedure Call – used in Windows networking                |
| 139  | NetBIOS-SSN      | Windows File/Printer sharing                                                |
| 445  | Microsoft-DS     | Windows SMB file sharing                                                    |
| 6464 | Unknown          | Unknown service, needs investigation                                        |
| 7    | Echo             | Diagnostic tool, filtered here (often blocked by firewalls)                 |

---

## 🔐 Potential Security Risks

- **Port 445 & 139 (SMB, NetBIOS):** Common targets for malware and ransomware attacks.
- **Port 135 (MSRPC):** Vulnerable if exposed; allows remote services to be executed.
- **Port 8009 (AJP13):** If misconfigured, could be exploited for remote code execution (e.g., Ghostcat vulnerability).
- **Unknown ports (6464, 49152):** May be custom services; need to verify if they are legitimate and secured.
- **iPhone-sync (62078):** Normally safe, but unnecessary open ports on personal devices can expose data if intercepted.

---

## 💾 Save Nmap Results

To save the output of the scan:

### Save as Text:
```bash
nmap -sS 192.168.1.0/24 -oN nmap_results.txt
```

### Save as XML (for HTML conversion):
```bash
nmap -sS 192.168.1.0/24 -oX nmap_results.xml
xsltproc nmap_results.xml -o nmap_results.html
```

---

## ✅ Final Recommendation

- Disable unnecessary services.
- Close unused ports via firewall/router settings.
- Keep all systems updated and apply security patches regularly.
- Use strong passwords and enable authentication where possible.
