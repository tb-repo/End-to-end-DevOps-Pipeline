# Sprint 4: Core Application Deployment (Kubernetes)

**Sprint Dates:** [Start Date + 42 days] – [Start Date + 56 days]  
**Sprint Goal:** Build a fully automated CI/CD pipeline that deploys the application to Kubernetes on AWS EKS.  
**Team Capacity:** 100 hours (5 members × 20 hours each)  
**Status:** ⬜ Not Started / 🟡 In Progress / 🟢 Completed

---

## Sprint Backlog

| Task ID | Issue # | Task Title | Assignee | Component | Pillar | Priority | Effort (hrs) | Status | Notes |
|---------|---------|------------|----------|-----------|--------|----------|--------------|--------|-------|
| 4.1 | # | Author Kubernetes manifests (Deployment, ClusterIP Service, Ingress) for the application | App & K8s Lead | Orchestration (K8s/EKS) | Implementation (75%) | High | 6 | ⬜ | Needs Docker image from Sprint 1 |
| 4.2 | # | Configure Kubernetes Horizontal Pod Autoscaler (HPA) and Liveness/Readiness probes | App & K8s Lead | Orchestration (K8s/EKS) | Implementation (75%) | High | 4 | ⬜ | Depends on 4.1 |
| 4.3 | # | Build multi-stage Jenkinsfile that builds Docker image, pushes to ECR, and executes kubectl apply | Config & Automation Lead | CI/CD (Jenkins) | Implementation (75%) | High | 8 | ⬜ | Needs ECR repo from Sprint 2 |
| 4.4 | # | Configure Kubernetes load balancing and auto-scaling in deployment pipeline | App & K8s Lead | Orchestration (K8s/EKS) | Implementation (75%) | High | 4 | ⬜ | Depends on 4.2 and 4.3 |
| 4.5 | # | Test end-to-end pipeline from code push to deployment on EKS | App & K8s Lead | CI/CD (Jenkins) | Implementation (75%) | High | 4 | ⬜ | Full integration test |
| 4.6 | # | Document Kubernetes deployment manifests and pipeline execution flow | Observability & Docs Lead | Architecture/Docs | Documentation (15%) | Medium | 3 | ⬜ | Depends on 4.1–4.5 |
| 4.7 | # | [Cost Optimization] Configure EKS cluster autoscaling with Graviton-based node groups where applicable | App & K8s Lead | Orchestration (K8s/EKS) | Cost Optimization (10%) | Medium | 4 | ⬜ | Graviton = 20% cheaper |

---

## Sprint Goal Breakdown

### What "Done" Looks Like for Sprint 4
- [ ] A code push to `develop` triggers the full Jenkins pipeline automatically
- [ ] Pipeline stages: Build → Push to ECR → Deploy to EKS → Verify
- [ ] Application is accessible via Ingress/ALB URL (even if just a health check endpoint)
- [ ] HPA is configured with min/max pod counts and CPU threshold
- [ ] Liveness and Readiness probes are configured and verified (pod restarts if unhealthy)
- [ ] EKS cluster autoscaling is configured (Cluster Autoscaler or Karpenter)
- [ ] (Optional) Graviton-based node groups are tested and cost savings documented
- [ ] K8s documentation is complete with manifest explanations and troubleshooting guide
- [ ] All code is reviewed and merged to `develop`

---

## Dependencies & Risks

### Internal Dependencies
```
Sprint 1 (Dockerfile) + Sprint 2 (EKS, ECR) + Sprint 3 (Jenkins pipeline) → Task 4.3 (Jenkinsfile)
                                                                                     ↓
                                                                              Task 4.1 (K8s manifests)
                                                                                     ↓
                                                                              Task 4.2 (HPA & probes)
                                                                                     ↓
                                                                              Task 4.4 (Load balancing)
                                                                                     ↓
                                                                              Task 4.5 (E2E test)
```

