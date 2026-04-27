# Week 1-12 Execution Plan (Python Track)
Last Updated: April 26, 2026
Time Budget: 15 hours/week
Track Focus: Backend SWE with Python
Primary Stack: Python, FastAPI, PostgreSQL, pytest, Docker, GitHub Actions

---

## How to Use This File
- Use this as the single execution plan for the Python track.
- Follow Spec-Driven Development plus TDD for every feature.
- Keep one weekly scorecard entry each Sunday.

### Weekly Template Workflow
- Start each feature with FEATURE-SPEC-TEMPLATE.md.
- Define failing tests in TEST-PLAN-TEMPLATE.md before implementation.
- Implement using red-green-refactor loops.

---

## Weekly Rhythm (15 hours)
- Build and implementation: 7 hours
- DSA/system design/fundamentals: 3 hours
- Applications/follow-up: 1.5 hours
- Networking: 0.5 hours
- Weekend polish/mock/retrospective: 3 hours

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
- Test coverage:
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Biggest win:
- Biggest blocker:
- Top 3 priorities next week:
```

---

## Week 1: Environment and Foundations
Goal: Set up professional Python backend baseline.

### Deliverables
- Repo with Python tooling and project skeleton
- Core CS refresh and 3 DSA problems
- Resume/LinkedIn/GitHub refresh

### Checklist
- [ ] Create repo with src, tests, docs, openapi folders
- [ ] Set up Python virtual env + dependency management (poetry or pip-tools)
- [ ] Add FastAPI app scaffold and /health endpoint
- [ ] Add formatting/linting: black, ruff, mypy
- [ ] Solve 3 easy DSA problems
- [ ] Update resume/LinkedIn/GitHub

---

## Week 2: API and Auth Foundations
Goal: Build auth-ready API structure with test-first workflow.

### Deliverables
- Validation and error handling
- JWT auth flow
- First 5 applications

### Checklist
- [ ] Write mini specs for signup/login and auth middleware
- [ ] Implement Pydantic request/response schemas
- [ ] Add JWT auth + password hashing (passlib)
- [ ] Add pytest tests for auth success/failure paths
- [ ] Add global exception handlers and structured error schema
- [ ] Submit 5 targeted applications
- [ ] Solve 2 medium DSA problems

---

## Week 3: Database and CRUD
Goal: Build production-style CRUD backend with PostgreSQL.

### Deliverables
- SQLAlchemy models + Alembic migrations
- CRUD endpoints + ownership checks
- 70%+ coverage baseline

### Checklist
- [ ] Define relational schema and generate Alembic migration
- [ ] Implement CRUD endpoints with service layer
- [ ] Add integration tests (pytest + httpx + test database)
- [ ] Add authorization checks for user-owned resources
- [ ] Reach 70%+ coverage on critical paths
- [ ] Submit 5 applications
- [ ] Run one system design drill

---

## Week 4: Deployment and Launch (Project 1)
Goal: Ship Project 1 publicly.

### Deliverables
- CI pipeline for lint/type/test/build
- Deployed FastAPI service
- README/docs + technical writeup

### Checklist
- [ ] Configure GitHub Actions for ruff/mypy/pytest
- [ ] Dockerize app and deploy to Render/Fly/Railway
- [ ] Verify live /health and key endpoints
- [ ] Publish technical writeup about architecture/test strategy
- [ ] Submit 10 applications
- [ ] Complete 4 DSA problems

---

## Week 5: Project 2 Scope and Scaffold
Goal: Start a more advanced Python backend project.

### Deliverables
- Project 2 spec and architecture
- Initial schema and endpoint skeleton

### Checklist
- [ ] Pick Project 2 domain (ticketing, booking, workflow, etc.)
- [ ] Write MVP + non-goals + acceptance criteria
- [ ] Add project scaffold with CI and tests
- [ ] Write specs for first two core endpoints
- [ ] Implement initial service logic test-first
- [ ] Submit 5 applications

---

## Week 6: Advanced Features
Goal: Add real-world backend depth.

### Deliverables
- Async background jobs and caching
- Payment/promo or equivalent domain complexity

### Checklist
- [ ] Add Redis caching strategy + invalidation
- [ ] Add Celery/RQ worker for async tasks
- [ ] Implement robust failure handling and retries
- [ ] Add admin/reporting endpoint set
- [ ] Spec and test failure paths
- [ ] Submit 5 applications + 5 outreaches
- [ ] Solve 4 DSA problems

---

## Week 7: Reliability and Performance
Goal: Production hardening.

### Deliverables
- Observability and standardized error model
- Query/perf optimization and security hardening

### Checklist
- [ ] Add structured logging (structlog or logging JSON)
- [ ] Add metrics/tracing basics (Prometheus/OpenTelemetry optional)
- [ ] Optimize SQL queries and add indexes
- [ ] Add rate limiting and stricter CORS/security headers
- [ ] Add contract tests for API error schema
- [ ] Submit 8-10 applications
- [ ] Solve 3 DSA problems

---

## Week 8: Project 2 Launch
Goal: Ship Project 2 and transition to interview-heavy mode.

### Deliverables
- Project 2 deployed and documented
- Interview prep kit created

### Checklist
- [ ] Deploy Project 2 and verify live health and key routes
- [ ] Finalize README/API docs/architecture notes
- [ ] Publish second technical writeup
- [ ] Create project demo scripts + STAR stories
- [ ] Complete 6 DSA problems (reach 40 cumulative)
- [ ] Submit 10-15 applications

---

## Week 9: Interview System Build
Goal: Build repeatable interview execution flow.

### Deliverables
- 3 mocks: coding, behavioral, system design
- Q&A bank and elevator pitch finalized

### Checklist
- [ ] Run timed Python coding mock
- [ ] Run behavioral mock and tighten answers
- [ ] Run system design mock using template
- [ ] Finalize 30-second intro + gap narrative
- [ ] Submit 5 applications + same-day outreach

---

## Week 10: Conversion Optimization
Goal: Increase pass-through rates.

### Deliverables
- 2 additional mocks
- Resume/LinkedIn tuned to Python backend roles

### Checklist
- [ ] Tune bullets with measurable impact
- [ ] Run mock on weakest coding topic
- [ ] Run deep-dive project mock discussion
- [ ] Send follow-ups on 7-day cadence
- [ ] Submit 4-5 high-fit roles

---

## Week 11: Final Round Readiness
Goal: Improve offer probability.

### Deliverables
- Full-loop mock and negotiation prep
- Referral-led submissions

### Checklist
- [ ] Run advanced system design mock
- [ ] Run ownership/prioritization behavioral mock
- [ ] Run full-loop mock (behavioral + coding + design)
- [ ] Prepare compensation decision matrix
- [ ] Ask warm contacts for referrals
- [ ] Final polish pass on both repos

---

## Week 12: Offer Conversion and Next 90 Days
Goal: Close active pipeline and define continuation path.

### Deliverables
- Pipeline triaged and follow-up protocol completed
- Post-12-week operating plan

### Checklist
- [ ] Prioritize hot/warm/cold opportunities
- [ ] Send interview thank-you notes same day
- [ ] Submit 2-3 precision roles only
- [ ] Finalize negotiation scripts
- [ ] Write 30/60/90 day continuation plan

---

## End-of-Program Targets
- 2 deployed Python backend projects
- 40+ DSA problems completed
- 60+ targeted applications
- 8 mock interviews
- 20+ warm networking connections
