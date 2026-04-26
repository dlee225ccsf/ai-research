# Week 5: Project 2 — Scope + Architecture
## Goal: Second project foundation, advanced architecture, system design practice

---

## Day 29 (Monday) — Project 2 Selection + Planning
**Time: 2.5 hours**

### Morning (1.5 hours) — Scope Definition
- [ ] Pick your Project 2 (recommended: **Event Ticketing System** or **Service Booking Platform**)
  - Event Ticketing: Build inventory management, purchase flow, webhooks
  - Service Booking: Calendar-based scheduling, confirmations, cancellations
  - Job Posting: Apply tracking, company profiles, messaging

- [ ] Define MVP (minimum viable product):
  ```markdown
  # Event Ticketing System - MVP

  ## Core Features (Week 5-8)
  1. Event Creation (admin only)
  2. Ticket Inventory Management (limited seats)
  3. Purchase Flow (checkout, payment mock)
  4. Order Confirmation (email notification mock)
  5. Admin Dashboard (view sales)

  ## Advanced Features (Week 6-8)
  1. Real-time inventory updates
  2. Discount codes / promo handling
  3. Webhook notifications
  4. Analytics (revenue, sell-through %)
  5. Refund processing

  ## Database Model
  Event → Tickets → Order → Payment
  ```

- [ ] Create GitHub repo (public, similar scaffold to Project 1)
- [ ] Write `PROJECT-SPEC.md` with requirements
- [ ] Commit: `git add . && git commit -m "chore: project 2 spec + planning"`

### Afternoon (1 hour) — Architecture Design
- [ ] Design database schema (5-6 tables minimum):
  ```
  Event (name, date, capacity, price)
  Ticket (event_id, buyer_id, order_id, status)
  Order (user_id, total, status, created_at)
  Payment (order_id, amount, status, provider)
  PromoCodes (code, discount, max_uses, expires_at)
  User (same as Project 1)
  ```
- [ ] Draw system architecture:
  ```
  Client → API Gateway → Auth → Business Logic → Database
                              ↓
                         Payment Provider (mock)
                              ↓
                         Email Service (mock)
  ```
- [ ] Write in `docs/ARCHITECTURE.md`

**Deliverable:** Clear project scope + database schema + architecture diagram

---

## Day 30 (Tuesday) — Project Scaffold + Advanced Setup
**Time: 2.5 hours**

### Morning (1.5 hours) — Project Skeleton
- [ ] Bootstrap TypeScript + Node + Express (copy from Project 1 or use template):
  ```bash
  npm init -y
  npm install express typescript @types/express cors helmet dotenv
  npm install @prisma/client prisma
  npm install --save-dev ts-node @types/node jest ts-jest supertest
  ```

- [ ] Set up advanced tools (new compared to Project 1):
  ```bash
  npm install bull redis  # Background jobs + caching
  npm install stripe     # Stripe mock (or local mock)
  npm install nodemailer # Email (will use mock)
  ```

- [ ] Folder structure:
  ```
  src/
  ├── app.ts
  ├── routes/
  │   ├── events.ts
  │   ├── orders.ts
  │   ├── payments.ts
  │   └── admin.ts
  ├── services/
  │   ├── eventService.ts
  │   ├── orderService.ts
  │   ├── paymentService.ts
  │   └── emailService.ts
  ├── jobs/
  │   └── emailQueue.ts
  ├── middleware/
  ├── auth/
  └── utils/
  ```

### Afternoon (1 hour) — Prisma Schema Advanced
- [ ] Create `prisma/schema.prisma` with complex relationships:
  ```prisma
  model Event {
    id    String @id @default(cuid())
    name  String
    date  DateTime
    capacity Int
    price Float
    tickets Ticket[]
    promoCodes PromoCode[]
    createdAt DateTime @default(now())
  }

  model Ticket {
    id    String @id @default(cuid())
    eventId String
    event Event @relation(fields: [eventId], references: [id], onDelete: Cascade)
    orderId String?
    order Order? @relation(fields: [orderId], references: [id], onDelete: SetNull)
    status String @default("AVAILABLE") // AVAILABLE, SOLD, RESERVED
    createdAt DateTime @default(now())
  }

  model Order {
    id    String @id @default(cuid())
    userId String
    user User @relation(fields: [userId], references: [id])
    tickets Ticket[]
    total Float
    promoCodeId String?
    promoCode PromoCode? @relation(fields: [promoCodeId], references: [id])
    payment Payment?
    status String @default("PENDING") // PENDING, CONFIRMED, REFUNDED
    createdAt DateTime @default(now())
    updatedAt DateTime @updatedAt
  }

  model Payment {
    id    String @id @default(cuid())
    orderId String @unique
    order Order @relation(fields: [orderId], references: [id], onDelete: Cascade)
    amount Float
    status String @default("PENDING") // PENDING, SUCCESS, FAILED
    provider String @default("STRIPE_MOCK")
    transactionId String?
    createdAt DateTime @default(now())
  }

  model PromoCode {
    id    String @id @default(cuid())
    code  String @unique
    discount Float // percentage or fixed amount
    maxUses Int
    usedCount Int @default(0)
    expiresAt DateTime?
    events Event[]
    orders Order[]
    createdAt DateTime @default(now())
  }

  // User model from Project 1 with relation to orders
  model User {
    id    String @id @default(cuid())
    email String @unique
    passwordHash String
    name  String
    orders Order[]
    createdAt DateTime @default(now())
  }
  ```

- [ ] Commit: `git add . && git commit -m "feat: project 2 scaffold + advanced schema"`

**Deliverable:** Advanced project setup with background jobs + caching structure

---

## Day 31 (Wednesday) — Core Business Logic (Inventory Management)
**Time: 2.5 hours**

### Morning (1.5 hours) — Inventory Service
- [ ] Create `src/services/eventService.ts`:
  ```typescript
  import { PrismaClient } from '@prisma/client';

  const prisma = new PrismaClient();

  export class EventService {
    async createEvent(data: {
      name: string;
      date: Date;
      capacity: number;
      price: number;
    }) {
      return prisma.event.create({
        data,
      });
    }

    async getAvailableTickets(eventId: string) {
      return prisma.ticket.count({
        where: {
          eventId,
          status: 'AVAILABLE',
        },
      });
    }

    async reserveTickets(eventId: string, quantity: number) {
      const available = await this.getAvailableTickets(eventId);
      if (available < quantity) {
        throw new Error('Not enough tickets available');
      }

      // Atomic transaction: mark tickets as reserved
      return prisma.$transaction(
        Array(quantity).fill(null).map(() =>
          prisma.ticket.updateMany({
            where: {
              eventId,
              status: 'AVAILABLE',
            },
            data: {
              status: 'RESERVED',
            },
          })
        )
      );
    }
  }
  ```

### Afternoon (1 hour) — Order Service
- [ ] Create `src/services/orderService.ts`:
  ```typescript
  export class OrderService {
    async createOrder(data: {
      userId: string;
      eventId: string;
      quantity: number;
      promoCodeId?: string;
    }) {
      const { userId, eventId, quantity, promoCodeId } = data;

      // Calculate total with promo
      const event = await prisma.event.findUnique({ where: { id: eventId } });
      let total = event!.price * quantity;

      if (promoCodeId) {
        const promo = await prisma.promoCode.findUnique({ where: { id: promoCodeId } });
        total -= total * (promo!.discount / 100);
      }

      return prisma.order.create({
        data: {
          userId,
          total,
          promoCodeId,
          status: 'PENDING',
        },
      });
    }

    async confirmOrder(orderId: string) {
      return prisma.order.update({
        where: { id: orderId },
        data: { status: 'CONFIRMED' },
      });
    }
  }
  ```

- [ ] Commit: `git add src/services/ && git commit -m "feat: event + order services (business logic)"`

**Deliverable:** Core services with inventory + order logic

---

## Day 32 (Thursday) — API Endpoints (Events + Orders)
**Time: 2.5 hours**

### Morning (1.5 hours) — Event + Order Routes
- [ ] Create `src/routes/events.ts`:
  ```typescript
  import express from 'express';
  import { EventService } from '../services/eventService';
  import { requireAuth } from '../middleware/auth';

  const router = express.Router();
  const eventService = new EventService();

  router.post('/api/v1/events', requireAuth, async (req, res) => {
    const { name, date, capacity, price } = req.body;
    const event = await eventService.createEvent({
      name,
      date: new Date(date),
      capacity,
      price,
    });
    res.status(201).json(event);
  });

  router.get('/api/v1/events/:id', async (req, res) => {
    const event = await prisma.event.findUnique({
      where: { id: req.params.id },
      include: {
        _count: { select: { tickets: true } },
      },
    });
    res.json(event);
  });

  router.get('/api/v1/events/:id/available', async (req, res) => {
    const available = await eventService.getAvailableTickets(req.params.id);
    res.json({ available });
  });

  export default router;
  ```

- [ ] Create `src/routes/orders.ts`:
  ```typescript
  router.post('/api/v1/orders', requireAuth, async (req, res) => {
    const { eventId, quantity, promoCodeId } = req.body;
    const order = await orderService.createOrder({
      userId: req.userId,
      eventId,
      quantity,
      promoCodeId,
    });
    res.status(201).json(order);
  });

  router.get('/api/v1/orders/:id', requireAuth, async (req, res) => {
    const order = await prisma.order.findUnique({
      where: { id: req.params.id },
    });
    res.json(order);
  });
  ```

### Afternoon (1 hour) — Tests for Orders
- [ ] Create `tests/orders.test.ts`:
  ```typescript
  describe('Orders API', () => {
    it('should create an order', async () => {
      const res = await request(app)
        .post('/api/v1/orders')
        .set('Authorization', `Bearer ${token}`)
        .send({ eventId: '123', quantity: 2 });

      expect(res.status).toBe(201);
      expect(res.body.total).toBeGreaterThan(0);
    });
  });
  ```

- [ ] Commit: `git add src/routes/ tests/ && git commit -m "feat: events + orders endpoints + tests"`

**Deliverable:** Event + Order APIs working with tests

---

## Day 33 (Friday) — DSA + Advanced System Design
**Time: 2.5 hours**

### Morning (1.5 hours) — 3 DSA Problems
- [ ] Solve 3 medium problems:
  1. Two Sum II (hash map variant)
  2. Longest Increasing Subsequence (DP)
  3. Course Schedule (graph/topological sort)
- [ ] Update `DSA-TRACKER.md`
- [ ] Total for week: 15 problems (cumulative: 27)
- [ ] Commit: `git add dsa-practice/ && git commit -m "feat: week 5 DSA (3 medium problems)"`

### Afternoon (1 hour) — System Design for Project 2
- [ ] Write in `SYSTEM-DESIGN-NOTES.md`:
  ```markdown
  ## Week 5: Event Ticketing at Scale

  ### Challenges at 1M Users
  - Race condition: 2 users buy last ticket simultaneously
  - Inventory consistency: tickets should never oversell
  - Performance: Event listing page must be <100ms
  - Concurrency: 10K concurrent buyers for hot events

  ### Solutions
  1. **Atomic Transactions** for ticket reservations
  2. **Redis Cache** for hot events
  3. **Inventory Sharding** by event ID
  4. **Queue System** for checkout (peak smoothing)
  5. **CQRS Pattern** for fast reads

  ### Database Indexes
  - CREATE INDEX event_id ON tickets(eventId);
  - CREATE INDEX user_id ON orders(userId);
  - CREATE INDEX status ON tickets(status);
  ```

**Deliverable:** 3 more DSA problems + advanced system design

---

## Day 34 (Saturday) — Job Applications (5) + Project Polish
**Time: 2 hours**

### Morning (1 hour) — Targeted Applications
- [ ] Apply to 5 more roles (focus on startups with ticketing/booking problems)
- [ ] Update `APPLICATIONS.md`
- [ ] Mention Project 1 in resume + tailored bullets

### Afternoon (1 hour) — Code Quality
- [ ] Run tests: `npm test`
- [ ] Ensure linting passes
- [ ] Commit: `git add . && git commit -m "chore: week 5 polish + 5 new applications"`

**Deliverable:** 5 applications, 25 cumulative

---

## Day 35 (Sunday) — Weekly Retrospective
**Time: 1.5 hours**

### Full Day
- [ ] Update `PROGRESS.md`:
  ```markdown
  ## Week 5 Metrics
  - DSA problems: 27 total (3 new)
  - Project 2: Scaffold + core services
  - Applications: 25 total (5 new)
  - Commits: 10

  ## Week 5 Wins
  - ✅ Project 2 architecture designed
  - ✅ Complex schema with relationships
  - ✅ Inventory service built
  - ✅ Order endpoints working

  ## Week 5 Learning
  - [Key insights about advanced backend]
  ```
- [ ] Plan Week 6: Advanced features (caching, background jobs)
- [ ] Commit: `git add PROGRESS.md && git commit -m "chore: week 5 retrospective"`

**Deliverable:** Week 5 complete, 27 DSA problems, Project 2 foundation solid

---

## Week 5 Summary
- ✅ Project 2 scope + architecture defined
- ✅ Advanced scaffold (Bull jobs, Redis)
- ✅ Complex Prisma schema (6 tables, relationships)
- ✅ Business logic (inventory, orders, promo codes)
- ✅ API endpoints (events, orders) + tests
- ✅ 27 total DSA problems
- ✅ 25 applications submitted
- ✅ System design thinking (concurrency, scale)

**Next: Week 6 — Advanced features (caching, webhooks, background jobs)**

---

# Week 6: Advanced Backend Features
## Goal: Project 2 depth, caching, background jobs, 40 DSA problems

---

## Day 36 (Monday) — Redis Caching Layer
**Time: 2.5 hours**

### Morning (1.5 hours) — Cache Implementation
- [ ] Create `src/cache/redisClient.ts`:
  ```typescript
  import redis from 'redis';

  const client = redis.createClient({
    host: process.env.REDIS_HOST || 'localhost',
    port: parseInt(process.env.REDIS_PORT || '6379'),
  });

  export const cacheKey = {
    event: (id: string) => `event:${id}`,
    availableTickets: (id: string) => `tickets:available:${id}`,
  };

  export async function getCache(key: string) {
    const data = await client.get(key);
    return data ? JSON.parse(data) : null;
  }

  export async function setCache(key: string, value: any, ttl = 300) {
    await client.setEx(key, ttl, JSON.stringify(value));
  }

  export async function invalidateCache(key: string) {
    await client.del(key);
  }
  ```

- [ ] Update event routes to use cache:
  ```typescript
  router.get('/api/v1/events/:id', async (req, res) => {
    const cached = await getCache(cacheKey.event(req.params.id));
    if (cached) return res.json(cached);

    const event = await prisma.event.findUnique({
      where: { id: req.params.id },
    });

    await setCache(cacheKey.event(req.params.id), event);
    res.json(event);
  });
  ```

### Afternoon (1 hour) — Test Cache
- [ ] Add cache tests:
  ```typescript
  describe('Cache', () => {
    it('should cache and retrieve event', async () => {
      await setCache('event:123', { id: '123', name: 'Test' });
      const cached = await getCache('event:123');
      expect(cached.name).toBe('Test');
    });
  });
  ```

- [ ] Commit: `git add src/cache/ tests/ && git commit -m "feat: redis caching layer + tests"`

**Deliverable:** Redis caching working, events cached for 5 min

---

## Day 37 (Tuesday) — Background Jobs + Email Queue
**Time: 2.5 hours**

### Morning (1.5 hours) — Bull Job Queue
- [ ] Create `src/jobs/emailQueue.ts`:
  ```typescript
  import Queue from 'bull';
  import nodemailer from 'nodemailer';

  export const emailQueue = new Queue('email', {
    redis: {
      host: process.env.REDIS_HOST || 'localhost',
      port: parseInt(process.env.REDIS_PORT || '6379'),
    },
  });

  // Mock email transporter
  const transporter = nodemailer.createTransport({
    host: 'localhost',
    port: 1025, // MailHog or similar
  });

  emailQueue.process(async (job) => {
    const { to, subject, html } = job.data;
    console.log(`Sending email to ${to}: ${subject}`);
    
    // Mock send
    return { sent: true };
  });

  export async function queueConfirmationEmail(orderId: string, email: string) {
    await emailQueue.add(
      {
        to: email,
        subject: `Order Confirmed: ${orderId}`,
        html: `Your order ${orderId} has been confirmed!`,
      },
      { delay: 1000, attempts: 3 }
    );
  }
  ```

### Afternoon (1 hour) — Integrate with Order Service
- [ ] Update `src/services/orderService.ts`:
  ```typescript
  import { queueConfirmationEmail } from '../jobs/emailQueue';

  async confirmOrder(orderId: string) {
    const order = await prisma.order.update({
      where: { id: orderId },
      data: { status: 'CONFIRMED' },
      include: { user: true },
    });

    // Queue email
    await queueConfirmationEmail(orderId, order.user.email);

    return order;
  }
  ```

- [ ] Commit: `git add src/jobs/ src/services/ && git commit -m "feat: bull job queue + async emails"`

**Deliverable:** Background email queue working, decoupled from API

---

## Day 38 (Wednesday) — Payment Processing (Mock)
**Time: 2.5 hours**

### Morning (1.5 hours) — Stripe Mock Integration
- [ ] Create `src/services/paymentService.ts`:
  ```typescript
  export class PaymentService {
    async processPayment(orderId: string, amount: number) {
      // Mock Stripe call
      const transactionId = `txn_${Date.now()}`;

      const payment = await prisma.payment.create({
        data: {
          orderId,
          amount,
          transactionId,
          status: 'SUCCESS', // In prod: async webhook
        },
      });

      // Confirm order after payment
      await orderService.confirmOrder(orderId);

      return payment;
    }

    async refundPayment(paymentId: string) {
      return prisma.payment.update({
        where: { id: paymentId },
        data: { status: 'REFUNDED' },
      });
    }
  }
  ```

### Afternoon (1 hour) — Payment Endpoints + Tests
- [ ] Create `src/routes/payments.ts`:
  ```typescript
  router.post('/api/v1/orders/:id/pay', requireAuth, async (req, res) => {
    const order = await prisma.order.findUnique({
      where: { id: req.params.id },
    });

    const payment = await paymentService.processPayment(order.id, order.total);
    res.status(201).json(payment);
  });
  ```

- [ ] Add payment tests
- [ ] Commit: `git add src/services/ src/routes/ tests/ && git commit -m "feat: mock payment processing"`

**Deliverable:** Payment service working with order confirmation

---

## Day 39 (Thursday) — Promo Codes + Discounts
**Time: 2.5 hours**

### Morning (1.5 hours) — Promo Code Logic
- [ ] Create `src/services/promoCodeService.ts`:
  ```typescript
  export class PromoCodeService {
    async validatePromoCode(code: string, eventId: string) {
      const promo = await prisma.promoCode.findUnique({
        where: { code },
      });

      if (!promo) throw new Error('Invalid promo code');
      if (promo.expiresAt && promo.expiresAt < new Date()) {
        throw new Error('Promo code expired');
      }
      if (promo.usedCount >= promo.maxUses) {
        throw new Error('Promo code limit reached');
      }

      // Check if valid for this event
      const valid = await prisma.event.findFirst({
        where: {
          id: eventId,
          promoCodes: { some: { id: promo.id } },
        },
      });

      if (!valid) throw new Error('Promo not valid for this event');

      return promo;
    }

    async applyPromoCode(orderId: string, code: string) {
      const promo = await this.validatePromoCode(code, '...');
      
      await prisma.promoCode.update({
        where: { id: promo.id },
        data: { usedCount: promo.usedCount + 1 },
      });

      return promo;
    }
  }
  ```

### Afternoon (1 hour) — Admin Endpoints
- [ ] Create `src/routes/admin.ts`:
  ```typescript
  router.post('/api/v1/admin/promo-codes', requireAdmin, async (req, res) => {
    const { code, discount, maxUses, expiresAt } = req.body;

    const promo = await prisma.promoCode.create({
      data: { code, discount, maxUses, expiresAt },
    });

    res.status(201).json(promo);
  });

  router.get('/api/v1/admin/orders/stats', requireAdmin, async (req, res) => {
    const total = await prisma.order.aggregate({
      _sum: { total: true },
      _count: true,
    });

    res.json(total);
  });
  ```

- [ ] Commit: `git add src/services/ src/routes/ && git commit -m "feat: promo codes + admin endpoints"`

**Deliverable:** Discount system + admin dashboard endpoints

---

## Day 40 (Friday) — DSA + System Design
**Time: 2.5 hours**

### Morning (1.5 hours) — 4 DSA Problems
- [ ] Solve 4 medium-hard problems:
  1. Merge K Sorted Lists (heap/priority queue)
  2. Word Ladder (BFS)
  3. Coin Change (DP)
  4. Serialize/Deserialize Binary Tree (tree traversal)
- [ ] Update `DSA-TRACKER.md`
- [ ] Total: 31 problems (cumulative: 31)
- [ ] Commit: `git add dsa-practice/ && git commit -m "feat: week 6 DSA (4 medium-hard)"`

### Afternoon (1 hour) — Webhook Pattern Study
- [ ] Write in `SYSTEM-DESIGN-NOTES.md`:
  ```markdown
  ## Week 6: Webhooks & Event-Driven Architecture

  ### Problem: Payment confirmation delays
  Traditional flow:
  - POST /pay → Stripe API (slow)
  - If timeout, unclear state

  ### Solution: Webhooks
  - POST /pay → Queue job → Return 202 Accepted
  - Stripe POSTs back to /webhook/payment
  - Confirm order asynchronously
  - Retry on failure

  ### Implementation
  - Endpoint: POST /webhook/payment-confirmed
  - Verify Stripe signature
  - Update order + send email
  - Idempotency: use idempotency key
  ```

**Deliverable:** 4 more DSA problems (31 total, on pace for 60)

---

## Day 41 (Saturday) — 5+ Applications + Networking
**Time: 2 hours**

### Morning (1 hour) — Job Applications
- [ ] Apply to 5-6 backend roles (preferably with payment/ticketing systems)
- [ ] Customize resume + cover letter
- [ ] Update `APPLICATIONS.md`

### Afternoon (1 hour) — Networking
- [ ] Message 3-5 engineers on LinkedIn:
  ```
  "Hi [Name], I noticed you work on [backend/payments] at [Company]. 
  I'm rebuilding my backend engineering skills and working on a ticketing 
  system project. Would love to grab 15 min to learn about your work 
  and how [Company] approaches inventory/payments. Happy to contribute 
  or brainstorm if helpful!"
  ```
- [ ] Update networking tracker
- [ ] Commit: `git add APPLICATIONS.md && git commit -m "docs: 5 new applications + networking"`

**Deliverable:** 30 total applications, 5 networking conversations started

---

## Day 42 (Sunday) — Weekly Retrospective
**Time: 1.5 hours**

### Full Day
- [ ] Update `PROGRESS.md`:
  ```markdown
  ## Week 6 Metrics
  - DSA: 31 total (4 new)
  - Caching (Redis) working
  - Background jobs (Bull) working
  - Payment service working
  - Promo codes + admin endpoints
  - Applications: 30 total (5 new)
  - Networking outreaches: 5

  ## Week 6 Wins
  - ✅ Advanced caching implemented
  - ✅ Background job queue working
  - ✅ Payment processing (mock) functional
  - ✅ Promo system complete

  ## Week 6 Learning
  - Job queues decouple systems
  - Cache invalidation is hard
  - Admin APIs are second-class citizens (easy to neglect)
  ```
- [ ] Commit: `git add PROGRESS.md && git commit -m "chore: week 6 retrospective"`

**Deliverable:** Week 6 complete, Project 2 advanced features done, 31 DSA problems

---

## Week 6 Summary
- ✅ Redis caching layer
- ✅ Bull job queue (async email)
- ✅ Payment processing (mock)
- ✅ Promo code system
- ✅ Admin endpoints (stats, promo management)
- ✅ 31 DSA problems
- ✅ 30 applications
- ✅ 5 networking outreaches
- ✅ Webhook pattern study

**Next: Week 7 — Observability, performance, final applications push**

---

# Week 7: Observability + Performance + Applications
## Goal: Production-ready monitoring, optimization, 40 DSA problems, 40+ applications

---

## Day 43 (Monday) — Structured Logging
**Time: 2.5 hours**

### Morning (1.5 hours) — Winston Logger Setup
- [ ] Install:
  ```bash
  npm install winston pino
  ```

- [ ] Create `src/logger/index.ts`:
  ```typescript
  import winston from 'winston';

  const logger = winston.createLogger({
    level: 'info',
    format: winston.format.combine(
      winston.format.timestamp(),
      winston.format.errors({ stack: true }),
      winston.format.json()
    ),
    defaultMeta: { service: 'ticketing-api' },
    transports: [
      new winston.transports.File({ filename: 'error.log', level: 'error' }),
      new winston.transports.File({ filename: 'combined.log' }),
    ],
  });

  if (process.env.NODE_ENV !== 'production') {
    logger.add(new winston.transports.Console({
      format: winston.format.simple(),
    }));
  }

  export default logger;
  ```

### Afternoon (1 hour) — Integrate Logging
- [ ] Middleware in `app.ts`:
  ```typescript
  app.use((req, res, next) => {
    const startTime = Date.now();
    res.on('finish', () => {
      const duration = Date.now() - startTime;
      logger.info({
        method: req.method,
        path: req.path,
        statusCode: res.statusCode,
        duration,
        userId: (req as AuthRequest).userId,
      });
    });
    next();
  });
  ```

- [ ] Log in services:
  ```typescript
  logger.info('Order created', { orderId, userId, total });
  logger.error('Payment failed', { orderId, error });
  ```

- [ ] Commit: `git add src/logger/ && git commit -m "feat: structured logging (winston)"`

**Deliverable:** All requests logged with context + errors tracked

---

## Day 44 (Tuesday) — Error Tracking + Sentry Mock
**Time: 2.5 hours**

### Morning (1.5 hours) — Centralized Error Handler
- [ ] Update `src/utils/errors.ts`:
  ```typescript
  export class AppError extends Error {
    constructor(
      public message: string,
      public statusCode: number = 500,
      public code?: string
    ) {
      super(message);
    }
  }

  // Error handler middleware
  export const errorHandler = (
    err: any,
    req: express.Request,
    res: express.Response,
    next: express.NextFunction
  ) => {
    const statusCode = err.statusCode || 500;
    const message = err.message || 'Internal Server Error';

    // Log error with context
    logger.error({
      message,
      statusCode,
      path: req.path,
      method: req.method,
      stack: err.stack,
      requestId: req.headers['x-request-id'],
    });

    // Send response
    res.status(statusCode).json({
      error: message,
      code: err.code || 'INTERNAL_ERROR',
      requestId: req.headers['x-request-id'],
    });
  };
  ```

### Afternoon (1 hour) — Performance Metrics
- [ ] Add performance monitoring:
  ```typescript
  export const trackMetric = (metricName: string, duration: number, tags?: any) => {
    logger.info({
      type: 'metric',
      name: metricName,
      duration,
      tags,
    });
  };
  ```

