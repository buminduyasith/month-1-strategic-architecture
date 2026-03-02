# Build vs Buy Analysis

## Component 1: Payment Processing

### Options
1. **Build:** Custom payment gateway
2. **Buy:** Stripe, Adyen, or similar
3. **Hybrid:** Buy + custom orchestration

### Evaluation Matrix
| Criterion | Weight | Build | Buy | Hybrid |
|-----------|--------|-------|-----|--------|
| Time to market | 20% | 2/5 | 5/5 | 4/5 |
| Total cost (3yr) | 25% | 2/5 | 4/5 | 3/5 |
| Flexibility | 20% | 5/5 | 3/5 | 4/5 |
| Maintenance burden | 15% | 1/5 | 5/5 | 3/5 |
| Strategic value | 20% | 3/5 | 3/5 | 4/5 |
| **Weighted Score** | | **2.4** | **3.9** | **3.6** |

### Recommendation
**Buy (Stripe)** with a small orchestration layer for retries, routing, and audit logs.

### Rationale
Buying reduces time to market and compliance risk. The business needs international rollout fast, and payment regulations differ by market. A light orchestration layer keeps flexibility without owning full payment infrastructure.

### Implementation Plan
- Select a primary provider (Stripe) and configure multi-currency support.
- Build an internal payment orchestration service with clear APIs.
- Add monitoring and fraud hooks.

---

## Component 2: Multi-Region Database

### Options
1. **Build:** Self-managed multi-region Postgres
2. **Buy:** Managed global database (Aurora Global, Spanner)
3. **Hybrid:** Managed core + regional read replicas

### Evaluation Matrix
| Criterion | Weight | Build | Buy | Hybrid |
|-----------|--------|-------|-----|--------|
| Time to market | 20% | 2/5 | 4/5 | 4/5 |
| Total cost (3yr) | 25% | 3/5 | 3/5 | 4/5 |
| Flexibility | 20% | 4/5 | 3/5 | 4/5 |
| Maintenance burden | 15% | 2/5 | 5/5 | 3/5 |
| Strategic value | 20% | 3/5 | 3/5 | 4/5 |
| **Weighted Score** | | **2.9** | **3.6** | **3.9** |

### Recommendation
**Hybrid:** Managed core database with regional read replicas and data residency rules.

### Rationale
This balances cost and complexity. It supports early regional expansion and meets data residency needs without deep operational overhead.

### Implementation Plan
- Move core DB to a managed service.
- Add read replicas for first two regions.
- Introduce data residency policy and regional backup plans.

---

## Component 3: B2B Commerce Engine

### Options
1. **Build:** In-house B2B engine
2. **Buy:** SaaS B2B platform
3. **Hybrid:** Buy catalog/pricing, build order flow

### Evaluation Matrix
| Criterion | Weight | Build | Buy | Hybrid |
|-----------|--------|-------|-----|--------|
| Time to market | 20% | 3/5 | 4/5 | 4/5 |
| Total cost (3yr) | 25% | 3/5 | 2/5 | 3/5 |
| Flexibility | 20% | 5/5 | 2/5 | 4/5 |
| Maintenance burden | 15% | 2/5 | 4/5 | 3/5 |
| Strategic value | 20% | 5/5 | 2/5 | 4/5 |
| **Weighted Score** | | **3.8** | **2.8** | **3.7** |

### Recommendation
**Build** a focused B2B engine inside the modular monolith, then extract it as a service in Phase 3.

### Rationale
B2B pricing, MOQ, and account workflows are core differentiators. Building in-house fits the roadmap and keeps long-term flexibility.

### Implementation Plan
- Start as a bounded module in Phase 2 with separate domain models.
- Create APIs for account pricing and bulk ordering.
- Extract the module into a service with its own database in Phase 3.

---

## Summary Matrix
| Component | Decision | Investment | Timeline |
|-----------|----------|------------|----------|
| Payments | Buy | $50K/year | Q1 2026 |
| Database | Hybrid | $300K | Q2 2026 |
| B2B Engine | Build | $500K | Q3-Q4 2026 |