### Risk Register
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| kubectl from Jenkins can't reach EKS | High | High | Verify IRSA (Sprint 1 Task 1.4) and kubeconfig; test `kubectl get nodes` in Jenkins |
| ECR push fails due to IAM permissions | Medium | High | Ensure Jenkins IAM role has `ecr:GetAuthorizationToken` and `ecr:PutImage` |
| Ingress/ALB not routing traffic | Medium | High | Verify AWS Load Balancer Controller is installed; check security group rules |
| HPA not scaling | Medium | Medium | Install metrics-server in EKS; verify `kubectl top pods` works |
| Application crashes in container | Medium | High | Test Docker image locally first; verify port mapping and env vars |
| Graviton compatibility issues | Medium | Medium | Test application on arm64 locally first; use multi-arch builds if needed |
| Pipeline takes too long | Medium | Low | Use multi-stage Dockerfile; cache layers; use ECR build caching |

---

## Sprint Review (To be completed at sprint end)

**Date:** [Fill in]  
**Attendees:** [All 5 team members]  
**Demoed:**
- [ ] Push code to `develop` → Jenkins pipeline triggers automatically (live screen recording)
- [ ] Jenkins console showing green stages: Build → Push → Deploy
- [ ] `kubectl get pods` showing application pods running in EKS
- [ ] Application URL responding with HTTP 200 (health check)
- [ ] `kubectl get hpa` showing scaling configuration
- [ ] Liveness probe test: kill container → watch it restart automatically
- [ ] Cost comparison: Graviton vs. x86 (if 4.7 completed)

**Feedback from team:**
> [Write feedback here]

**Sprint Goal Achieved?** ⬜ Yes / ⬜ Partially / ⬜ No

---

## Sprint Retrospective (To be completed at sprint end)

**What went well?**
> [Fill in]

**What could be improved?**
> [Fill in]

**Action items for Sprint 5:**
- [ ] [Action item 1, owner, due date]
- [ ] [Action item 2, owner, due date]

**Velocity:** [X] story points / hours completed out of 100 planned

---

## Key Decisions Log

| Date | Decision | Made By | Rationale | Impact |
|------|----------|---------|-----------|--------|
| | Cluster Autoscaler vs. Karpenter | | | Complexity vs. efficiency |
| | ALB Ingress vs. NLB | | | Layer 7 routing vs. raw TCP |
| | Rolling update vs. blue/green | | | Simplicity vs. zero downtime |
| | HPA metrics (CPU vs. custom) | | | Generic vs. application-specific |
| | Graviton adoption scope | | | Cost savings vs. compatibility risk |

---

## Cost Tracking (Sprint 4)

| Service | Resource | Running Monthly Cost | Sprint 4 Changes | Infracost Estimate | Variance |
|---------|----------|---------------------|------------------|-------------------|----------|
| EKS | Cluster control plane | ~$73/mo | | | |
| EKS | Node group (current) | ~$133/mo | | | |
| EKS | Graviton nodes (if 4.7) | ~$106/mo | ~$27/mo savings | | |
| ECR | Image storage | ~$5/mo | | | |
| ALB | Load balancer | ~$22/mo | New | | |
| Data transfer | ALB + NAT GW | ~$15/mo | Increased | | |

**Total Sprint 4 AWS Cost Estimate:** ~$170–$200/mo ongoing (depends on ALB and node group choices)

> 📌 Note: This is the highest-cost sprint because ALB is added and EKS is fully utilized. Task 4.7 (Graviton) can reduce compute costs by ~20%. Document all costs carefully — this is your 10% optimization grade.

---

## Checklist for Moving to Sprint 5

- [ ] All Sprint 4 issues marked `Done`
- [ ] End-to-end pipeline tested and verified (code push → live app)
- [ ] Application is accessible via URL and responding
- [ ] HPA and probes verified working
- [ ] K8s documentation reviewed and merged
- [ ] Cost comparison (Graviton vs. x86) documented in `/docs/cost-analysis/` if Task 4.7 done
- [ ] Sprint 5 planning completed — monitoring stack scope clarified
- [ ] Sprint 5 tasks created, assigned, and in `Todo` status

---

*Last updated: [Date] by [Name]*