- [ ] Use in services:
  ```typescript
  const start = Date.now();
  const result = await processOrder(orderId);
  trackMetric('order_processing', Date.now() - start);
  ```

- [ ] Commit: `git add src/utils/ && git commit -m "feat: centralized error handling + metrics"`

**Deliverable:** All errors logged, metrics tracked

---

## Day 45 (Wednesday) — Database Query Optimization
**Time: 2.5 hours**

### Morning (1.5 hours) — N+1 Query Prevention
- [ ] Find and fix N+1 queries in orders endpoint:
  ```typescript
  // ❌ Bad: N+1 queries
  const orders = await prisma.order.findMany({ where: { userId } });
  for (const order of orders) {
    order.payment = await prisma.payment.findFirst({
      where: { orderId: order.id },
    });
  }

  // ✅ Good: One query with include
  const orders = await prisma.order.findMany({
    where: { userId },
    include: { payment: true, user: true, promoCode: true },
  });
  ```

- [ ] Add indexes to schema:
  ```prisma
  model Order {
    // ... fields
    @@index([userId])
    @@index([status])
    @@index([createdAt])
  }
  ```

- [ ] Run migration: `npx prisma migrate dev --name add_indexes`

### Afternoon (1 hour) — Query Performance Tests
- [ ] Test query performance:
  ```typescript
  describe('Query Performance', () => {
    it('should get orders in <50ms', async () => {
      const start = Date.now();
      await prisma.order.findMany({
        where: { userId: 'test' },
        include: { payment: true },
        take: 10,
      });
      const duration = Date.now() - start;
      expect(duration).toBeLessThan(50);
    });
  });
  ```

- [ ] Commit: `git add prisma/ tests/ && git commit -m "feat: database optimization + indexes"`

**Deliverable:** N+1 queries fixed, database indexes added

---

## Day 46 (Thursday) — API Rate Limiting + Security
**Time: 2.5 hours**

### Morning (1.5 hours) — Rate Limiting
- [ ] Install:
  ```bash
  npm install express-rate-limit
  ```

- [ ] Create `src/middleware/rateLimiter.ts`:
  ```typescript
  import rateLimit from 'express-rate-limit';

  export const generalLimiter = rateLimit({
    windowMs: 15 * 60 * 1000, // 15 minutes
    max: 100, // limit each IP to 100 requests per windowMs
    message: 'Too many requests from this IP',
  });

  export const authLimiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 5, // limit login attempts
  });

  export const checkoutLimiter = rateLimit({
    windowMs: 1 * 60 * 1000, // 1 minute
    max: 3, // max 3 orders per minute (prevent abuse)
  });
  ```

- [ ] Use in routes:
  ```typescript
  app.use(generalLimiter);
  app.post('/api/v1/auth/login', authLimiter, ...);
  app.post('/api/v1/orders', checkoutLimiter, ...);
  ```

### Afternoon (1 hour) — Security Headers + CORS
- [ ] Already have helmet, but add specific headers:
  ```typescript
  app.use(helmet({
    hsts: { maxAge: 31536000, includeSubDomains: true },
    contentSecurityPolicy: {
      directives: {
        defaultSrc: ["'self'"],
        styleSrc: ["'self'", "'unsafe-inline'"],
      },
    },
  }));
  ```

- [ ] Configure CORS strictly:
  ```typescript
  app.use(cors({
    origin: process.env.CORS_ORIGIN || 'http://localhost:3000',
    credentials: true,
  }));
  ```

- [ ] Commit: `git add src/middleware/ && git commit -m "feat: rate limiting + security headers"`

**Deliverable:** Rate limiting + security hardened

---

## Day 47 (Friday) — DSA + Application Blitz
**Time: 2.5 hours**

### Morning (1.5 hours) — 3 More DSA Problems
- [ ] Solve 3 hard problems:
  1. Median of Two Sorted Arrays (binary search)
  2. Trap Rain Water (two pointer/DP)
  3. LRU Cache (hash map + linked list)
- [ ] Total: 34 problems
- [ ] Commit: `git add dsa-practice/ && git commit -m "feat: week 7 DSA (3 hard)"`

### Afternoon (1 hour) — Application Push
- [ ] Apply to 10 roles (focus: payment/ticketing companies)
- [ ] Mention Project 1 in resume
- [ ] Reference Project 2 progress (coming in 1 week)
- [ ] Update `APPLICATIONS.md`

**Deliverable:** 34 DSA problems, 40 total applications

---

## Day 48 (Saturday) — Project Polish + Networking
**Time: 2 hours**

### Morning (1 hour) — Code Quality
- [ ] Final test run: `npm test`
- [ ] Coverage report: target 75%+
- [ ] Fix any failing tests
- [ ] Final commit: `git add . && git commit -m "chore: week 7 polish + test coverage 75%"`

### Afternoon (1 hour) — Networking Push
- [ ] Send 5 more LinkedIn messages (engineers at companies you applied to)
- [ ] Schedule 2 coffee chats
- [ ] Track in networking spreadsheet

**Deliverable:** Networking gaining traction

---

## Day 49 (Sunday) — Weekly Retrospective
**Time: 1.5 hours**

### Full Day
- [ ] Update `PROGRESS.md`:
  ```markdown
  ## Week 7 Metrics
  - DSA: 34 total (3 new)
  - Structured logging (Winston) ✅
  - Error tracking ✅
  - Database optimized (indexes, N+1 fixed)
  - Rate limiting ✅
  - Security hardened ✅
  - Applications: 40 total (10 new)
  - Networking: 10 outreaches

  ## Week 7 Wins
  - ✅ Production-grade observability
  - ✅ Performance optimized
  - ✅ Security hardened
  - ✅ 40 applications reached

  ## Milestone: 40 Applications
  We've now submitted 40 applications. Law of large numbers: expect 2-4 interviews soon.
  ```
