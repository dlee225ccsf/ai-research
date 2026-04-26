# Week 4: Deploy + CI/CD + Documentation + Project Launch
## Goal: Ship Project 1 to production, CI/CD pipeline live, technical post published

---

## Day 22 (Monday) — GitHub Actions CI/CD Pipeline
**Time: 2.5 hours**

### Morning (1.5 hours) — GitHub Actions Workflow Setup
- [ ] Create `.github/workflows/ci.yml`:
  ```yaml
  name: CI/CD Pipeline

  on:
    push:
      branches: [main, develop]
    pull_request:
      branches: [main, develop]

  jobs:
    test:
      runs-on: ubuntu-latest

      services:
        postgres:
          image: postgres:15
          env:
            POSTGRES_USER: test
            POSTGRES_PASSWORD: test
            POSTGRES_DB: test_db
          options: >-
            --health-cmd pg_isready
            --health-interval 10s
            --health-timeout 5s
            --health-retries 5
          ports:
            - 5432:5432

      steps:
        - uses: actions/checkout@v3

        - name: Set up Node.js
          uses: actions/setup-node@v3
          with:
            node-version: '18'
            cache: 'npm'

        - name: Install dependencies
          run: npm ci

        - name: Run linter
          run: npm run lint

        - name: Run tests
          env:
            DATABASE_URL: postgresql://test:test@localhost:5432/test_db
          run: npm test -- --coverage

        - name: Upload coverage
          uses: codecov/codecov-action@v3
          with:
            files: ./coverage/coverage-final.json

        - name: Build
          run: npm run build

    deploy:
      needs: test
      runs-on: ubuntu-latest
      if: github.ref == 'refs/heads/main' && github.event_name == 'push'

      steps:
        - uses: actions/checkout@v3

        - name: Deploy to Render
          run: |
            curl https://api.render.com/deploy/srv-${{ secrets.RENDER_SERVICE_ID }}?key=${{ secrets.RENDER_API_KEY }}
  ```

- [ ] Add secrets to GitHub repo (Settings → Secrets):
  - `RENDER_SERVICE_ID` (from Render)
  - `RENDER_API_KEY` (from Render)

- [ ] Update `package.json` scripts:
  ```json
  "scripts": {
    "lint": "eslint src/",
    "build": "tsc",
    "test": "jest"
  }
  ```

### Afternoon (1 hour) — Linter Setup (ESLint + Prettier)
- [ ] Install:
  ```bash
  npm install --save-dev eslint prettier eslint-config-prettier
  ```
- [ ] Create `.eslintrc.json`:
  ```json
  {
    "env": {
      "node": true,
      "es2021": true
    },
    "extends": ["eslint:recommended", "prettier"],
    "parser": "@typescript-eslint/parser",
    "parserOptions": {
      "ecmaVersion": "latest",
      "sourceType": "module"
    },
    "rules": {
      "no-console": "warn",
      "prefer-const": "error"
    }
  }
  ```
- [ ] Create `.prettierrc`:
  ```json
  {
    "semi": true,
    "singleQuote": true,
    "trailingComma": "es5",
    "printWidth": 100
  }
  ```
- [ ] Commit: `git add .github/workflows/ .eslintrc.json .prettierrc && git commit -m "ci: add github actions + linting"`

**Deliverable:** GitHub Actions pipeline configured + runs on every push

---

## Day 23 (Tuesday) — Deployment to Render
**Time: 2.5 hours**

