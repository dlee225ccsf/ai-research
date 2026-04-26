# Test Plan Template
Last Updated: April 26, 2026

Use this immediately after the feature spec and before implementation.

---

## 1) Test Plan Summary
- Feature:
- Owner:
- Related spec:
- Test status: Not Started | In Progress | Complete

## 2) Test Strategy
- Unit tests:
- Integration tests:
- Contract/API tests:
- End-to-end tests (if applicable):

## 3) Red-Green-Refactor Plan
List failing tests you will write first.

1. Test name:
   - Expected failure reason:
2. Test name:
   - Expected failure reason:
3. Test name:
   - Expected failure reason:

## 4) Test Environment
- Local dependencies:
- Test database setup:
- Seed data:
- Required env vars:

## 5) Test Cases by Category
### Happy Path
- [ ]
- [ ]

### Validation Errors (400)
- [ ] Missing required fields
- [ ] Invalid field formats
- [ ] Boundary values

### Auth/Authz (401/403)
- [ ] No token
- [ ] Invalid token
- [ ] Valid token but unauthorized user

### Resource State and Business Rules
- [ ] Not found (404)
- [ ] Conflict cases (409)
- [ ] Duplicate submission handling

### Failure Handling
- [ ] Downstream dependency failure
- [ ] Timeout/retry behavior
- [ ] Queue/cache/webhook failure path

## 6) Contract Test Cases
- Request/response schema checks:
- Error payload schema checks:
- Backward compatibility checks:

## 7) Non-Functional Tests
- Performance target test (p95):
- Rate-limit behavior:
- Logging and metric assertions:

## 8) Coverage Targets
- Unit coverage target:
- Integration coverage target:
- Critical path fully covered: Yes | No

## 9) Execution Checklist
- [ ] All tests written before implementation
- [ ] Tests fail first (red)
- [ ] Minimum implementation passes tests (green)
- [ ] Refactor completed with tests still green
- [ ] CI passes (lint, test, build)

## 10) Traceability (Spec -> Tests)
- AC-1 -> Test(s):
- AC-2 -> Test(s):
- AC-3 -> Test(s):

## 11) Results and Sign-off
- Test run summary:
- Known gaps:
- Risk level: Low | Medium | High
- Sign-off:
- Date:
