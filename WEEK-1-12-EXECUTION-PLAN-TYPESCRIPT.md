# Week 1-12 Execution Plan (Single Consolidated)
Last Updated: April 26, 2026
Time Budget: 15 hours/week
Track Focus: Backend SWE (TypeScript, Node.js, PostgreSQL)

---

## How to Use This File
- Use this as the single source of truth for the full 12-week program.
- Execute checklist items Monday-Sunday.
- Keep one weekly scorecard entry per week.
- Use Spec-Driven Development + TDD on every feature.

### Weekly Template Workflow
- At the start of each feature, copy [FEATURE-SPEC-TEMPLATE.md](FEATURE-SPEC-TEMPLATE.md) and fill it.
- Before coding, copy [TEST-PLAN-TEMPLATE.md](TEST-PLAN-TEMPLATE.md) and define failing tests first.
- Track completion using the Spec/TDD fields in the scorecard.
- Keep spec and test files next to related feature artifacts.

---

## Unified Weekly Operating Rhythm (Weeks 1-12)

### Monday to Friday (about 12 hours)
- Build/interview core work: 7 hours
- DSA/system design/fundamentals: 3 hours
- Applications + follow-up: 1.5 hours
- Networking or cleanup: 0.5 hours

### Saturday to Sunday (about 3 hours)
- Quality/polish pass: 1 hour
- Mock or rehearsal: 1 hour
- Retrospective + next-week plan: 1 hour

---

## Spec-Driven + TDD Operating Model
1. Write a short feature spec before implementation.
2. Define acceptance criteria, failure cases, and constraints.
3. Write failing tests from the spec first.
4. Implement minimum code to pass.
5. Refactor with tests still green.
6. Mark done only when acceptance criteria map to passing tests.

---

## Weekly Scorecard Template

```markdown
## Week X Scorecard
- DSA problems completed:
- System design sessions:
- Applications submitted:
- Follow-ups sent:
- Networking outreaches:
- Recruiter screens:
- Technical interviews:
- Mock interviews:
- Project deliverables shipped:
- Commits this week:
- Test coverage (if applicable):
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Refactors completed with green tests:
- Biggest win:
- Biggest blocker:
- Top 3 priorities next week:
```

---

## Week 1: Foundation Reset
Goal: Re-establish development rhythm and public professional presence.

### Deliverables
- Project scaffold initialized
- CS fundamentals refresh
- 3 DSA problems solved
- Resume v1 drafted
- LinkedIn and GitHub refreshed
- Progress tracking created

### Checklist
- [ ] Initialize TypeScript + Node repo and baseline structure
- [ ] Add `.env.example` and initial README
- [ ] Review Big-O, DS, SQL and log notes
- [ ] Solve 3 easy DSA problems and document complexity
- [ ] Rewrite resume into role-focused v1
- [ ] Update LinkedIn and GitHub profile
- [ ] Create `PROGRESS.md` and DSA tracker

---

## Week 2: API Fundamentals and Auth
Goal: Build core backend API capability and begin targeted applications.

### Deliverables
- Express route structure + middleware
- Validation and centralized error handling
- JWT auth and password hashing
- Resume polish with current project context
- 5 targeted applications
- 2 additional DSA problems

### Checklist
- [ ] Build health endpoint and route organization
- [ ] Add validation middleware and error utilities
- [ ] Implement JWT auth flow and password hashing
- [ ] Write mini specs for auth and validation features
- [ ] Apply red-green-refactor loop for auth/middleware tests
- [ ] Submit first 5 targeted applications
- [ ] Solve 2 medium DSA problems

---

## Week 3: Database, CRUD, and Test Coverage
Goal: Move from API shell to production-style backend behavior.

### Deliverables
- Prisma schema + migrations
- Full CRUD for core resource
- Unit/integration tests
- Coverage baseline 70%+
- 4 additional DSA problems
- 5 additional applications

### Checklist
- [ ] Define schema and run migration
- [ ] Implement CRUD endpoints with ownership checks
- [ ] Add Jest + Supertest integration tests
- [ ] Write endpoint specs before implementation
- [ ] Keep all CRUD work in red-green-refactor cycles
- [ ] Validate coverage and fix critical test gaps
- [ ] Submit 5 applications and run one system design drill

---

## Week 4: Deploy, CI/CD, and Launch
Goal: Ship Project 1 publicly as a strong hiring signal.

### Deliverables
- CI pipeline for lint/test/build
- Production deployment live
- README + architecture docs
- Technical post published
- 10 additional applications
- 4 additional DSA problems

### Checklist
- [ ] Configure GitHub Actions pipeline
- [ ] Deploy and verify `/health` endpoint
- [ ] Finalize docs and changelog
- [ ] Add contract tests for success/failure API responses
- [ ] Publish one technical write-up
- [ ] Tag v1.0.0 and pin project
- [ ] Submit 10 targeted applications

---

## Week 5: Project 2 Foundation
Goal: Define and scaffold Project 2 with strong architecture.

### Deliverables
- Project 2 scope/MVP finalized
- Schema + architecture doc complete
- Base repo scaffolded with CI/test setup
- First core services/endpoints live
- 3 DSA problems
- 5 targeted applications

