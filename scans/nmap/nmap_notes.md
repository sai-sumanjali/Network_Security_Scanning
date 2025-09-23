# 🛠 Nmap Command Notes:

### 1. 🎯 TARGET SPECIFICATION

* `-iL <inputfilename>`: Input target list from a file

```cmd
nmap -iL targets.txt
```

**Scenario**: You have multiple IPs or domains in a file (`targets.txt`) and want to scan all of them at once.

### 2. 🌐 HOST DISCOVERY

* `-sL`: List Scan – list targets only

```cmd
nmap -sL zero.webappsecurity.com
```

**Scenario**: Just check the hostname resolution for review, without scanning ports.

* `-sn`: Ping Scan – check if host is up, no ports scanned

```cmd
nmap -sn zero.webappsecurity.com
```

**Scenario**: Confirm if the host is live before deeper scanning.

* `-Pn`: Assume host is up, skip ping check

```cmd
nmap -Pn zero.webappsecurity.com
```

**Scenario**: Use when host blocks ICMP/ping (still want port scan).

### 3. ⚙️ SCAN TECHNIQUES

* `-sS`: TCP SYN scan (stealth scan)

```cmd
nmap -sS zero.webappsecurity.com
```

**Scenario**: Identify open ports without completing TCP handshake.

* `-sT`: TCP connect scan

```cmd
nmap -sT zero.webappsecurity.com
```

**Scenario**: Useful if you're running as a normal user (non-root).

* `-sA`: ACK scan

```cmd
nmap -sA zero.webappsecurity.com
```

**Scenario**: Check firewall rules or filtering behavior.

* `-sU`: UDP scan

```cmd
nmap -sU zero.webappsecurity.com
```

**Scenario**: Identify open UDP services (like DNS, SNMP).

### 4. 🚪 PORT SPECIFICATION AND SCAN ORDER

* `-p <ports>`: Scan specific ports

```cmd
nmap -p 80,443 zero.webappsecurity.com
```

**Scenario**: Limit scan to known web service ports.

* `--exclude-ports <ports>`: Skip specific ports

```cmd
nmap --exclude-ports 22,25 zero.webappsecurity.com
```

**Scenario**: Avoid scanning SSH and mail ports.

* `-F`: Fast scan (limited ports)

```cmd
nmap -F zero.webappsecurity.com
```

**Scenario**: Quick scan of the most common ports.

* `-r`: Scan ports sequentially

```cmd
nmap -r zero.webappsecurity.com
```

**Scenario**: Avoid randomization for analysis or teaching purposes.

### 5. 🔍 SERVICE/VERSION DETECTION

* `-sV`: Detect service versions

```cmd
nmap -sV zero.webappsecurity.com
```

**Scenario**: Understand what software/version is running on open ports.

* `--version-intensity <level>`

```cmd
nmap -sV --version-intensity 2 zero.webappsecurity.com
```

**Scenario**: Perform lighter version detection to avoid detection.

* `--version-light`

```cmd
nmap -sV --version-light zero.webappsecurity.com
```

**Scenario**: Use the most common probes only.

* `--version-all`

```cmd
nmap -sV --version-all zero.webappsecurity.com
```

**Scenario**: Perform a full and deep version probe.

* `--version-trace`

```cmd
nmap -sV --version-trace zero.webappsecurity.com
```

**Scenario**: See how Nmap tries to identify each service.

### 6. 📜 SCRIPT SCAN

* `-sC`: Run default scripts

```cmd
nmap -sC zero.webappsecurity.com
```

**Scenario**: Run built-in checks (like SSH version, HTTP headers).

* `--script=<script>`: Run specific NSE script

```cmd
nmap --script=http-title zero.webappsecurity.com
```

**Scenario**: Extract the page title from the site (simple recon).

### 7. ⏱ TIMING AND PERFORMANCE

* `-T<0-5>`: Set timing (0 = paranoid, 5 = insane)

```cmd
nmap -T4 zero.webappsecurity.com
```

**Scenario**: Faster scan suitable for internal testing.

### 8. 🧠 OS DETECTION

* `-O`: Try to identify OS

```cmd
nmap -O zero.webappsecurity.com
```

**Scenario**: Helps understand what operating system is running (Linux/Windows).

### 9. 📄 OUTPUT OPTIONS

* `-oN`, `-oX`, `-oS`, `-oG`: Output formats

```cmd
nmap -oN nmap_scan.txt zero.webappsecurity.com
```

**Scenario**: Save your scan result to a file.

