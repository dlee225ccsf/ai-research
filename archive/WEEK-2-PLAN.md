# Week 2: API Fundamentals + Authentication
## Goal: Build production-grade REST endpoints, add auth, resume polish, start applications

---

## Day 8 (Monday) — Express Server + Routing Foundation
**Time: 2.5 hours**

### Morning (1.5 hours) — Set Up Express + Middleware
- [ ] Install dependencies:
  ```bash
  npm install express cors helmet dotenv express-validator
  npm install --save-dev @types/express
  ```
- [ ] Create `src/app.ts`:
  ```typescript
  import express from 'express';
  import cors from 'cors';
  import helmet from 'helmet';
  import dotenv from 'dotenv';

  dotenv.config();

  const app = express();
  const PORT = process.env.PORT || 3000;

  // Middleware
  app.use(helmet()); // Security headers
  app.use(cors());
  app.use(express.json());

  // Health check
  app.get('/health', (req, res) => {
    res.json({ status: 'ok', timestamp: new Date().toISOString() });
  });

  // Error handling middleware (placeholder)
  app.use((err: any, req: express.Request, res: express.Response, next: express.NextFunction) => {
    console.error(err);
    res.status(err.status || 500).json({ error: err.message || 'Internal Server Error' });
  });

  app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
  });

  export default app;
  ```
- [ ] Update `package.json` scripts:
  ```json
  "scripts": {
    "start": "node dist/app.js",
    "dev": "ts-node src/app.ts",
    "build": "tsc",
    "lint": "eslint src/"
  }
  ```
- [ ] Test locally: `npm run dev` → visit http://localhost:3000/health

### Afternoon (1 hour) — Basic Route Structure
- [ ] Create `src/routes/index.ts`:
  ```typescript
  import express from 'express';

  const router = express.Router();

  router.get('/api/v1/status', (req, res) => {
    res.json({ message: 'API v1 ready' });
  });

  export default router;
  ```
- [ ] Mount in `app.ts`: `app.use(router);`
- [ ] Commit: `git add . && git commit -m "feat: express server setup with middleware"`

**Deliverable:** Express server running locally with health check + basic routes

---

## Day 9 (Tuesday) — Request Validation + Error Handling
**Time: 2.5 hours**

### Morning (1.5 hours) — Validation Middleware
- [ ] Create `src/middleware/validation.ts`:
  ```typescript
  import { body, validationResult, ValidationChain } from 'express-validator';
  import { Request, Response, NextFunction } from 'express';

  // Reusable validators
  export const validateEmail = () => body('email').isEmail().normalizeEmail();
  export const validatePassword = () => body('password').isLength({ min: 8 }).withMessage('Password must be at least 8 characters');
  export const validateRequired = (field: string) => body(field).notEmpty().withMessage(`${field} is required`);

  // Middleware to check validation results
  export const handleValidationErrors = (req: Request, res: Response, next: NextFunction) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    next();
  };

  // Example: Sign-up validation chain
  export const validateSignUp = [
    validateRequired('name'),
    validateEmail(),
    validatePassword(),
    handleValidationErrors,
  ];
  ```

### Afternoon (1 hour) — Centralized Error Handling
- [ ] Create `src/utils/errors.ts`:
  ```typescript
  export class AppError extends Error {
    constructor(
      public message: string,
      public statusCode: number = 500,
    ) {
      super(message);
      this.name = 'AppError';
    }
  }

  export const asyncHandler = (fn: Function) => (req: any, res: any, next: any) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
  ```
- [ ] Update error middleware in `app.ts`:
  ```typescript
  app.use((err: any, req: express.Request, res: express.Response, next: express.NextFunction) => {
    const statusCode = err.statusCode || 500;
    const message = err.message || 'Internal Server Error';
    res.status(statusCode).json({ error: message, statusCode });
  });
  ```
- [ ] Commit: `git add . && git commit -m "feat: validation + error handling middleware"`

**Deliverable:** Reusable validation + error handling system in place

---

## Day 10 (Wednesday) — Authentication Foundation (JWT)
**Time: 2.5 hours**

### Morning (1.5 hours) — JWT Setup
- [ ] Install dependencies:
  ```bash
  npm install jsonwebtoken bcryptjs
  npm install --save-dev @types/jsonwebtoken @types/bcryptjs
  ```