### Checklist
- [ ] Pick Project 2 domain and define MVP
- [ ] Create schema with meaningful relationships
- [ ] Write specs for first two core endpoints
- [ ] Implement business services and baseline integration tests
- [ ] Run red-green-refactor for each core endpoint
- [ ] Submit 5 targeted roles

---

## Week 6: Advanced Features
Goal: Add depth through caching, async processing, and payment/promo logic.

### Deliverables
- Redis caching
- Async queue/jobs
- Payment (mock) and promo logic
- Admin/analytics endpoint
- 4 DSA problems
- 5 applications + 5 networking outreaches

### Checklist
- [ ] Implement cache strategy and invalidation points
- [ ] Add background jobs for non-blocking workflows
- [ ] Implement payment success/failure states
- [ ] Implement promo validation and usage constraints
- [ ] Spec and test failure paths (cache/queue/payment)
- [ ] Run full test/lint quality pass
- [ ] Submit 5 applications and send 5 outreaches

---

## Week 7: Observability and Performance
Goal: Make Project 2 production-ready with reliability and tuning.

### Deliverables
- Structured logging + centralized error schema
- Query optimization and indexes
- Rate limiting and security hardening
- 3 DSA problems
- 8-10 high-quality applications

### Checklist
- [ ] Add request/response logging with context
- [ ] Standardize error schema and failure codes
- [ ] Fix N+1/high-latency query paths
- [ ] Add/validate database indexes
- [ ] Add rate limiting and harden CORS/headers
- [ ] Add contract tests for standardized error responses
- [ ] Submit 8-10 targeted applications

---

## Week 8: Project 2 Launch and Interview Transition
Goal: Ship Project 2 publicly and shift into interview mode.

### Deliverables
- Project 2 deployed with CI/CD
- Strong README + architecture notes
- Technical post published
- Interview prep kit created
- 6 DSA problems (reach 40 cumulative)
- 10-15 applications

### Checklist
- [ ] Deploy and verify production health checks
- [ ] Finalize docs (README/API/architecture/changelog)
- [ ] Publish one technical post on tradeoffs
- [ ] Build interview assets (intro, demo script, STAR)
- [ ] Map interview points to spec decisions and test evidence
- [ ] Complete 6 DSA problems and submit 10-15 applications

---

## Week 9: Interview System Build
Goal: Establish repeatable mock interview workflow.

### Deliverables
- 3 mocks (DSA/behavioral/system design)
- Interview Q&A bank finalized
- 5 targeted applications
- 5 outreach follow-ups

### Checklist
- [ ] Run timed DSA mock and review mistakes
- [ ] Run behavioral mock and tighten STAR answers
- [ ] Run system design mock with fixed framework
- [ ] Finalize 30-second intro and gap narrative
- [ ] Submit 5 applications with same-day outreach

---

## Week 10: Conversion Optimization
Goal: Improve pass-through from recruiter screen to technical round.

### Deliverables
- 2 additional mocks
- Resume/LinkedIn tuned to active role keywords
- Follow-up system running on 7-day cadence
- 4-5 high-quality applications

### Checklist
- [ ] Tune resume bullets with measurable impact
- [ ] Run DSA mock on weakest topic
- [ ] Run project deep-dive mock
- [ ] Send due follow-ups/second touches
- [ ] Submit 4-5 highly relevant roles

---

## Week 11: Final Round Readiness
Goal: Reduce interview variance and improve offer odds.

### Deliverables
- 3 mocks (design/behavioral/full-loop)
- Negotiation and decision prep sheet
- 3-4 referral-led applications
- Final portfolio polish

### Checklist
- [ ] Run advanced system design mock
- [ ] Run behavioral mock on ownership/prioritization
- [ ] Run full-loop mock session
- [ ] Prepare compensation/decision matrix
- [ ] Ask warm contacts for referrals
- [ ] Final polish pass on both project repos

---

## Week 12: Offer Conversion and Continuation Plan
Goal: Close active opportunities and lock next 90-day operating system.

### Deliverables
- Pipeline triaged (hot/warm/cold)
- Follow-up/thank-you process executed
- Offer decision framework ready
- 2-3 precision applications
- Post-Week-12 plan documented

### Checklist
- [ ] Prioritize active opportunities and remove low-fit distractions
- [ ] Prepare company-specific interview notes/questions
- [ ] Send same-day thank-you notes after interviews
- [ ] Submit 2-3 top-fit roles only
- [ ] Finalize negotiation and acceptance templates
- [ ] Write next 30/60/90 day plan

---

## Cumulative Targets by End of Week 12
- 2 deployed projects, demo-ready
- 40+ DSA problems completed/reviewed
- 60+ targeted applications total
- 8 mock interviews completed
- 20+ warm networking connections
- Active interview funnel with weekly conversion tracking

---

## If No Offer by End of Week 12
- Continue in 4-week sprints with this same rhythm.
- Add one credibility lever:
  - Open-source contributions (20+ commits/month)
  - One specialization track (cloud/data/security/distributed systems)
  - One additional advanced project
- Keep referral-first strategy active.