* `-v`, `-vv`, `-vvv`: Increase verbosity

```cmd
nmap -vv zero.webappsecurity.com
```

**Scenario**: Useful during live scans for detailed output.

### 10. 🧩 MISCELLANEOUS

* `-A`: Aggressive mode (OS detect, version, scripts, traceroute)

```cmd
nmap -A zero.webappsecurity.com
```

---

## Targeting and Host Enumeration

### Scan a Specific IP Range or Subnet

```bash
nmap 192.168.1.0/24
```

Use to discover all hosts on a class C network.

### Load Targets from a File

```bash
nmap -iL targets.txt
```

Useful in automation or when reusing results from earlier discovery phases.

### Skip Hosts Listed in a File

```bash
nmap --exclude 192.168.1.100,192.168.1.200
```

Exclude specific hosts during broad subnet scans.

### Randomize Target Scan Order

```bash
nmap --randomize-hosts -iL targets.txt
```

Avoid pattern detection in enterprise environments.

### List Targets Without Scanning

```bash
nmap -sL 10.0.0.0/24
```

Validates input structure and DNS resolution pre-scan.

---

## Host Discovery in Restricted Networks

### ARP Ping Scan (Local Only)

```bash
nmap -PR 192.168.0.0/24
```

Quick way to detect live hosts within LAN.

### Disable Ping Checks

```bash
nmap -Pn 10.10.10.10
```

Used where ICMP is blocked by firewall.

### TCP SYN Ping

```bash
nmap -PS22,80,443 192.168.1.0/24
```

Detect hosts based on TCP response from known open ports.

### ICMP Echo, Timestamp, and Address Mask

```bash
nmap -PE -PP -PM 192.168.1.0/24
```

Layered ICMP probes for broad detection.

### IPv6 Discovery

```bash
nmap -6 -sn fe80::/64
```

Scans hosts in IPv6-enabled networks.

---

## Scan Techniques and Modes

### SYN Scan

```bash
sudo nmap -sS 192.168.0.10
```

Standard stealth scan for TCP services.

### UDP Scan

```bash
sudo nmap -sU -p 53,161 192.168.1.10
```

Identifies DNS, SNMP, and other UDP-based services.

### Connect Scan

```bash
nmap -sT 10.0.0.5
```

Fallback method when raw socket access is unavailable.

### ACK Scan

```bash
nmap -sA 192.168.1.100
```

Used to map firewall rules (filtered vs unfiltered ports).

### Idle Scan

```bash
nmap -sI zombiehost 192.168.0.10
```

Scan via third-party idle host for anonymity.

---

## Port Management and Performance

### Full Port Range

```bash
nmap -p- 192.168.1.50
```

Scans all 65535 ports.

### Top Ports by Relevance

```bash
nmap --top-ports 100 192.168.0.5
```

Efficient enumeration using Nmap's frequency database.

### Avoid Commonly Monitored Ports

```bash
nmap -p 1-65535 --exclude-ports 22,3389
```

Avoid triggering security alerts on critical services.

### Sequential Scan

```bash
nmap -r -p1-1000 10.10.10.10
```

Disables random port order to assist with pattern-based analysis.

### Quick Tuning

```bash
nmap -F -T4 192.168.1.1
```

Fast scan using default top 100 ports with aggressive timing.

---

## Version Detection and Fingerprinting

### Standard Version Scan

```bash
nmap -sV 192.168.1.100
```

Used to determine service versions.

### Intense Version Probe

```bash
nmap -sV --version-intensity 9 192.168.1.100
```

Deep detection of evasive or lightly fingerprinted services.

### Light Version Scan

```bash
nmap -sV --version-light 192.168.0.10
```

Faster scans with less intrusive probing.

### Enable Service Guessing

```bash
nmap -sV --version-all 10.0.0.5
```

Enables all probes to maximize coverage.

### Debug Version Fingerprinting

```bash
nmap -sV --version-trace 192.168.1.15
```

Used to understand probe behavior in debugging or learning mode.

---

## NSE Script Scanning

### Default Script Scan

```bash
nmap -sC -sV 192.168.1.10
```

Performs default info gathering.

### Vulnerability Checks

```bash
nmap --script vuln -p 80,443 192.168.0.10
```

Looks for publicly known vulnerabilities.

### SSL Enumeration

```bash
nmap --script ssl-enum-ciphers -p 443 10.10.10.5
```

Audits HTTPS services for weak cipher suites.

### SMB Security Mode

