# Week 3: Database Layer + CRUD Endpoints + Testing
## Goal: Database-backed API, comprehensive testing, first project core functionality

---

## Day 15 (Monday) — Database Design + Prisma Setup
**Time: 2.5 hours**

### Morning (1.5 hours) — Schema Design
- [ ] Define your project's data model. Example (Job Application Tracker):
  ```
  User
  - id (UUID, primary key)
  - email (unique)
  - passwordHash
  - name
  - createdAt
  
  Application
  - id (UUID, primary key)
  - userId (foreign key to User)
  - companyName
  - jobTitle
  - jobUrl
  - status (enum: Applied, Interviewing, Rejected, Offered)
  - appliedDate
  - notes
  - createdAt
  - updatedAt
  
  Interview
  - id (UUID, primary key)
  - applicationId (foreign key to Application)
  - interviewDate
  - interviewType (Phone, Technical, Onsite, etc.)
  - notes
  - completed (boolean)
  ```
- [ ] Draw diagram (even ascii):
  ```
  User (1) ──→ (many) Application
  Application (1) ──→ (many) Interview
  ```
- [ ] Document in `docs/SCHEMA.md` in your repo

### Afternoon (1 hour) — Prisma Installation
- [ ] Install Prisma:
  ```bash
  npm install @prisma/client
  npm install --save-dev prisma
  npx prisma init
  ```
- [ ] Update `.env`:
  ```
  DATABASE_URL="postgresql://user:password@localhost:5432/job_tracker"
  ```
- [ ] Create `prisma/schema.prisma`:
  ```prisma
  // This is your Prisma schema file
  datasource db {
    provider = "postgresql"
    url      = env("DATABASE_URL")
  }

  generator client {
    provider = "prisma-client-js"
  }

  model User {
    id    String     @id @default(cuid())
    email String     @unique
    passwordHash String
    name  String
    applications Application[]
    createdAt DateTime @default(now())
    updatedAt DateTime @updatedAt
  }

  model Application {
    id      String     @id @default(cuid())
    userId  String
    user    User       @relation(fields: [userId], references: [id], onDelete: Cascade)
    companyName String
    jobTitle String
    jobUrl  String?
    status  ApplicationStatus @default(APPLIED)
    appliedDate DateTime
    interviews Interview[]
    notes   String?
    createdAt DateTime @default(now())
    updatedAt DateTime @updatedAt
  }

  model Interview {
    id      String     @id @default(cuid())
    applicationId String
    application Application @relation(fields: [applicationId], references: [id], onDelete: Cascade)
    interviewDate DateTime
    interviewType String
    notes   String?
    completed Boolean @default(false)
    createdAt DateTime @default(now())
  }

  enum ApplicationStatus {
    APPLIED
    INTERVIEWING
    REJECTED
    OFFERED
  }
  ```
- [ ] Run migrations:
  ```bash
  # Set up PostgreSQL locally or use cloud DB (Supabase free tier)
  npx prisma migrate dev --name init
  ```
- [ ] Commit: `git add prisma/ .env.example && git commit -m "feat: prisma schema + initial migration"`

**Deliverable:** Prisma schema defined + database migrations running

---

## Day 16 (Tuesday) — Testing Framework Setup (Jest)
**Time: 2.5 hours**

### Morning (1.5 hours) — Jest Installation + Configuration
- [ ] Install Jest:
  ```bash
  npm install --save-dev jest @types/jest ts-jest
  npm install --save-dev supertest @types/supertest
  ```
- [ ] Create `jest.config.js`:
  ```javascript
  module.exports = {
    preset: 'ts-jest',
    testEnvironment: 'node',
    roots: ['<rootDir>/src', '<rootDir>/tests'],
    testMatch: ['**/__tests__/**/*.ts', '**/?(*.)+(spec|test).ts'],
    collectCoverageFrom: [
      'src/**/*.ts',
      '!src/**/*.d.ts',
      '!src/index.ts',
    ],
    coverageThreshold: {
      global: {
        branches: 70,
        functions: 70,
        lines: 70,
        statements: 70,
      },
    },
  };
  ```
