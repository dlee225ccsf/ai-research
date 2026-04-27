# Week 1-12 Execution Plan (Java Track)
Last Updated: April 26, 2026
Time Budget: 15 hours/week
Track Focus: Backend SWE with Java
Primary Stack: Java 21, Spring Boot, PostgreSQL, JUnit 5, Testcontainers, Docker, GitHub Actions

---

## How to Use This File
- Use this as the single execution plan for the Java track.
- Apply Spec-Driven Development and TDD to each feature.
- Keep one weekly scorecard entry each Sunday.

### Weekly Template Workflow
- Start each feature with FEATURE-SPEC-TEMPLATE.md.
- Define tests first with TEST-PLAN-TEMPLATE.md.
- Build with red-green-refactor cycles.

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
Goal: Set up professional Java backend baseline.

### Deliverables
- Spring Boot repo scaffold
- CS refresh and 3 DSA problems
- Resume/LinkedIn/GitHub refresh

### Checklist
- [ ] Create Spring Boot app with Gradle or Maven
- [ ] Add package structure: controller/service/repository/domain
- [ ] Add /health endpoint (Spring Actuator)
- [ ] Add quality tooling: Spotless/Checkstyle + Sonar rules
- [ ] Configure JUnit 5 baseline tests
- [ ] Solve 3 easy DSA problems
- [ ] Update resume/LinkedIn/GitHub

---

## Week 2: API and Auth Foundations
Goal: Build auth-ready API architecture.

### Deliverables
- DTO validation and global exception handling
- JWT auth with Spring Security
- First 5 applications

### Checklist
- [ ] Write specs for signup/login/auth middleware behavior
- [ ] Implement Bean Validation on DTOs
- [ ] Add global exception handler with consistent error schema
- [ ] Implement JWT auth filter and secure endpoints
- [ ] Add JUnit + MockMvc auth tests
- [ ] Submit 5 targeted applications
- [ ] Solve 2 medium DSA problems

---

## Week 3: Database and CRUD
Goal: Add persistence and production-style CRUD.

### Deliverables
- JPA entities + Flyway migrations
- CRUD endpoints with ownership checks
- 70%+ coverage baseline

### Checklist
- [ ] Define entities/repositories and run Flyway migration
- [ ] Implement service-layer CRUD operations
- [ ] Add integration tests with Testcontainers
- [ ] Add authorization checks for user-owned resources
- [ ] Reach 70%+ coverage on critical services
- [ ] Submit 5 applications
- [ ] Run one system design drill

---

## Week 4: Deployment and Launch (Project 1)
Goal: Ship Project 1 publicly.

### Deliverables
- CI pipeline for build/test/lint
- Deployed Spring service
- README/docs + technical writeup

### Checklist
- [ ] Configure GitHub Actions for build, tests, static checks
- [ ] Containerize app and deploy to Render/Fly/Railway
- [ ] Verify live health and key endpoint behavior
- [ ] Add contract tests for success/failure responses
- [ ] Publish technical writeup
- [ ] Submit 10 applications
- [ ] Complete 4 DSA problems

---

## Week 5: Project 2 Scope and Scaffold
Goal: Launch advanced Java backend project.

### Deliverables
- Project 2 architecture and MVP
- New Spring scaffold with CI/tests

### Checklist
- [ ] Pick Project 2 domain and define MVP/non-goals
- [ ] Model schema and service boundaries
- [ ] Write specs for first two key endpoints
- [ ] Implement first core services test-first
- [ ] Submit 5 targeted applications

---

## Week 6: Advanced Features
Goal: Add real-world distributed/backend depth.

### Deliverables
- Caching and async processing
- Domain complexity (payment/promo or equivalent)

### Checklist
- [ ] Add Redis caching with cache eviction strategy
- [ ] Add async jobs/events (Spring async/Kafka/Rabbit optional)
- [ ] Implement robust failure handling and retries
- [ ] Add admin analytics endpoint set
- [ ] Spec and test failure paths
- [ ] Submit 5 applications + 5 outreaches
- [ ] Solve 4 DSA problems

---

## Week 7: Reliability and Performance
Goal: Production hardening.

### Deliverables
- Structured logging + metrics
- Query/performance/security improvements

### Checklist
- [ ] Add structured logs (Logback JSON)
- [ ] Add metrics (Micrometer + Prometheus endpoint)
- [ ] Optimize N+1 queries and add indexes
- [ ] Add rate limiting and harden security settings
- [ ] Add contract tests for error response schema
- [ ] Submit 8-10 applications
- [ ] Solve 3 DSA problems

---

## Week 8: Project 2 Launch
Goal: Ship Project 2 and switch to interview-heavy mode.

### Deliverables
- Project 2 deployed/documented
- Interview prep assets ready

### Checklist
- [ ] Deploy and verify health and core paths
- [ ] Finalize docs and architecture writeup
- [ ] Publish second technical post
- [ ] Prepare project demo scripts + STAR stories
- [ ] Complete 6 DSA problems (reach 40 cumulative)
- [ ] Submit 10-15 applications

---

## Week 9: Interview System Build
Goal: Build repeatable interview execution.

### Deliverables
- 3 mocks: coding, behavioral, system design
- Q&A bank and pitch narrative finalized

### Checklist
- [ ] Run timed Java coding mock
- [ ] Run behavioral mock and tighten answers
- [ ] Run system design mock with template
- [ ] Finalize intro and gap narrative
- [ ] Submit 5 applications + same-day outreach

---

## Week 10: Conversion Optimization
Goal: Increase pass-through rates.

### Deliverables
- 2 additional mocks
- Resume/LinkedIn tuned to Java backend roles

### Checklist
- [ ] Tune bullets with measurable impact
- [ ] Run mock on weakest coding topic
- [ ] Run deep-dive project mock
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
- [ ] Run full-loop mock session
- [ ] Prepare compensation decision matrix
- [ ] Ask warm contacts for referrals
- [ ] Final polish pass on both repos

---

## Week 12: Offer Conversion and Next 90 Days
Goal: Close active pipeline and define continuation path.

### Deliverables
- Pipeline triaged and follow-up protocol done
- Post-12-week operating plan

### Checklist
- [ ] Prioritize hot/warm/cold opportunities
- [ ] Send interview thank-you notes same day
- [ ] Submit 2-3 precision roles only
- [ ] Finalize negotiation scripts
- [ ] Write 30/60/90 day continuation plan

---

## End-of-Program Targets
- 2 deployed Java backend projects
- 40+ DSA problems completed
- 60+ targeted applications
- 8 mock interviews
- 20+ warm networking connections
