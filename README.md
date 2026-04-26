# ai-research
Research using AI

Primary execution plans:
- [WEEK-1-4-EXECUTION-PLAN.md](WEEK-1-4-EXECUTION-PLAN.md)
- [WEEK-5-12-EXECUTION-PLAN.md](WEEK-5-12-EXECUTION-PLAN.md)

## Spec-Driven Development Tooling

Starter OpenAPI spec and lint/mock tooling are configured.

- Spec file: [openapi/openapi.yaml](openapi/openapi.yaml)
- Spectral config: [.spectral.yaml](.spectral.yaml)

Install dependencies:

```bash
npm install
```

Lint the API spec:

```bash
npm run spec:lint
```

Run a local mock server:

```bash
npm run spec:mock
```

Mock server URL:

```text
http://127.0.0.1:4010
```
