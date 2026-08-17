# Reconnaissance and Information Gathering Skill

> Systematically collect intelligence about a target organization, infrastructure, personnel, and attack surface before a penetration test.

## When to Use

- Beginning a penetration test engagement (Phase 1)
- Conducting a red team assessment
- Building an attack surface map for an organization
- Preparing for a social engineering engagement
- Performing OSINT (Open Source Intelligence) research on a target
- Validating an organization's external exposure
- Threat intelligence gathering for a security operations center
- Bug bounty reconnaissance before vulnerability hunting

## Prerequisites

- Written authorization (scope document, Rules of Engagement)
- Clear understanding of in-scope and out-of-scope targets
- VPN or designated testing IP for active reconnaissance
- Dedicated testing environment to avoid attribution issues
- Familiarity with Linux command line

## Tools

| Tool | Category | Purpose | License |
|------|----------|---------|---------|
| Amass | DNS | Subdomain enumeration and OSINT | Apache-2.0 |
| Subfinder | DNS | Passive subdomain discovery | MIT |
| httpx | Web | HTTP probing and technology detection | MIT |
| Nuclei | Scanning | Template-based vulnerability scanning | MIT |
| Shodan | OSINT | Internet-connected device search engine | API-based |
| Censys | OSINT | Certificate and host intelligence | API-based |
| theHarvester | OSINT | Email, subdomain, and name harvesting | GPL |
| Recon-ng | Framework | Modular reconnaissance framework | GPL |
| SpiderFoot | OSINT | Automated OSINT collection | MIT |
| crt.sh | Certificate | Certificate transparency log search | Free |
| Wayback Machine | Archive | Historical website snapshots | Free |
| Hunter.io | OSINT | Email address discovery | Freemium |
| WHOIS | DNS | Domain registration information | Free |

## Step-by-Step Procedure

### Phase 1: Passive Reconnaissance (No Direct Contact)

Passive recon does not send any traffic directly to the target. All information is gathered from third-party sources.

#### 1.1 Domain and DNS Intelligence

```bash
# Enumerate subdomains (passive sources)
subfinder -d target.com -o subdomains.txt
amass enum -passive -d target.com -o amass_subs.txt

# Certificate transparency logs
curl -s "https://crt.sh/?q=%25.target.com&output=json" | jq -r '.[].name_value' | sort -u

# DNS records
dig target.com ANY
dig target.com MX
dig target.com TXT
dig target.com NS

# WHOIS lookup
whois target.com

# Historical DNS (SecurityTrails, DNSDumpster)
```

#### 1.2 Technology Fingerprinting

```bash
# Probe live hosts and detect technologies
cat subdomains.txt | httpx -tech-detect -status-code -title -o live_hosts.txt

# Web technology identification
whatweb https://target.com

# Check Wappalyzer / BuiltWith for technology stack
```

#### 1.3 Search Engine Reconnaissance

- **Google Dorking**:
  - `site:target.com filetype:pdf` — Find PDF documents
  - `site:target.com filetype:sql` — Find exposed SQL files
  - `site:target.com inurl:admin` — Find admin panels
  - `site:target.com inurl:login` — Find login pages
  - `"target.com" password` — Find leaked passwords
  - `site:pastebin.com target.com` — Find leaked data on Pastebin
- **Bing, Yandex, Baidu**: Run equivalent queries on other search engines.
- **GitHub/GitLab Search**:
  - Search for the organization name, domain, and common project names.
  - Look for committed secrets: API keys, passwords, tokens, connection strings.
  - Check `.git/config`, `.env`, `docker-compose.yml` in public repos.

#### 1.4 Shodan and Censys

```bash
# Shodan search
shodan search "org:TargetCompany" --fields ip_str,port,org,os,product

# Censys search
censys search "TargetCompany"

# Look for:
# - Open ports and services
# - SSL/TLS certificates
# - IoT devices
# - Exposed databases (MongoDB, Elasticsearch, Redis)
# - Remote access (RDP, SSH, VNC)
```

