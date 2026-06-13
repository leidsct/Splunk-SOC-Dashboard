# 🔵 Splunk SOC Dashboard — DNS Threat Analysis

> A Security Operations Center (SOC) project using Splunk Enterprise to analyze real DNS network logs and detect suspicious activity.

---

## 📋 Project Overview

This project demonstrates real-world SOC analyst skills by:
- Ingesting real network DNS logs into Splunk
- Performing threat hunting using SPL (Splunk Processing Language)
- Identifying suspicious hosts and DNS activity
- Building a SOC security dashboard for visualization

---

## 🛠️ Tools Used

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)

- **Splunk Enterprise** — SIEM platform for log analysis
- **DNS Logs** — Real network data from MACCDC2012 dataset (SecRepo.com)

---

## 📊 Dataset

- **Source:** SecRepo.com — MACCDC2012 Network Dataset
- **File:** `dns.log.gz`
- **Total Events:** 422,130 DNS events
- **Type:** Real network traffic including scanning, recon, and exploitation activity

---

## 🔍 Investigation Steps

### Step 1 — Ingested DNS Logs
Uploaded `dns.log.gz` into Splunk Enterprise and configured source type as `dns_logs`.

### Step 2 — Searched for REFUSED DNS Queries
```spl
source="dns.log.gz" REFUSED
```
**Result: 1,767 REFUSED events detected** 🚨

### Step 3 — Identified Suspicious Host
```spl
source="dns.log.gz" 192.168.202.88 REFUSED | stats count
```
**Result: 1,636 REFUSED queries from a single IP — 192.168.202.88** 🚨

### Step 4 — Analyzed DNS Patterns
```spl
source="dns.log.gz" 192.168.202.88 | stats count by punct | sort -count
```
**Result: 23 unique DNS patterns — top pattern appeared 1,320 times**

### Step 5 — Built SOC Dashboard
Created visualization showing DNS pattern distribution for suspicious host.

---

## 🚨 Findings

| Finding | Details | Severity |
|---|---|---|
| Suspicious Host | 192.168.202.88 | 🔴 High |
| REFUSED Queries | 1,636 events from single IP | 🔴 High |
| DNS Pattern Anomaly | Top pattern: 1,320 occurrences | 🟡 Medium |
| Total REFUSED Events | 1,767 across all hosts | 🟡 Medium |

---

## 📸 Dashboard Screenshot

![SOC DNS Analysis Dashboard](./soc-dns-dashboard.png)

---

## 💡 Key Learnings

- How to ingest and index logs in Splunk
- Using SPL (Search Processing Language) for threat hunting
- Identifying suspicious DNS activity — REFUSED queries, NXDOMAIN
- Building security dashboards in Splunk
- Detecting potential C2 communication via DNS anomalies

---

## 🗺️ Part of My SOC Analyst Journey

This project is **Phase 6** of my SOC Analyst roadmap:

```
Phase 1 — Linux Foundation        ✅ DONE
Phase 2 — Networking              ✅ DONE
Phase 3 — Python Basics           ✅ DONE
Phase 4 — Cybersecurity Fundamentals ✅ DONE
Phase 5 — Wireshark + Log Analysis   ✅ DONE
Phase 6 — SIEM + Splunk              🔄 IN PROGRESS ← THIS PROJECT
Phase 7 — Portfolio + Resume         🔄 IN PROGRESS
```

---

*Part of my cybersecurity portfolio — github.com/leidsct*
