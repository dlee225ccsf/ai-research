# Job Search Preparation: 12-Week Plan for CS Graduates
**Last Updated:** April 26, 2026  
**Context:** CS graduate, 2+ year employment gap, aiming for backend/full-stack SWE roles  
**Commitment:** 15 hours/week over 12 weeks

---

## Execution Files
- Consolidated Week 1-4 (primary): `WEEK-1-4-EXECUTION-PLAN.md`
- Consolidated Week 5-12 (primary): `WEEK-5-12-EXECUTION-PLAN.md`
- Archived detailed weekly files: `archive/`

---

## Table of Contents
1. [Overview & Strategy](#overview--strategy)
2. [12-Week Plan At A Glance](#12-week-plan-at-a-glance)
3. [Stack Selection](#stack-selection)
4. [Weekly Breakdown](#weekly-breakdown)
5. [Key Principles](#key-principles)
6. [Positioning Your Gap](#positioning-your-gap)
7. [Project Ideas](#project-ideas)
8. [KPIs & Tracking](#kpis--tracking)
9. [Resume Bullets](#resume-bullets)
10. [Application Strategy](#application-strategy)
11. [Interview Preparation Roadmap](#interview-preparation-roadmap)

---

## Overview & Strategy

### The Problem
- CS degree but 2+ year employment gap
- Job market uncertain; need to stay sharp and competitive
- Risk: skills atrophy, gaps accumulate, interviewing gets harder

### The Solution
**Rebuild via production-grade portfolio + deliberate practice + visible momentum.**

Instead of waiting for market recovery, become the candidate hiring managers *want* to hire:
- Ship 2 real, tested, deployed projects
- Demonstrate deep understanding (not just tutorials)
- Show consistent learning + public signals
- Build interview confidence through mock practice
- Create referral opportunities through networking

### Core Belief
**Consistency + Visibility = Competitive Advantage**

Recruiters check GitHub, LinkedIn, and recent work. By Week 12, yours should scream: *"This person is ready now."*

---

## 12-Week Plan At A Glance

| Phase | Weeks | Goal | Outcome |
|-------|-------|------|---------|
| **Foundation** | 1-4 | Rebuild CS fundamentals, ship first project | 1 deployed API, resume polished, 12 DSA problems solved |
| **Portfolio** | 5-8 | Advanced features, second project, interview prep | 2 deployed projects, 40+ DSA problems, 15 applications, visible write-up |
| **Job Ready** | 9-12 | Interview simulation, final polish, market entry | Interview-ready profile, 30-40 applications, 8 mock interviews, referral network warm |

---

## Stack Selection

### Why TypeScript + Node.js + PostgreSQL + Docker?
- **Market demand:** High (2026 job market)
- **Learning curve:** Moderate (JavaScript syntax familiar to CS grads)
- **Breadth:** Covers backend, APIs, database, deployment, DevOps basics
- **Depth available:** Auth, caching, queues, microservices patterns later
- **Portfolio impact:** "Production-grade" signal to hiring teams

### Core Tech Stack
```
Language:        TypeScript (JavaScript with types)
Runtime:         Node.js
Framework:       Express.js
Database:        PostgreSQL
ORM:             Prisma (easy + great docs) or TypeORM (enterprise-like)
Testing:         Jest
API Style:       REST (GraphQL optional in Week 5+)
Deployment:      Render or Railway (simple), AWS (stretch)
CI/CD:           GitHub Actions
Containerization: Docker + docker-compose
Version Control:  Git + GitHub
```

### Complementary Skills (Add in Weeks 5-12)
- Redis (caching basics)
- Message queues (Bull/RabbitMQ optional)
- Monitoring (basic logging + error tracking)
- System design patterns

---

## Weekly Breakdown

### Weeks 1-4: Build Foundations + First Project

#### Week 1: Rebuild Fundamentals
- Set up project scaffold (TypeScript + Node + GitHub)
- Refresh CS fundamentals (Big-O, data structures, SQL)
- Solve 3 DSA problems (easy level)
- Rewrite resume emphasizing "rebuilding + shipping"
- Update LinkedIn + GitHub profile
- Create tracking system

**Deliverable:** Public GitHub repo, 3 DSA problems, polished resume/profiles

#### Week 2: API Fundamentals + Authentication
- Build Express server with middleware (validation, error handling)
- Implement JWT auth + password hashing
- Polish resume with Project 1 bullets
- Submit first 5 applications (tailored)
- Solve 2 more DSA problems (medium level)
- Introduce system design concepts

**Deliverable:** Production-style Express server, 5 applications, 5 total DSA problems

#### Week 3: Database Layer + CRUD Endpoints
- Design database schema (project-specific)
- Set up Prisma or TypeORM
- Build CRUD endpoints (Create, Read, Update, Delete)
- Add unit + integration testing (Jest)
- Continue 4 DSA problems/week
- Start light system design practice

**Deliverable:** Database-backed API, test suite, 9 total DSA problems

#### Week 4: Deploy + CI/CD + Documentation
- Add GitHub Actions pipeline (lint + test on PR)
- Deploy to Render/Railway (free tier)
- Write production-grade README
- Create project video walkthrough or write technical post
- Submit 10+ more applications
- First 12 DSA problems done

**Deliverable:** Live Project 1, CI/CD pipeline, technical post, 12 DSA problems

---

### Weeks 5-8: Advanced Features + Strong Portfolio Signal

#### Week 5: Project 2 — Scope + Architecture
- Choose more advanced project (job tracker, booking system, etc.)
- Design architecture (domain model, API contract, DB schema)
- Set up repo with scaffold
- Continue 4 DSA problems/week
- 1 system design exercise

**Deliverable:** Project 2 skeleton, clear architecture, 16 DSA problems

#### Week 6: Advanced Backend Features
- Pagination, filtering, sorting
- Caching (Redis optional, or in-memory)
- Background jobs or async queues
- Advanced auth (2FA, refresh tokens optional)
- API documentation (Swagger/OpenAPI)
- 4 DSA problems, 1 system design

**Deliverable:** Advanced features shipped, API docs, 20 DSA problems

#### Week 7: Observability + Quality
- Structured logging (Winston or Pino)
- Centralized error tracking
- Performance profiling
- 10+ tailored applications
- Weekly system design practice
- 4 DSA problems

**Deliverable:** Production-ready logging/error setup, 24 DSA problems

#### Week 8: Deploy Project 2 + Publish
- Deploy Project 2
- Publish technical blog post (architecture decisions, tradeoffs)
- Polish both project READMEs
- 15 more applications (batch submission)
- 4 DSA problems
- 1 system design exercise

**Deliverable:** Live Project 2, published write-up, 28 DSA problems, 30+ total applications

---

### Weeks 9-12: Interview Preparation + Job Market Entry

#### Week 9: Mock Interview Week 1
- 1 full DSA mock interview (timed, 45 min)
- 1 behavioral mock (practice STAR stories)
- Refine "gap explanation" (30-45 sec elevator pitch)
- 5 common behavioral questions answered + memorized
- 4 DSA problems (focus on weak patterns)

**Deliverable:** STAR stories written, gap narrative polished, 32 DSA problems

#### Week 10: Portfolio Polish Sprint
- Bug fixes on both projects
- Improve documentation
- Add 1 "wow" feature (role-based access, webhooks, etc.)
- Deploy improvements
- Continue applications (10-12 roles)
- 4 DSA problems, 1 system design

**Deliverable:** Portfolio v2 quality, 36 DSA problems

#### Week 11: Mock Interview Week 2 + Final Applications
- 1 full system design mock
- 1 project deep-dive interview (explain your code)
- 1 behavioral + technical combined mock
- 12-15 final applications + referral pushes
- Finish strong on DSA (target 40 total)
- 1 system design exercise

**Deliverable:** Interview muscle memory, 40 DSA problems, 25+ applications this month

#### Week 12: Final Packaging + 30/60/90 Plan
- Resume v2 (quantified impact added)
- GitHub profile final polish (pinned repos, bio, readme)
- Cover letter template (reusable)
- 30/60/90-day onboarding plan (for interviews)
- Networking push: 5 coffee chats or informational interviews
- Celebrate + retrospective

**Deliverable:** Job-market-ready profile bundle, 30-40 total applications submitted, ongoing system ready

---

## Key Principles

### 1. Consistency > Perfection
- Commit code daily (even small wins)
- Recruiters see GitHub activity streak
- 1 hour/day beats 15 hours on Sunday

### 2. Visibility Wins
- Public repos > private code
- GitHub profile > no profile
- LinkedIn posts > silent work
- Technical writing proves depth

### 3. "Production-Grade" Signal
- Tests included (not optional)
- CI/CD pipeline (not "someday")
- Deployed live (not just `npm install` locally)
- Clean README (not amateur hour)

### 4. Portfolio > Credentials
- 2 shipped projects > 5 online courses
- Tests > "it works on my machine"
- Deploy > local-only code
- Real tradeoffs > textbook solutions

### 5. Deliberate Practice
- Timed DSA sessions (practice interview pressure)
- Explain solutions out loud
- Review mistakes (don't move on)
- Track patterns learned

### 6. Network Early, Ask Late
- Connect with engineers on LinkedIn now (week 1)
- Coffee chats start week 4
- Referrals warm by week 8-9
- Applications go much smoother with warm intro

---

## Positioning Your Gap

### The Script (30-45 seconds)
Use this in interviews, cover letters, LinkedIn:

> "I graduated in 2022 and took intentional time to rebuild my engineering skills and stay current with modern backend development. I focused on shipping production-grade projects in TypeScript + Node.js, practicing system design, and preparing for the technical interview process. I built two fully tested, deployed APIs with authentication, databases, and CI/CD pipelines. I've been practicing 40+ data structure problems and doing mock interviews weekly. I'm now highly motivated to contribute to a strong team and ship real features at scale."

### Key Messaging
- **Intentional** (not desperate)
- **Shipped** (not studied)
- **Ready** (practiced, prepared)
- **Excited** (clear about what's next)

### In Resume
Add a line under summary:
> "CS graduate focused on backend engineering. Recently rebuilt and sharpened skills by shipping two production-grade REST APIs. Actively practicing system design and interview preparation."

---

## Project Ideas

### Option A: Job Application Tracker SaaS
- Features: Track applications, set reminders, analytics dashboard
- Tech: Auth, database, background jobs (email reminders), dashboards
- Complexity: Medium
- Why: Relatable problem (you're doing this now!)

### Option B: Service Booking Platform
- Features: Calendar, availability, booking flow, payments (mock)
- Tech: Complex state management, scheduling, webhooks
- Complexity: Medium-Hard
- Why: Real business logic, common interview pattern

### Option C: Event Ticketing System
- Features: Inventory management, purchase flow, ticket generation
- Tech: Transactions, concurrency, file generation
- Complexity: Medium-Hard
- Why: Teaches critical backend concepts (inventory, atomicity)

### Option D: Incident Management Tool (like PagerDuty lite)
- Features: Create incidents, escalations, audit logs, alerts
- Tech: Queues, event sourcing, real-time updates
- Complexity: Hard
- Why: Demonstrates DevOps-aware thinking

**Recommendation:** Pick **Option A or B** for Project 1 (medium complexity, done by Week 4), then **Option C or D** for Project 2 (more complex, done by Week 8).

---

## KPIs & Tracking

### What To Measure (by Week 12)
| Metric | Target | Actual |
|--------|--------|--------|
| DSA problems solved | 40-60 | ___ |
| Projects deployed | 2 | ___ |
| Applications submitted | 30-40 | ___ |
| Mock interviews | 8 | ___ |
| Networking outreaches | 20+ | ___ |
| Technical posts/writeups | 3 | ___ |
| GitHub commits | 100+ | ___ |
| GitHub profile visitors | Rising trend | ___ |

### Tracking System
Create `PROGRESS.md` in project:
```markdown
# 12-Week Progress Tracker

## Week N (Date Range)
- [x] Day 1: [Task]
- [ ] Day 2: [Task]

## Metrics This Week
- DSA solved: X
- Commits: Y
- Applications: Z

## Wins This Week
- [Achievement]

## Blockers
- [Challenge + how resolved]
```

Review **every Friday at 3pm** (consistent habit).

---

## Resume Bullets

### Generic Project 1 Bullet
```
[Project Name] | TypeScript, Node.js, PostgreSQL, Express.js, Docker
• Designed and deployed a production-grade REST API with 
  JWT authentication and role-based access control
• Built comprehensive test suite achieving 85%+ code coverage 
  via unit and integration tests
• Automated CI/CD pipeline using GitHub Actions with linting, 
  testing, and deployment stages
• Containerized application for reproducible deployments; 
  deployed to [Render/Railway]
```

### Generic Project 2 Bullet (More Complex)
```
[Project Name] | TypeScript, Node.js, PostgreSQL, Redis, Prisma, Docker
• Architected advanced backend system handling pagination, 
  filtering, and real-time updates for 1000+ concurrent users
• Implemented background job processing using [Bull/Queue] 
  for email notifications and data exports
• Built observability stack with structured logging, centralized 
  error tracking, and performance metrics
• Achieved <200ms p95 latency via caching strategy and 
  database query optimization
```

### Quantification Tips
- Replace "built" with "shipped" or "deployed"
- Add numbers: "100+ endpoints", "85% test coverage", "1000 users"
- Add business value: "reduced response time by 60%"
- Add rigor: "comprehensive", "production-grade", "observability"

---

## Application Strategy

### Targeting Strategy (30-40 applications total)
- **Weeks 1-4:** 5 applications (early signal, learn process)
- **Week 5-8:** 15-20 applications (portfolio building + volume)
- **Weeks 9-12:** 10-15 applications (final push, quality over quantity)

### Where To Apply
1. **LinkedIn Job Board** (easiest, most reach)
2. **AngelList / Wellfound** (startups, equity upside)
3. **Company Career Pages** (direct submission)
4. **GitHub Jobs** (tech-forward companies)
5. **Referrals** (by week 5, warm intros > cold applies)

### Filtering Criteria
- ✅ Remote or local
- ✅ Junior, Entry-level, Associate, or unspecified level
- ✅ Backend, Full-stack, SDE roles
- ✅ Your tech stack (Node/Python/Java preferred)
- ✅ Series A+ startups or established companies (avoid pre-seed chaos)

### Application Process (20 min per app)
1. Read job description → extract 3-5 key skills
2. Tailor resume bullets to match keywords
3. Write 3-paragraph cover letter:
   - Why this company/role appeals to you
   - How your portfolio demonstrates relevant skills
   - Brief, enthusiastic closing
4. Submit via company site (preferred) or LinkedIn
5. Log in `APPLICATIONS.md` tracker

### Referral Leverage (Week 5+)
- Find 2-3 engineers at each target company
- LinkedIn message: "Hey [name], I noticed you work at [company] on backend systems. Would love to grab 15 min to learn more about your team and how I could contribute."
- If warm: ask for referral
- Always thank them + give update on interview progress

---

## Interview Preparation Roadmap

### Phase 1: Foundation (Weeks 1-6)
- 3-4 DSA problems/week
- Focus on patterns: arrays, hashmaps, strings, trees
- No time pressure initially; understand solutions deeply

### Phase 2: Pressure Training (Weeks 7-9)
- 4-5 DSA problems/week with **timer** (45 min)
- Talk through solutions out loud
- Practice explaining tradeoffs

### Phase 3: Full Simulation (Weeks 9-12)
- Mock DSA interview 1x/week (timed, filmed if possible)
- Mock system design 1x/week (whiteboard or doc)
- Mock behavioral + project deep-dive 1x/week
- Review recordings; identify patterns

### DSA Topics to Cover (by difficulty)
| Easy | Medium | Hard |
|------|--------|------|
| Two Sum | Longest Substring | Trapping Rain Water |
| Valid Parentheses | Best Time to Buy Stock | Word Ladder |
| Merge Sorted Array | LCS | Median of Two Sorted Arrays |
| Remove Duplicates | Binary Tree Level Order | Skyline Problem |
| Climbing Stairs | Top K Frequent Elements | LRU Cache |

**Resource:** NeetCode.io (structured, 150-question list)

### System Design Topics
1. **Fundamentals:** Load balancing, caching, databases, CDNs
2. **Patterns:** Microservices, event-driven, CQRS
3. **Real Systems:** Twitter, YouTube, Uber (practice designing)
4. **Your Projects:** Be able to explain them at scale
   - "How would your app handle 1M users?"
   - "Where's the bottleneck?"
   - "How would you cache this?"

### Behavioral Preparation
Prepare STAR stories for:
- Handling conflict in a team
- Learning a new technology quickly
- Debugging a production issue
- Shipping under tight deadline
- Learning from failure

---

## Weekly Time Budget (15 hours total)

```
Monday - Friday (10 hours)
├─ Project Building: 6 hours
│  ├─ Code: 4 hours
│  └─ Code review/testing: 2 hours
├─ Interview Prep: 2.5 hours
│  ├─ DSA: 1.5 hours (3-4 problems)
│  └─ System design: 1 hour
├─ Applications: 1 hour
│  └─ Tailoring + submission
└─ Networking: 0.5 hours
   └─ LinkedIn messages / outreach

Weekend (5 hours)
├─ Project Polish: 2 hours
├─ Public Proof: 1 hour
│  └─ Blog post / README / GitHub update
├─ Interview Practice: 1.5 hours
│  └─ Mock interview or deep prep
└─ Reflection: 0.5 hours
   └─ Weekly review + next week planning
```

---

## Success Checklist

### By End of Week 4
- [ ] GitHub repo public + polished
- [ ] Express server with auth working
- [ ] 12 DSA problems solved
- [ ] Resume updated + on GitHub
- [ ] LinkedIn/GitHub profiles professional
- [ ] 5 applications submitted
- [ ] Tracking system created

### By End of Week 8
- [ ] Project 1 deployed + live
- [ ] Project 2 foundation built
- [ ] 28 DSA problems solved
- [ ] Published 1 technical post
- [ ] 30+ applications submitted
- [ ] Started networking (5+ outreaches)

### By End of Week 12
- [ ] 2 projects deployed, tested, documented
- [ ] 40-60 DSA problems solved
- [ ] 8 mock interviews completed
- [ ] 30-40 applications submitted
- [ ] 20+ networking conversations
- [ ] Interview-ready profile + story

---

## Tips for Success

1. **Commit daily.** Code is visible; consistency speaks volumes.
2. **Tailor applications.** Generic resumes lose to tailored ones.
3. **Ship, don't study.** Tests + deployment > perfect code.
4. **Network early.** Referrals > cold applications (often 3-5x callback rate).
5. **Document learning.** Blog posts prove depth + teach others.
6. **Mock interview seriously.** Pressure training = edge in real interview.
7. **Track rigorously.** Metrics keep you honest + motivated.
8. **Celebrate wins.** Shipping a feature > studying a course.
9. **Be patient with the market.** By Week 12, you'll be ready. Market will follow.
10. **Tell someone your plan.** Accountability is powerful.

---

## What Happens Next

### After Week 12
If not hired yet (likely scenario in slow market):
- Continue same routine: 2 projects/month, 20+ applications/month, 4 DSA problems/week
- Deepen one specialization: system design, distributed systems, or DevOps
- Contribute to open source (20+ commits)
- Build 1 more advanced project
- Attend local meetups, conferences

You'll be significantly more hirable in Month 4-6 than Month 1-3.

### If You Get Offers in Weeks 8-12
- Don't stop interviewing until you sign
- Negotiate (salary, benefits, WLB)
- Ramp quickly on day 1
- Stay in touch with the community you built

---

## Final Thoughts

**You have a real advantage:** intentionality. Most graduates job-hunt passively. You're building *visibly* and *deliberately*. By Week 12, recruiters will see:
- Working code on GitHub
- Tests and deployments
- Technical writing
- Interview readiness
- Hunger to contribute

That's hiring material.

The market will recover. By the time it does, you'll be competing from a position of strength, not desperation.

**Go build. 🚀**

---

## Quick Links & Resources

### Learning
- [NeetCode.io](https://neetcode.io/) - DSA practice
- [System Design Primer](https://github.com/donnemartin/system-design-primer) - Reference
- [HighScalability.com](http://highscalability.com/) - Real systems
- [Dev.to](https://dev.to/) - Technical writing platform

### Platforms
- [LinkedIn Jobs](https://www.linkedin.com/jobs/)
- [AngelList](https://wellfound.com/) - Startups
- [GitHub Jobs](https://github.com/jobs) - Tech companies
- [Referral networks](https://www.triplebyte.com/) - Optional paid

### Tools
- [GitHub](https://github.com/) - Version control + portfolio
- [Render.com](https://render.com/) or [Railway.app](https://railway.app/) - Free deployment
- [Prisma](https://www.prisma.io/) - ORM + great docs
- [Jest](https://jestjs.io/) - Testing framework

### Writing
- [Medium](https://medium.com/)
- [Dev.to](https://dev.to/)
- [Hashnode](https://hashnode.com/)

---

**Created:** April 26, 2026  
**Review Date:** Update monthly with progress + learnings