#### 1.5 Social Media and Personnel

- **LinkedIn**: Identify employees, roles, technologies mentioned in profiles.
- **Twitter/X**: Search for the company name, employees, and tech stack mentions.
- **GitHub**: Identify developers, their code repositories, and coding patterns.
- **Hunter.io**: Find email patterns (`firstname.lastname@target.com`).
- **theHarvester**: Aggregate emails and names from multiple sources.

#### 1.6 Wayback Machine and Cached Content

```bash
# Historical URLs
waybackurls target.com | sort -u > wayback_urls.txt

# Look for:
# - Old endpoints that may still be active
# - Leaked configuration files
# - JavaScript files with API keys or internal URLs
# - Sensitive pages that were "removed" but still cached
```

### Phase 2: Active Reconnaissance (Direct Interaction)

Active recon sends traffic to the target. Requires explicit authorization.

#### 2.1 DNS Brute Forcing

```bash
# Subdomain brute force
amass enum -active -d target.com -brute -w /usr/share/wordlists/subdomains.txt

# Alternative with gobuster
gobuster dns -d target.com -w /usr/share/wordlists/subdomains.txt -t 50

# Virtual host discovery
gobuster vhost -u https://target.com -w /usr/share/wordlists/vhosts.txt
```

#### 2.2 Port and Service Scanning

```bash
# Quick initial scan (top 1000 ports)
nmap -sV -sC -T4 target.com -oA initial_scan

# Full port scan (all 65535 ports)
nmap -sV -sC -p- -T4 target.com -oA full_scan

# UDP scan (top 100 ports)
nmap -sU --top-ports 100 target.com -oA udp_scan

# Service-specific scanning
nmap -sV -p 80,443,8080,8443 target.com --script=http-enum,http-headers
```

#### 2.3 Web Application Mapping

```bash
# Directory and file brute forcing
gobuster dir -u https://target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,js,txt -o dirs.txt

# API endpoint discovery
feroxbuster -u https://target.com -w /usr/share/wordlists/seclists/Discovery/Web-Content/api/api-endpoints.txt

# Spider/crawl the application
gospider -s https://target.com -d 2 -c 10 -o output/

# JavaScript file analysis
cat live_hosts.txt | grep "\.js$" | httpx -mc 200 | while read url; do
  echo "=== $url ==="
  curl -s "$url" | grep -oE 'https?://[^"'"'"' ]+' | sort -u
done
```

#### 2.4 Screenshot and Visual Recon

```bash
# Take screenshots of all live hosts
cat live_hosts.txt | httpx -screenshot -o screenshots/

# Eyewitness for visual grouping
eyewitness --file live_hosts.txt --web --output eyewitness_report/
```

### Phase 3: Attack Surface Compilation

1. **Consolidate all findings** into a single document:
   - Domain and subdomain list (with IP addresses).
   - Live hosts with ports and services.
   - Technology stack per host.
   - Discovered endpoints and parameters.
   - Employee names and email addresses.
   - Interesting files and configurations.
2. **Create a prioritized target list**:
   - Internet-facing applications (highest priority).
   - VPN/remote access endpoints.
   - Email servers.
   - Development/staging environments (often less secured).
   - Third-party services with the company's data.
3. **Identify potential attack vectors** based on the reconnaissance.

## Templates

### Reconnaissance Report Template

