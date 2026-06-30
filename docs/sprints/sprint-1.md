# Sprint 1: Foundational Architecture & CI/CD Bootstrap

**Sprint Dates:** [Start Date] – [End Date + 14 days]  
**Sprint Goal:** Complete the application architecture, Dockerize the application, and establish a Jenkins server for CI/CD.  
**Team Capacity:** 100 hours (5 members × 20 hours each)  
**Status:** 🟡 In Progress / ⬜ Not Started / 🟢 Completed

---

## Sprint Backlog

| Task ID | Issue # | Task Title | Assignee | Component | Pillar | Priority | Effort (hrs) | Status | Notes |
|---------|---------|------------|----------|-----------|--------|----------|--------------|--------|-------|
| 1.1 | # | Design end-to-end AWS EKS architecture diagram (VPC, Subnets, EKS, ALB) | Tech Lead | Architecture/Docs | Implementation (75%) | High | 4 | ⬜ | Blocks 1.2, 2.1, 2.2 |
| 1.2 | # | Dockerize web application & create optimized multi-stage Dockerfile | App & K8s Lead | CI/CD (Jenkins) | Implementation (75%) | High | 6 | ⬜ | Needs architecture diagram first |
| 1.3 | # | Provision Jenkins server on AWS EC2 & install Docker, AWS CLI, Kubernetes plugins | Config & Automation Lead | CI/CD (Jenkins) | Implementation (75%) | High | 6 | ⬜ | Needs architecture diagram |
| 1.4 | # | Configure IAM Roles for Service Accounts (IRSA) for Jenkins-to-AWS/EKS secure authentication | Infrastructure Lead | Infrastructure (Terraform) | Implementation (75%) | High | 4 | ⬜ | Depends on 1.1 and 1.3 |
| 1.5 | # | Initialize Git repository with folder structure and branch protection rules | Tech Lead | Architecture/Docs | Documentation (15%) | Medium | 2 | ⬜ | Should be done first |
| 1.6 | # | Document Sprint 1 architecture decisions and setup guide | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | Medium | 3 | ⬜ | Depends on 1.1 and 1.5 |

---

## Sprint Goal Breakdown

### What "Done" Looks Like for Sprint 1
- [ ] Architecture diagram is reviewed by all team members and stored in `/docs/architecture/`
- [ ] Jenkins EC2 instance is running and accessible via web UI
- [ ] Docker image builds successfully locally and is < 200 MB (if optimized multi-stage)
- [ ] Git repository has branch protection on `main` and `develop`, all 5 members have access
- [ ] IRSA trust policy is configured for Jenkins to assume EKS role
- [ ] Sprint 1 documentation is complete and peer-reviewed

---

## Dependencies & Risks

### Internal Dependencies
```
Task 1.5 (Repo setup) → Task 1.1 (Architecture) → Task 1.2 (Dockerize)
                                    ↓
                            Task 1.3 (Jenkins EC2)
                                    ↓
                            Task 1.4 (IRSA config)
```

### Risk Register
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| AWS free tier limits exceeded | Medium | High | Use t2.micro/t3.micro where possible; set up billing alerts immediately |
| Jenkins plugin compatibility issues | Medium | Medium | Pin plugin versions in setup script; test in local Docker first |
| Team member AWS account access delay | Low | High | Share one AWS account with IAM users; have backup credentials ready |
| Architecture diagram disagreements | Medium | Low | Schedule 1-hour alignment meeting within first 3 days |

---

## Sprint Review (To be completed at sprint end)

**Date:** [Fill in]  
**Attendees:** [All 5 team members]  
**Demoed:**
- [ ] Architecture diagram walkthrough
- [ ] Jenkins server live URL
- [ ] Docker build command and image size
- [ ] Git repo structure + branch protection demo

**Feedback from team:**
> [Write feedback here]

**Sprint Goal Achieved?** ⬜ Yes / ⬜ Partially / ⬜ No

---

## Sprint Retrospective (To be completed at sprint end)

**What went well?**
> [Fill in]

**What could be improved?**
> [Fill in]

**Action items for Sprint 2:**
- [ ] [Action item 1, owner, due date]
- [ ] [Action item 2, owner, due date]

**Velocity:** [X] story points / hours completed out of 100 planned

---

## Key Decisions Log

| Date | Decision | Made By | Rationale | Impact |
|------|----------|---------|-----------|--------|
| | AWS region chosen | | | Affects all infrastructure |
| | Jenkins vs. GitHub Actions | | | Affects CI/CD pipeline design |
| | Web app language/framework | | | Affects Dockerfile and K8s manifests |
| | AWS account sharing model | | | Security and access control |

---

## Cost Tracking (Sprint 1)

| Service | Instance Type | Estimated Monthly Cost | Sprint 1 Actual | Notes |
|---------|---------------|------------------------|-----------------|-------|
| Jenkins EC2 | t3.medium | ~$30 | | 2-week sprint prorated |
| ECR storage | | ~$0 | | No images yet |
| Data transfer | | ~$0 | | Minimal |

**Total Sprint 1 AWS Cost Estimate:** ~$15 (prorated 2 weeks)

> 📌 Remember: Infracost integration starts in Sprint 2. For Sprint 1, track costs manually in this table.

---

## Checklist for Moving to Sprint 2

- [ ] All Sprint 1 issues marked `Done` (not just closed)
- [ ] All PRs merged to `develop` via squash merge
- [ ] Feature branches deleted
- [ ] Sprint 1 documentation peer-reviewed
- [ ] Architecture diagram signed off by Tech Lead
- [ ] Jenkins EC2 is accessible and documented
- [ ] Cost tracker updated with actuals
- [ ] Sprint 2 planning meeting completed
- [ ] Sprint 2 tasks are created as Issues and assigned

---

*Last updated: [Date] by [Name]*
