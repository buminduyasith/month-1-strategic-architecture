# Technology Roadmap: 2026-2028

## Strategic Objectives

1. Enable international expansion (5 markets)
2. Launch B2B wholesale platform
3. Scale to 10M users and $200M revenue
4. Improve development velocity through controlled architectural evolution

---

## Current System (2026 Baseline)

- Single-region monolithic application
- Shared relational database
- Tightly coupled modules (Orders, Catalog, Payments, Users)
- Limited observability
- Manual scaling (mostly vertical)
- No B2B capability
- External payment integrations embedded inside monolith
- No regional data isolation

**Current Limitations**

- High regression risk when releasing features
- Difficult to scale specific domains independently
- Hard to expand internationally
- Deployment bottlenecks

---

## Roadmap Overview

### Phase 1: Foundation – Modular Monolith (Q1-Q2 2026)

**Theme:** Break Legacy Complexity

| Initiative                                                                | Dependencies      | Team Size | Investment |
| ------------------------------------------------------------------------- | ----------------- | --------- | ---------- |
| Refactor to Modular Monolith (Orders, Catalog, Inventory, Auth, B2B Core) | Existing Monolith | 10        | $400K      |
| Bug Backlog Reduction (40%)                                               | Existing Codebase | 8         | Included   |
| Monitoring & Observability Setup                                          | None              | 4         | $120K      |
| CI/CD Pipeline Improvement                                                | None              | 3         | $100K      |

**Exit Criteria:**

- [ ] Clear internal domain boundaries established
- [ ] 40% critical bug reduction
- [ ] Deployment frequency improved 1.5x
- [ ] Performance dashboards active

---

### Phase 2: B2B & International MVP (Q3-Q4 2026)

**Theme:** Revenue Expansion

| Initiative                                              | Dependencies     | Team Size | Investment |
| ------------------------------------------------------- | ---------------- | --------- | ---------- |
| B2B Core Features (Company accounts, bulk pricing, MOQ) | Modular Refactor | 10        | $400K      |
| Localization & Multi-currency                           | Modular Refactor | 6         | $250K      |
| Tax & Regional Pricing Engine                           | Localization     | 5         | $200K      |
| Disaster Recovery (RTO < 4h)                            | Monitoring       | 4         | $120K      |

**Exit Criteria:**

- [ ] First international market live
- [ ] 10+ B2B customers onboarded
- [ ] Multi-currency checkout operational
- [ ] DR drill successfully completed

---

### Phase 3: Selective Service Extraction (Q1-Q2 2027)

**Theme:** Controlled Microservice Adoption

| Initiative                              | Dependencies       | Team Size | Investment |
| --------------------------------------- | ------------------ | --------- | ---------- |
| Extract B2B as Independent Service      | Stable B2B Module  | 8         | $300K      |
| Introduce API Gateway                   | Service Extraction | 4         | $150K      |
| Separate B2B Database                   | B2B Extraction     | 4         | $100K      |
| Event Bus (Kafka/SNS) for domain events | Modular Refactor   | 4         | $150K      |
| Read Replicas & Caching (Redis/CDN)     | Monitoring         | 6         | $200K      |
| Regional Deployment (3 Markets Total)   | Localization       | 8         | $350K      |

**Exit Criteria:**

- [ ] B2B running as independent deployable service
- [ ] B2B using its own database
- [ ] 3 markets active
- [ ] P95 latency < 300ms at projected load
- [ ] B2B contributing 15% revenue

---

### Phase 4: Microservice Maturity & Security Hardening (Q3-Q4 2027 – 2028)

**Theme:** Global Scale & Compliance

| Initiative                                     | Dependencies         | Team Size | Investment |
| ---------------------------------------------- | -------------------- | --------- | ---------- |
| Extract Auth as Independent Service            | API Gateway          | 6         | $250K      |
| Separate Auth Database                         | Auth Extraction      | 3         | $80K       |
| Hire Security Lead                             | None                 | 1         | $180K      |
| External Security Audit (Pen Test + SAST/DAST) | Service Architecture | Shared    | $200K      |
| GDPR & Data Residency Controls                 | Regional Deployment  | 6         | $250K      |
| Load Testing for 10M MAU                       | Service Scaling      | 6         | $200K      |

**Exit Criteria:**

- [ ] 5 international markets active
- [ ] Core DB, B2B DB, Auth DB fully isolated
- [ ] 10M MAU supported
- [ ] 99.9% uptime maintained
- [ ] Zero critical vulnerabilities post-audit
- [ ] $200M annual revenue run rate achieved

---

## Dependencies and Risks

| Risk                                  | Probability | Impact | Mitigation                           |
| ------------------------------------- | ----------- | ------ | ------------------------------------ |
| Learning curve for service extraction | Medium      | Medium | Modular foundation before extraction |
| Over-fragmentation of services        | Medium      | High   | Extract only high-impact domains     |
| Regulatory non-compliance             | Medium      | High   | Security lead + external audit       |
| Infrastructure cost growth            | Medium      | Medium | Incremental scaling approach         |
| Cross-service data coupling           | Medium      | Medium | Strict database per-domain policy    |

---

## Resource Plan

### Team Structure Evolution

- Core Retail Squad (Core Commerce)
- B2B Squad (Owns B2B Service + DB)
- Platform Squad (API Gateway, infra, scaling)
- Security Lead (Compliance & audits)

### Skills Requirements

- Domain-driven design
- Distributed systems fundamentals
- Cloud scaling & regional deployments
- Security & compliance expertise

### Hiring Plan

- 2026: 6–8 Engineers (Backend, Fullstack, DevOps)
- 2027: 5 Engineers (service extraction & scaling)
- Late 2027: 1 Security Lead
- External security firm engagement in Phase 4

---

## Success Metrics

| Milestone        | Metric                   | Target           |
| ---------------- | ------------------------ | ---------------- |
| Phase 1 Complete | Deployment Frequency     | 1.5x baseline    |
| Phase 2 Complete | B2B Revenue              | 5% total revenue |
| Phase 3 Complete | Markets                  | 3 live           |
| Phase 4 Complete | MAU                      | 10M              |
| Revenue Goal     | Annual Revenue           | $200M            |
| Reliability      | Uptime                   | 99.9%            |
| Security         | Critical Vulnerabilities | 0 unresolved     |
