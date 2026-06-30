# Sprint 5: Enterprise Observability & Feedback Loops

**Sprint Dates:** [Start Date + 56 days] – [Start Date + 70 days]  
**Sprint Goal:** Provide real-time monitoring and alerting using Prometheus, Grafana, and Jenkins notifications for efficient infrastructure management.  
**Team Capacity:** 100 hours (5 members × 20 hours each)  
**Status:** ⬜ Not Started / 🟡 In Progress / 🟢 Completed

---

## Sprint Backlog

| Task ID | Issue # | Task Title | Assignee | Component | Pillar | Priority | Effort (hrs) | Status | Notes |
|---------|---------|------------|----------|-----------|--------|----------|--------------|--------|-------|
| 5.1 | # | Deploy Prometheus Operator into EKS cluster using Helm/Manifests | Observability & Docs Lead | Observability (Prometheus/Grafana) | Implementation (75%) | High | 6 | ⬜ | Needs EKS cluster from Sprint 2 |
| 5.2 | # | Build Grafana dashboards displaying Cluster CPU/Memory utilization and application health | Observability & Docs Lead | Observability (Prometheus/Grafana) | Implementation (75%) | High | 6 | ⬜ | Depends on 5.1 |
| 5.3 | # | Configure Slack/Email alert notifications inside Jenkins for pipeline failures | Config & Automation Lead | CI/CD (Jenkins) | Implementation (75%) | High | 4 | ⬜ | Needs Slack webhook or email SMTP |
| 5.4 | # | Configure Prometheus Alertmanager rules for critical metrics and resource thresholds | Observability & Docs Lead | Observability (Prometheus/Grafana) | Implementation (75%) | High | 4 | ⬜ | Depends on 5.1 |
| 5.5 | # | Integrate Jenkins with Prometheus/Grafana to monitor job and infrastructure health | Observability & Docs Lead | Observability (Prometheus/Grafana) | Implementation (75%) | High | 4 | ⬜ | Depends on 5.1 and 5.3 |
| 5.6 | # | Test monitoring and alerting to ensure visibility into infrastructure and application health | Observability & Docs Lead | Observability (Prometheus/Grafana) | Implementation (75%) | High | 4 | ⬜ | Full integration test |
| 5.7 | # | Document monitoring setup, alerting rules, and dashboard interpretation guide | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | Medium | 3 | ⬜ | Depends on 5.1–5.6 |

---

## Sprint Goal Breakdown

### What "Done" Looks Like for Sprint 5
- [ ] Prometheus is scraping metrics from EKS nodes, pods, and application endpoints
- [ ] Grafana is accessible (via port-forward or Ingress) and has at least 2 dashboards:
  - Cluster-level: CPU, memory, disk, network
  - Application-level: request rate, error rate, latency, pod health
- [ ] Alertmanager is configured with at least 3 alert rules:
  - Pod crash / restart loop
  - Node high CPU/memory
  - Jenkins pipeline failure
- [ ] Alerts reach Slack channel or email inbox within 60 seconds of trigger
- [ ] Jenkins pipeline failures notify the team automatically (Slack/Email)
- [ ] Prometheus can scrape Jenkins metrics (build duration, success rate, queue depth)
- [ ] All monitoring configs are stored in Git (Infrastructure as Code)
- [ ] Monitoring documentation is complete with dashboard screenshots and alert response guide
- [ ] All code is reviewed and merged to `develop`

---

## Dependencies & Risks

### Internal Dependencies
```
Sprint 2 (EKS cluster) + Sprint 4 (App running in EKS) → Task 5.1 (Prometheus deploy)
                                                                    ↓
                                                             Task 5.2 (Grafana dashboards)
                                                                    ↓
                                                             Task 5.4 (Alertmanager rules)
                                                                    ↓
                                                             Task 5.6 (Testing)

Sprint 1 (Jenkins) + Sprint 4 (Jenkins pipeline) → Task 5.3 (Jenkins alerts)
                                                         ↓
                                                  Task 5.5 (Jenkins metrics integration)
```

### External Dependencies
- Slack workspace with webhook URL (or email SMTP credentials)
- Prometheus Helm chart repository access (or raw manifests ready)
- Grafana admin password management (Kubernetes secret or Vault)