```bash
nmap --script smb-security-mode -p 445 192.168.1.30
```

Identifies SMB signing, authentication policies.

### HTTP Headers Review

```bash
nmap --script http-headers -p 80,443 10.0.0.15
```

Pulls and reviews HTTP response headers.

---

## Timing and Reliability Options

### Timing Template (Balanced)

```bash
nmap -T3 -p 22,80 192.168.1.10
```

Safe for external enterprise scans.

### Maximum Retries

```bash
nmap --max-retries 2 192.168.1.1
```

Reduces latency from non-responsive hosts.

### Host Timeout

```bash
nmap --host-timeout 30s 192.168.1.5
```

Ensures scans exit early for slow or filtered hosts.

### Parallel Host Scan

```bash
nmap --min-parallelism 5 --max-parallelism 20 192.168.0.0/24
```

Manages resource allocation in large-scale scans.

### Scan Delay and Jitter

```bash
nmap --scan-delay 100ms --max-rate 1000 192.168.0.1
```

Useful for IDS evasion or rate-controlled environments.

---

## OS Detection

### Passive OS Fingerprint

```bash
nmap -O 192.168.1.1
```

Guesses OS based on TCP/IP behavior.

### OS Detection with Aggressive Scan

```bash
nmap -A 10.0.0.1
```

Combines multiple scan types for full fingerprinting.

### Disable DNS During OS Scan

```bash
nmap -O -n 192.168.1.10
```

Speeds up scanning and avoids revealing queries.

### Compare Against Known Signatures

```bash
nmap -O --osscan-guess 192.168.0.15
```

Tries harder to match based on incomplete response sets.

### Log Detected OS to File

```bash
nmap -O -oN os_output.txt 192.168.1.20
```

Maintains OS info for audit logs or reports.

---

## Output and Reporting

### Grepable Output

```bash
nmap -oG live_hosts.txt 192.168.1.0/24
```

Quick parsing using grep/awk tools.

### Normal Output for Reports

```bash
nmap -oN nmap_scan.txt 192.168.0.1
```

Readable and useful in assessments.

### XML Format

```bash
nmap -oX results.xml 192.168.1.100
```

Used in automation pipelines.

### Combined Output Formats

```bash
nmap -oA fullscan 192.168.0.5
```

Generates `.nmap`, `.xml`, and `.gnmap` in one command.

### JSON via XML Convertors

Use `xsltproc`, `xml2json`, or third-party dashboards to visualize and process Nmap outputs.

---

### 1. Advanced Evasion, Obfuscation, and Stealth Scanning Techniques

#### 1.1 Fragmented Packets to Evade IDS

```bash
nmap -f 192.168.1.10
```

**Scenario:** During a Red Team internal recon, use fragmented packets to bypass basic IDS packet reassembly logic.

#### 1.2 Decoy Traffic Simulation

```bash
nmap -D RND:5,ME 10.0.0.15
```

**Scenario:** Simulate 5 random decoy IPs and hide true origin during pen-testing an exposed public interface.

#### 1.3 Timing Obfuscation

```bash
nmap -T0 --scan-delay 5s 192.168.1.0/24
```

**Scenario:** Slow scan across sensitive subnets to avoid triggering rate-based detection.

#### 1.4 Spoofed Source IP

```bash
nmap -S 172.16.0.100 -e eth0 target.com
```

**Scenario:** During adversary emulation, mimic traffic from a compromised trusted IP range.

#### 1.5 Encrypted Output + Obfuscation

```bash
nmap -oX - target.com | openssl enc -aes-256-cbc -out scan.enc
```

**Scenario:** Securely transport scan results without storing plaintext.

---

### 2. Firewall/IDS/IPS Testing Tactics

#### 2.1 FIN Scan to Bypass Stateless Filtering

```bash
nmap -sF target.com
```

**Scenario:** Map unfiltered ports on outdated stateless packet filters.

#### 2.2 Invalid TCP Flag Combinations

```bash
nmap --data-length 50 --badsum target.com
```

**Scenario:** Test firewall response to malformed packets or invalid checksums.

#### 2.3 NSE-Based WAF Detection

```bash
nmap --script http-waf-detect,target-ip
```

**Scenario:** Detect presence of cloud WAFs like Cloudflare, AWS Shield, etc.

#### 2.4 DNS-based WAF Evasion

```bash
nmap -sS www.target.com --dns-servers 1.1.1.1
```

**Scenario:** Override enterprise DNS resolution to bypass response-based WAF detections.

