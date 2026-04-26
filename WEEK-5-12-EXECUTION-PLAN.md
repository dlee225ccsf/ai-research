# Week 5-12 Execution Plan (Consolidated)
Last Updated: April 26, 2026
Time Budget: 15 hours/week
Track Focus: Backend SWE (TypeScript, Node.js, PostgreSQL)

---

## How to Use This File
- Use this as the single source of truth for Weeks 5-12.
- Run the weekly checklist Monday-Sunday.
- Keep only one weekly scorecard entry per week.
- Do not duplicate planning in other files unless you are changing strategy.

### Weekly Template Workflow
- At the start of each feature, copy [FEATURE-SPEC-TEMPLATE.md](FEATURE-SPEC-TEMPLATE.md) and fill it.
- Before implementation, copy [TEST-PLAN-TEMPLATE.md](TEST-PLAN-TEMPLATE.md) and define red tests.
- Track completion in your weekly scorecard using the Spec/TDD checklist fields.
- Keep spec and test plan files next to related feature artifacts for interview-ready evidence.

---

## Unified Weekly Operating Rhythm (Weeks 5-12)

### Monday to Friday (about 12 hours)
- Project/Interview core work: 7 hours
- DSA/system design practice: 3 hours
- Applications and follow-up: 1.5 hours
- Networking: 0.5 hours

### Saturday to Sunday (about 3 hours)
- Polish and quality pass: 1 hour
- Mock or rehearsal: 1 hour
- Weekly retrospective and scorecard update: 1 hour

---

## Spec-Driven + TDD Operating Model
Use this for every feature and every interview-facing project change.

1. Write a small feature spec before implementation.
2. List acceptance criteria, edge cases, and failure behavior.
3. Write tests first (unit, integration, or contract) from the criteria.
4. Implement minimum code to pass.
5. Refactor while tests stay green.
6. Merge only when tests cover acceptance criteria.

### Feature Spec Template

```markdown
## Feature: <name>
- Problem:
- User story:
- API contract:
  - Endpoint:
  - Request:
  - Success response:
  - Error responses:
- Validation rules:
- Authorization rules:
- Acceptance criteria:
  - [ ]
  - [ ]
- Non-functional targets:
  - p95 latency:
  - logging/observability:
  - fallback behavior:
```

### Weekly Spec/TDD Checklist

```markdown
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Refactors completed with green tests:
```

---

## Weekly Scorecard Template
Copy this block once per week into your tracker.

```markdown
## Week X Scorecard
- Applications submitted:
- Follow-ups sent:
- Networking outreaches:
- Recruiter screens:
- Technical interviews:
- Mock interviews:
- DSA problems completed:
- System design sessions:
- Project deliverables shipped:
- Biggest win:
- Biggest blocker:
- Top 3 priorities next week:
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Refactors completed with green tests:
```

---

## Week 5: Project 2 Foundation
Goal: Define and scaffold Project 2 with strong architecture and core domain model.

### Deliverables
- Project 2 scope and MVP finalized
- Database schema and architecture doc complete
- Base repo scaffolded with CI, test setup, and environment config
- First core services/endpoints live
- 3 DSA problems solved
- 5 targeted applications submitted

### Checklist
- [ ] Pick Project 2 domain (ticketing, booking, or similar)
- [ ] Write MVP scope and non-goals
- [ ] Create Prisma schema with meaningful relationships
- [ ] Write feature specs for first two core endpoints before coding
- [ ] Implement first business services (inventory/order flow)
- [ ] Add baseline integration tests
- [ ] Run red-green-refactor loop for each core endpoint
- [ ] Submit 5 targeted roles and log follow-up dates
- [ ] Run one system design drill: "Project 2 at 10x scale"

---

## Week 6: Advanced Features
Goal: Add depth through caching, async processing, and payment/promo logic.

### Deliverables
- Redis caching layer for hot reads
- Queue-based async job flow (email/notifications)
- Payment flow (mock) and promo code handling
- Admin or analytics endpoints
- 4 DSA problems solved
- 5 more targeted applications submitted
- 5 networking outreaches sent

### Checklist
- [ ] Add cache strategy and cache invalidation points
- [ ] Add background jobs for non-blocking operations
- [ ] Implement payment success/failure states
- [ ] Implement promo code validation and usage constraints
- [ ] Add admin stats endpoint (orders, revenue, usage)
- [ ] Spec and test key failure paths (cache miss, queue failure, payment failure)
- [ ] Run test and lint quality pass
- [ ] Submit 5 applications and send 5 outreach messages

---

## Week 7: Observability and Performance
Goal: Make Project 2 production-ready with logging, reliability, and performance tuning.

