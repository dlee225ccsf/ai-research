# ai-research
Research using AI

Primary execution plan:
- [WEEK-1-12-EXECUTION-PLAN-TYPESCRIPT.md](WEEK-1-12-EXECUTION-PLAN-TYPESCRIPT.md)

Language-specific Week 1-12 plans:
- [WEEK-1-12-EXECUTION-PLAN-PYTHON.md](WEEK-1-12-EXECUTION-PLAN-PYTHON.md)
- [WEEK-1-12-EXECUTION-PLAN-JAVA.md](WEEK-1-12-EXECUTION-PLAN-JAVA.md)
- [WEEK-1-12-EXECUTION-PLAN-CPP.md](WEEK-1-12-EXECUTION-PLAN-CPP.md)

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

## Git Push/Auth Fix (403 Permission Denied)

If push fails with a 403 error, your local auth may be tied to the wrong GitHub account or token.

1. Clear token environment variables for current shell:

```bash
unset GITHUB_TOKEN
unset GH_TOKEN
```

2. Clear cached github.com credential from macOS keychain:

```bash
printf "protocol=https\nhost=github.com\n" | git credential-osxkeychain erase
```

3. Re-authenticate GitHub CLI with the correct account:

```bash
gh auth login -h github.com -p https -w
gh auth setup-git
gh auth status -h github.com
```

4. Verify remote and retry push:

```bash
git remote -v
git status -sb
git push
```

5. If it still fails:
- Confirm you are logged into the account that owns the repo, or
- Add your current account as a collaborator, or
- Push to your fork by changing origin URL.