- [ ] Create `src/auth/jwt.ts`:
  ```typescript
  import jwt from 'jsonwebtoken';

  const JWT_SECRET = process.env.JWT_SECRET || 'your-secret-key-change-in-prod';
  const JWT_EXPIRY = process.env.JWT_EXPIRY || '7d';

  export const generateToken = (userId: string) => {
    return jwt.sign({ userId }, JWT_SECRET, { expiresIn: JWT_EXPIRY });
  };

  export const verifyToken = (token: string) => {
    try {
      return jwt.verify(token, JWT_SECRET) as { userId: string };
    } catch (err) {
      throw new Error('Invalid or expired token');
    }
  };
  ```
- [ ] Create `src/auth/password.ts`:
  ```typescript
  import bcrypt from 'bcryptjs';

  export const hashPassword = async (password: string) => {
    const salt = await bcrypt.genSalt(10);
    return bcrypt.hash(password, salt);
  };

  export const comparePassword = async (password: string, hash: string) => {
    return bcrypt.compare(password, hash);
  };
  ```

### Afternoon (1 hour) — Auth Middleware
- [ ] Create `src/middleware/auth.ts`:
  ```typescript
  import { Request, Response, NextFunction } from 'express';
  import { verifyToken } from '../auth/jwt';
  import { AppError } from '../utils/errors';

  export interface AuthRequest extends Request {
    userId?: string;
  }

  export const requireAuth = (req: AuthRequest, res: Response, next: NextFunction) => {
    const token = req.headers.authorization?.split(' ')[1];
    if (!token) {
      throw new AppError('No token provided', 401);
    }
    const decoded = verifyToken(token);
    req.userId = decoded.userId;
    next();
  };
  ```
- [ ] Update `.env.example`:
  ```
  PORT=3000
  JWT_SECRET=your-super-secret-key
  JWT_EXPIRY=7d
  DATABASE_URL=postgresql://user:password@localhost:5432/mydb
  ```
- [ ] Commit: `git add . && git commit -m "feat: JWT auth + password hashing"`

**Deliverable:** JWT token generation + protected route middleware

---

## Day 11 (Thursday) — Resume Polish + First Draft
**Time: 2.5 hours**

### Morning (1.5 hours) — Resume Formatting
- [ ] Convert `RESUME-v1.md` to `.pdf` using:
  - Option A: Markdown resume template (download from GitHub: `Markdown-Resume`)
  - Option B: Google Docs → PDF export
  - Option C: Online tool like `jsonresume.org`
- [ ] Make sure formatting includes:
  - Clear sections: Summary | Skills | Education | Projects
  - Consistent date formatting
  - Professional font (Calibri, Arial, or Helvetica)
  - 1-page format (tight but readable)

### Afternoon (1 hour) — Portfolio-Ready Bullets
- [ ] Add **Project 1 (In Progress)** bullets to resume:
  ```
  [Job Application Tracker] | Node.js, TypeScript, PostgreSQL
  • Architected RESTful API with JWT authentication and 
    role-based access control
  • Implemented validation layer with 95%+ code coverage via 
    unit + integration tests
  • Deployed containerized application on Render with 
    GitHub Actions CI/CD pipeline
  ```
- [ ] Update GitHub Projects section to mention:
  - "Building 2 production-grade backend projects (GitHub repos public)"
- [ ] Upload PDF resume to GitHub (create `Resume.pdf` in root)
- [ ] Commit: `git add Resume.pdf && git commit -m "docs: resume v1 with project context"`

**Deliverable:** Professional, polished resume + Project 1 positioning

---

## Day 12 (Friday) — First Job Applications
**Time: 2.5 hours**

### Morning (1.5 hours) — Application Setup
- [ ] Create `APPLICATIONS.md` tracker in project root:
  ```markdown
  # Job Application Tracker

  ## Week 2 (Apr 29 - May 5)

  | Date | Company | Role | Status | Follow-up |
  |------|---------|------|--------|-----------|
  | 4/29 | TechCorp | Backend Engineer (Jr) | Applied | - |
  | 4/30 | StartupXYZ | Full-Stack Engineer | Applied | 5/7 |
  | 5/1  | BigTech | SDE II | Rejected | - |

  ## Strategy
  - Target 5 roles this week
  - Mix: 2 startups, 2 mid-size, 1 big tech
  - Tailor resume/cover letter to each role
  ```
- [ ] Research + identify 5 roles:
  - Look on: LinkedIn, AngelList, Wellfound, Indeed, company career pages
  - Filter: "Junior" OR "Entry-level" OR "Associate" backend/full-stack
  - Note: location flexibility (remote preferred)

### Afternoon (1 hour) — Tailored Applications
- [ ] For each role, spend 15-20 min:
  - Read job description, extract 3-5 key skills/tools
  - Tailor resume bullets to match those keywords
  - Write short cover letter (3 paragraphs):
    1. Why this company/role
    2. Relevant skills + portfolio proof
    3. Closing: enthusiasm + next steps
  - Apply via company site or LinkedIn