### Deliverables
- Structured logging and centralized error handling
- Query optimization and index improvements
- Rate limiting and security hardening
- Improved API reliability under load
- 3 DSA problems solved
- 8 to 10 high-quality applications submitted

### Checklist
- [ ] Add request/response logging with context
- [ ] Standardize error schema and failure codes
- [ ] Fix N+1 and high-latency query paths
- [ ] Add key indexes and validate query performance
- [ ] Add rate limiting on auth and checkout-like endpoints
- [ ] Harden CORS and headers
- [ ] Add contract tests for standardized error response shapes
- [ ] Submit 8 to 10 targeted applications

---

## Week 8: Project 2 Launch and Interview Transition
Goal: Ship Project 2 publicly and shift into interview-heavy mode.

### Deliverables
- Project 2 deployed with CI/CD
- Strong README and architecture notes
- Technical write-up/post published
- Interview prep kit created
- 6 DSA problems solved (reach 40 cumulative)
- 10 to 15 applications submitted

### Checklist
- [ ] Deploy Project 2 and verify production health endpoints
- [ ] Finalize docs (README, API, architecture, changelog)
- [ ] Publish one technical post about design tradeoffs
- [ ] Create interview assets: intro, project demos, STAR stories
- [ ] Map top interview talking points to spec decisions and test evidence
- [ ] Complete 6 DSA problems to hit target pace
- [ ] Send 10 to 15 applications

---

## Week 9: Interview System Build
Goal: Establish repeatable mock-interview and response workflow.

### Deliverables
- 3 mocks completed (DSA, behavioral, system design)
- Interview Q&A bank and pitch narrative finalized
- 5 targeted applications submitted
- 5 outreach follow-ups sent

### Checklist
- [ ] Run one timed DSA mock and review mistakes
- [ ] Run one behavioral mock and tighten STAR answers
- [ ] Run one system design mock with a fixed framework
- [ ] Finalize 30-second intro and gap narrative
- [ ] Submit 5 applications with same-day outreach
- [ ] Prepare 5-minute demo script for each project

---

## Week 10: Conversion Optimization
Goal: Improve pass-through rate from recruiter screen to technical round.

### Deliverables
- 2 more mocks completed
- Resume and LinkedIn tuned to active role keywords
- Follow-up engine operating on 7-day cadence
- 4 to 5 quality applications submitted

### Checklist
- [ ] Tune resume bullets with measured impact
- [ ] Run DSA mock on weakest topic
- [ ] Run project deep-dive mock with tradeoff discussion
- [ ] Send all due follow-ups and second-touch messages
- [ ] Submit 4 to 5 highly relevant roles

---

## Week 11: Final Round Readiness
Goal: Reduce interview variance and improve offer probability.

### Deliverables
- 3 mocks completed (design, behavioral, full-loop)
- Offer evaluation and negotiation prep sheet done
- 3 to 4 referral-led applications submitted
- Final portfolio polish pass completed

### Checklist
- [ ] Run advanced system design mock with reliability focus
- [ ] Run behavioral mock on ownership/prioritization themes
- [ ] Run full-loop mock (behavioral + coding + design)
- [ ] Prepare compensation and decision matrix
- [ ] Ask warm contacts directly for referrals
- [ ] Final polish on both project repos

---

## Week 12: Offer Conversion and Continuation Plan
Goal: Close active opportunities and lock in the next 90-day operating system.

### Deliverables
- Pipeline triaged (hot/warm/cold)
- Follow-up and thank-you protocol executed
- Offer decision framework ready
- 2 to 3 precision applications submitted
- Post-Week-12 plan documented

### Checklist
- [ ] Prioritize all active opportunities and remove low-fit distractions
- [ ] Prepare company-specific interview questions and prep notes
- [ ] Send same-day thank-you notes after interviews
- [ ] Submit 2 to 3 top-fit roles only
- [ ] Finalize negotiation and acceptance response templates
- [ ] Write next 30/60/90 day plan (offer or no-offer path)

---

## Cumulative Targets by End of Week 12
- 2 deployed projects, both demo-ready
- 40+ DSA problems completed and reviewed
- 60+ targeted applications total
- 8 mock interviews completed
- 20+ warm networking connections
- Active interview funnel with weekly conversion tracking

---

## If No Offer by End of Week 12
- Continue in 4-week sprints using this same rhythm.
- Add one credibility lever:
  - Open-source contributions (20+ commits/month)
  - One specialization track (cloud, data, security, or distributed systems)
  - One additional advanced project
- Keep referral-first job search strategy active.