### Morning (1 hour) — Render Setup
- [ ] Sign up for [Render.com](https://render.com/) (free tier)
- [ ] Create new Web Service:
  - Connect GitHub repo
  - Build command: `npm install && npm run build`
  - Start command: `node dist/app.js`
  - Environment variables:
    - `NODE_ENV=production`
    - `PORT=3000`
    - `JWT_SECRET=[generate strong secret]`
    - `DATABASE_URL=[Render PostgreSQL or Supabase URL]`
- [ ] Deploy (Render auto-deploys on push to main)

### Afternoon (1.5 hours) — Database for Production
- [ ] Option A: Use Supabase (free PostgreSQL):
  - Sign up at [supabase.com](https://supabase.com/)
  - Create new project
  - Copy connection string
  - Run migrations: `prisma migrate deploy`

- [ ] Option B: Use Render PostgreSQL:
  - Create PostgreSQL database on Render
  - Connect from Render app
  - Run migrations via Render CLI or manually

- [ ] Test live deployment:
  - Visit `https://your-app.render.com/health`
  - Should return: `{ "status": "ok", "timestamp": "..." }`

- [ ] Commit: `git add render.yaml (if applicable) && git commit -m "deploy: project 1 live on render"`

**Deliverable:** Project 1 accessible at live URL (e.g., https://job-tracker-api.render.com)

---

## Day 24 (Wednesday) — Production-Grade README
**Time: 2.5 hours**

### Morning (1.5 hours) — Write Comprehensive README
- [ ] Update `README.md` to include:
  ```markdown
  # Job Application Tracker API

  A production-grade REST API for managing job applications, interviews, and tracking your job search journey.

  **Live Demo:** [https://job-tracker-api.render.com](https://job-tracker-api.render.com)

  ---

  ## Features
  - 🔐 JWT Authentication with secure password hashing
  - 📝 Full CRUD operations for job applications
  - 📊 Filter & paginate applications by status
  - 🎯 Track interviews and outcomes
  - 🧪 Comprehensive test coverage (72%+)
  - 🐳 Containerized with Docker
  - 🚀 CI/CD pipeline with GitHub Actions
  - 📖 Full API documentation

  ---

  ## Tech Stack
  - **Backend:** Node.js + Express + TypeScript
  - **Database:** PostgreSQL
  - **ORM:** Prisma
  - **Testing:** Jest + Supertest
  - **Deployment:** Render + GitHub Actions
  - **Documentation:** API docs (see below)

  ---

  ## Quick Start

  ### Prerequisites
  - Node.js 18+
  - PostgreSQL 14+
  - npm

  ### Installation
  ```bash
  git clone https://github.com/yourusername/job-tracker-api.git
  cd job-tracker-api
  npm install
  ```

  ### Environment Setup
  ```bash
  cp .env.example .env
  # Edit .env with your database URL and JWT secret
  ```

  ### Database Setup
  ```bash
  npx prisma migrate dev --name init
  npx prisma db seed  # Optional: seed data
  ```

  ### Running Locally
  ```bash
  npm run dev  # Starts on http://localhost:3000
  ```

  ### Running Tests
  ```bash
  npm test              # Run all tests
  npm run test:watch    # Watch mode
  npm run test:coverage # Coverage report
  ```

  ---

  ## API Documentation

  ### Authentication
  All endpoints (except `/auth/signup` and `/auth/login`) require JWT token in header:
  ```
  Authorization: Bearer <token>
  ```

  ### Endpoints

  #### Auth
  - `POST /api/v1/auth/signup` - Register new user
  - `POST /api/v1/auth/login` - Login (returns JWT token)

  #### Applications
  - `GET /api/v1/applications` - List your applications (paginated)
  - `POST /api/v1/applications` - Create new application
  - `GET /api/v1/applications/:id` - Get single application
  - `PATCH /api/v1/applications/:id` - Update application
  - `DELETE /api/v1/applications/:id` - Delete application

  #### Interviews
  - `GET /api/v1/applications/:id/interviews` - List interviews for application
  - `POST /api/v1/applications/:id/interviews` - Add interview
  - `PATCH /api/v1/interviews/:id` - Update interview

  ---

  ## Architecture

  ### System Design
  ```
  Client (Browser/Mobile)
         ↓
  API Gateway (Express)
         ↓
  Auth Middleware (JWT)
         ↓
  Route Handler
         ↓
  Prisma ORM
         ↓
  PostgreSQL Database
  ```

  ### Design Decisions

  **1. JWT Authentication**
  - Stateless, scalable authentication
  - No session storage needed
  - Works across multiple servers

  **2. Prisma ORM**
  - Type-safe database queries
  - Auto-generated migrations
  - Great dev experience

  **3. Pagination**
  - Required for scale
  - Default: 10 items per page
  - Query params: `skip` and `take`

  **4. Soft Deletes (Future Enhancement)**
  - Consider soft deletes for audit trails
  - Preserve application history

  ---

  ## Testing

  ### Test Coverage
  - Unit tests for auth, utils
  - Integration tests for API endpoints
  - Database tests with real migrations

  **Current Coverage:** 72%

  ### Example Test
  ```typescript
  describe('Applications API', () => {
    it('should create a new application', async () => {
      const res = await request(app)
        .post('/api/v1/applications')
        .set('Authorization', `Bearer ${token}`)
        .send({
          companyName: 'TechCorp',
          jobTitle: 'Backend Engineer',
          appliedDate: new Date().toISOString(),
        });

      expect(res.status).toBe(201);
      expect(res.body.companyName).toBe('TechCorp');
    });
  });
  ```

  ---

  ## Deployment

  ### Deployment to Render
  1. Create Render account
  2. Connect GitHub repo
  3. Set environment variables
  4. Deploy (auto-deploys on push to main)

  ### Database Migration in Production
  ```bash
  render exec "npx prisma migrate deploy"
  ```

  ---

  ## Performance Considerations

  ### Current Optimizations
  - Database indexes on `userId` and `appliedDate`
  - Pagination (required for large datasets)
  - Connection pooling via Prisma

  ### Future Improvements
  - Add Redis caching for user's applications
  - Implement query optimization (N+1 prevention)
  - Add API rate limiting
  - Consider async job processing for exports

  ---

  ## Security

  - ✅ JWT tokens with expiry (7 days)
  - ✅ Password hashing with bcrypt (10 rounds)
  - ✅ Input validation (express-validator)
  - ✅ CORS enabled
  - ✅ Helmet.js for security headers
  - ⚠️ TODO: Rate limiting (express-rate-limit)
  - ⚠️ TODO: 2FA for added security

  ---

  ## Project Structure
  ```
  src/
  ├── app.ts              # Express app setup
  ├── routes/             # API routes
  │   ├── auth.ts
  │   ├── applications.ts
  │   └── interviews.ts
  ├── middleware/         # Express middleware
  │   ├── auth.ts
  │   └── validation.ts
  ├── auth/               # Auth logic
  │   ├── jwt.ts
  │   └── password.ts
  ├── models/             # Database models (Prisma)
  └── utils/              # Helper functions
      └── errors.ts

  tests/
  ├── auth.test.ts
  ├── applications.test.ts
  └── setup.ts

  prisma/
  ├── schema.prisma       # Database schema
  └── migrations/         # Schema history

  docs/
  ├── SCHEMA.md           # Database design
  └── API.md              # API reference
  ```

  ---

  ## Contributing
  1. Fork the repo
  2. Create a feature branch: `git checkout -b feature/your-feature`
  3. Commit changes: `git commit -am 'Add feature'`
  4. Push: `git push origin feature/your-feature`
  5. Open Pull Request

  ---

  ## Future Features
  - [ ] Email reminders for upcoming interviews
  - [ ] Dashboard with analytics (offers, rejection rate, etc.)
  - [ ] Export applications to CSV
  - [ ] Bulk upload from job board URLs
  - [ ] Interview preparation tips
  - [ ] Salary tracker
  - [ ] Team collaboration

  ---

  ## Troubleshooting

  ### Database Connection Error
  ```
  Error: connect ECONNREFUSED 127.0.0.1:5432
  ```
  Solution: Ensure PostgreSQL is running locally or DATABASE_URL is correct.

  ### JWT Token Expired
  ```
  Error: Invalid or expired token
  ```
  Solution: Login again to get a new token. Tokens expire after 7 days.

  ### Tests Failing
  ```
  npm run test -- --verbose
  ```
  Solution: Check logs for specific failures. Ensure database is set up for tests.

  ---

  ## Performance Metrics

  - **API Response Time:** <200ms (p95)
  - **Database Query Time:** <50ms (typical)
  - **Test Suite:** 2.3s total
  - **Build Time:** 8s

  ---

  ## License
  MIT

  ---

  ## Contact & Support
  - **GitHub Issues:** [Report bugs or request features](https://github.com/yourusername/job-tracker-api/issues)
  - **Email:** your.email@example.com

  ---

  ## Changelog
  See [CHANGELOG.md](CHANGELOG.md) for version history.

  **Last Updated:** April 26, 2026
  ```

### Afternoon (1 hour) — Create Supporting Docs
- [ ] Create `docs/SCHEMA.md` (from Week 3):
  - Your database schema with descriptions

- [ ] Create `CHANGELOG.md`:
  ```markdown
  # Changelog

  ## [1.0.0] - 2026-04-30

  ### Added
  - Initial release
  - JWT authentication
  - Full CRUD for applications
  - Interview tracking
  - Comprehensive test coverage (72%)
  - GitHub Actions CI/CD
  - Live deployment on Render

  ### TODO
  - Email reminders
  - Analytics dashboard
  - CSV export
  ```

- [ ] Commit: `git add README.md docs/ CHANGELOG.md && git commit -m "docs: comprehensive readme + project documentation"`

**Deliverable:** Production-grade README + supporting docs

---

## Day 25 (Thursday) — Technical Blog Post
**Time: 2.5 hours**

### Morning (1.5 hours) — Write Blog Post
- [ ] Create `blog-post.md` (or draft on Medium/Dev.to):
  ```markdown
  # Building a Production-Ready Job Application Tracker API

  ## Introduction
  This project was a deliberate effort to rebuild my backend engineering skills after a 2-year employment gap. I wanted to ship something real—not just follow tutorials. Here's what I learned.

  ## What I Built
  A REST API for tracking job applications, interviews, and job search progress. Features include:
  - JWT authentication
  - Full CRUD operations
  - Interview tracking
  - Pagination + filtering
  - Comprehensive testing (72%+ coverage)
  - CI/CD pipeline
  - Live deployment

  ## Key Technical Decisions

  ### 1. TypeScript + Node.js + Express
  **Why?** Large job market demand, moderate learning curve, and strong ecosystem for building scalable APIs.

  **Trade-off:** Extra compilation step, but worth it for type safety and catching bugs early.

  ### 2. Prisma ORM
  **Why?** Auto-migrations, type-safe queries, and excellent developer experience.

  **Trade-off:** Less control than raw SQL, but much faster to iterate.

  ### 3. Pagination from Day 1
  **Why?** Designing for scale from the beginning is easier than retrofitting later.

  **Example:**
  ```typescript
  GET /api/v1/applications?skip=0&take=10&status=APPLIED
  ```

  ### 4. Testing Strategy
  - Unit tests for auth, utilities
  - Integration tests for API endpoints
  - Database tests with real migrations
  - Target: 70%+ coverage (we achieved 72%)

  **Why?** Tests catch regressions and give confidence to ship.

  ## Lessons Learned

  ### 1. Commit Often
  First commit: Day 1 (scaffold)
  Final count: 50+ commits
  This shows velocity and helps reviewers understand the journey.

  ### 2. Documentation Matters
  A clean README + architecture diagram makes projects 10x more impressive to recruiters.

  ### 3. Deployment is Not Optional
  Local-only code doesn't prove anything. Deployed code proves you can ship.

  ### 4. Tests Enable Iteration
  Tests took extra time upfront but saved time when refactoring and adding features.

  ### 5. Security is Not Afterthought
  JWT, password hashing, input validation—built in from Day 1.

  ## Performance & Scaling

  ### Current State
  - Single server (Render free tier)
  - Single PostgreSQL database
  - <200ms response time
  - 72% test coverage

  ### Future State (at 1M users)
  - Add Redis caching layer
  - Database read replicas
  - API rate limiting
  - Async job queue for background tasks

  ## What's Next?

  This project is my proof of concept for backend engineering. Next steps:
  1. Build a second, more complex project (Event Ticketing System)
  2. Deepen system design knowledge
  3. Practice mock interviews
  4. Network with engineers
  5. Apply to 30+ backend roles

  ## Open Source
  This project is open source: [GitHub Link]

  Feel free to fork, modify, or suggest improvements!

  ---

  **Key Metrics:**
  - Build time: 4 weeks
  - Code: 2,000+ lines
  - Tests: 500+ lines
  - Commits: 50+
  - Deployment: Render (free)
  - Cost: $0

  ---

  If you're also rebuilding after a gap, drop a comment or reach out on Twitter/LinkedIn. Happy to help!
  ```

### Afternoon (1 hour) — Publish + Promote
- [ ] Publish on:
  - Dev.to
  - Medium
  - LinkedIn (link + summary)
  - Twitter/X (short thread)
- [ ] Link from GitHub repo (add to README)
- [ ] Commit: `git add blog-post.md && git commit -m "docs: published technical blog post"`

**Deliverable:** Published technical post (visible to recruiters)

---

## Day 26 (Friday) — Final Applications Push + Project Announcement
**Time: 2.5 hours**

### Morning (1.5 hours) — Tailored Applications (10+)
- [ ] Research 10-15 backend/full-stack roles
- [ ] For each, customize:
  - Resume (highlight relevant bullets)
  - Cover letter (specific reasons for company)
- [ ] Include project link in resume:
  ```
  Portfolio: GitHub.com/yourusername/job-tracker-api (Live: job-tracker-api.render.com)
  ```
- [ ] Apply through company sites preferentially
- [ ] Update `APPLICATIONS.md`

### Afternoon (1 hour) — GitHub + LinkedIn Announcement
- [ ] Push final code to GitHub
- [ ] Create GitHub "Release" (tag v1.0.0):
  ```bash
  git tag -a v1.0.0 -m "Release: Project 1 complete"
  git push origin v1.0.0
  ```
- [ ] Post on LinkedIn:
  ```
  Just shipped my first project rebuilding after a gap! 

  Job Application Tracker API — a production-grade REST API for tracking 
  your job search.

  Tech: TypeScript, Node.js, PostgreSQL, Docker, GitHub Actions
  Deployed: https://job-tracker-api.render.com

  72% test coverage, full CRUD, JWT auth, live CI/CD.

  Building a second project now. 2/2 by end of May.

  Open source: [GitHub Link]
  Blog post: [Blog Link]

  #backend #hiring #opensourcedev
  ```
- [ ] Commit: `git add . && git commit -m "chore: week 4 final push + release"`

**Deliverable:** 10+ applications, GitHub release, public announcement

---

## Day 27 (Saturday) — DSA + System Design
**Time: 2 hours**

### Morning (1 hour) — 2 More DSA Problems
- [ ] Solve 2 medium-hard problems:
  1. Number of Islands (graph/DFS)
  2. Decode Ways (DP)
- [ ] Update `DSA-TRACKER.md`
- [ ] Total for week: 12 problems
- [ ] Commit: `git add dsa-practice/ && git commit -m "feat: week 4 DSA (2 medium-hard problems)"`

### Afternoon (1 hour) — System Design Study
- [ ] Watch: [YouTube System Design Interview](https://www.youtube.com/watch?v=q0KGYwNbMJ0) (1 hour)
- [ ] Notes on key patterns:
  - Sharding
  - Cache invalidation
  - Message queues
  - Database replication

**Deliverable:** 12 total DSA problems (on pace for 48 by week 12)

---

## Day 28 (Sunday) — Weekly Retrospective + Week 5 Planning
**Time: 1.5 hours**

### Morning (45 min) — Final Checks
- [ ] Verify live deployment: `https://your-app.render.com/health`
- [ ] Check GitHub Actions: all tests passing
- [ ] Verify GitHub profile: Project 1 pinned
- [ ] LinkedIn: updated with project link
- [ ] Final commit: `git add . && git commit -m "chore: week 4 complete + project 1 shipped"`

### Afternoon (45 min) — Reflection + Planning
- [ ] Update `PROGRESS.md`:
  ```markdown
  ## Week 4 Metrics
  - DSA problems: 12 total (4 new this week)
  - Commits: 15
  - Applications: 20 total (10 new this week)
  - Project 1: ✅ DEPLOYED
  - Blog posts: 1 published
  - GitHub Actions: ✅ Working
  - Test coverage: 72%+

  ## Week 4 Wins
  - ✅ Project 1 live on Render
  - ✅ CI/CD pipeline working
  - ✅ Comprehensive README + docs
  - ✅ Technical blog post published
  - ✅ 10 applications submitted
  - ✅ GitHub release v1.0.0

  ## Blockers Solved
  - [Any issues and how resolved]

  ## Month 1 Summary (Weeks 1-4)
  - ✅ Rebuilt CS fundamentals
  - ✅ Shipped 1 production project
  - ✅ Solved 12 DSA problems
  - ✅ Published 1 technical post
  - ✅ 20 applications
  - ✅ Resume + LinkedIn + GitHub polished

  ## Month 2 Focus (Weeks 5-8)
  - Build Project 2 (more complex)
  - Reach 40 DSA problems
  - 40+ applications
  - 2 technical posts
  - Start mock interviews
  ```
- [ ] Commit: `git add PROGRESS.md && git commit -m "chore: week 4 retrospective + planning"`

**Deliverable:** Week 4 complete, Project 1 live + documented

---

## Week 4 Checklist Summary
- [x] GitHub Actions CI/CD pipeline configured
- [x] Linting + prettier set up
- [x] Project deployed to Render
- [x] PostgreSQL database in production
- [x] Comprehensive README written
- [x] Supporting docs (SCHEMA, CHANGELOG) created
- [x] Technical blog post published
- [x] 10 tailored applications submitted
- [x] GitHub release v1.0.0 tagged
- [x] LinkedIn announcement posted
- [x] 4 more DSA problems (12 total)
- [x] System design foundations

---

## By End of Week 4, You Should Have:
1. **Project 1 live** on the internet
2. **CI/CD pipeline** automatically testing + deploying
3. **Professional documentation** (README + supporting docs)
4. **Published technical post** (recruiters see you write code)
5. **20 applications** in pipeline (early traction signal)
6. **12 DSA problems** solved (on track for 60)
7. **Portfolio signal** visible across GitHub, LinkedIn, Medium

---

## What Makes Project 1 Stand Out

### For Recruiters
- ✅ Deployed, accessible URL (proof of execution)
- ✅ Tests included (professional standard)
- ✅ CI/CD pipeline (shows you know DevOps)
- ✅ Clean README (shows communication skills)
- ✅ Recent commits (shows active development)

### For Interviewers
- ✅ Can talk about architecture decisions
- ✅ Can explain database schema trade-offs
- ✅ Can discuss performance considerations
- ✅ Can describe scaling challenges
- ✅ Shows full-stack capability (DB → API → Deployment)

---

## Tips for Week 4
- **Deployment is the final exam.** It proves you can ship end-to-end.
- **README is your elevator pitch.** Make it count.
- **Blog post builds authority.** Show your thinking, not just code.
- **GitHub is your portfolio.** Recruiters spend 2 minutes there. Make it count.
- **Celebrate this win.** You shipped something real. That's rare.

---

## Next: Week 5 Preview (Project 2 Begins)
Week 5 you'll start **Project 2** with more complexity:
- More advanced features (caching, background jobs, etc.)
- Better architecture
- Real business logic
- Deeper system design

You'll also start **networking** and **mock interviews**.

**Project 1 is complete. Now ship Project 2. 🚀**

---

## One Month Summary

### What You've Done
- Built and shipped 1 production project
- Published 1 technical post
- Solved 12 DSA problems
- Submitted 20 applications
- Built a professional portfolio presence
- Demonstrated execution + communication

### Market Readiness
You're now in **top 20%** of job applicants in your cohort:
- Most graduates don't ship anything
- Most don't write about their work
- Most don't practice interviews

You're doing all three. Momentum is on your side.

### Confidence Boost
You can now say in interviews: *"I built and shipped a production REST API with tests, CI/CD, and deployment. Here's the live demo."*

That's a conversation starter.

---

**Keep shipping! 🚀 See you in Week 5.**
