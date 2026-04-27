# Week 1-4 Execution Plan (Consolidated)
Last Updated: April 26, 2026
Time Budget: 15 hours/week
Track Focus: Backend SWE (TypeScript, Node.js, PostgreSQL)

---

## How to Use This File
- Use this as the single source of truth for Weeks 1-4.
- Execute checklist items Monday-Sunday.
- Keep one weekly scorecard entry per week.
- Use this together with Week 5-12 consolidated plan for full continuity.

### Weekly Template Workflow
- At the start of each feature, copy [FEATURE-SPEC-TEMPLATE.md](FEATURE-SPEC-TEMPLATE.md) and fill it.
- Before coding, copy [TEST-PLAN-TEMPLATE.md](TEST-PLAN-TEMPLATE.md) and define failing tests first.
- Track completion in your weekly scorecard using the Spec/TDD checklist fields.
- Keep spec and test plan files in the same folder as the feature work for easy review.

---

## Unified Weekly Operating Rhythm (Weeks 1-4)

### Monday to Friday (about 12 hours)
- Build and implementation: 7 hours
- DSA and fundamentals: 3 hours
- Profile/resume/applications: 1.5 hours
- Review and cleanup: 0.5 hours

### Saturday to Sunday (about 3 hours)
- Polish and docs: 1 hour
- Catch-up: 1 hour
- Retrospective and next-week prep: 1 hour

---

## Spec-Driven + TDD Operating Model
Use this for every feature in Weeks 1-4.

1. Write a short feature spec before coding.
2. Define acceptance criteria and error cases.
3. Write failing tests from the spec first.
4. Implement the minimum code to pass tests.
5. Refactor with tests still green.
6. Mark feature done only when acceptance criteria are covered by tests.

### Feature Spec Template
Copy and fill this before implementation.

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
```

### Weekly Spec/TDD Checklist
Add this to each week scorecard.

```markdown
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Refactors completed with green tests:
```

---

## Weekly Scorecard Template
Copy this once per week into your tracker.

```markdown
## Week X Scorecard
- DSA problems completed:
- Core deliverables shipped:
- Applications submitted:
- Networking outreaches:
- Commits this week:
- Test coverage (if applicable):
- Biggest win:
- Biggest blocker:
- Top 3 priorities next week:
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Refactors completed with green tests:
```

---

## Week 1: Foundation Reset
Goal: Re-establish development rhythm and public professional presence.

### Deliverables
- Project repo initialized with clean scaffold
- CS fundamentals refreshed (Big-O, DS, SQL)
- 3 DSA problems solved and tracked
- Resume v1 drafted
- LinkedIn and GitHub profiles refreshed
- Tracking system established

### Checklist
- [ ] Create public project repo and initialize TypeScript + Node scaffold
- [ ] Add baseline project structure and `.env.example`
- [ ] Refresh fundamentals and write summary notes
- [ ] Solve 3 easy DSA problems and document complexity
- [ ] Rewrite resume into concise, role-focused v1
- [ ] Update LinkedIn headline/about and GitHub profile bio
- [ ] Create `PROGRESS.md` and DSA tracker

---

## Week 2: API Fundamentals and Auth
Goal: Build core backend API capability and begin targeted applications.

### Deliverables
- Express app with middleware and route structure
- Validation and centralized error handling
- JWT auth and password hashing integrated
- Resume polished with active project context
- 5 targeted applications submitted
- 2 additional DSA problems solved

### Checklist
- [ ] Build Express app with health endpoint and clean routing
- [ ] Add request validation and reusable error utilities
- [ ] Implement JWT token generation and auth middleware
- [ ] Add password hashing and auth flow scaffolding
- [ ] Write mini spec for auth and validation flows before coding
- [ ] Use red-green-refactor cycle for auth and middleware tests
- [ ] Polish resume for current backend narrative
- [ ] Submit first 5 targeted applications and log follow-up dates
- [ ] Solve 2 medium DSA problems and update tracker

---

## Week 3: Database, CRUD, and Test Coverage
Goal: Move from API shell to production-like data-backed functionality.

### Deliverables
- Prisma schema and migrations operational
- Full CRUD endpoints for core resource
- Unit and integration tests in place
- Coverage baseline at 70%+
- 4 additional DSA problems solved
- 5 more applications submitted

### Checklist
- [ ] Define relational schema and create Prisma migration
- [ ] Implement create/read/update/delete endpoints
- [ ] Add auth-aware ownership checks to protected resources
- [ ] Add Jest + Supertest integration tests
- [ ] Create endpoint specs for CRUD and error behavior before implementation
- [ ] Keep all CRUD changes inside red-green-refactor loops
- [ ] Validate test coverage and close critical path gaps
- [ ] Submit 5 additional applications
- [ ] Run one system design session for your app at scale

---

## Week 4: Deployment, CI/CD, and Launch
Goal: Ship Project 1 publicly and convert it into hiring signal.

### Deliverables
- CI pipeline active (lint, test, build)
- Project deployed and health-checked in production
- Production-grade README and supporting docs complete
- Technical post published
- 10 additional targeted applications submitted
- 4 additional DSA problems solved

### Checklist
- [ ] Configure GitHub Actions workflow for PR and main branch
- [ ] Deploy to Render/Railway and verify `/health`
- [ ] Add clear README, architecture summary, and changelog
- [ ] Publish one technical write-up on your project decisions
- [ ] Add contract tests for key API success and failure responses
- [ ] Tag release (v1.0.0) and pin project in GitHub profile
- [ ] Submit 10 targeted applications with project links
- [ ] Complete 4 DSA problems and update tracker

---

## Cumulative Targets by End of Week 4
- 1 deployed project, demo-ready
- 12 DSA problems completed
- 20 targeted applications submitted
- Resume/LinkedIn/GitHub polished and current
- CI/CD pipeline and test coverage baseline established

---

## If Week 1-4 Slips
- Prioritize in this order:
  1. Deployed project
  2. Resume/profile updates
  3. Applications and follow-ups
  4. DSA volume
- Keep shipping cadence: a smaller complete artifact beats an unfinished large one.

This sets a strong base for Week 5-12 interview conversion.