#### 2.5 Dynamic Source Port Rotation

```bash
nmap -g 20,53,443,1024 target.com
```

**Scenario:** Simulate legitimate services while probing for firewall holes.

---

### 3. Host Discovery Across Segmented and IPv6 Networks

#### 3.1 IPv6 Neighbor Discovery

```bash
nmap -6 -sU -p546 ff02::1%eth0
```

**Scenario:** Discover active IPv6 hosts via router-advertised multicast.

#### 3.2 Firewall-Bypass TTL Scanning

```bash
nmap --ttl 3 10.10.10.0/24
```

**Scenario:** Identify access points through hop-limited segments.

#### 3.3 Layered Broadcast Inventory

```bash
nmap -sU --script=broadcast-netbios-ns
```

**Scenario:** Inventory Windows machines in flat internal segments.

#### 3.4 VPN Discovery Through Leak Paths

```bash
nmap -Pn -sT --script ip-geolocation-* target.com
```

**Scenario:** Determine VPN exits or misconfigured tunnel routes.

#### 3.5 Traceroute Depth Recon

```bash
nmap -sn --traceroute 10.10.0.0/16
```

**Scenario:** Map DMZ, trust boundaries and internal links.

---

### 4. Complex NSE, Cloud, VPN Recon Use Cases

#### 4.1 Azure Public Services Exposure Check

```bash
nmap --script azure-enum target.azurewebsites.net
```

**Scenario:** Validate misconfigured open ports on Azure App Services.

#### 4.2 AWS EC2 Enumeration by IP Block

```bash
nmap -Pn -T4 -p- -iL aws-ip-ranges.txt
```

**Scenario:** Red team scans across elastic IP allocations for dev/test leaks.

#### 4.3 VPN Concentrator Fingerprinting

```bash
nmap -sU -p500,4500 --script ike-version target.com
```

**Scenario:** Identify IPsec VPN devices and supported encryption.

#### 4.4 Cloud Metadata Access Check

```bash
nmap --script http-cloud-metadata -p80 target.com
```

**Scenario:** Test for SSRF or leaked internal metadata URLs.

#### 4.5 NSE for Git Leaks

```bash
nmap --script http-git target.com
```

**Scenario:** Search for exposed .git directories and sensitive commits.

---

### 5. CI/CD, Reporting, Red/Blue Integration

#### 5.1 Scheduled Nmap via Jenkins

```bash
nmap -oX scan.xml target.com && curl -F "file=@scan.xml" https://ci.internal/upload
```

**Scenario:** Automate regular scan pipeline for exposed services audit.

#### 5.2 Blue Team SIEM Alerts via Log Parsing

```bash
nmap -oG - target.com | tee logs.txt | grep open
```

**Scenario:** Feed real-time alerting for newly exposed services to SIEM.

#### 5.3 Audit Baseline Comparison

```bash
nmap -sV -oX current.xml target.com && diff previous.xml current.xml
```

**Scenario:** Detect deviation in server services or versions.

#### 5.4 Merge with OpenVAS or Nessus Asset IDs

```bash
nmap -oX results.xml && ./map_assets.py results.xml openvas.csv
```

**Scenario:** Correlate scan data with existing vulnerability tracking.

#### 5.5 Red Team Discovery & Trigger Mapping

```bash
nmap -sV --script=banner -iL targets.txt -oX full_discovery.xml
```

**Scenario:** Feed pre-engagement scans into exploit framework or triggers.

---

### 6. VAPT Testing Use Cases

#### 6.1 Web App Recon

```bash
nmap -sS -sV --script=http-enum -p80,443 target.com
```

**Scenario:** Detect backend services, frameworks, and admin panels.

#### 6.2 API Endpoint Fuzzing

```bash
nmap --script http-methods,http-headers -p443 target.com
```

**Scenario:** Discover undocumented APIs or weak header configs.

#### 6.3 Cloud SaaS Port Exposure

```bash
nmap -Pn -T4 -p1-1000 saas-target.corp.com
```

**Scenario:** Identify old/unused dev/test ports left open externally.

#### 6.4 Endpoint/EDR Agent Discovery

```bash
nmap --script=banner -p22,135,445,3389 10.0.0.0/8
```

**Scenario:** Identify machines running security agents or RMM.

#### 6.5 Internal Network VAPT Mapping

```bash
nmap -A -sV -O -iL internal.txt --top-ports 1000 -oA fullmap
```

**Scenario:** Build comprehensive map before exploit phase.

---