- [ ] Commit: `git add PROGRESS.md && git commit -m "chore: week 7 retrospective"`

**Deliverable:** Week 7 complete, 40 applications, Project 2 production-ready

---

## Week 7 Summary
- ✅ Structured logging (Winston)
- ✅ Centralized error tracking
- ✅ Database query optimization
- ✅ N+1 queries fixed
- ✅ Rate limiting implemented
- ✅ Security headers hardened
- ✅ 34 DSA problems
- ✅ 40 total applications (major milestone)
- ✅ 10+ networking outreaches

**Next: Week 8 — Deploy Project 2, interview prep intensive, final polish**

---

# Week 8: Project 2 Deployment + Final Polish
## Goal: Ship Project 2, deploy with CI/CD, 40 DSA problems complete, interview prep

---

## Day 50 (Monday) — Deploy Project 2
**Time: 2.5 hours**

### Morning (1.5 hours) — GitHub Actions for Project 2
- [ ] Copy CI/CD from Project 1, customize for Project 2
- [ ] Add `SERVICE_ID` and `API_KEY` to secrets
- [ ] Test deploy: merge to main, verify GitHub Actions runs
- [ ] Verify API is live: `https://ticketing-api.render.com/health`

### Afternoon (1 hour) — Database Setup in Production
- [ ] Create PostgreSQL database (Supabase or Render)
- [ ] Run migrations: `npx prisma migrate deploy`
- [ ] Seed admin data (sample events)
- [ ] Verify database connections

**Deliverable:** Project 2 deployed and live

---

## Day 51 (Tuesday) — Project 2 README + Blog Post
**Time: 2.5 hours**

### Morning (1.5 hours) — Production README
- [ ] Write comprehensive README:
  ```markdown
  # Event Ticketing System API

  Production-grade API for managing events, tickets, and orders.

  Features:
  - Event management
  - Inventory tracking (prevent overselling)
  - Order processing with payment
  - Promo code discounts
  - Admin analytics dashboard
  - Background job queue (email notifications)
  - Redis caching
  - Comprehensive monitoring (logging + error tracking)
  - Rate limiting + security hardened

  Tech: TypeScript, Node.js, PostgreSQL, Redis, Bull, Docker

  Live: https://ticketing-api.render.com

  [Same structure as Project 1]
  ```

### Afternoon (1 hour) — Blog Post #2
- [ ] Write and publish:
  ```markdown
  # Building an Event Ticketing System: Lessons in Scale & Concurrency

  This is my second production project, and it taught me about:
  1. Handling race conditions (concurrent ticket purchases)
  2. Caching strategies (Redis for hot events)
  3. Background jobs (async email notifications)
  4. Admin interfaces (often overlooked)
  5. Rate limiting (protecting your API)

  Key decision: Atomic transactions over distributed locks
  Why: Simpler, fewer edge cases, easier to debug

  [Share learnings + code snippets]
  ```

- [ ] Publish on Dev.to + Medium + LinkedIn

**Deliverable:** Project 2 documented + published

---

## Day 52 (Wednesday) — Mock Interview Week 1
**Time: 2.5 hours**

### Morning (1.5 hours) — DSA Mock Interview
- [ ] Set up: 45-minute timer, no notes
- [ ] Solve 1 hard problem under pressure
- [ ] Record yourself explaining approach
- [ ] Review recording afterwards
- [ ] Document mistakes + learnings

### Afternoon (1 hour) — Behavioral Practice
- [ ] Prepare STAR stories:
  1. "Tell me about a time you handled a difficult coworker"
  2. "Describe a project you shipped under deadline"
  3. "What's your biggest technical debt?"
  4. "How do you stay current with tech?"
- [ ] Record yourself answering (1 min each)
- [ ] Review and refine

**Deliverable:** 1 DSA mock + 4 behavioral stories recorded

---

## Day 53 (Thursday) — Mock Interview Week 1 (Continued)
**Time: 2.5 hours**

### Morning (1.5 hours) — System Design Mock
- [ ] Problem: "Design Instagram at scale"
- [ ] Time: 45 minutes
- [ ] Cover: Data model, API design, scaling challenges, caching
- [ ] Record explanation
- [ ] Self-review

### Afternoon (1 hour) — Project Deep-Dive Practice
- [ ] Prepare to explain Project 2 in 10 minutes:
  - Problem statement
  - Architecture decisions
  - Key challenges overcome
  - Trade-offs
- [ ] Record + review

**Deliverable:** System design mock + project deep-dive prepared

---

## Day 54 (Friday) — Final DSA Problems + 15 Applications
**Time: 2.5 hours**

### Morning (1.5 hours) — 6 Final DSA Problems
- [ ] Solve 6 problems (mix of easy-hard):
  1. Merge K Sorted Lists (revisit)
  2. Word Ladder II
  3. Sudoku Solver
  4. Binary Tree Max Path Sum
  5. Regex Pattern Matching
  6. Regular Expression Matcher
- [ ] Total: 40 problems ✅
- [ ] Commit: `git add dsa-practice/ && git commit -m "feat: week 8 DSA complete (40 problems)"`

### Afternoon (1 hour) — Final Application Push
- [ ] Apply to 15 roles (final batch before interview phase)
- [ ] Update `APPLICATIONS.md`
- [ ] Total: 55 applications
- [ ] Commit: `git add APPLICATIONS.md && git commit -m "docs: 55 applications completed"`

