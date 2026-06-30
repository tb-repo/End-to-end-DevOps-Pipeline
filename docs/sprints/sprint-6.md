# Sprint 6: Validation, Hardening & Offboarding

**Sprint Dates:** [Start Date + 70 days] – [Start Date + 84 days]  
**Sprint Goal:** Finalize and document the CI/CD pipeline, testing its readiness for production deployment. Prepare for viva and presentation.  
**Team Capacity:** 100 hours (5 members × 20 hours each)  
**Status:** ⬜ Not Started / 🟡 In Progress / 🟢 Completed

---

## Sprint Backlog

| Task ID | Issue # | Task Title | Assignee | Component | Pillar | Priority | Effort (hrs) | Status | Notes |
|---------|---------|------------|----------|-----------|--------|----------|--------------|--------|-------|
| 6.1 | # | Write test cases to validate application functionality, deployment success, and infrastructure integrity | Tech Lead | Architecture/Docs | Implementation (75%) | High | 4 | ⬜ | Regression testing |
| 6.2 | # | Execute end-to-end chaos/failure testing to validate alerting systems | Observability & Docs Lead | Observability (Prometheus/Grafana) | Implementation (75%) | High | 4 | ⬜ | Kill pods, scale nodes, test alerts |
| 6.3 | # | Automate Jenkins job triggers for each stage (code change → build → deploy) | Config & Automation Lead | CI/CD (Jenkins) | Implementation (75%) | High | 4 | ⬜ | Webhook triggers, poll SCM, or both |
| 6.4 | # | Compile complete technical documentation runbook (Architecture docs, disaster recovery, pipeline setup) | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | High | 6 | ⬜ | Master documentation deliverable |
| 6.5 | # | [Cost Optimization] Run AWS Cost Explorer review to document savings realized via Graviton instances, right-sizing, and reserved capacity | Infrastructure Lead | Infrastructure (Terraform) | Cost Optimization (10%) | Medium | 3 | ⬜ | Final cost analysis |
| 6.6 | # | Conduct final end-to-end testing to verify stability of CI/CD, monitoring, and infrastructure setup | Tech Lead | Architecture/Docs | Implementation (75%) | High | 4 | ⬜ | Final validation before viva |
| 6.7 | # | Gather team feedback and make adjustments for production-ready setup | Tech Lead | Architecture/Docs | Documentation (15%) | Medium | 2 | ⬜ | Team retrospective action items |
| 6.8 | # | Create final presentation deck and viva preparation materials | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | High | 6 | ⬜ | Slides, demo script, Q&A prep |

---

## Sprint Goal Breakdown

### What "Done" Looks Like for Sprint 6
- [ ] All test cases pass: application builds, deploys, serves traffic, and recovers from failures
- [ ] Chaos test executed: pod killed → HPA scales → alert fires → Slack notification received → pod recovers
- [ ] Jenkins pipeline is fully automated: push to `develop` → build → test → deploy → verify (no manual clicks)
- [ ] Complete documentation runbook exists in `/docs/` with:
  - Architecture diagram and component descriptions
  - Disaster recovery procedures (what to do if EKS fails, Jenkins fails, etc.)
  - Pipeline setup guide (how to rebuild from scratch)
  - Troubleshooting guide (common errors and fixes)
- [ ] Cost analysis report is complete with:
  - Estimated monthly costs by service
  - Savings from Graviton (if implemented), right-sizing, or other optimizations
  - Before/after comparison where applicable
- [ ] Final end-to-end test completed with all team members present
- [ ] Presentation deck is ready with:
  - Problem statement and goals (1 slide)
  - Architecture diagram (1 slide)
  - CI/CD pipeline walkthrough (2–3 slides)
  - Demo screenshots or live demo plan (2–3 slides)
  - Cost analysis and optimization (1 slide)
  - Team contributions and learnings (1 slide)
- [ ] Viva Q&A prep: each team member knows their primary component inside-out
- [ ] All AWS resources are either documented for handoff or scheduled for deletion (if required)

---

## Dependencies & Risks

### Internal Dependencies
```
Sprints 1–5 complete → All Sprint 6 tasks

Task 6.1 (Test cases) + Task 6.2 (Chaos tests) → Task 6.6 (Final E2E test)
                                                          ↓
                                                   Task 6.4 (Docs runbook)
                                                          ↓
                                                   Task 6.8 (Presentation)
```

### Risk Register
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Chaos test breaks the demo environment | Medium | High | Run chaos test in a separate namespace or schedule it after screenshots are captured |
| Documentation incomplete due to time crunch | High | High | Start drafting docs in Sprint 5; use the `/docs/` structure from Day 1 |
| Cost report missing data | Medium | Medium | Enable AWS Cost Explorer on Day 1; export data every sprint |
| Presentation too technical for evaluators | Medium | Medium | Practice with a non-technical friend; include "why this matters" on every slide |
| Team member unprepared for viva Q&A | Medium | High | Assign 2–3 questions per person based on their component; do mock viva |
| AWS bill unexpectedly high | Medium | Medium | Set up billing alerts in Sprint 1; review costs weekly; delete unnecessary resources |
| Live demo fails during presentation | Medium | High | Have screenshots as backup; pre-record a 2-minute demo video; test demo 3 times before viva |

