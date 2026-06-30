# Sprint 2: Immutable Infrastructure with Terraform

**Sprint Dates:** [Start Date + 14 days] – [Start Date + 28 days]  
**Sprint Goal:** Automate AWS infrastructure provisioning through Jenkins and Terraform, enabling reproducible environments.  
**Team Capacity:** 100 hours (5 members × 20 hours each)  
**Status:** ⬜ Not Started / 🟡 In Progress / 🟢 Completed

---

## Sprint Backlog

| Task ID | Issue # | Task Title | Assignee | Component | Pillar | Priority | Effort (hrs) | Status | Notes |
|---------|---------|------------|----------|-----------|--------|----------|--------------|--------|-------|
| 2.1 | # | Write Terraform modules for networking (VPC, Public/Private Subnets, NAT Gateway) | Infrastructure Lead | Infrastructure (Terraform) | Implementation (75%) | High | 8 | ⬜ | Blocks all infra tasks |
| 2.2 | # | Write Terraform scripts for managed AWS EKS cluster and Node Groups | Infrastructure Lead | Infrastructure (Terraform) | Implementation (75%) | High | 8 | ⬜ | Depends on 2.1 |
| 2.3 | # | Configure remote state management using AWS S3 Bucket and DynamoDB for state locking | Infrastructure Lead | Infrastructure (Terraform) | Implementation (75%) | High | 4 | ⬜ | Should be done before 2.1/2.2 apply |
| 2.4 | # | Implement Jenkins pipeline job to run terraform plan/apply automatically on Git PR merge | Config & Automation Lead | CI/CD (Jenkins) | Implementation (75%) | High | 6 | ⬜ | Needs Jenkins + Terraform ready |
| 2.5 | # | [Cost Optimization] Integrate Infracost into the Terraform Jenkins pipeline to estimate costs before provisioning | Infrastructure Lead | Infrastructure (Terraform) | Cost Optimization (10%) | Medium | 4 | ⬜ | Infracost API key needed |
| 2.6 | # | Document Terraform module usage and state management procedures | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | Medium | 3 | ⬜ | Depends on 2.1–2.3 |

---

## Sprint Goal Breakdown

### What "Done" Looks Like for Sprint 2
- [ ] Terraform `plan` runs successfully from local machine and Jenkins
- [ ] VPC with public/private subnets across 2 AZs exists in AWS
- [ ] EKS cluster is created with managed node groups
- [ ] S3 bucket + DynamoDB table exist for remote state (no local `.tfstate` files)
- [ ] Jenkins pipeline automatically triggers `terraform plan` on PRs and `apply` on merge
- [ ] Infracost runs in the pipeline and posts cost estimates as PR comments or logs
- [ ] Terraform documentation is complete with module diagrams and variable descriptions
- [ ] All code is reviewed and merged to `develop`

---

## Dependencies & Risks

### Internal Dependencies
```
Task 2.3 (Remote state) → Task 2.1 (VPC module) → Task 2.2 (EKS cluster)
                                      ↓
                              Task 2.4 (Jenkins pipeline)
                                      ↓
                              Task 2.5 (Infracost integration)
```

### External Dependencies
- Sprint 1 completion (Jenkins running, repo initialized, architecture finalized)
- AWS account with sufficient service limits (EKS clusters, VPCs per region)
- Infracost API key (free for open source / academic use — apply at infracost.io)

### Risk Register
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Terraform state lock conflicts | Medium | High | DynamoDB state locking configured in 2.3; always run via Jenkins, never local `apply` |
| AWS EKS cluster creation fails | Medium | High | Verify IAM permissions; use `aws eks` CLI to debug; keep CloudTrail logs enabled |
| Infracost API rate limits | Low | Medium | Cache API responses; run cost check only on PRs, not every commit |
| NAT Gateway costs surprise | Medium | High | Infracost catches this in 2.5; default to single NATGW for dev, discuss HA for prod |
| Terraform module syntax errors | High | Low | Run `terraform validate` in pre-commit hook; Jenkins runs it before plan |

---

## Sprint Review (To be completed at sprint end)

**Date:** [Fill in]  
**Attendees:** [All 5 team members]  
**Demoed:**
- [ ] `terraform plan` output from Jenkins console
- [ ] AWS Console showing VPC, subnets, EKS cluster
- [ ] S3 bucket containing `.tfstate` file
- [ ] Infracost cost estimate output (if 2.5 completed)
- [ ] PR merge triggering Jenkins pipeline automatically

**Feedback from team:**
> [Write feedback here]

**Sprint Goal Achieved?** ⬜ Yes / ⬜ Partially / ⬜ No

---

## Sprint Retrospective (To be completed at sprint end)

**What went well?**
> [Fill in]

**What could be improved?**
> [Fill in]

**Action items for Sprint 3:**
- [ ] [Action item 1, owner, due date]
- [ ] [Action item 2, owner, due date]

**Velocity:** [X] story points / hours completed out of 100 planned

---

## Key Decisions Log

| Date | Decision | Made By | Rationale | Impact |
|------|----------|---------|-----------|--------|
| | Terraform version pinned | | | Reproducibility across team |
| | Single NAT Gateway vs. per-AZ | | | Cost vs. availability tradeoff |
| | EKS managed vs. unmanaged node groups | | | Complexity vs. control |
| | State file encryption method | | | Security compliance |

---

## Cost Tracking (Sprint 2)

| Service | Resource | Estimated Monthly Cost | Sprint 2 Actual | Infracost Estimate | Variance |
|---------|----------|------------------------|-----------------|-------------------|----------|
| VPC | NAT Gateway | ~$32/mo | | | |
| EKS | Cluster control plane | ~$73/mo | | | |
| EKS | Node group (t3.medium × 2) | ~$60/mo | | | |
| S3 | State storage | ~$0.50/mo | | | |
| DynamoDB | State locking | ~$0 | | | On-demand pricing |
| Data transfer | NAT Gateway egress | ~$5/mo | | | |

**Total Sprint 2 AWS Cost Estimate:** ~$85–$100 (prorated 2 weeks + ongoing infra)

> 📌 Note: Infrastructure created in Sprint 2 persists into Sprints 3–6. Track cumulative running costs. Use Infracost output (Task 2.5) to validate estimates.

---

## Checklist for Moving to Sprint 3

- [ ] All Sprint 2 issues marked `Done`
- [ ] Terraform code merged to `develop`
- [ ] `terraform plan` runs clean in Jenkins with zero errors
- [ ] AWS infrastructure verified in console (VPC, EKS, S3, DynamoDB)
- [ ] Infracost cost estimate captured and saved to `/docs/cost-analysis/`
- [ ] Terraform documentation reviewed and merged
- [ ] Sprint 3 planning completed — Ansible playbook scope clarified
- [ ] Sprint 3 tasks created, assigned, and in `Todo` status

---

*Last updated: [Date] by [Name]*