- [ ] Log each in `APPLICATIONS.md`
- [ ] Commit: `git add APPLICATIONS.md && git commit -m "docs: application tracker + week 2 batch"`

**Deliverable:** 5 applications submitted + tracking system live

---

## Day 13 (Saturday) — DSA + System Design
**Time: 2 hours**

### Morning (1 hour) — 2 More DSA Problems
- [ ] Solve 2 **Medium** problems:
  1. Best Time to Buy and Sell Stock (greedy or DP)
  2. LongestSubstring Without Repeating Characters (sliding window)
- [ ] Document in `DSA-TRACKER.md`
- [ ] Push to GitHub with commit: `git add dsa-practice/ && git commit -m "feat: week 2 DSA (2 medium problems)"`

### Afternoon (1 hour) — System Design Intro
- [ ] Watch: [System Design Primer - YouTube](https://www.youtube.com/watch?v=UzLRB40zFTA) (10 min)
- [ ] Read: [Scale From Zero to Millions](https://www.youtube.com/watch?v=vg5onp8TU6Q) (high level)
- [ ] Document in `SYSTEM-DESIGN-NOTES.md`:
  ```markdown
  # System Design Notes

  ## Key Concepts
  - Vertical vs Horizontal Scaling
  - Load Balancing (round-robin, sticky sessions)
  - Caching (in-memory, CDN, Redis)
  - Databases: SQL vs NoSQL tradeoffs
  - Message Queues (async processing)
  - API Gateway pattern

  ## Next Week
  - Design: "How would you build a job application tracker at scale?"
  ```

**Deliverable:** 2 more DSA problems + system design notebook started

---

## Day 14 (Sunday) — Weekly Catch-Up + Week 2 Retrospective
**Time: 1.5 hours**

### Morning (45 min) — Finish Any Gaps
- [ ] Complete unchecked items from Days 8-13
- [ ] Run tests: `npm run lint` + any unit tests (if started)
- [ ] Verify health check: `npm run dev` → http://localhost:3000/health
- [ ] Final commit: `git add . && git commit -m "chore: week 2 polish + cleanup"`

### Afternoon (45 min) — Reflection + Week 3 Planning
- [ ] Update `PROGRESS.md`:
  ```markdown
  ## Week 2 Metrics
  - DSA problems solved: 5 total (2 new)
  - Project commits: 8
  - Applications: 5
  - Networking outreaches: 0 (plan for week 3)
  
  ## Week 2 Wins
  - Express server + middleware working
  - JWT auth implemented
  - Resume polished + on GitHub
  - First batch of applications out
  
  ## Week 2 Challenges
  - [Note any blockers or learnings]
  
  ## Week 3 Focus
  - Database setup (PostgreSQL + models)
  - CRUD endpoints
  - Testing (unit + integration)
  ```
- [ ] Commit: `git add PROGRESS.md && git commit -m "chore: week 2 retrospective"`

**Deliverable:** Week 2 complete + retrospective logged

---

## Week 2 Checklist Summary
- [x] Express server with middleware
- [x] Request validation system
- [x] Centralized error handling
- [x] JWT authentication
- [x] Password hashing
- [x] Resume polished + PDF
- [x] 5 job applications submitted
- [x] 2 more DSA problems solved
- [x] System design notes started

---

## By End of Week 2, You Should Have:
1. **Production-style Express server** with validation + error handling
2. **JWT auth system** ready for user endpoints
3. **Professional resume + GitHub repo** visible to recruiters
4. **5 applications in the pipeline** (early signal you're serious)
5. **7 DSA problems solved** (on track for 40-60 by week 12)
6. **System design foundation** (will deepen next weeks)

---

## Tips for Week 2 Success
- **Commit daily.** Show recruiter activity (GitHub shows commit streak).
- **Tailor applications.** Generic resumes lose to tailored ones. Spend 20 min per app.
- **Auth is critical.** Get JWT working solid; it'll be in every interview.
- **Test as you go.** Don't write auth, then realize it's broken mid-way.
- **Network early.** Don't wait until job search intensifies. Connect with 1-2 engineers this week on LinkedIn.

---

## Next: Week 3 Preview
Week 3 you'll add the **database layer**:
- PostgreSQL schema design
- ORM setup (TypeORM or Prisma)
- CRUD endpoints (Create, Read, Update, Delete)
- Testing framework (Jest)

Applications will start looking "shipped" — not just "in progress."

**Keep building! 🔥**