---

## Sprint Review (To be completed at sprint end)

**Date:** [Fill in]  
**Attendees:** [All 5 team members + evaluator (if applicable)]  
**Demoed:**
- [ ] Full pipeline: code push → Jenkins build → ECR push → EKS deploy → live app
- [ ] Grafana live dashboard with real-time metrics
- [ ] Simulated failure: delete pod → watch HPA recover → alert in Slack
- [ ] Cost savings report (Graviton comparison, right-sizing evidence)
- [ ] Documentation runbook walkthrough (5-minute overview)
- [ ] Team presentation rehearsal (full 15–20 minute run-through)

**Feedback from team / evaluator:**
> [Write feedback here]

**Sprint Goal Achieved?** ⬜ Yes / ⬜ Partially / ⬜ No

---

## Sprint Retrospective (Final Project Retrospective)

**What went well across all 6 sprints?**
> [Fill in]

**What could be improved if we did this again?**
> [Fill in]

**Key metrics:**
- Total issues completed: [X] out of 39
- Total hours logged: [X] out of 600
- PRs merged: [X]
- Bugs found and fixed: [X]
- Cost optimization achieved: $[X] / month
- Documentation pages written: [X]

**Team shout-outs:**
> [Recognize team members for specific contributions]

---

## Key Decisions Log

| Date | Decision | Made By | Rationale | Impact |
|------|----------|---------|-----------|--------|
| | Demo live vs. pre-recorded vs. screenshots | | | Risk of failure vs. polish |
| | Resources to keep vs. delete post-viva | | | Cost vs. future reference |
| | Presentation time allocation per section | | | 15 min total — prioritize demos |
| | Viva Q&A assignment per person | | | Each person owns their component |
| | Final AWS cost responsibility | | | Who pays / how to split |

---

## Cost Tracking (Sprint 6)

### Final Cost Summary

| Service | Monthly Cost (Before Optimization) | Monthly Cost (After Optimization) | Savings | Method |
|---------|-----------------------------------|-----------------------------------|---------|--------|
| EKS Compute | | | | |
| ALB | | | | |
| NAT Gateway | | | | |
| ECR | | | | |
| Storage (Prometheus) | | | | |
| Data Transfer | | | | |
| **Total** | | | | |

### Cumulative Project Cost
- **Sprint 1–2:** Infrastructure setup (~$15–$100)
- **Sprint 3–4:** Full deployment (~$170–$200/mo)
- **Sprint 5:** Monitoring added (~$163–$209/mo)
- **Sprint 6:** Optimization applied — final state

> 📌 **Document this in your viva!** The evaluator will specifically ask about cost optimization. Show numbers, not just concepts.

---

## Checklist for Project Completion

### Implementation (75%)
- [ ] All 39 tasks marked `Done` in GitHub Project
- [ ] All PRs merged to `develop` (and `main` if applicable)
- [ ] Feature branches deleted
- [ ] Application is live and accessible
- [ ] Jenkins pipeline is fully automated
- [ ] Terraform, Ansible, K8s, and monitoring configs are all in Git
- [ ] Chaos test evidence (screenshots/logs) is saved

### Documentation (15%)
- [ ] Architecture diagram and overview is complete
- [ ] Jenkins setup guide is complete
- [ ] Terraform module docs are complete
- [ ] Ansible playbook docs are complete
- [ ] K8s deployment docs are complete
- [ ] Monitoring and alerting guide is complete
- [ ] Disaster recovery runbook is complete
- [ ] All docs are in `/docs/` and linked from README.md

### Cost Optimization (10%)
- [ ] Infracost integration is working (Sprint 2)
- [ ] Graviton or right-sizing evidence is documented (Sprint 4)
- [ ] Final AWS Cost Explorer review is complete (Sprint 6)
- [ ] Before/after cost comparison is in `/docs/cost-analysis/`
- [ ] Cost savings are quantified with dollar amounts

### Presentation & Viva
- [ ] Presentation deck is complete (8–12 slides)
- [ ] Demo script is written and rehearsed
- [ ] Each team member knows their 3 primary talking points
- [ ] Mock viva completed with Q&A practice
- [ ] Backup plan ready (screenshots, video) if live demo fails

---

## Post-Project: Resource Cleanup (If Required)

- [ ] Delete EKS cluster: `terraform destroy -target=module.eks` (or full destroy)
- [ ] Delete Jenkins EC2 instance (or keep for future use)
- [ ] Delete S3 bucket contents (unless needed for portfolio)
- [ ] Delete DynamoDB table
- [ ] Delete ECR images
- [ ] Delete ALB and associated security groups
- [ ] Verify AWS Cost Explorer shows $0 or near-$0 after cleanup
- [ ] Export final project files (GitHub repo, docs, screenshots) to personal storage

---

*Last updated: [Date] by [Name]*  
*Project Status: ⬜ In Progress / ⬜ Completed / ⬜ Presented*
