# Network Scanning with Nmap Skill

> Master Nmap for network discovery, port scanning, service enumeration, and vulnerability detection in authorized security assessments.

## When to Use

- Mapping a network's attack surface during a penetration test
- Discovering live hosts and open ports on a target network
- Identifying running services and their versions for vulnerability assessment
- Detecting operating systems and firewall configurations
- Performing compliance checks (verifying only expected ports are open)
- Auditing network segmentation and firewall rules
- Scripting automated network reconnaissance
- Preparing for a red team engagement by mapping the infrastructure

## Prerequisites

- Written authorization for the target network
- Nmap installed (latest stable version recommended)
- Root/administrator privileges for certain scan types (SYN scan, OS detection, traceroute)
- Understanding of TCP/IP networking fundamentals
- Familiarity with common port numbers and protocols

## Nmap Scan Types Reference

| Scan Type | Flag | Description | Privilege |
|-----------|------|-------------|-----------|
| TCP SYN | `-sS` | Half-open scan, fast and stealthy | Root |
| TCP Connect | `-sT` | Full TCP handshake scan | Any |
| UDP Scan | `-sU` | UDP port scanning (slow) | Root |
| ACK Scan | `-sA` | Firewall rule detection | Root |
| Window Scan | `-sW` | TCP window-based detection | Root |
| NULL Scan | `-sN` | No flags set, firewall evasion | Root |
| FIN Scan | `-sF` | FIN flag only, firewall evasion | Root |
| XMAS Scan | `-sX` | FIN+PSH+URG flags, firewall evasion | Root |
| Idle Scan | `-sI` | Zombie host-based blind scan | Root |
| Version Scan | `-sV` | Service and version detection | Any |
| Script Scan | `-sC` | Default NSE scripts | Any |
| OS Detection | `-O` | Operating system fingerprinting | Root |
| Traceroute | `--traceroute` | Network path discovery | Root |

## Step-by-Step Procedure

### Phase 1: Host Discovery

Before port scanning, identify live hosts on the network.

```bash
# Ping sweep on a subnet
nmap -sn 192.168.1.0/24 -oA host_discovery

# ARP scan (local network only, most reliable)
nmap -sn -PR 192.168.1.0/24

# TCP SYN ping on common ports
nmap -sn -PS22,80,443,3389 192.168.1.0/24

# ICMP echo ping (may be blocked by firewalls)
nmap -sn -PE 192.168.1.0/24

# List scan (DNS resolution only, no packets sent)
nmap -sL 192.168.1.0/24

# Scan from a file of targets
nmap -sn -iL targets.txt -oA host_discovery
```

### Phase 2: Port Scanning

#### 2.1 Quick Initial Scan

```bash
# Top 1000 ports (default) with version detection
nmap -sV -T4 192.168.1.1-254 -oA quick_scan

# Top 100 ports (faster)
nmap --top-ports 100 -T4 192.168.1.0/24 -oA top100_scan
```

#### 2.2 Comprehensive Scan

```bash
# All 65535 TCP ports with version and scripts
nmap -sS -sV -sC -p- -T4 192.168.1.100 -oA full_tcp

# UDP top 200 ports (UDP scanning is slow)
nmap -sU --top-ports 200 -T4 192.168.1.100 -oA udp_scan

# Combined TCP and UDP
nmap -sS -sU -sV --top-ports 100 -T4 192.168.1.100 -oA combined_scan
```

#### 2.3 Timing and Performance

| Flag | Name | Speed | Stealth | Use Case |
|------|------|-------|---------|----------|
| `-T0` | Paranoid | Very slow | Very stealthy | IDS evasion |
| `-T1` | Sneaky | Slow | Stealthy | IDS evasion |
| `-T2` | Polite | Moderate | Moderate | Low-bandwidth networks |
| `-T3` | Normal | Default | Default | General use |
| `-T4` | Aggressive | Fast | Noisy | Controlled environments |
| `-T5` | Insane | Very fast | Very noisy | Speed-critical testing |

```bash
# Control scan speed
nmap -sS -T3 --max-rate 100 192.168.1.0/24  # Max 100 packets/sec
nmap -sS -T4 --min-rate 1000 192.168.1.0/24  # Min 1000 packets/sec

# Parallel scanning
nmap -sS --min-parallelism 64 192.168.1.0/24
```

### Phase 3: Service Enumeration

```bash
# Version detection with intensity
nmap -sV --version-intensity 5 192.168.1.100  # Default intensity
nmap -sV --version-intensity 9 192.168.1.100  # Maximum intensity

# Banner grabbing
nmap -sV --version-all 192.168.1.100

# Specific service scripts
nmap -p 80,443 --script http-enum 192.168.1.100      # Web enumeration
nmap -p 21 --script ftp-anon 192.168.1.100             # Anonymous FTP
nmap -p 445 --script smb-enum-shares 192.168.1.100     # SMB shares
nmap -p 25 --script smtp-enum-users 192.168.1.100      # SMTP users
nmap -p 53 --script dns-brute 192.168.1.100            # DNS brute force
nmap -p 161 --script snmp-brute 192.168.1.100          # SNMP community strings
```