```markdown
## Reconnaissance Report — [Target]

### Engagement Details
- **Client**: [Organization]
- **Scope**: [In-scope domains/IPs]
- **Date**: [YYYY-MM-DD]
- **Tester**: [Name]
- **Authorization Ref**: [Document ID]

### Domain Intelligence
| Domain | IP | Hosting | Technologies | Notes |
|--------|----|---------|-------------|-------|
| target.com | 1.2.3.4 | AWS | Nginx, React, Node.js | Main site |
| api.target.com | 1.2.3.5 | AWS | Express.js, PostgreSQL | API |

### Subdomains Discovered
Total: [N] subdomains, [M] live

| Subdomain | IP | Status | Ports | Tech |
|-----------|----|--------|-------|------|
| www | 1.2.3.4 | 200 | 80,443 | Nginx |
| api | 1.2.3.5 | 200 | 443 | Express |
| admin | 1.2.3.6 | 403 | 443 | Apache |

### Employee Intelligence
| Name | Role | Email | GitHub | LinkedIn |
|------|------|-------|--------|----------|
| John Doe | DevOps | jdoe@target.com | @jdoe | /in/jdoe |

### Interesting Findings
1. Staging environment exposed: `staging.target.com`
2. Old WordPress site: `blog.target.com` (WordPress 5.2 — outdated)
3. Exposed `.git` directory on `dev.target.com`
4. Default credentials on `jenkins.target.com`

### Recommended Next Steps
1. Test staging environment for sensitive data exposure.
2. Attempt credential reuse with discovered email addresses.
3. Test exposed Jenkins for RCE.
4. Perform web application testing on main site and API.
```

### Google Dork Quick Reference

| Dork | Purpose |
|------|---------|
| `site:target.com filetype:pdf` | Find PDF documents |
| `site:target.com filetype:sql OR filetype:bak` | Find database backups |
| `site:target.com inurl:admin OR inurl:dashboard` | Find admin panels |
| `site:target.com intitle:"index of"` | Find directory listings |
| `site:pastebin.com "target.com"` | Find leaked data |
| `site:github.com "target.com" password` | Find committed secrets |
| `site:target.com ext:xml inurl:sitemap` | Find sitemaps |
| `"target.com" "@" filetype:txt` | Find email lists |

## Common Pitfalls

- **Skipping passive reconnaissance** — Passive recon is low-risk and high-value. Never jump straight to active scanning.
- **Not documenting as you go** — Reconnaissance generates massive amounts of data. Record findings in real time; reconstructing later is painful.
- **Scanning too aggressively** — Aggressive scanning can trigger IDS/IPS, WAF blocks, and legal complaints. Start passive, escalate gradually.
- **Ignoring historical data** — Old endpoints, cached pages, and archived code often reveal vulnerabilities that current scans miss.
- **Not checking certificate transparency** — CT logs are a goldmine for discovering subdomains, internal hostnames, and forgotten services.
- **Attribution mistakes** — Use a VPN or dedicated testing infrastructure. Direct scanning from a personal IP creates legal and attribution issues.
- **Scope creep** — Recon will inevitably discover out-of-scope assets. Document them but do not test them without authorization.

## Legal Considerations

- **Written Authorization is Mandatory**: Never perform active reconnaissance without a signed contract and scope document.
- **Passive Recon Limitations**: While passive reconnaissance is generally legal, aggregating information from certain sources may violate their terms of service.
- **Scanning Laws**: In many jurisdictions, port scanning is a gray area. The CFAA (US) and Computer Misuse Act (UK) may apply even to scanning.
- **DoS Risk**: Aggressive scanning can cause service degradation. Use rate limiting and appropriate timing.
- **Third-Party Infrastructure**: If the target uses cloud services (AWS, Azure), the cloud provider's acceptable use policies also apply.
- **Data Handling**: Any personal information collected (employee names, emails) must be handled according to privacy regulations (GDPR, CCPA).
- **Attribution**: Use designated testing infrastructure. Never scan from personal or corporate networks that could create misattribution.

## Further Reading

- [OWASP Testing Guide: Information Gathering](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/01-Information_Gathering/)
- [PTES: Intelligence Gathering](http://www.pentest-standard.org/index.php/Intelligence_Gathering)
- [NIST SP 800-115: Technical Guide to Information Security Testing](https://csrc.nist.gov/publications/detail/sp/800-115/final)
- [SANS: Reconnaissance Best Practices](https://www.sans.org/)
- [OSINT Framework](https://osintframework.com/)
- [Hacking the Cloud: OSINT](https://hackingthe.cloud/)
