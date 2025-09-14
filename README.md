# 0xdbm-cracking

> **Red Team Operator · Adversary Emulation · Offensive Engineering**

---

```
██████╗  ██████╗ ██████╗  ██████╗ ███╗   ███╗   _____  _    _  _____ _  __
██╔══██╗██╔═══██╗██╔══██╗██╔═══██╗████╗ ████║  / ____|| |  | ||  __ \ |/ /
██████╔╝██║   ██║██████╔╝██║   ██║██╔████╔██║ | |     | |__| || |  | ' / 
██╔══██╗██║   ██║██╔══██╗██║   ██║██║╚██╔╝██║ | |     |  __  || |  |  <  
██║  ██║╚██████╔╝██║  ██║╚██████╔╝██║ ╚═╝ ██║ | |____ | |  | || |__| . \ 
╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═╝ ╚═════╝ ╚═╝     ╚═╝  \_____||_|  |_||_____/|_|\_\

           Operate under authority. Harden without mercy.
```

---

## 😈 Tone — Sharp, Sinister, Relentless

This README is unapologetically **aggressive**. It’s for operators who prefer the knife edge: surgical, silent, and merciless in testing — but always under legal authority. Expect blunt language, dark aesthetics, and pragmatic playbooks.

---

## 🎯 Mission — Break It, Then Fix It Better

I am **0xdbm-cracking**: I don’t whisper — I pressure-test until defenses scream. The goal: expose failure modes, force defenders to evolve, and hand them the tools to fight back.

> *"If you want comfort, hire auditors. If you want truth, hire a red team."*

---

## 🛠️ Tools & Stack (No fluff)

* Recon: amass, subfinder, certstream, crt.sh
* Ports & Scanning: masscan, nmap, rustscan
* AD & Windows: BloodHound, SharpHound, PowerView (lab-only)
* Post-ex & automation: custom Go tools, PowerShell frameworks (logging-aware)
* Web: Burp Suite, ZAP, manual code review
* Cloud: AWS CLI, Azure CLI, ScoutSuite, Prowler (all in isolated test accounts)
* Telemetry & Detection: ELK, Splunk, OSQuery, Sigma rules

---

## ⚖️ Rules of Engagement — Absolutely Mandatory

1. **Written Authorization** — signed scope & PoA before any action.
2. **Known Blast Radius** — define: what can be touched, what cannot.
3. **Kill Switch** — safe-word or channel that halts activity instantly.
4. **Data Handling** — do not copy or exfiltrate real production data.
5. **Sanitize Deliverables** — no raw secrets in reports; redact and hash.

No excuses.

---

## 🧪 Lab Playbooks — Brutal, But Safe

**NOTE:** I will **not** reference or direct you to clone any repo I haven’t explicitly created and published. Below are **generic, actionable playbooks and templates** you can use to build your own isolated labs. Adapt them — do not run in production.

---

### AD Emulation Lab — Minimal, Isolated

Purpose: emulate enterprise Active Directory: users, groups, GPOs, a couple of Windows hosts, and a Windows Domain Controller. Capture telemetry with an ELK or Splunk instance.

Environment: a single host with nested virtualization or a lab host (VirtualBox / VMware / Proxmox).

Steps (high-level):

1. **Provision VMs** (isolated network)

   * Create a private virtual network (e.g., `lab-net`), no outside routing.
   * Spin up 1 Domain Controller (Windows Server) and 2-3 Windows targets plus 1 Linux attacker (Kali).

2. **Baseline Telemetry**

   * Install filebeat/winlogbeat on Windows hosts or configure syslog to forward to ELK/Splunk in the lab network.

3. **Populate AD**

   * Create test users, an admin account, a handful of service accounts, and at least one high-value ‘svc’ account.
   * Seed the environment with realistic but fake artifacts (documents, simulated credentials stored in accessible locations).

4. **Run Emulations**

   * Map AD with SharpHound from the attacker VM.
   * Simulate credential theft in a controlled fashion (lab-only) and measure detections.

5. **After-Action**

   * Collect logs, evidence, and telemetry. Sanitize outputs. Produce detection rules.

**Example: quick Vagrant skeleton** (adapt to your images/providers):

```ruby
Vagrant.configure("2") do |config|
  config.vm.define "dc" do |dc|
    dc.vm.box = "generic/windows2019"
    dc.vm.network "private_network", ip: "192.168.56.10"
  end

  config.vm.define "win1" do |win1|
    win1.vm.box = "generic/windows10"
    win1.vm.network "private_network", ip: "192.168.56.20"
  end

  config.vm.define "kali" do |kali|
    kali.vm.box = "kalilinux/rolling"
    kali.vm.network "private_network", ip: "192.168.56.30"
  end
end
```

> Fill the provisioning scripts yourself. Do not run domain controllers on networks connected to your home/business without strict isolation.

---

### Cloud Misconfiguration Lab — Isolated Test Account

Purpose: safely simulate cloud misconfigurations (IAM over-permission, S3 buckets, insecure roles) in an account you control.

Principles:

* Use a dedicated test account/subscription with no production data.
* Tag everything `redteam_lab=true` and maintain a short lifecycle.

Playbook:

1. Create an isolated test account (AWS/Azure/GCP).
2. Provision minimal infra: one VM, one storage bucket, one IAM role.
3. Deliberately misconfigure a resource (e.g., overly broad IAM policy or public storage) — record exact changes.
4. From attacker VM, enumerate and simulate abuse using CLI tools.
5. Observe telemetry and craft detection rules.

**Terraform skeleton (conceptual):**

```hcl
provider "aws" { region = "us-east-1" }

resource "aws_s3_bucket" "lab_bucket" {
  bucket = "redteam-lab-${random_id.suffix.hex}"
  acl    = "private"
}

# create an IAM role with wide permissions — DO NOT APPLY IN REAL PROD
resource "aws_iam_role" "lab_role" {
  name = "redteam_lab_role"
  assume_role_policy = <<POLICY
{...}
POLICY
}
```

> Always destroy lab resources when done: `terraform destroy`.

---

## 🧾 Detection Recipes & Hunting Notes (Sinister Edition)

* Hunt for **sudden high-volume domain lookups** from internal systems — often reconnaissance.
* Detect **new service binaries** written to `C:\Windows\Temp` or `%APPDATA%` with odd execution patterns.
* Flag **unusual auth patterns**: service accounts attempting RDP or interactive logins.
* Monitor for **credential dumping indicators** and abnormal LSASS access events.

If you want specific Sigma rules or Splunk queries, say which SIEM and I’ll draft hardened rules (requires authorization context).

---

## 🧾 Deliverables — What You’ll Get (If You Hire Me)

* **Executive Hit-List:** succinct, merciless summary of impact and business risk.
* **Technical Kill-Chain:** step-by-step reproduction (redacted when needed).
* **IOC & Detection Pack:** Sigma rules / Splunk searches / ELK queries.
* **Purple Team Session:** live walkthrough, detection tuning, and re-tests.

---

## ⚠️ Legal & Ethics — No Gray Zones

This work is *only* for authorized testing and education. Any misuse will be condemned and reported. You provide authorization; I provide the pressure test and the remedy.

---

## 📞 Contact

* **GitHub:** `github.com/0xdbm-cracking`
* **Ops:** [ops@0xdbm.example](mailto:ops@0xdbm.example) (PGP available on request)

---

```
_Operate under authority. Harden without mercy._
— 0xdbm-cracking
```