**Deliverable:** 40 DSA problems completed, 55 applications submitted

---

## Day 55 (Saturday) — Final Portfolio Polish
**Time: 2 hours**

### Morning (1 hour) — GitHub Profile Final Polish
- [ ] Ensure both projects pinned
- [ ] Update bio: "Backend Engineer | 2 Production Projects | Hiring"
- [ ] Check README in profile: up to date
- [ ] Verify all recent commits visible

### Afternoon (1 hour) — Resume Final Edition
- [ ] Update with both projects:
  ```
  ## Projects
  
  Job Application Tracker | TypeScript, Node.js, PostgreSQL, Docker, GitHub Actions
  - [GitHub] | [Live]
  - JWT auth, full CRUD, 72% test coverage, deployed on Render
  
  Event Ticketing System | TypeScript, Node.js, PostgreSQL, Redis, Bull
  - [GitHub] | [Live]
  - Advanced inventory mgmt, concurrency handling, async queues, 75% test coverage
  ```

- [ ] Commit: `git add Resume.pdf && git commit -m "docs: final resume v2 with both projects"`

**Deliverable:** Portfolio package complete

---

## Day 56 (Sunday) — Month 2 Retrospective + 30/60/90 Plan
**Time: 1.5 hours**

### Full Day
- [ ] Update `PROGRESS.md` final Month 2:
  ```markdown
  ## Month 2 Complete (Weeks 5-8)

  ### Shipped
  - ✅ Project 2 (advanced ticketing system)
  - ✅ 40 DSA problems
  - ✅ 55 total applications
  - ✅ 2 technical blog posts
  - ✅ Production-grade observability
  - ✅ Performance optimized
  - ✅ Security hardened

  ### Metrics
  - Code: 4,000+ lines across 2 projects
  - Tests: 1,000+ lines
  - Blog reach: 500+ views
  - Networking: 15+ outreaches, 2 coffee chats scheduled
  - Applications: 55 submitted, 2-4 interviews likely soon

  ### Confidence Boost
  I can now speak authoritatively about:
  - Inventory management + concurrency
  - Caching strategies (Redis)
  - Background jobs (async processing)
  - Database optimization
  - Rate limiting + security
  - Full deployment pipeline

  ## 30/60/90 Day Plan (If No Offer Yet)

  ### 30 Days (Weeks 9-12)
  - Mock interviews: 8 sessions
  - Final portfolio polish
  - Networking: 20+ outreaches
  - Continue 2-3 applications/week
  - Start 3rd advanced project (optional)

  ### 60 Days (Months 3-4)
  - Interview phase (if callbacks coming)
  - Deepen system design (distributed systems)
  - Contribute to open source (20+ commits)
  - Network at local meetups/conferences
  - 1 more advanced project

  ### 90 Days (Months 4-5)
  - Job offers likely (or close to it)
  - Strong referral network in place
  - Interview muscle memory solid
  - Multiple offers to compare
  - Ready for negotiation

  ### By Day 90
  You'll be top 5% of job seekers in your cohort:
  - 3 production projects shipped
  - 60+ DSA problems mastered
  - 50+ applications with polished story
  - 10+ networking relationships warm
  - Interview-ready confidence
  ```

- [ ] Create `NEXT-STEPS.md`:
  ```markdown
  # Next Steps (Weeks 9-12)

  ## Week 9: Mock Interview Sprint
  - 2 DSA mocks
  - 1 system design mock
  - Behavioral practice
  - Refine "gap" story

  ## Week 10: Interview Prep Deepening
  - 1 DSA + 1 system design + 1 project mock
  - Network: 5 coffee chats
  - Continue applications (2-3/week)

  ## Week 11: Final Interview Push
  - 1 DSA + 1 system design + 1 behavioral mock
  - 5-10 final applications
  - Warm referral pushes

  ## Week 12: Celebrate + Plan Next
  - Expect interviews/offers by now
  - If not hired, 3rd project or open source
  - Evaluate offers
  - Plan negotiation strategy
  ```

- [ ] Commit: `git add PROGRESS.md NEXT-STEPS.md && git commit -m "chore: month 2 retrospective + 30/60/90 plan"`

**Deliverable:** Month 2 complete, 55 applications, all interview prep ready

---

## Week 8 Summary
- ✅ Project 2 deployed (live)
- ✅ Production README + blog post
- ✅ 1 DSA mock interview
- ✅ 1 system design mock
- ✅ 1 behavioral + project deep-dive practiced
- ✅ 40 DSA problems completed
- ✅ 55 total applications (major milestone)
- ✅ Portfolio package complete

---

## End of Month 2 Status

### What You've Accomplished
- 2 production projects deployed
- 40 DSA problems mastered
- 55 applications submitted
- 2 technical blog posts published
- 15+ networking relationships
- Full interview pipeline ready
- Production observability + security
- Database optimization + caching
- Background job processing

### Market Readiness Assessment
You're now in **top 5%** of job applicants:
- Most don't ship 2 projects (you have)
- Most don't publish technical writing (you did)
- Most aren't networked (you are)
- Most haven't practiced interviews (you have)
- Most can't explain architecture (you can)

### What To Expect Next
- Week 9-10: Interviews likely starting
- Week 11-12: Potential offers
- If not hired yet, very close (3rd project will seal it)

**You're ready. Time to interview. 🎉**

---

**Weeks 5-8 complete. See you in Week 9 (interview phase)!**