### Phase 4: NSE Script Scanning

Nmap Scripting Engine (NSE) extends Nmap with powerful automated checks.

```bash
# Default scripts (equivalent to -sC)
nmap --script=default 192.168.1.100

# Vulnerability category
nmap --script vuln 192.168.1.100

# Safe scripts (non-intrusive)
nmap --script safe 192.168.1.100

# Specific scripts
nmap --script=http-title,http-server-header 192.168.1.100

# Script with arguments
nmap --script http-brute --script-args http-brute.path=/admin 192.168.1.100

# List available scripts
ls /usr/share/nmap/scripts/ | grep <keyword>
nmap --script-help "smb-*"
```

#### Key NSE Script Categories

| Category | Flag | Purpose | Examples |
|----------|------|---------|---------|
| auth | `--script auth` | Authentication testing | `http-brute`, `ftp-anon` |
| broadcast | `--script broadcast` | Network discovery | `broadcast-ping` |
| brute | `--script brute` | Brute force attacks | `ssh-brute`, `ftp-brute` |
| default | `-sC` | Standard safe scripts | `http-title`, `ssh-hostkey` |
| discovery | `--script discovery` | Network enumeration | `dns-brute`, `snmp-sysdescr` |
| dos | `--script dos` | Denial of service (use cautiously) | Various |
| exploit | `--script exploit` | Active exploitation | Various |
| external | `--script external` | External queries | `http-google-malware` |
| fuzzer | `--script fuzzer` | Protocol fuzzing | Various |
| intrusive | `--script intrusive` | May impact target | Various |
| malware | `--script malware` | Malware detection | `smtp-strangeport` |
| safe | `--script safe` | Non-intrusive | Various |
| version | `--script version` | Version detection | Various |
| vuln | `--script vuln` | Vulnerability checks | `smb-vuln-ms17-010` |

### Phase 5: OS Detection and Traceroute

```bash
# OS detection
nmap -O 192.168.1.100

# OS detection with version
nmap -O --osscan-guess 192.168.1.100

# Traceroute
nmap --traceroute 192.168.1.100

# Combined aggressive scan
nmap -A 192.168.1.100  # Equivalent to -sV -sC -O --traceroute
```

### Phase 6: Firewall Evasion Techniques

```bash
# Fragment packets
nmap -f 192.168.1.100

# Specify MTU
nmap --mtu 24 192.168.1.100

# Decoy scan (mix real IP with decoys)
nmap -D RND:10 192.168.1.100
nmap -D 10.0.0.1,10.0.0.2,ME 192.168.1.100

# Source port manipulation
nmap --source-port 53 192.168.1.100

# Idle/zombie scan
nmap -sI zombie_host:port 192.168.1.100

# Append random data
nmap --data-length 25 192.168.1.100

# Randomize host order
nmap --randomize-hosts 192.168.1.0/24

# Spoof MAC
nmap --spoof-mac 0 192.168.1.100

# Custom TTL
nmap --ttl 128 192.168.1.100

# Bad checksum (some firewalls drop these)
nmap --badsum 192.168.1.100
```

### Phase 7: Output and Reporting

```bash
# Normal output
nmap -oN scan_results.txt 192.168.1.100

# XML output (for processing)
nmap -oX scan_results.xml 192.168.1.100

# Grepable output (for scripting)
nmap -oG scan_results.gnmap 192.168.1.100

# All formats at once
nmap -oA scan_results 192.168.1.100

# Verbosity and debugging
nmap -v 192.168.1.100    # Verbose
nmap -vv 192.168.1.100   # More verbose
nmap -d 192.168.1.100    # Debug
nmap -dd 192.168.1.100   # More debug
nmap --reason 192.168.1.100  # Show reason for port state
```

## Templates

### Full Assessment Scan Script

