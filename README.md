<div align="center">
<img src="https://img.shields.io/badge/RiskWatchPro-Threat%20Intelligence-e94560?style=for-the-badge&logoColor=white" alt="RiskWatchPro"/>

# ⚡ RiskWatchPro
### Threat Intelligence · Incident Response · GRC Automation

**Real-time CVE tracking · MITRE ATT&CK mapping · EPSS scoring · GRC compliance · FAIR risk modeling**

[![Live Platform](https://img.shields.io/badge/🌐%20Live-riskwatchpro.online-e94560?style=flat-square)](https://riskwatchpro.online)
[![Anubis Engine](https://img.shields.io/badge/⚡%20Engine-riskwatchpro.online-7c3aed?style=flat-square)](https://riskwatchpro.online)
[![GitHub](https://img.shields.io/badge/Built%20by-ramiz--alsafi-24292e?style=flat-square&logo=github)](https://github.com/ramiz-alsafi)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-ramiz--alsafi-0a66c2?style=flat-square&logo=linkedin)](https://linkedin.com/in/ramiz-alsafi-57b8b437b)

![Python](https://img.shields.io/badge/Python-3776ab?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-61dafb?style=flat-square&logo=react&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-dc382d?style=flat-square&logo=redis&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-EC2%20%2B%20S3%20%2B%20IAM-ff9900?style=flat-square&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ed?style=flat-square&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-e6522c?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-f46800?style=flat-square&logo=grafana&logoColor=white)
![WireGuard](https://img.shields.io/badge/WireGuard-VPN%20Mesh-88171a?style=flat-square&logo=wireguard&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh-Hardened-00aef0?style=flat-square)

</div>

---

## 🔍 What is RiskWatchPro?

RiskWatchPro is a production-grade threat intelligence SaaS platform built on top of **Anubis**, a custom Python engine that ingests, enriches, and correlates threat data from 60+ sources every 4 hours.

It answers the question every security team actually cares about:

> *"Of the 20,000 CVEs published this year, which 12 are going to hit us this week, and what does it cost if they do?"*

**Live stats (auto-updated every 4 hours):**
- 🔴 20,000+ threats indexed
- ⚡ 60+ concurrent intelligence sources
- 📡 WebSocket real-time feed
- 🛡 ISO 27001 · NIST 800-53 · SOC 2 · PCI DSS coverage

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        ANUBIS ENGINE v9.0                           │
│                                                                     │
│  60+ Threat Feeds  (concurrent via ThreadPoolExecutor)              │
│  ├── NVD · CISA KEV · VulnCheck KEV · Exploit-DB · OSV              │
│  ├── Metasploit/Rapid7 · ZDI · Feodo Tracker · AbuseIPDB            │
│  ├── MalwareBazaar · ThreatFox · URLHaus · OTX · Shodan             │
│  ├── Vendor Advisories (Fortinet, Cisco, Palo Alto, MSRC, F5…)      │
│  └── News (BleepingComputer, TheHackerNews, SANS ISC, NCSC…)        │
│                            │                                        │
│           Normalisation & Deduplication                             │
│                            │                                        │
│  Enrichment Layer                                                   │
│  ├── EPSS scores (FIRST.org)                                        │
│  ├── MITRE ATT&CK STIX (691 techniques mapped)                      │
│  ├── Metasploit module cross-reference (3,000+ CVEs)                │
│  ├── AttackerKB exploitation context                                │
│  ├── ZDI advisory correlation                                       │
│  └── IP Geo/ASN enrichment · NVD full detail                        │
│                            │                                        │
│  Composite Risk Scoring                                             │
│  CVSS × EPSS × KEV membership × Exploit availability × Activity     │
│                            │                                        │
│        Scheduler: every 4h · max_instances=1 · coalesce=True        │
└────────────────────────────┬────────────────────────────────────────┘
                             │
                      PostgreSQL
                             │
┌────────────────────────────▼────────────────────────────────────────┐
│                    RISKWATCHPRO PLATFORM  v9.0                      │
│                                                                     │
│  FastAPI Backend (Dockerized)                                       │
│  ├── Threat intelligence API (paginated, filterable, sortable)      │
│  ├── Stats & heatmap service                                        │
│  ├── Sandbox detonation service                                     │
│  ├── GRC compliance report engine                                   │
│  ├── Auth service (JWT + TOTP 2FA)                                  │
│  ├── Billing service                                                │
│  ├── Email service (digest, preferences, unsubscribe)               │
│  ├── IOC lookup & news feed                                         │
│  └── Email Inspector (phishing analysis, IP reputation, PDF report) │
│                                                                     │
│  React Frontend                                                     │
│  ├── Landing (animated stats, live ticker, pricing)                 │
│  ├── Email Inspector (free, no login — public phishing analysis)    │
│  ├── Dashboard (MITRE heatmap, severity charts, run tracker)        │
│  ├── Threats (20,000+ CVEs, filters, enriched detail)               │
│  ├── Intel Center (IOC lookup, threat actors)                       │
│  ├── Sandbox (URL/IP/file detonation)                               │
│  ├── GRC & Compliance                                               │
│  ├── News & Intel feed                                              │
│  ├── Pricing (Free / Pro / checkout)                                │
│  ├── Help & Support (live chat, FAQ, contact)                       │
│  └── Profile (account, billing, API keys, TOTP, sessions)           │
│                                                                     │
│  Infrastructure                                                     │
│  ├── Docker Compose                                                 │
│  ├── Redis 7                                                        │
│  ├── PostgreSQL                                                     │
│  ├── Nginx                                                          │
│  ├── WireGuard                                                      │
│  ├── Wazuh Agent                                                    │
│  ├── GitHub Actions CI/CD                                           |
|  ├── pgAdmin                                                        │
│  └── Tawk.to live support                                           │
│                                                                     │
│  Observability Stack                                                │
│  ├── Prometheus — metrics collection                                │
│  ├── Grafana — dashboards                                           │
│  ├── Node Exporter — Host metrics                                   │
│  ├── prometheus-fastapi-instrumentator                              |
|  ├── PostgreSQL Exporter                                            |
|  └── NGINX Exporter                                                 |
└─────────────────────────────────────────────────────────────────────┘
```

---

## ✨ Features

| Feature | Free | Pro | Enterprise |
|---|:---:|:---:|:---:|
| Threat database (20,000+) | ✓ | ✓ | ✓ |
| Real-time WebSocket feed | ✓ | ✓ | ✓ |
| EPSS + CVSS + Risk scoring | ✓ | ✓ | ✓ |
| MITRE ATT&CK heatmap | ✓ | ✓ | ✓ |
| FAIR Risk Calculator | ✓ | ✓ | ✓ |
| **Email Inspector** (phishing analysis) | ✓ | ✓ | ✓ |
| CVE lookups/day | 100 | Unlimited | Unlimited |
| IOC Lookup | Limited | ✓ | ✓ |
| GRC Compliance Reports | — | ✓ | ✓ |
| Sandbox emulation | — | 10/mo | Unlimited |
| API access | — | ✓ | ✓ |
| TOTP 2FA | ✓ | ✓ | ✓ |
| Email digest notifications | ✓ | ✓ | ✓ |
| Team seats | — | — | 10 |
| Dedicated support + SLA | — | — | ✓ |

---

## 📁 Project Structure

```
anubis-platform/
├── backend/
│   ├── app/
│   │   ├── api/         
│   │   ├── core/         
│   │   ├── models/      
│   │   ├── schemas/      
│   │   ├── services/     
│   │   └── main.py
│   ├── alembic/
│   └── Dockerfile
│
├── frontend/
│   └── src/
│       ├── pages/        
│       ├── components/  
│       ├── api/
│       ├── context/     
│       └── store/
│
├── monitoring/
│   ├── prometheus.yml
│   └── grafana/
│
├── .github/
│   └── workflows/
│       └── deploy.yml   
│
└── docker-compose.yml
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
- Rapid7 / Metasploit Framework (3,000+ modules)
- Zero Day Initiative (ZDI)
- Huntr AI/ML CVEs

**Threat Feeds**
- MalwareBazaar
- ThreatFox
- URLHaus
- AbuseIPDB
- AlienVault OTX
- Feodo Tracker (C2 IPs)
- Shodan

**Vendor Advisories**
- Microsoft Security Response Center (MSRC)
- Fortinet PSIRT
- Cisco Talos
- Palo Alto Networks
- Check Point
- F5
- SonicWall
- Sophos

**Security News**
- SANS Internet Storm Center (ISC)
- BleepingComputer
- The Hacker News
- CyberSecurityNews
- SecurityWeek
- CERT/CC
- NCSC

</details>

---

## 🛡 Security & Infrastructure

- **Hardened AMI** — custom AWS EC2 image, minimal attack surface
- **WireGuard VPN mesh** — no traditional remote access ports exposed
- **Wazuh Agent** — real-time log monitoring, FIM, rootcheck, active response (auto IP blocking)
- **IAM least-privilege** — scoped roles, no wildcard permissions
- **Cloudflare proxy** — DDoS protection, WAF, IP whitelisting
- **Nginx** — HTTPS only, security headers, buffer-tuned, rate-limited per endpoint
- **Redis cache layer** — TTL-based in-memory caching middleware on all read-heavy API endpoints
- **JWT Auth** — short-lived access tokens, refresh rotation
- **TOTP 2FA** — per-user authenticator app support
- **Email service** — digest, preferences, opt-in/out, unsubscribe, manual trigger
- **Rate limiting** — per-endpoint, per-user, per-plan

---

## 📊 Observability

Full self-hosted monitoring stack running as Docker services alongside the platform:

| Service | Role |
|---|---|
| **Prometheus** | Metrics collection |
| **Grafana** | Dashboards |
| **Node Exporter** | Host metrics |
| **cAdvisor** | Container metrics |
| **Redis Exporter** | Redis metrics |
| **prometheus-fastapi-instrumentator** | Request rates, latency, status codes |


## 📊 Roadmap

- [x] Anubis v9.0 — 60+ source engine
- [x] RiskWatchPro — full-stack SaaS platform
- [x] Real-time WebSocket feed
- [x] MITRE ATT&CK heatmap (all 20,000+ threats)
- [x] FAIR risk calculator
- [x] GRC module
- [x] Geographic threat actor map
- [x] TOTP 2FA authentication
- [x] Email digest & preferences API
- [x] Live execution tracker
- [x] Pricing page + payment method selector
- [x] Help & Support center
- [x] Redis caching layer
- [x] Nginx proxy buffer tuning
- [x] WireGuard VPN mesh
- [x] Cloudflare hardening
- [x] Full observability stack 
- [x] **Email Inspector** 
- [x] **GitHub Actions CI/CD**
- [x] observability exporters
- [x] SEO hardening 
- [x] Google Analytics 4 + GDPR compliant
- [x] Frontend code splitting 
- [ ] **Billing go-live** 
- [ ] SIEM push
- [ ] Mobile app

---

## 👤 Author

**Ramiz Alsafi** — Penetration Tester · Red Team Operator · Threat Intelligence Engineer

📍 Alexandria, Egypt
🔗 [LinkedIn](https://linkedin.com/in/ramiz-alsafi-57b8b437b)
🐙 [GitHub](https://github.com/ramiz-alsafi)
💬 [WhatsApp](https://wa.me/201002921824)
📞 +20 100 292 1824

---

## 📄 License

```
MIT License — see LICENSE for details.
Commercial use requires a license key obtained via the platform.
```
