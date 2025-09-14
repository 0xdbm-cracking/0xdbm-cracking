# 0xdbm-cracking
![Hacker Banner](https://media.giphy.com/media/3oEjI6SIIHBdRxXI40/giphy.gif)

> **Red Team / Offensive Cyber Simulation Lab**  
> High-intensity training ground for red team operators, malware analysts, penetration testers, and threat researchers. Everything here is framed as simulated and lab-only.

---

`[ERROR] ↳ Injecting RAT payload into target | [C2 Beacon Detected] | [Status: System Breached]`

---

## Red Team Operations

Welcome to the **Offensive Cyber Simulation Lab** — a high-intensity training ground engineered for **red team operators, malware analysts, penetration testers, and threat researchers**. Here, you dive deep into real-world adversary techniques including advanced malware deployment, live attack chain emulation, covert command & control operations, Google dork reconnaissance, SQL injection exploitation, and dark web intelligence gathering.

**All exercises and tools are strictly for authorized simulation, hands-on training, and cybersecurity research purposes only.** This environment empowers you to sharpen offensive skills with cutting-edge methods used by today’s threat actors — in labs only.

---

## 🕵️‍♂️ Dark Web Onion Sites: Entry Points to Hidden Networks

Accessing the Tor network and onion services is essential for deep-dive threat intelligence and privacy-focused research. Below are popular onion site directories and search engines to navigate the dark web:

- [onion.live](http://onion.live) — fast, user-friendly directory for active onion sites.  
- [dark.fail](http://dark.fail) — trusted list of verified onion services with uptime checks.  
- [Ahmia](http://ahmia.fi) — search engine indexing hundreds of onion sites.  
- [TorLink](http://tor.link) — simple onion site portal.  
- [Not Evil](http://notevil) — Tor search engine with extensive onion site database.  
- [Onion.city](http://onion.city) — onion site proxy for clearnet access.

**Note:** Always use the official Tor Browser to access onion services safely. Dark web exploration carries risks — prioritize operational security.

---

## 🕵️ OSINT & Doxing Research Tools

This module highlights widely-used tools in reconnaissance and pre-exploitation. These OSINT resources support **target profiling, infrastructure mapping, metadata discovery, and identity tracing**.

- 🔍 [OSINT Framework](https://www.osintframework.com/) — categorized directory of OSINT tools.  
- 🔎 [Whoxy](https://www.whoxy.com/) — WHOIS & domain ownership intelligence.  
- 📧 [Have I Been Pwned](https://haveibeenpwned.com/) — identify breached emails & leaks.  
- 📷 [Exif.tools](https://exif.tools/) — extract EXIF metadata from images.  
- 📱 [IntelX](https://intelx.io/) — search dark web dumps, pastes, emails, and leaked credentials.  
- 🧠 [Social Searcher](https://www.social-searcher.com/) — monitor digital footprint across social platforms.  
- 🗂️ [WiGLE](https://wigle.net/) — locate wireless networks and map WiFi geolocation data.  
- 🛑 [Wayback Machine](https://archive.org/) — retrieve historical versions of websites and deleted content.

---

## 💀 Simulated Malware Arsenal

> **Simulated / modeled items for lab training only.** Not actual payloads included.

- **RAT.exe** – modeled after Quasar / njRAT-style remote access trojans.  
- **PhantomStealer** – credential/data stealer akin to RedLine / Vidar.  
- **WormInjector** – network-spreading payload inspired by SMBv1 EternalBlue behaviors.  
- **CrimsonLoader** – polymorphic dropper using LOLBAS tactics and PowerShell stagers.  
- **SleepyCat** – stealthy fileless implant using in-memory techniques.

---

## 🎯 Simulated Attack Chain

- **Initial Access:** Spear-phishing, malicious Office/HTA payloads (MalwareBazaar-style), USB HID attacks.  
- **Execution:** Living-off-the-land binaries (`mshta`, `regsvr32`, `rundll32`), obfuscated script execution.  
- **Persistence:** Scheduled tasks, registry run keys, WMI event consumers.  
- **Privilege Escalation:** Local CVEs, token impersonation, DLL sideloading (see Exploit-DB).  
- **Defense Evasion:** AMSI & ETW bypass, API unhooking, custom packers.  
- **Exfiltration:** Encrypted channels over HTTPS, DNS tunneling, staging to simulated C2 endpoints.

---

## 📡 Simulated C2 Infrastructure



c2.ghostops.internal
rat.0xdbm-cracking.local
dropzone.secops.dev





---

## 🔗 Malware Research & Intelligence Sources

- [VX Underground](https://www.vx-underground.org/) — malware archive for research.  
- [Malpedia](https://malpedia.caad.fkie.fraunhofer.de/) — threat actor & family profiles.  
- [MalwareBazaar](https://bazaar.abuse.ch/) — analyst-contributed payload samples.  
- [VirusTotal](https://www.virustotal.com/) — static & dynamic analysis.  
- [Any.Run](https://any.run/) — interactive sandbox for live analysis.  
- [GitHub red-team topics](https://github.com/topics/red-team) — curated offensive tooling (use ethically).

---

## 🔍 Google Dorking 2025: Advanced Search for Attack Surface Discovery

**Google Dorking** uses advanced search operators to find unintentionally exposed content. Useful for attack surface discovery and defensive audits.

**Common Google Dorks Examples:**

- `intitle:"index of" "backup"` — finds public backup directories.  
- `filetype:env db_password` — searches for environment files leaking credentials.  
- `site:gov confidential` — targets government domains for exposed docs.  
- `inurl:"/admin/login.php"` — locates exposed admin login pages.  
- `ext:log "error" "password"` — finds exposed log files.  
- `filetype:sql "insert into" "password"` — finds SQL dumps with credentials.  
- `intitle:"index of" "private"` — directories named “private”.  
- `intext:"confidential" filetype:pdf` — PDFs labeled confidential.  
- `allinurl: admin config` — URLs containing “admin” and “config”.  
- `ext:bak OR ext:old OR ext:backup` — exposed backup file types.  
- `site:edu "student records"` — educational domains with exposed student info.  
- `intitle:"phpinfo()" "published by the PHP Group"` — public PHP info pages.  
- `inurl:"?id=" AND "union select"` — pages that may contain SQLi indicators.  
- `filetype:xls "password"` — Excel files with plaintext passwords.

**Defensive Tip:** Regularly scan your public assets with dorks to find and remediate leaks.

---

## 💉 SQL Injection 2025: Breaching Databases with Malicious Queries

**SQL Injection (SQLi)** remains a critical web vulnerability where untrusted input is interpreted as part of database queries, enabling data theft, unauthorized access, or destructive actions.

In 2025, automation and AI accelerate discovery and exploitation of SQLi (including blind and second-order variants).

> **Examples shown here are from the provided simulation content. Use only in controlled lab environments.**

**Common SQL Injection Examples (as provided in simulation content):**

- `' OR '1'='1'; --` — classic authentication bypass pattern.  
- `UNION SELECT username, password FROM users;` — illustrate data exfiltration via union-based injection.  
- `'; DROP TABLE users; --` — destructive payload example.  
- `AND 1=CAST((SELECT TOP 1 password FROM users) AS INT); --` — blind-extraction style example.

**Defensive Tips:** Use prepared statements / parameterized queries, sanitize inputs, enforce least-privilege DB accounts, enable WAFs, and test applications in staging with authorized scanners.

---

## 💣 Ransomware 2025: Digital Hostage Tactics

Ransomware continues to evolve: modern strains use strong encryption, double extortion (steal then encrypt), targeted campaigns, and supply-chain compromises.

**How Ransomware Spreads:**

- Phishing with malicious attachments/links.  
- Exploiting public-facing services (RDP, VPN).  
- Trojans/droppers like `CrimsonLoader`.  
- Supply-chain compromises.

**Signs of Infection:**

- Files renamed/unavailable with weird extensions.  
- Ransom notes demanding crypto payment.  
- Unusual traffic to external IPs/C2.  
- Disabled security tools or backups.

**Prevention:** Maintain offline backups, patch quickly, train users, use EDR, and apply robust segmentation.

---

## 📚 Ethical Use Disclaimer

This simulation environment is designed solely for **educational use, cyber defense training, and legal red teaming engagements**.

No real malware is executed or transmitted in this README. Always operate under authorized conditions and comply with laws and ethical guidelines.

---

## Repo Structure (Suggested)
/README.md
/ctf-writeups/
/osint/
/malware-analysis/ # notes only — no live samples in public
---

## Responsible Disclosure & Rules

- All testing must be authorized with written permission.  
- Do not publish exploited data or active malware samples in public repos.  
- If you find a vulnerability on third-party systems: follow responsible disclosure (vendor/CERT/coordinated disclosure).  
- Respect privacy and applicable laws.

---

**Relentless research. Lab-only execution. Full respect for law & ethics.**

/tools/
/playbooks/
/notes/