### Risk Register
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Prometheus can't scrape EKS metrics | Medium | High | Verify metrics-server is installed; check Prometheus `ServiceMonitor` or `scrape_configs` |
| Grafana dashboards show "No data" | Medium | Medium | Verify Prometheus data source URL; check time range selector; test PromQL queries directly |
| Alertmanager not sending Slack alerts | Medium | High | Test webhook with `curl` first; verify Alertmanager config reload; check Slack channel permissions |
| Jenkins metrics plugin not installed | Medium | Medium | Install Prometheus metrics plugin on Jenkins; verify `/prometheus` endpoint is accessible |
| High cardinality crashing Prometheus | Low | High | Limit label cardinality; avoid unbounded pod labels; use recording rules |
| Grafana exposed without auth | Medium | High | Enable basic auth or OAuth; do not expose Grafana to public internet without authentication |

---

## Sprint Review (To be completed at sprint end)

**Date:** [Fill in]  
**Attendees:** [All 5 team members]  
**Demoed:**
- [ ] Grafana dashboard showing live cluster metrics (CPU, memory graphs)
- [ ] Grafana dashboard showing application metrics (requests, errors, latency)
- [ ] Prometheus targets page showing all endpoints `UP` (green)
- [ ] Alertmanager UI showing configured alert rules
- [ ] Live alert trigger: simulate high CPU → alert fires → Slack notification received in `#jenkins-alerts`
- [ ] Jenkins pipeline failure → Slack notification received within 60 seconds
- [ ] Jenkins metrics visible in Grafana (build duration graph)

**Feedback from team:**
> [Write feedback here]

**Sprint Goal Achieved?** ⬜ Yes / ⬜ Partially / ⬜ No

---

## Sprint Retrospective (To be completed at sprint end)

**What went well?**
> [Fill in]

**What could be improved?**
> [Fill in]

**Action items for Sprint 6:**
- [ ] [Action item 1, owner, due date]
- [ ] [Action item 2, owner, due date]

**Velocity:** [X] story points / hours completed out of 100 planned

---

## Key Decisions Log

| Date | Decision | Made By | Rationale | Impact |
|------|----------|---------|-----------|--------|
| | Prometheus Operator vs. Helm vs. raw manifests | | | Maintainability vs. control |
| | Grafana access method (port-forward vs. Ingress) | | | Security vs. convenience |
| | Slack vs. Teams vs. email for alerts | | | Team preference and integration ease |
| | Alert threshold values (CPU > 80%, memory > 85%, etc.) | | | False alarm vs. early warning balance |
| | Retention period for Prometheus metrics | | | Storage cost vs. historical analysis need |
| | Jenkins plugin: Prometheus vs. InfluxDB | | | Native Prometheus integration vs. external DB |

---

## Cost Tracking (Sprint 5)

| Service | Resource | Running Monthly Cost | Sprint 5 Changes | Infracost Estimate | Variance |
|---------|----------|---------------------|------------------|-------------------|----------|
| EKS | Cluster + nodes | ~$133–$179/mo | | | Depends on 4.7 Graviton choice |
| ALB | Load balancer | ~$22/mo | | | |
| Prometheus | Storage (EBS/GP3) | ~$5/mo | New | | 50GB GP3 volume |
| Grafana | No extra cost | ~$0 | | | Runs in same cluster |
| Slack | Free tier | ~$0 | | | Webhook is free |
| Data transfer | Prometheus scrape + alerts | ~$3/mo | Increased | | Minimal |

**Total Sprint 5 AWS Cost Estimate:** ~$163–$209/mo ongoing (Prometheus storage added)

> 📌 Note: Observability tools run inside the EKS cluster, so no new EC2 costs. The main new cost is Prometheus persistent storage (EBS). Keep it small (~20–50GB) for the capstone to avoid surprises.

---

## Checklist for Moving to Sprint 6

- [ ] All Sprint 5 issues marked `Done`
- [ ] Grafana is accessible and dashboards are functional
- [ ] At least one alert rule tested end-to-end (trigger → notification)
- [ ] Jenkins pipeline alerts are received in Slack/email
- [ ] Monitoring documentation reviewed and merged
- [ ] All monitoring configs are in Git (Helm values, manifests, alert rules)
- [ ] Sprint 6 planning completed — validation, hardening, and viva prep scope
- [ ] Sprint 6 tasks created, assigned, and in `Todo` status

---

*Last updated: [Date] by [Name]*
