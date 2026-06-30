# Sprint 3: Configuration Management Automation

**Sprint Dates:** [Start Date + 28 days] – [Start Date + 42 days]  
**Sprint Goal:** Automate configuration management with Ansible through Jenkins, ensuring consistent and reliable server configurations.  
**Team Capacity:** 100 hours (5 members × 20 hours each)  
**Status:** ⬜ Not Started / 🟡 In Progress / 🟢 Completed

---

## Sprint Backlog

| Task ID | Issue # | Task Title | Assignee | Component | Pillar | Priority | Effort (hrs) | Status | Notes |
|---------|---------|------------|----------|-----------|--------|----------|--------------|--------|-------|
| 3.1 | # | Write Ansible playbooks to provision/verify dependencies (kubectl, docker) on target EC2/worker hosts | Config & Automation Lead | Configuration (Ansible) | Implementation (75%) | High | 8 | ⬜ | Needs EC2 targets from Sprint 2 |
| 3.2 | # | Create automated Jenkins pipeline stage to invoke Ansible playbooks sequentially post-Terraform apply | Config & Automation Lead | Configuration (Ansible) | Implementation (75%) | High | 6 | ⬜ | Depends on 3.1 and 2.4 |
| 3.3 | # | Test Ansible playbooks on infrastructure provisioned by Terraform to validate configurations | Config & Automation Lead | Configuration (Ansible) | Implementation (75%) | High | 4 | ⬜ | Depends on 3.2 |
| 3.4 | # | Document Ansible playbook structure, inventory setup, and execution flow | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | Medium | 3 | ⬜ | Depends on 3.1–3.3 |
| 3.5 | # | [Cost Optimization] Review and optimize EC2 instance types in Ansible inventory for cost-efficiency | Infrastructure Lead | Configuration (Ansible) | Cost Optimization (10%) | Low | 3 | ⬜ | Optional: right-size instances |

---

## Sprint Goal Breakdown

### What "Done" Looks Like for Sprint 3
- [ ] Ansible playbook successfully installs Docker, kubectl, and AWS CLI on target EC2 instances
- [ ] Jenkins pipeline has a distinct stage that runs Ansible **after** Terraform completes
- [ ] Ansible inventory is dynamically generated or maintained in `/ansible/inventory/`
- [ ] Playbook execution is idempotent (running twice doesn't break anything)
- [ ] All playbooks are tested in the staging/dev environment created by Terraform
- [ ] Documentation covers playbook structure, inventory format, and how to add new hosts
- [ ] (Optional) Cost optimization review identifies cheaper instance types with no performance loss

---

## Dependencies & Risks

### Internal Dependencies
```
Sprint 2 complete (Terraform EC2, EKS, Jenkins pipeline) → Task 3.1 (Playbooks)
                                                                  ↓
                                                           Task 3.2 (Jenkins stage)
                                                                  ↓
                                                           Task 3.3 (Testing)
                                                                  ↓
                                                           Task 3.4 (Documentation)
```

### Risk Register
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Ansible SSH connection fails to EC2 | High | Medium | Ensure security groups allow SSH (port 22) from Jenkins IP; use AWS Systems Manager as fallback |
| Jenkins agent lacks Ansible | Medium | High | Install Ansible on Jenkins EC2 in Sprint 1; verify with `ansible --version` |
| Playbook not idempotent | Medium | Medium | Run playbook twice in test; second run should show 0 changes |
| Python version mismatch on targets | Medium | Medium | Pin Python version in playbook `vars`; use `ansible_python_interpreter` |
| Inventory file becomes outdated | Medium | Low | Generate inventory from Terraform output (`terraform output` → `inventory.ini`) |

---

## Sprint Review (To be completed at sprint end)

**Date:** [Fill in]  
**Attendees:** [All 5 team members]  
**Demoed:**
- [ ] Jenkins pipeline showing Terraform stage → Ansible stage sequence
- [ ] Ansible playbook output showing 0 failures
- [ ] Target EC2 instance with `docker --version` and `kubectl version` verified
- [ ] Documentation page for Ansible setup

**Feedback from team:**
> [Write feedback here]

**Sprint Goal Achieved?** ⬜ Yes / ⬜ Partially / ⬜ No

---

## Sprint Retrospective (To be completed at sprint end)

**What went well?**
> [Fill in]

**What could be improved?**
> [Fill in]

**Action items for Sprint 4:**
- [ ] [Action item 1, owner, due date]
- [ ] [Action item 2, owner, due date]

**Velocity:** [X] story points / hours completed out of 100 planned

---

## Key Decisions Log

| Date | Decision | Made By | Rationale | Impact |
|------|----------|---------|-----------|--------|
| | Ansible vs. cloud-init/user-data | | | Simplicity vs. AWS-native approach |
| | Dynamic vs. static inventory | | | Automation vs. simplicity |
| | Ansible playbook organization (one file vs. roles) | | | Maintainability |
| | SSH key management strategy | | | Security |

---

## Cost Tracking (Sprint 3)

| Service | Resource | Running Monthly Cost | Sprint 3 Changes | Infracost Estimate | Variance |
|---------|----------|---------------------|------------------|-------------------|----------|
| EC2 | Jenkins server | ~$15/mo | | | |
| EKS | Cluster + nodes | ~$133/mo | | | |
| VPC | NAT Gateway | ~$32/mo | | | |
| Ansible | No new resources | ~$0 | | | Tool runs on existing Jenkins |

**Total Sprint 3 AWS Cost Estimate:** No new infrastructure costs (~$0 incremental)

> 📌 Note: Sprint 3 is primarily configuration work on existing infrastructure. Main cost risk is if you provision new EC2 instances for Ansible testing. Use existing EKS worker nodes or Jenkins EC2 where possible.

---

## Checklist for Moving to Sprint 4

- [ ] All Sprint 3 issues marked `Done`
- [ ] Ansible playbooks merged to `develop`
- [ ] Jenkins pipeline runs Terraform → Ansible end-to-end with zero manual steps
- [ ] Target hosts verified (Docker, kubectl installed and running)
- [ ] Ansible documentation reviewed and merged
- [ ] Cost optimization review (Task 3.5) findings documented in `/docs/cost-analysis/`
- [ ] Sprint 4 planning completed — K8s deployment scope clarified
- [ ] Sprint 4 tasks created, assigned, and in `Todo` status

---

*Last updated: [Date] by [Name]*
