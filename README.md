# 🔍 Local Network Port Scan Report using Nmap

> **Date:** June 23, 2025  
> **Scanner Tool Used:** [Nmap](https://nmap.org)  
> **Scan Command Used:**  
```bash
nmap -sS 192.168.1.0/24
#network configuration
| Item            | Value          |
| --------------- | -------------- |
| IPv4 Address    | 192.168.1.10   |
| Subnet Mask     | 255.255.255.0  |
| Default Gateway | 192.168.1.1    |
| Scanned Range   | 192.168.1.0/24 |

# scan results

| IP Address   | Open Ports             | Services                                  |
| ------------ | ---------------------- | ----------------------------------------- |
| 192.168.1.1  | 443                    | HTTPS                                     |
| 192.168.1.2  | None                   | All ports closed                          |
| 192.168.1.3  | None                   | All ports closed                          |
| 192.168.1.5  | 8008, 8009, 8443, 9000 | HTTP, AJP13, HTTPS-ALT, CSLISTENER        |
| 192.168.1.8  | 49152, 62078           | Unknown, iPhone-sync                      |
| 192.168.1.10 | 135, 139, 445, 6464    | MSRPC, NetBIOS-SSN, Microsoft-DS, Unknown |
| 192.168.1.11 | 7                      | Echo (filtered)                           |

#common services
| Port  | Service      | Description                                     |
| ----- | ------------ | ----------------------------------------------- |
| 443   | HTTPS        | Secure web traffic                              |
| 8008  | HTTP (Alt)   | Alternate port for HTTP                         |
| 8009  | AJP13        | Apache JServ Protocol                           |
| 8443  | HTTPS-ALT    | Alternate HTTPS for secure web UIs              |
| 9000  | CSLISTENER   | Used for internal/debugging listeners           |
| 62078 | iPhone-sync  | Apple sync service                              |
| 135   | MSRPC        | Microsoft Remote Procedure Call                 |
| 139   | NetBIOS-SSN  | Windows File/Printer Sharing                    |
| 445   | Microsoft-DS | Windows SMB file sharing                        |
| 6464  | Unknown      | Unknown (requires investigation)                |
| 7     | Echo         | Diagnostic service, often filtered by firewalls |

#Potential Security Risks

Port 445 & 139: Frequently targeted by malware (e.g. WannaCry). Close if not needed.

Port 135: May allow remote exploitation if unpatched.

Port 8009: Can be vulnerable (e.g. Ghostcat in Apache Tomcat).

Unknown ports (6464, 49152): Should be verified for legitimacy.

iPhone-sync (62078): Valid for Apple devices, but ensure device trust.

#Save Scan Results
nmap -sS 192.168.1.0/24 -oN scan_results.txt
#save  as html
nmap -sS 192.168.1.0/24 -oX scan.xml
xsltproc scan.xml -o scan.html