- [ ] Create `tests/setup.ts`:
  ```typescript
  import { PrismaClient } from '@prisma/client';

  const prisma = new PrismaClient();

  beforeAll(async () => {
    // Optional: seed test data
  });

  afterAll(async () => {
    await prisma.$disconnect();
  });
  ```
- [ ] Update `package.json`:
  ```json
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage"
  }
  ```

### Afternoon (1 hour) — First Unit Test
- [ ] Create `tests/auth.test.ts`:
  ```typescript
  import { hashPassword, comparePassword } from '../src/auth/password';

  describe('Password Hashing', () => {
    it('should hash a password', async () => {
      const password = 'test-password-123';
      const hash = await hashPassword(password);
      expect(hash).not.toBe(password);
    });

    it('should verify a correct password', async () => {
      const password = 'test-password-123';
      const hash = await hashPassword(password);
      const match = await comparePassword(password, hash);
      expect(match).toBe(true);
    });

    it('should reject incorrect password', async () => {
      const password = 'test-password-123';
      const hash = await hashPassword(password);
      const match = await comparePassword('wrong-password', hash);
      expect(match).toBe(false);
    });
  });
  ```
- [ ] Run tests: `npm test`
- [ ] Commit: `git add jest.config.js tests/ package.json && git commit -m "test: jest setup + password tests"`

**Deliverable:** Jest configured + first test suite passing

---

## Day 17 (Wednesday) — CRUD Endpoints (Create + Read)
**Time: 2.5 hours**

### Morning (1.5 hours) — Create User + Application Endpoints
- [ ] Create `src/routes/applications.ts`:
  ```typescript
  import express, { Request, Response } from 'express';
  import { PrismaClient } from '@prisma/client';
  import { requireAuth, AuthRequest } from '../middleware/auth';
  import { asyncHandler } from '../utils/errors';
  import { body, validationResult } from 'express-validator';

  const router = express.Router();
  const prisma = new PrismaClient();

  // POST /api/v1/applications - Create new application
  router.post(
    '/api/v1/applications',
    requireAuth,
    [
      body('companyName').notEmpty().withMessage('Company name required'),
      body('jobTitle').notEmpty().withMessage('Job title required'),
      body('appliedDate').isISO8601().withMessage('Valid date required'),
    ],
    asyncHandler(async (req: AuthRequest, res: Response) => {
      const errors = validationResult(req);
      if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
      }

      const { companyName, jobTitle, jobUrl, appliedDate, notes } = req.body;

      const application = await prisma.application.create({
        data: {
          userId: req.userId!,
          companyName,
          jobTitle,
          jobUrl,
          appliedDate: new Date(appliedDate),
          notes,
        },
      });

      res.status(201).json(application);
    })
  );

  // GET /api/v1/applications - List user's applications
  router.get(
    '/api/v1/applications',
    requireAuth,
    asyncHandler(async (req: AuthRequest, res: Response) => {
      const { skip = 0, take = 10, status } = req.query;

      const where: any = { userId: req.userId };
      if (status) where.status = status;

      const applications = await prisma.application.findMany({
        where,
        skip: parseInt(skip as string),
        take: parseInt(take as string),
        include: { interviews: true },
        orderBy: { appliedDate: 'desc' },
      });

      res.json(applications);
    })
  );

  // GET /api/v1/applications/:id - Get single application
  router.get(
    '/api/v1/applications/:id',
    requireAuth,
    asyncHandler(async (req: AuthRequest, res: Response) => {
      const { id } = req.params;

      const application = await prisma.application.findUnique({
        where: { id },
        include: { interviews: true },
      });

      if (!application) {
        return res.status(404).json({ error: 'Application not found' });
      }

      if (application.userId !== req.userId) {
        return res.status(403).json({ error: 'Unauthorized' });
      }

      res.json(application);
    })
  );

  export default router;
  ```
- [ ] Mount in `app.ts`: `app.use(applicationsRouter);`

