# Four Essential Cybersecurity Search Engines

> *A practical reference guide for cybersecurity students*

## Why This Guide?

Most cybersecurity students know Google. Few know Shodan, Censys, Have I Been Pwned, and VirusTotal — the tools professionals use daily to find exposed devices, analyze malware, and check for breached credentials.

This guide covers:
- What each tool does
- Key features and use cases
- Real search examples 
- Limitations you should know
- When to use which one

---

## Quick Reference Table

| Tool | Best for | Free tier? | Website |
| :--- | :--- | :--- | :--- |
| **Shodan** | Finding exposed internet devices | Limited | [shodan.io](https://www.shodan.io) |
| **Censys** | Deep SSL/TLS certificate analysis | Limited | [censys.io](https://search.censys.io/) |
| **Have I Been Pwned** | Checking breached credentials |  Full | [haveibeenpwned.com](https://haveibeenpwned.com) |
| **VirusTotal** | Scanning files/URLs for malware |  Full | [virustotal.com](https://www.virustotal.com) |

---

## 1. Shodan 

**Website:** [https://www.shodan.io](https://www.shodan.io)

### Overview

Shodan is a search engine that indexes devices connected to the internet (servers, IoT devices, webcams, routers, and more). While Google indexes websites, Shodan indexes **IP addresses and open ports**.

### Key Features

| Feature | What it does |
| :--- | :--- |
|  IP/port/service search | Find devices by specific technical attributes |
|  Banner grabbing | Retrieves service information (version, OS, etc.) |
|  Advanced filters | Filter by country, organization, or operating system |
|  Exposure monitoring | Alert when new devices appear |

### Real Search Examples

| Query | What it does |
| :--- | :--- |
| `port:22 country:US` | finds SSH servers in the United States |
| `org:"Google"` | filters devices owned by Google |
| `ssl:"example.com"` | filters devices with SSL certificates for example.com |
| `hostname:google.com` | filters devices with google.com in their hostname |

### Use Cases

- Identifying exposed devices in your organization
- Detecting misconfigured services (e.g., open databases)
- Reconnaissance during authorized penetration tests

### Limitations

- Many useful features require a paid subscription
- Scan data may not be real-time or fully up to date
- Can be overwhelming for beginners

### When to use Shodan

> * When you need a quick, broad view of what's exposed on the internet.*

---

## 2. Censys

**Website:** [https://censys.io](https://search.censys.io/)

### Overview

Censys is an internet scanning platform focused on structured data and deep analysis. It excels at certificate transparency logs and host metadata.

**Important:** Censys has two different search interfaces with different syntaxes. The table below shows both.

### Key Features

| Feature | What it does |
| :--- | :--- |
| Detailed host data | IP geolocation, open ports, services, and protocols |
| Certificate analysis | Full SSL/TLS certificate inspection and history |
| SQL-like queries | Powerful search language for precise filtering |
| Internet-wide datasets | Downloadable datasets for research |

### Real Search Examples

| What you want to find | Legacy Search (`search.censys.io`) | Platform (`platform.censys.io`) |
| :--- | :--- | :--- |
| **HTTP services** | `services.service_name: "HTTP"` | `host.services.service_name: "HTTP"` |
| **specific port** | `services.port: 443` | `host.services.port: 443` |
| **specific country** | `location.country: "United States"` | `host.location.country: "United States"` |
| **specific software** | `services.software.product: "OpenSSH"` | `host.services.software.product: "OpenSSH"` |
| **IP address range** | `ip: 192.168.0.0/24` | `host.ip: 192.168.0.0/24` |

>  **Which one should you use?**  
> - If you go to `search.censys.io` → use the **Legacy** column  
> - If you go to `platform.censys.io` → use the **Platform** column  
> 
> The Platform is newer and more powerful, but both work. Censys provides a [Query Converter](https://docs.censys.com/docs/query-converter) to help translate between them.

### Use Cases

- Asset discovery and inventory
- Threat hunting across the internet
- Attack surface analysis before penetration tests

### Shodan vs Censys 

| Aspect | Shodan | Censys |
| :--- | :--- | :--- |
| Speed | Faster for quick lookups | Slower, but deeper |
| Query language | Simple filters | More powerful (SQL-like) |
| Certificate data | Basic | **Excellent** (certificate transparency) |
| Learning curve | Gentle | Steeper |

### Limitations

- Paid plans required for large-scale queries
- Smaller community than Shodan (fewer shared search examples)
- Two different syntaxes can be confusing for beginners

### When to use Censys

> * When you need deep certificate analysis or complex, structured internet-wide queries.*

---

## 3. Have I Been Pwned 

**Website:** [https://haveibeenpwned.com](https://haveibeenpwned.com)

### Overview

Have I Been Pwned (HIBP) is a free service that allows users to check whether their email addresses or passwords have been exposed in known data breaches. It's maintained by security researcher Troy Hunt.

### Key Features

| Feature | What it does |
| :--- | :--- |
|  Email breach search | Check if an email appears in any breach |
|  Password exposure check | Test if a password has ever been leaked |
|  Breach notifications | Get alerts when new breaches include your email |
|  Public breach database | Browse and search known breaches |

### Real Search Examples

**Free features (no account required):**

| What you want to do | How to do it |
| :--- | :--- |
| Check if an email was in a breach | visit https://haveibeenpwned.com and enter your eamil in the search box |
| Check if a password has been leaked | visit https://haveibeenpwned.com/Passwords and enter the first 5 characters of a SHA-1 password hash |
| Browse all known breaches | visit https://haveibeenpwned.com/PwnedWebsites |

>**Security Note:** Never type your actual password into any website. Use HIBP's password checker with a **hash prefix** (k-anonymity) so the website never sees your full password.

**Domain search (requires paid subscription & domain verification) :**

If you own a domain and want to check all emails @yourcompany.com, you need a paid HIBP subscription and must verify domain ownership first. This is not available as a free, public link.

### Use Cases

- Personal security hygiene (checking your own accounts)
- Detecting compromised corporate credentials
- Supporting security audits and incident response

### Limitations

- Only covers known, public breaches , not zero-days or private leaks
- You cannot download full breach datasets (only check specific emails)

### When to use Have I Been Pwned

> * When you want to know if your credentials have ever been leaked in a breach.*

---

## 4. VirusTotal 

**Website:** [https://www.virustotal.com](https://www.virustotal.com)

### Overview

VirusTotal is a threat intelligence platform that analyzes files, URLs, domains, and IP addresses using over 70 antivirus engines and URL scanners.

### Key Features

| Feature | What it does |
| :--- | :--- |
|  Multi-engine scanning | Checks files against 70+ antivirus engines |
|  File hash lookup | Search by MD5, SHA-1, or SHA-256 hash |
|  URL/domain analysis | Checks if links are malicious or phishing |
|  Community comments | Security researchers often leave notes and insights |

### Real Search Examples
Search by file hash:
https://www.virustotal.com/gui/search/d41d8cd98f00b204e9800998ecf8427e

Search by URL:
Go to https://www.virustotal.com/gui/home/url
Paste a suspicious link and submit

Search by IP address:
https://www.virustotal.com/gui/search/8.8.8.8

Search by domain:
https://www.virustotal.com/gui/search/google.com

Upload a file directly:
Go to https://www.virustotal.com/gui/home/upload

**Warning:** Files you upload **may become public** so never upload sensitive or personal files.

### Use Cases

- Malware detection and analysis
- Investigating suspicious files, emails, or downloads
- Threat intelligence and indicator of compromise (IOC) validation

### Limitations

- Files you upload may become public, just dont upload sensitive data
- Not a replacement for full antivirus software (only a scanning tool)
- Malware authors can submit their own samples to test detection

### When to use VirusTotal

> * When you receive a suspicious file, hash, or URL and want a quick multi-engine verdict.*

---

## Summary: Which Tool Should You Use First?

| Your goal | Tool to use |
| :--- | :--- |
| Find exposed devices on the internet | **Shodan** |
| Perform deep SSL/TLS certificate analysis | **Censys** |
| Check if your email was in a breach | **Have I Been Pwned** |
| Scan a suspicious file or URL for malware | **VirusTotal** |
| Broad internet reconnaissance (fast) | **Shodan** |
| Complex structured internet queries | **Censys** |

---
## References & Further Reading

- [Shodan Help Center](https://help.shodan.io/)
- [Censys Documentation](https://search.censys.io/docs)
- [Censys Query Converter](https://docs.censys.com/docs/query-converter)
- [Have I Been Pwned API Documentation](https://haveibeenpwned.com/API/v3)
- [VirusTotal API & Documentation](https://developers.virustotal.com/reference/overview)
- [Troy Hunt's Blog (creator of HIBP)](https://www.troyhunt.com/)

---

## About This Guide

**Author:** Mohamed Amine ESSOUSSI 
**Date:** 4/26/2026  
**Purpose:** A reference guide for cybersecurity students learning about specialized search tools.

*Feel free to share this guide with anyone who might find it useful.*
