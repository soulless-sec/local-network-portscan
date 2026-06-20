README - Network Reconnaissance
=================================

Project: Local Network Port Scan
Date: Mon Sep 22, 2025
Tool(s) used:
 - Nmap 7.95 (TCP SYN scan -sS)
 - Wireshark (optional)

Summary:
You scanned the local network range 10.89.195.0/24 using a TCP SYN scan. Below are the key findings extracted from your scan results.

Scan command used:
 sudo nmap -sS 10.89.195.0/24 -oN results.txt -oX results.xml

Key findings (hosts with open/filtered ports):
1) 10.89.195.145
 - Host is up (0.012s latency)
 - Port found: 5060/tcp (state: filtered) - SIP (Session Initiation Protocol)

2) 10.89.195.230
 - Host is up (0.0081s latency)
 - Port found: 53/tcp (state: open) - DNS (domain)

3) 10.89.195.46
 - Host is up (0.0000020s latency)
 - Ports found:
    - 80/tcp (state: open)  - HTTP (web server)
    - 7070/tcp (state: open) - realserver (often used by streaming servers)

Total: 256 IP addresses scanned; 3 hosts responded (as reported in results.txt).

How to reproduce the scan:
1. Identify your local IP range:
   - On Linux: ip a
   - On Windows: ipconfig

2. Run the TCP SYN scan:
   sudo nmap -sS <your-network-range> -oN results.txt -oX results.xml

3. (Optional) Convert XML to HTML for human-friendly viewing:
   xsltproc results.xml -o results.html

Security notes and recommendations:
 - 5060 (SIP): If you don't use VoIP/SIP on that device, consider blocking it at the firewall or disabling the SIP service. SIP can be targeted for VoIP fraud and enumeration.
 - 53 (DNS): An open DNS resolver can be abused for DNS amplification DDoS attacks. Ensure your DNS server is not an open resolver to the internet; restrict to intended clients only.
 - 80 (HTTP): Verify the web application running on port 80 is up-to-date. Look for default pages, admin panels, or known vulnerable applications. If possible, move services behind an authenticated proxy or use HTTPS (port 443).
 - 7070 (RealServer): Often used for streaming; if not required, disable or restrict access. Check the software version for known CVEs.

Next steps (optional):
 - Run version/service detection: sudo nmap -sV -sS 10.89.195.0/24
 - Run OS detection (if authorized): sudo nmap -O 10.89.195.0/24
 - Perform targeted scans against specific hosts/ports for deeper enumeration
 - Capture network traffic with Wireshark while scanning to learn packet-level behavior

Legal/Ethical reminder:
Only scan networks and devices you own or have explicit permission to test. Unauthorized scanning can be illegal and may be treated as malicious activity.

Prepared by: soulless