### Afternoon (1 hour) — Integration Test
- [ ] Create `tests/applications.test.ts`:
  ```typescript
  import request from 'supertest';
  import app from '../src/app';
  import { generateToken } from '../src/auth/jwt';

  describe('Applications API', () => {
    const userId = 'test-user-123';
    const token = generateToken(userId);

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

    it('should list applications', async () => {
      const res = await request(app)
        .get('/api/v1/applications')
        .set('Authorization', `Bearer ${token}`);

      expect(res.status).toBe(200);
      expect(Array.isArray(res.body)).toBe(true);
    });
  });
  ```
- [ ] Run: `npm test`
- [ ] Commit: `git add src/routes/ tests/ && git commit -m "feat: applications CRUD + integration tests"`

**Deliverable:** POST/GET endpoints working with integration tests

---

## Day 18 (Thursday) — CRUD Endpoints (Update + Delete) + More Tests
**Time: 2.5 hours**

### Morning (1.5 hours) — Update + Delete Endpoints
- [ ] Add to `src/routes/applications.ts`:
  ```typescript
  // PATCH /api/v1/applications/:id - Update application
  router.patch(
    '/api/v1/applications/:id',
    requireAuth,
    asyncHandler(async (req: AuthRequest, res: Response) => {
      const { id } = req.params;
      const { status, notes } = req.body;

      const application = await prisma.application.findUnique({ where: { id } });
      if (!application || application.userId !== req.userId) {
        return res.status(403).json({ error: 'Unauthorized' });
      }

      const updated = await prisma.application.update({
        where: { id },
        data: {
          ...(status && { status }),
          ...(notes && { notes }),
        },
      });

      res.json(updated);
    })
  );

  // DELETE /api/v1/applications/:id - Delete application
  router.delete(
    '/api/v1/applications/:id',
    requireAuth,
    asyncHandler(async (req: AuthRequest, res: Response) => {
      const { id } = req.params;

      const application = await prisma.application.findUnique({ where: { id } });
      if (!application || application.userId !== req.userId) {
        return res.status(403).json({ error: 'Unauthorized' });
      }

      await prisma.application.delete({ where: { id } });
      res.status(204).send();
    })
  );
  ```

### Afternoon (1 hour) — More Tests + Coverage Report
- [ ] Add to `tests/applications.test.ts`:
  ```typescript
  it('should update an application', async () => {
    // First, create one
    const createRes = await request(app)
      .post('/api/v1/applications')
      .set('Authorization', `Bearer ${token}`)
      .send({ companyName: 'Test', jobTitle: 'Job', appliedDate: new Date().toISOString() });

    const id = createRes.body.id;

    // Then update it
    const updateRes = await request(app)
      .patch(`/api/v1/applications/${id}`)
      .set('Authorization', `Bearer ${token}`)
      .send({ status: 'INTERVIEWING' });

    expect(updateRes.status).toBe(200);
    expect(updateRes.body.status).toBe('INTERVIEWING');
  });

  it('should delete an application', async () => {
    const res = await request(app)
      .delete(`/api/v1/applications/${someId}`)
      .set('Authorization', `Bearer ${token}`);

    expect(res.status).toBe(204);
  });
  ```
- [ ] Run coverage: `npm run test:coverage`
- [ ] Commit: `git add src/ tests/ && git commit -m "feat: full CRUD endpoints + test coverage"`

**Deliverable:** Full CRUD (Create, Read, Update, Delete) working with tests

---

## Day 19 (Friday) — DSA + System Design
**Time: 2.5 hours**

### Morning (1.5 hours) — 2 More DSA Problems (Medium)
- [ ] Solve 2 medium problems:
  1. Longest Repeating Character Replacement (sliding window)
  2. Kth Largest Element in Array (heap/quickselect)
- [ ] Write solutions with explanations
- [ ] Update `DSA-TRACKER.md`
- [ ] Commit: `git add dsa-practice/ && git commit -m "feat: week 3 DSA (2 medium problems)"`

