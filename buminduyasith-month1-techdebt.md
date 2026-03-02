# Technical Debt Strategy

## Current Debt Inventory

### Critical (Must Address)
| Item | Impact | Effort | Risk if Ignored |
|------|--------|--------|-----------------|
| Monolith coupling | High | Large | Blocks expansion |
| Shared DB cross-domain tables | High | Large | Data residency and scaling limits |
| Legacy auth module | High | Medium | Security risk and audit failure |

### High Priority (Should Address)
| Item | Impact | Effort | Risk if Ignored |
|------|--------|--------|-----------------|
| Embedded payment logic | High | Medium | Slow compliance and change risk |
| Manual deployment steps | Medium | Medium | Release delays and errors |
| Weak observability | Medium | Medium | Slow incident response |

### Medium Priority (Could Address)
| Item | Impact | Effort | Risk if Ignored |
|------|--------|--------|-----------------|
| Inconsistent API contracts | Medium | Low | Client breakages |
| Limited caching strategy | Medium | Medium | Higher latency |
| Low test coverage in catalog | Medium | Medium | Regression risk |

### Low Priority (Won't Address Now)
| Item | Impact | Effort | Risk if Ignored | Justification |
|------|--------|--------|-----------------|---------------|
| Outdated UI components | Low | Medium | UX inconsistency | Not blocking growth goals |
| Legacy reporting scripts | Low | Low | Minor errors | Replace after B2B launch |

## Debt Categories

### Intentional Debt
- Fast delivery of Phase 1 modular refactor may leave some duplicated code.
- Payback plan: remove duplicates during Phase 2 hardening.

### Accidental Debt
- Cross-module dependencies grown over years without clear boundaries.
- Payback plan: map dependencies and enforce module ownership rules.

### Environmental Debt
- Framework versions nearing end-of-life.
- Payback plan: upgrade during Phase 3 when services are stable.

## Payback Strategy

### Approach
1. **20% Time Rule:** Each sprint uses 20% capacity for debt tasks.
2. **Strategic Refactoring:** Larger refactors planned between releases.
3. **Opportunistic:** Fix debt when touching nearby code.

### Prioritization Framework
Score = (Impact × Risk) / (Effort × Cost)

### Annual Debt Budget
- Q1: $150K (Critical items)
- Q2: $100K (High priority)
- Q3: $100K (Ongoing)
- Q4: $150K (Pre-expansion)

## Governance

### Debt Review Process
```mermaid
flowchart LR
  intake[New debt item] --> triage[Triage + scoring]
  triage --> plan[Add to backlog]
  plan --> sprint[Include in sprint 20% rule]
  sprint --> review[Monthly review]
  review --> close[Close or re-score]
```

### Metrics
| Metric | Current | Target |
|--------|---------|--------|
| Known debt items | 47 | <30 |
| Critical items | 8 | 0 |
| Debt ratio | 35% | <20% |

### Reporting
- Quarterly summary to business leadership.
- Monthly review with engineering leads.
- Highlight debt items that block market expansion or compliance.
