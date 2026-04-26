# Feature Spec Template
Last Updated: April 26, 2026

Use this before writing code. Keep it short and concrete.

---

## 1) Feature Summary
- Feature name:
- Owner:
- Status: Draft | In Progress | Done
- Target date:

## 2) Problem and Outcome
- Problem statement:
- Why now:
- Desired outcome:

## 3) User Story
As a <user type>, I want to <action> so that <benefit>.

## 4) Scope
### In scope
- 
- 

### Out of scope
- 
- 

## 5) API Contract
- Endpoint:
- Method:
- Auth required: Yes | No
- Request body:
```json
{}
```
- Success response:
```json
{}
```
- Error responses:
  - 400:
  - 401:
  - 403:
  - 404:
  - 409:
  - 500:

## 6) Validation and Authorization Rules
### Validation
- 
- 

### Authorization
- 
- 

## 7) Data Model and Side Effects
- Tables/models touched:
- Fields added or changed:
- Migrations needed: Yes | No
- Side effects (queue, webhook, email, cache):

## 8) Acceptance Criteria
- [ ]
- [ ]
- [ ]

## 9) Failure and Edge Cases
- 
- 
- 

## 10) Non-Functional Targets
- p95 latency target:
- Logging requirements:
- Metrics to emit:
- Rate limits:
- Security constraints:

## 11) Test Mapping
Map each acceptance criterion to at least one test.

- AC-1 -> Test:
- AC-2 -> Test:
- AC-3 -> Test:

## 12) Rollout Plan
- Release strategy: feature flag | direct release
- Backward compatibility notes:
- Rollback plan:

## 13) Observability
- Dashboard/queries to monitor:
- Alert conditions:

## 14) Sign-off
- Engineering:
- QA/self-test:
- Date:
