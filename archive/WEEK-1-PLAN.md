# Week 1: Rebuild Foundations + Ship Project 1
## Goal: Project setup, fundamentals refresh, study tracker, initial DSA practice

---

## Day 1 (Monday) — Project Setup & Stack Commitment
**Time: 2.5 hours**

### Morning (1 hour)
- [ ] Decide project name: e.g., `job-application-tracker` or `service-booking-api`
- [ ] Create GitHub repo (public, good README template)
- [ ] Initialize Node.js + TypeScript
  ```bash
  mkdir project-name && cd project-name
  npm init -y
  npm install --save-dev typescript ts-node @types/node eslint prettier
  npx tsc --init
  git init && git remote add origin <your-repo>
  git add . && git commit -m "Initial commit: TypeScript + Node setup"
  ```
- [ ] Create folder structure:
  ```
  src/
    app.ts
    routes/
    middleware/
    models/
    utils/
  tests/
  .github/workflows/
  docker-compose.yml
  Dockerfile
  .env.example
  ```

### Afternoon (1.5 hours)
- [ ] Write initial README (template):
  - What it does (1-2 sentences)
  - Tech stack
  - Quick start instructions
  - Architecture diagram (ascii or link)
  - Running tests
- [ ] Add `.env.example` with placeholder config
- [ ] First git commit: "chore: project scaffold"
- [ ] Pin this repo on GitHub profile

**Deliverable:** Public GitHub repo with clean scaffold + working local environment

---

## Day 2 (Tuesday) — Core CS Refresh
**Time: 2.5 hours**

### Morning (1.5 hours) — Big-O & Data Structures
- [ ] Quick refresher (30 min):
  - Read: [Big-O Cheatsheet](https://www.bigocheatsheet.com/) (skim)
  - Watch: [Big-O Explained in 5 min](https://www.youtube.com/watch?v=D6xkbJLQDKc)
- [ ] Data structures review (1 hour):
  - Arrays: insertion, lookup, deletion complexity
  - HashMaps: O(1) average, collisions
  - Linked lists, stacks, queues
  - Trees: BST, height, traversal
  - Graphs: adjacency list vs matrix
- [ ] Create study file: `cs-fundamentals.md` with notes

### Afternoon (1 hour) — SQL Basics
- [ ] Install PostgreSQL locally (or use pgAdmin)
- [ ] Basic queries refresher:
  - SELECT, WHERE, JOIN (INNER/LEFT/RIGHT)
  - GROUP BY, aggregates (COUNT, SUM, AVG)
  - Indexes and query performance
  - Transactions, ACID basics
- [ ] Write 5 practice queries in a SQL file

**Deliverable:** `cs-fundamentals.md` + SQL practice queries in project

---

## Day 3 (Wednesday) — DSA Practice Kickoff
**Time: 2.5 hours**

### Morning (1.5 hours) — Problem Solving
- [ ] Pick platform: LeetCode or NeetCode (I recommend NeetCode — curated, shorter)
- [ ] Solve 3 **Easy** problems:
  1. Two Sum (hash map pattern)
  2. Valid Parentheses (stack pattern)
  3. Merge Sorted Array (two-pointer pattern)
- [ ] For each:
  - Write clean solution with comments
  - Explain time/space complexity
  - Save in `dsa-practice/` folder with solution file

### Afternoon (1 hour) — Document & Share
- [ ] Create `DSA-TRACKER.md` in project:
  ```markdown
  # DSA Practice Tracker
  
  ## Week 1
  - [ ] Two Sum (Easy) — Hash Map — O(n) time, O(n) space
  - [ ] Valid Parentheses (Easy) — Stack — O(n) time, O(n) space
  - [ ] Merge Sorted Array (Easy) — Two Pointer — O(n+m) time, O(1) space
  
  ## Week 2
  - [ ] TBD
  ```
- [ ] Push to GitHub with commit: "feat: DSA week 1 setup"

**Deliverable:** 3 solved problems documented in tracking file

---

## Day 4 (Thursday) — Resume Rewrite
**Time: 2.5 hours**

### Morning (1.5 hours) — Content Audit
- [ ] Open your current resume
- [ ] Audit:
  - Remove vague bullets ("worked on projects")
  - Identify quantifiable wins from past internships/projects
  - Remove outdated tech (if any)
  - Keep: relevant skills, graduation date, GPA (if 3.5+)
- [ ] Create new file: `RESUME-v1.md` in project

### Afternoon (1 hour) — Rewrite Core Sections
- [ ] **Professional Summary** (new):
  ```
  Software Engineer with CS degree. Currently building production-grade 
  backend systems in Node.js + TypeScript. Experienced with REST APIs, 
  database design, and testing. Seeking backend role to ship features 
  and systems at scale.
  ```
- [ ] **Skills** section (be specific):
  ```
  Languages: TypeScript, JavaScript, Python, SQL
  Backend: Node.js, Express, PostgreSQL, REST APIs
  Tools: Git, Docker, GitHub Actions, Linux
  Concepts: Data Structures, Algorithms, System Design, ACID
  ```
- [ ] **Education**:
  ```
  B.S. Computer Science | [University] | May 2022
  ```
- [ ] **Projects** (placeholder for Week 4):
  ```
  [Job Application Tracker] | TypeScript, Node.js, PostgreSQL, Docker
  Built production-ready REST API with authentication, testing, and CI/CD...
  ```

**Deliverable:** `RESUME-v1.md` in plain text (will format later)

---

## Day 5 (Friday) — LinkedIn + GitHub Profile Setup
**Time: 2.5 hours**

### Morning (1 hour) — LinkedIn Refresh
- [ ] Update headline:
  ```
  CS Graduate | Backend Engineer | Building APIs & Shipping Products | 
  Hiring Open 🔍
  ```
- [ ] Update About section (100-150 words):
  ```
  Software engineer rebuilding skills and shipping production-quality projects. 
  I'm focused on backend engineering, APIs, and systems design. Currently 
  practicing DSA and building two real-world projects this quarter. Open to 
  conversations about opportunities in backend/full-stack engineering.
  
  Stack: TypeScript, Node.js, PostgreSQL, Docker, GitHub Actions
  ```
- [ ] Add your GitHub link to profile
- [ ] Change profile picture to professional headshot (good lighting, simple background)

### Afternoon (1.5 hours) — GitHub Profile Cleanup
- [ ] Update GitHub bio:
  ```
  Backend Engineer | TypeScript + Node | Open to opportunities
  ```
- [ ] Add profile README (`.github/README.md`):
  ```markdown
  # Hi, I'm [Your Name]
  
  Backend engineer building APIs and systems that scale.
  
  **Current focus:** Rebuilding my skills and shipping production projects.
  
  **Tech:** TypeScript, Node.js, PostgreSQL, Docker, AWS
  
  **Projects:** Check my repos below.
  ```
- [ ] Pin your Week 1 project repo to profile
- [ ] Follow 10-15 engineers/companies you admire

**Deliverable:** Updated LinkedIn + GitHub profile as portfolio signal

---

## Day 6 (Saturday) — Study System Setup
**Time: 1.5 hours**

### Full Day
- [ ] Create tracking system (pick one):
  - **Option A:** Markdown file in project: `PROGRESS.md`
  - **Option B:** Simple Notion/Obsidian setup
  - **Option C:** GitHub Projects board
- [ ] Structure:
  ```
  # 12-Week Progress Tracker
  
  ## Week 1 (Apr 26 - May 2)
  - [x] Day 1: Project setup
  - [x] Day 2: CS fundamentals
  - [x] Day 3: DSA kickoff (3 problems)
  - [x] Day 4: Resume rewrite
  - [x] Day 5: LinkedIn + GitHub
  - [ ] Day 6: Study system
  - [ ] Day 7: Catch-up + review
  
  ## Metrics (Week 1)
  - DSA problems solved: 3/12 target
  - Project commits: 5
  - Applications: 0 (too early)
  
  ## Metrics (Target by Week 12)
  - DSA problems solved: 40-60
  - Projects deployed: 2
  - Applications submitted: 30-40
  - Mock interviews: 8
  - Networking outreaches: 20+
  ```
- [ ] Commit to GitHub
- [ ] Set a recurring weekly review (Friday 3pm)

**Deliverable:** Tracking system live + first week logged

---

## Day 7 (Sunday) — Catch-Up + Review
**Time: 1.5 hours**

### Morning (45 min) — Finish Any Gaps
- [ ] Complete any unchecked items from Days 1-6
- [ ] Push final commits to GitHub
- [ ] Verify all repos/docs public and polished

### Afternoon (45 min) — Weekly Retrospective
- [ ] Answer (write down):
  - What went well this week?
  - What was harder than expected?
  - What will you change next week?
  - Do you feel re-energized? Motivated?
- [ ] Update `PROGRESS.md` with reflection
- [ ] Plan Week 2 kickoff (write outline)
- [ ] Final commit: "chore: week 1 complete + retrospective"

**Deliverable:** Week 1 retrospective logged + ready for Week 2

---

## Week 1 Checklist Summary
- [x] GitHub repo initialized and public
- [x] TypeScript + Node project scaffold
- [x] CS fundamentals refresher
- [x] 3 DSA problems solved
- [x] Resume rewritten (v1)
- [x] LinkedIn headline + About updated
- [x] GitHub profile cleaned up + README added
- [x] Tracking system created
- [x] Progress logged

---

## By End of Week 1, You Should Have:
1. **Public GitHub repo** with clean project structure
2. **3 solved DSA problems** documented
3. **Updated resume** emphasizing "rebuilding skills + shipping"
4. **Professional LinkedIn + GitHub profile** visible and polished
5. **Tracking system** for next 11 weeks
6. **Mental clarity** on the plan and commitment

---

## Tips for Success This Week
- **Consistency > Perfection.** Commit something every day.
- **Public signals matter.** Recruiters check GitHub/LinkedIn; make them impressive.
- **"Gap narrative" is your edge.** You're intentional, not desperate. Show it.
- **No applications yet.** This week is about *getting ready*, not rushing out.
- **Tell someone your plan.** Accountability helps immensely.

---

## Next: Week 2 Preview
Week 2 you'll build the **API foundation** — Express server, validation, error handling, and authentication. Projects start looking "real."

**Go ship it! 🚀**