### Afternoon (1 hour) — System Design Practice
- [ ] Write in `SYSTEM-DESIGN-NOTES.md`:
  ```markdown
  ## Week 3: Design Your Project at Scale

  ### Problem: Job Application Tracker at Scale
  - Current: Single server, PostgreSQL, ~100 users
  - Scale: 1 million users, 100K concurrent

  ### Challenges
  1. Database bottleneck: Query applications for 1M users
  2. API latency: Need <200ms response
  3. Storage: 1M users × 100 applications = 100M records

  ### Solutions
  - Add Redis caching for user's applications
  - Pagination (mandatory, not optional)
  - Database indexes on (userId, appliedDate)
  - CDN for static assets
  - Consider sharding if needed

  ### Trade-offs
  - Redis adds complexity, but reduces DB load
  - Pagination improves UX, but more requests
  - Async archival of old records after 6 months
  ```

**Deliverable:** 2 more DSA problems (total 9 in week) + system design notes

---

## Day 20 (Saturday) — Project Polish + 5 More Applications
**Time: 2 hours**

### Morning (1 hour) — Code Polish
- [ ] Fix any failing tests
- [ ] Improve error messages (specific, actionable)
- [ ] Add request logging (use `morgan`):
  ```bash
  npm install morgan
  ```
  ```typescript
  import morgan from 'morgan';
  app.use(morgan('combined'));
  ```
- [ ] Clean up console errors

### Afternoon (1 hour) — More Job Applications
- [ ] Apply to 5 more roles (focus: backend, medium-size companies)
- [ ] Use tailored resume bullets for each
- [ ] Update `APPLICATIONS.md`
- [ ] Commit: `git add APPLICATIONS.md && git commit -m "docs: 5 new applications week 3"`

**Deliverable:** 5 new applications, project cleaner

---

## Day 21 (Sunday) — Weekly Catch-Up + Retrospective
**Time: 1.5 hours**

### Morning (45 min) — Final Gaps
- [ ] Run full test suite: `npm test`
- [ ] Run coverage: `npm run test:coverage` (aim for 70%+)
- [ ] Verify all endpoints work: test locally
- [ ] Final commit: `git add . && git commit -m "chore: week 3 polish + all tests passing"`

### Afternoon (45 min) — Retrospective
- [ ] Update `PROGRESS.md`:
  ```markdown
  ## Week 3 Metrics
  - DSA problems solved: 9 total
  - Commits: 12
  - Applications: 10 total (5 new this week)
  - Test coverage: 72%
  
  ## Week 3 Wins
  - Full CRUD working with database
  - Comprehensive test coverage
  - System design thinking started
  
  ## Week 3 Blockers
  - [Any issues you hit and solved]
  
  ## Week 4 Focus
  - Deployment (GitHub Actions + Render)
  - Production-ready README
  - Technical blog post
  ```
- [ ] Commit: `git add PROGRESS.md && git commit -m "chore: week 3 retrospective"`

**Deliverable:** Week 3 complete, 9 DSA problems, 10 applications, CRUD API fully tested

---

## Week 3 Checklist Summary
- [x] Prisma schema designed + migrations running
- [x] Jest testing framework set up
- [x] CREATE application endpoint + tests
- [x] READ (list + single) endpoints + tests
- [x] UPDATE application endpoint + tests
- [x] DELETE application endpoint + tests
- [x] 9 total DSA problems solved (4 new this week)
- [x] System design notes expanded
- [x] 10 applications submitted (cumulative)
- [x] Code coverage 70%+

---

## By End of Week 3, You Should Have:
1. **Database-backed API** with Prisma migrations
2. **Full CRUD functionality** tested
3. **70%+ test coverage** with Jest
4. **9 DSA problems** solved
5. **10 applications** in the pipeline
6. **System design thinking** initiated
7. **Production-like code quality** (logging, errors, tests)

---

## Tips for Week 3
- **Tests first, then code.** Write test, watch fail, write code to pass.
- **Commit often.** Every endpoint, every test suite.
- **Database is critical.** If migrations fail, everything fails. Verify locally first.
- **Coverage matters.** 70%+ is the bar; aim for critical paths.
- **Pagination is not optional.** Design with it from Day 1.

---

## Next: Week 4 Preview
Week 4 you'll **deploy and document**:
- GitHub Actions CI/CD pipeline
- Live deployment (Render or Railway)
- Production-grade README
- Technical blog post
- Final batch of applications (10+)

Project 1 will be **done** and **public**.

**Keep shipping! 🚀**