```bash
#!/bin/bash
# Comprehensive Nmap Assessment Script
# Usage: ./nmap_assessment.sh <target>

TARGET=$1
OUTPUT_DIR="nmap_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$OUTPUT_DIR"

echo "[*] Starting Nmap assessment of $TARGET"
echo "[*] Results will be saved to $OUTPUT_DIR/"

# Phase 1: Host discovery
echo "[+] Phase 1: Host Discovery"
nmap -sn -PS22,80,443,3389,8080 "$TARGET" \
  -oA "$OUTPUT_DIR/01_host_discovery"

# Phase 2: Quick port scan
echo "[+] Phase 2: Quick Port Scan (top 1000)"
nmap -sS -sV -T4 --top-ports 1000 "$TARGET" \
  -oA "$OUTPUT_DIR/02_quick_ports"

# Phase 3: Full port scan
echo "[+] Phase 3: Full Port Scan (all 65535)"
nmap -sS -p- -T4 "$TARGET" \
  -oA "$OUTPUT_DIR/03_full_ports"

# Phase 4: Service enumeration on discovered ports
echo "[+] Phase 4: Service Enumeration"
PORTS=$(grep "^[0-9]" "$OUTPUT_DIR/03_full_ports.gnmap" 2>/dev/null \
  | cut -d' ' -f2 | tr '\n' ',' | sed 's/,$//')
if [ -n "$PORTS" ]; then
  nmap -sV -sC -p "$PORTS" "$TARGET" \
    -oA "$OUTPUT_DIR/04_service_enum"
fi

# Phase 5: Vulnerability scan
echo "[+] Phase 5: Vulnerability Scan"
if [ -n "$PORTS" ]; then
  nmap --script vuln -p "$PORTS" "$TARGET" \
    -oA "$OUTPUT_DIR/05_vuln_scan"
fi

# Phase 6: OS detection
echo "[+] Phase 6: OS Detection"
nmap -O --osscan-guess "$TARGET" \
  -oA "$OUTPUT_DIR/06_os_detection"

# Phase 7: Traceroute
echo "[+] Phase 7: Traceroute"
nmap --traceroute "$TARGET" \
  -oA "$OUTPUT_DIR/07_traceroute"

echo "[*] Assessment complete. Results in $OUTPUT_DIR/"
```

### Scan Results Template

```markdown
## Nmap Scan Results — [Target]

### Scan Parameters
- **Target**: 192.168.1.0/24
- **Date**: 2024-01-15
- **Scan Type**: TCP SYN (-sS) + Version (-sV) + Scripts (-sC)
- **Ports**: All 65535 (-p-)
- **Timing**: Aggressive (-T4)

### Summary
- **Hosts Up**: 24
- **Hosts Down**: 232
- **Total Open Ports**: 87

### Results by Host

#### 192.168.1.1 (gateway)
| Port | State | Service | Version | Notes |
|------|-------|---------|---------|-------|
| 22/tcp | open | ssh | OpenSSH 8.9 | |
| 80/tcp | open | http | nginx 1.24 | Redirect to HTTPS |
| 443/tcp | open | https | nginx 1.24 | TLS 1.3 |

#### 192.168.1.100 (webserver)
| Port | State | Service | Version | Notes |
|------|-------|---------|---------|-------|
| 22/tcp | open | ssh | OpenSSH 8.9 | |
| 80/tcp | open | http | Apache 2.4.57 | Default page |
| 3306/tcp | open | mysql | MySQL 8.0 | Accessible from LAN |
| 8080/tcp | open | http-proxy | Jenkins 2.401 | Admin panel exposed |

### Interesting Findings
1. MySQL (3306) accessible from LAN without firewall restriction.
2. Jenkins admin panel on port 8080 with default credentials.
3. SSH with weak key exchange algorithms enabled.
```

## Common Pitfalls

- **Scanning without authorization** — Unauthorized port scanning is illegal in most jurisdictions. Always obtain written permission.
- **Using aggressive timing on production** — `-T5` or high parallelism can crash services or saturate network links. Use `-T3` on production systems.
- **Not scanning all ports** — Default scans only check the top 1000 ports. Services on uncommon ports (e.g., 8443, 9090, 27017) will be missed.
- **Ignoring UDP** — UDP services (DNS, SNMP, TFTP, NTP) are often overlooked but can be critical attack vectors. At least scan the top 100 UDP ports.
- **Not verifying findings** — Nmap's version detection and script output can be inaccurate. Always verify manually.
- **Scan output not saved** — Always use `-oA` to save results in all formats. Re-running a full scan is time-consuming.
- **Forgetting to rescan** — Networks change. Rescan after firewall rule changes, server deployments, or at the start of each engagement.

## Legal Considerations

- **Authorization**: Scanning networks you do not own requires explicit written authorization. This applies to all scan types, including "ping sweeps."
- **Scope Compliance**: Stay within the authorized IP ranges. Scanning adjacent networks, even accidentally, can trigger legal issues.
- **Service Disruption**: Aggressive scans can cause service degradation. Use appropriate timing and monitor the target.
- **Firewall/IDS Triggering**: Your scans will likely be logged. Ensure the security operations team is aware of your activity.
- **Cloud Providers**: AWS, GCP, and Azure have specific policies for security testing. Review their terms before scanning cloud-hosted resources.
- **Idle Scans**: Using a zombie host without its owner's permission is unauthorized access to that host.
- **Export Controls**: Some NSE scripts perform active exploitation. Using them without authorization crosses from testing into attack.

## Further Reading

- [Nmap Official Documentation](https://nmap.org/book/man.html)
- [Nmap NSE Documentation](https://nmap.org/book/nse.html)
- [Nmap Cheat Sheet (StationX)](https://www.stationx.net/nmap-cheat-sheet/)
- [SANS Nmap Poster](https://www.sans.org/)
- [HackTricks: Nmap](https://book.hacktricks.xyz/generic-methodologies-and-resources/external-recon-methodology/nmap)
- [Nmap Network Scanning (Book)](https://nmap.org/book/)
