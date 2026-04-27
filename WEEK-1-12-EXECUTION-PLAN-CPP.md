# Week 1-12 Execution Plan (C++ Track)
Last Updated: April 26, 2026
Time Budget: 15 hours/week
Track Focus: C++ SWE (backend/systems)
Primary Stack: C++20, CMake, Conan or vcpkg, Catch2 or GoogleTest, Docker, GitHub Actions

---

## How to Use This File
- Use this as the single execution plan for the C++ track.
- Apply Spec-Driven Development and TDD on every feature.
- Keep one weekly scorecard entry each Sunday.

### Weekly Template Workflow
- Start each feature with FEATURE-SPEC-TEMPLATE.md.
- Define tests first in TEST-PLAN-TEMPLATE.md.
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
- Memory/performance checks passed:
- Specs written before implementation:
- Test-first features completed:
- Acceptance criteria mapped to tests:
- Biggest win:
- Biggest blocker:
- Top 3 priorities next week:
```

---

## Week 1: Environment and Foundations
Goal: Build modern C++ dev environment and baseline architecture.

### Deliverables
- C++ repo scaffold with CMake and testing
- Tooling for formatting/lint/static analysis
- 3 DSA problems and profile refresh

### Checklist
- [ ] Create CMake project with src/include/tests layout
- [ ] Add dependencies via Conan or vcpkg
- [ ] Add Catch2/GoogleTest and first passing test
- [ ] Add clang-format, clang-tidy, cppcheck
- [ ] Add AddressSanitizer/UBSan config
- [ ] Solve 3 easy DSA problems
- [ ] Update resume/LinkedIn/GitHub

---

## Week 2: API/Module Foundations
Goal: Establish clean module boundaries and error handling.

### Deliverables
- Input validation and typed error model
- Auth/session or access-control baseline (if backend project)
- First 5 applications

### Checklist
- [ ] Write specs for core module contracts
- [ ] Implement public interfaces and validation guards
- [ ] Add consistent error/result handling strategy
- [ ] Add unit tests for happy/error paths
- [ ] Add logging abstraction (spdlog)
- [ ] Submit 5 targeted applications
- [ ] Solve 2 medium DSA problems

---

## Week 3: Data and CRUD/State Operations
Goal: Build stateful behavior with persistence and tests.

### Deliverables
- Persistence layer (SQLite/Postgres or file-backed for systems project)
- CRUD/state transitions with ownership/rule checks
- 70%+ coverage baseline on core modules

### Checklist
- [ ] Define data model and migration strategy
- [ ] Implement CRUD/state APIs with clear invariants
- [ ] Add integration tests for persistence behavior
- [ ] Add ownership/authorization checks where relevant
- [ ] Run ASan/UBSan in test pipeline
- [ ] Submit 5 applications
- [ ] Run one system design drill

---

## Week 4: Deployment/Release and Launch (Project 1)
Goal: Ship Project 1 as portfolio proof.

### Deliverables
- CI for build/test/lint/sanitizers
- Runnable release artifact and usage docs
- Technical writeup and 10 additional applications

### Checklist
- [ ] Configure GitHub Actions for matrix build (Linux/macOS)
- [ ] Add release build profile and packaging steps
- [ ] Validate with sanitizer and valgrind checks
- [ ] Publish README with architecture and benchmarks
- [ ] Publish technical writeup
- [ ] Submit 10 applications
- [ ] Complete 4 DSA problems

---

## Week 5: Project 2 Scope and Scaffold
Goal: Start advanced C++ project emphasizing performance/concurrency.

### Deliverables
- Project 2 architecture and MVP
- Initial modules and test harness

### Checklist
- [ ] Pick Project 2 domain (order book, scheduler, storage engine, gateway)
- [ ] Define MVP/non-goals and performance targets
- [ ] Write specs for first core modules
- [ ] Implement first features test-first
- [ ] Submit 5 targeted applications

---

## Week 6: Advanced Features
Goal: Add concurrency and production-grade robustness.

### Deliverables
- Thread-safe components and async processing
- Domain complexity and failure handling

### Checklist
- [ ] Implement concurrency primitives safely (mutex/lock-free where justified)
- [ ] Add queue/job pipeline and retry policies
- [ ] Add failure-path tests and race condition tests
- [ ] Add metrics hooks and structured logs
- [ ] Submit 5 applications + 5 outreaches
- [ ] Solve 4 DSA problems

---

## Week 7: Reliability and Performance
Goal: Hardening with profiling and optimization.

### Deliverables
- Profiling-informed optimizations
- Security and robustness checks

### Checklist
- [ ] Profile hotspots (perf/VTune/Callgrind)
- [ ] Optimize memory allocations and data structures
- [ ] Add fuzz tests for parser/input boundaries (if applicable)
- [ ] Add contract tests for API/module boundaries
- [ ] Run sanitizer + static analysis clean pass
- [ ] Submit 8-10 applications
- [ ] Solve 3 DSA problems

---

## Week 8: Project 2 Launch
Goal: Ship Project 2 and transition to interview-heavy mode.

### Deliverables
- Project 2 released with benchmark notes
- Interview prep assets ready

### Checklist
- [ ] Publish release artifact and reproducible build instructions
- [ ] Finalize docs and architecture rationale
- [ ] Publish second technical writeup
- [ ] Prepare demo scripts and tradeoff narratives
- [ ] Complete 6 DSA problems (reach 40 cumulative)
- [ ] Submit 10-15 applications

---

## Week 9: Interview System Build
Goal: Build repeatable C++ interview workflow.

### Deliverables
- 3 mocks: coding, behavioral, system design
- Q&A bank finalized

### Checklist
- [ ] Run timed C++ coding mock (STL-heavy)
- [ ] Run behavioral mock and tighten stories
- [ ] Run systems design mock (latency/throughput focus)
- [ ] Finalize intro and gap narrative
- [ ] Submit 5 applications + outreach

---

## Week 10: Conversion Optimization
Goal: Increase pass-through rates.

### Deliverables
- 2 additional mocks
- Resume/LinkedIn tuned to C++ roles

### Checklist
- [ ] Tune bullets with measurable performance outcomes
- [ ] Run mock on weakest topic (graphs/DP/concurrency)
- [ ] Run deep-dive project walkthrough mock
- [ ] Send follow-ups on 7-day cadence
- [ ] Submit 4-5 high-fit roles

---

## Week 11: Final Round Readiness
Goal: Improve offer probability.

### Deliverables
- Full-loop mock and negotiation prep
- Referral-led submissions

### Checklist
- [ ] Run advanced systems design mock
- [ ] Run behavioral mock for ownership/prioritization
- [ ] Run full-loop mock session
- [ ] Prepare compensation decision matrix
- [ ] Ask warm contacts for referrals
- [ ] Final polish pass on both repos

---

## Week 12: Offer Conversion and Next 90 Days
Goal: Close active pipeline and define continuation path.

### Deliverables
- Pipeline triage and follow-up protocol complete
- Post-12-week operating plan

### Checklist
- [ ] Prioritize hot/warm/cold opportunities
- [ ] Send interview thank-you notes same day
- [ ] Submit 2-3 precision roles only
- [ ] Finalize negotiation scripts
- [ ] Write 30/60/90 day continuation plan

---

## End-of-Program Targets
- 2 deployed/released C++ projects
- 40+ DSA problems completed
- 60+ targeted applications
- 8 mock interviews
- 20+ warm networking connections
