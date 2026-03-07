<div align="center">

<img src="https://img.shields.io/badge/RiskWatchPro-Enterprise%20Threat%20Intelligence-e94560?style=for-the-badge&logoColor=white" alt="RiskWatchPro"/>

# ⚡ RiskWatchPro

### Enterprise Threat Intelligence Platform

**Real-time CVE tracking · MITRE ATT&CK mapping · EPSS scoring · GRC compliance · FAIR risk modeling**

[![Live Platform](https://img.shields.io/badge/🌐%20Live-riskwatchpro.duckdns.org-e94560?style=flat-square)](https://riskwatchpro.duckdns.org)
[![Anubis Engine](https://img.shields.io/badge/⚡%20Engine-anubispro.duckdns.org-7c3aed?style=flat-square)](https://anubispro.duckdns.org)
[![GitHub](https://img.shields.io/badge/Built%20by-ramiz--alsafi-24292e?style=flat-square&logo=github)](https://github.com/ramiz-alsafi)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-ramez--alsafy-0a66c2?style=flat-square&logo=linkedin)](https://linkedin.com/in/ramez-alsafy-57b8b437b)

![Python](https://img.shields.io/badge/Python-3.11-3776ab?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.110-009688?style=flat-square&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-18-61dafb?style=flat-square&logo=react&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-336791?style=flat-square&logo=postgresql&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-EC2%20%2B%20S3%20%2B%20IAM-ff9900?style=flat-square&logo=amazonaws&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh-Hardened-00aef0?style=flat-square)

</div>

---

## 🔍 What is RiskWatchPro?

RiskWatchPro is a production-grade threat intelligence SaaS platform built on top of **Anubis** — a custom Python engine that ingests, enriches, and correlates threat data from 60+ sources in real time.

It answers the question every security team actually cares about:

> *"Of the 20,000 CVEs published this year — which 12 are going to hit us this week, and what does it cost if they do?"*

**Live stats (auto-updated):**
- 🔴 11,500+ threats indexed
- ⚡ 60+ concurrent intelligence sources
- 📡 WebSocket real-time feed
- 🛡 ISO 27001 · NIST 800-53 · SOC 2 · PCI DSS coverage

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        ANUBIS ENGINE v6.5.1                     │
│                                                                 │
│  60+ Threat Feeds (concurrent via ThreadPoolExecutor)           │
│  ├── NVD · CISA KEV · VulnCheck KEV · Exploit-DB               │
│  ├── Metasploit/Rapid7 · ZDI · PacketStorm · OSV               │
│  ├── MalwareBazaar · ThreatFox · URLHaus · AbuseIPDB · Shodan   │
│  ├── Vendor Advisories (Fortinet, Cisco, Palo Alto, MSRC...)    │
│  └── News (BleepingComputer, TheHackerNews, SecurityWeek...)    │
│                          │                                      │
│  Normalisation & Deduplication                                  │
│                          │                                      │
│  Enrichment Layer                                               │
│  ├── EPSS scores (FIRST.org)                                    │
│  ├── AttackerKB exploitation context                            │
│  ├── MITRE ATT&CK STIX (691 techniques)                        │
│  ├── Metasploit module cross-reference (3000+ CVEs)             │
│  ├── ZDI advisory correlation                                   │
│  └── IP Geo/ASN · NVD full detail                              │
│                          │                                      │
│  Composite Risk Scoring                                         │
│  CVSS + EPSS + KEV membership + Exploit availability + Activity │
└──────────────────────┬──────────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────────┐
│                     RISKWATCHPRO PLATFORM                       │
│                                                                 │
│  FastAPI Backend          React Frontend                        │
│  ├── REST API             ├── Real-time dashboard               │
│  ├── WebSocket feed       ├── MITRE ATT&CK heatmap              │
│  ├── Auth (JWT)           ├── Geographic threat map             │
│  ├── Subscription gates   ├── FAIR risk calculator              │
│  └── Paymob billing       └── GRC compliance module            │
│                                                                 │
│  PostgreSQL · Nginx · AWS EC2 · Wazuh · Docker                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✨ Features


|---------|------|-----|------------|
| Threat database (11,500+) | 
| Real-time WebSocket feed | 
| EPSS + CVSS scoring |
| MITRE ATT&CK mapping |
| IOC Lookup | Limited |
| FAIR Risk Calculator |
| GRC Compliance (ISO/NIST/SOC2/PCI) |
| Sandbox emulation |
| Detection rule generation |
| API access |
| SIEM push (Splunk/Sentinel) |
| SLA + dedicated support |

---

## 🚀 Quick Start (Self-hosted)

## 📁 Project Structure

```
riskwatchpro/
├── Anubis/                    # Threat intelligence engine
│   ├── main.py                # Entry point, orchestrator
│   ├── fetchers/              # Per-source fetch modules
│   ├── enrichment/            # EPSS, ATT&CK, MSF enrichers
│   ├── scoring/               # Composite risk scoring
│   ├── cache/                 # Per-feed TTL cache layer
│   └── output/                # PostgreSQL, Excel, HTML writers
│
├── backend/                   # FastAPI application
│   ├── main.py                # App entry point
│   ├── api/                   # Route handlers
│   │   ├── threats.py         # /api/v1/threats
│   │   ├── news.py            # /api/v1/news
│   │   ├── stats.py           # /api/v1/stats
│   │   ├── auth.py            # /api/v1/auth
│   │   ├── billing.py         # /api/v1/billing (Paymob)
│   │   └── grc.py             # /api/v1/grc
│   ├── models/                # SQLAlchemy models
│   ├── schemas/               # Pydantic schemas
│   ├── middleware/             # Auth, rate limiting, plan gates
│   └── alembic/               # DB migrations
│
├── frontend/                  # React application
│   └── src/
│       ├── pages/             # Route-level components
│       ├── components/        # Shared UI components
│       ├── api/               # API client
│       ├── context/           # Auth, theme context
│       └── store/             # State management
│
├── docs/                      # Documentation
│   ├── nginx.conf             # Production Nginx config
│   ├── architecture.md        # Detailed architecture docs
│   └── api.md                 # API reference
│
├── .github/
│   └── workflows/
│       ├── deploy.yml         # Auto-deploy to EC2 on push to main
│       └── ci.yml             # Lint + test on PRs
│
├── docker-compose.yml         # Full stack local development
└── .env.example               # Environment template
```

---

## 🔴 Threat Intelligence Sources (60+)

<details>
<summary>Click to expand full source list</summary>

**Vulnerability Databases**
- National Vulnerability Database (NVD)
- CISA Known Exploited Vulnerabilities (KEV)
- VulnCheck KEV
- Open Source Vulnerabilities (OSV)
- Red Hat CVE Database
- Ubuntu Security Notices

**Exploit Intelligence**
- Exploit-DB
- Rapid7 / Metasploit Framework (3000+ modules)
- Zero Day Initiative (ZDI)
- PacketStorm Security
- Huntr AI/ML CVEs

**Threat Feeds**
- MalwareBazaar
- ThreatFox
- URLHaus
- AbuseIPDB
- AlienVault OTX
- Shodan

**Vendor Advisories**
- Microsoft Security Response Center (MSRC)
- Fortinet PSIRT
- Cisco Talos
- Palo Alto Networks
- Check Point
- SonicWall
- Sophos

**Security News**
- SANS Internet Storm Center (ISC)
- BleepingComputer
- The Hacker News
- SecurityWeek
- CERT/CC
- NCSC

</details>


## 🛡 Security & Infrastructure

- **Hardened AMI** — custom AWS EC2 image, minimal attack surface
- **Wazuh Agent** — real-time log monitoring, FIM, rootcheck, active response (auto IP blocking)
- **IAM least-privilege** — scoped roles, no wildcard permissions
- **Nginx** — HTTPS only, HSTS, security headers
- **JWT Auth** — short-lived access tokens, refresh rotation
- **Rate limiting** — per-endpoint, per-user, per-plan limits

---

## 📊 Roadmap

- [x] Anubis v6 — 60+ source engine
- [x] RiskWatchPro v1 — Full-stack SaaS platform
- [x] Real-time WebSocket feed
- [x] MITRE ATT&CK heatmap
- [x] FAIR risk calculator
- [x] GRC module (ISO/NIST/SOC2/PCI)
- [x] Geographic threat actor map
- [ ] **Paymob billing integration** (in progress)
- [ ] **AI/ML threat prioritisation layer** (up next)
- [ ] **Cloud-native deployment** (ECS Fargate + Lambda + RDS Multi-AZ + CloudFront)
- [ ] SIEM push (Splunk / Microsoft Sentinel)
- [ ] Mobile app (React Native)

---

## 👤 Author

**Ramiz Alsafi** — Penetration Tester · Red Team Operator · Threat Intelligence Engineer

📍 Alexandria, Egypt
🔗 [LinkedIn](https://linkedin.com/in/ramez-alsafy-57b8b437b)
🐙 [GitHub](https://github.com/ramiz-alsafi)
💬 [WhatsApp](https://wa.me/201002921824)
📞 +20 100 292 1824

---

## 📄 License

```
MIT License — see LICENSE for details.
Commercial use requires a license key obtained via the platform.
```

---

<div align="center">
<sub>Built in Alexandria, Egypt 🇪🇬 · Powered by Anubis · Deployed on AWS</sub>
</div>
