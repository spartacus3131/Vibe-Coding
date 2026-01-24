# Phase 4.5: DevOps Infrastructure

**Set up automated testing and deployment.** 30-60 minutes, huge time savings.

Load this AFTER Phase 4 (Cursor Rules) if you're shipping to production.

---

## WHAT THIS DOES

| Before Phase 4.5 | After Phase 4.5 |
|------------------|-----------------|
| Manually run tests | Tests run automatically on push |
| Manually deploy to staging | Staging deploys automatically |
| Manually deploy to production | One-click production deploy |
| 30-90 min per deployment | 5-10 min per deployment |

---

## THE THREE PILLARS

### 1. Continuous Integration (CI) = Automated Testing
Every push → tests run automatically → notified if fail

### 2. Continuous Deployment (CD) = Automated Deployment
Tests pass → deploy to staging automatically
Manual approval → deploy to production

### 3. Environment Parity
Staging = Production (same database type, same services)
Catch bugs before they hit users.

---

## PLATFORM OPTIONS

| Code Platform | CI/CD Platform | Complexity |
|---------------|----------------|------------|
| GitHub | GitHub Actions | Easy (built-in) |
| GitLab | GitLab CI | Easy (built-in) |
| Any | CircleCI | Medium |

**Recommendation:** GitHub + GitHub Actions

---

## SETUP: GITHUB ACTIONS (30 min)

### Step 1: Create Test Workflow

Create `.github/workflows/test.yml`:

```yaml
name: Test Suite

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: testpass
          POSTGRES_DB: test_db
        ports:
          - 5432:5432
    
    steps:
      - uses: actions/checkout@v4
      
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - run: npm ci
      - run: npm run lint
      - run: npm test
      - run: npm run build
```

### Step 2: Create Staging Deploy Workflow

Create `.github/workflows/deploy-staging.yml`:

```yaml
name: Deploy to Staging

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm test
  
  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      # Choose ONE based on your hosting:
      
      # Vercel
      - run: npx vercel deploy --prod --token ${{ secrets.VERCEL_TOKEN }}
      
      # Railway
      # - run: npx @railway/cli up --token ${{ secrets.RAILWAY_TOKEN }}
      
      # Render
      # - run: curl -X POST ${{ secrets.RENDER_DEPLOY_HOOK }}
```

### Step 3: Create Production Deploy Workflow

Create `.github/workflows/deploy-production.yml`:

```yaml
name: Deploy to Production

on:
  workflow_dispatch:  # Manual trigger only

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm test
  
  deploy:
    needs: test
    runs-on: ubuntu-latest
    environment: production  # Requires approval
    steps:
      - uses: actions/checkout@v4
      - run: npx vercel deploy --prod --token ${{ secrets.VERCEL_TOKEN }}
```

### Step 4: Add GitHub Secrets

Go to: Repository → Settings → Secrets → Actions → New secret

Add:
- `VERCEL_TOKEN` (from vercel.com/account/tokens)
- Any other API keys needed

### Step 5: Enable Manual Approval

Go to: Settings → Environments → New environment "production" → Add required reviewers

---

## HOSTING OPTIONS

| Platform | Best For | Pros |
|----------|----------|------|
| **Vercel** | Next.js, React | Auto-deploys, preview URLs, free tier |
| **Railway** | Full-stack | Simple, good for databases |
| **Render** | Full-stack | Similar to Railway |
| **Supabase** | Edge Functions | If already using Supabase |

**For vibe coders:** Start with Vercel or Railway.

---

## ROLLBACK PROCEDURE

Create `ROLLBACK.md`:

```markdown
# Rollback Procedure

## If Production is Broken

### Option 1: Instant Rollback (30 seconds)
Vercel: Deployments → Previous → "Promote to Production"
Railway: Deploys → Previous → "Rollback"

### Option 2: Revert Commit (2 minutes)
```bash
git revert HEAD
git push origin main
# CI auto-deploys the revert
```

### Option 3: Manual Redeploy
Re-run the last successful workflow from GitHub Actions.

## Preventing Rollbacks

1. Always test in staging first
2. Use feature flags for risky changes
3. Monitor immediately after deploy
```

---

## SMOKE TESTS

Quick tests that verify the app still works after deploy.

Create `tests/smoke.test.js`:

```javascript
describe('Smoke Tests', () => {
  it('can load homepage', async () => {
    const response = await fetch(process.env.APP_URL);
    expect(response.status).toBe(200);
  });
  
  it('can call health endpoint', async () => {
    const response = await fetch(`${process.env.APP_URL}/api/health`);
    const data = await response.json();
    expect(data.status).toBe('healthy');
  });
});
```

Add to deploy workflow:
```yaml
- run: npm run test:smoke
  env:
    APP_URL: ${{ secrets.STAGING_URL }}
```

---

## ERROR TRACKING

Set up monitoring to catch errors in production.

### Sentry (Recommended)

```bash
npm install @sentry/node
```

```javascript
import * as Sentry from "@sentry/node";

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
});
```

Add `SENTRY_DSN` to GitHub secrets.

---

## DAILY WORKFLOW

```
Morning:
  Code feature
  ↓
  Commit and push
  ↓
  Tests run automatically ✓
  ↓
  Staging deploys automatically ✓
  ↓
  Test in staging
  ↓
  Click "Deploy to Production" in GitHub
  ↓
  Production deploys ✓
  ↓
  Done!
```

---

## TROUBLESHOOTING

| Problem | Solution |
|---------|----------|
| Tests fail in CI but pass locally | Check Node version, use same as CI |
| Deployment hangs | Check logs, increase timeout |
| Staging works but production broken | Check environment variables |
| Can't find secrets | Repository → Settings → Secrets |

---

## COMPLETION CHECKLIST

- [ ] `.github/workflows/test.yml` created
- [ ] `.github/workflows/deploy-staging.yml` created
- [ ] `.github/workflows/deploy-production.yml` created
- [ ] GitHub secrets added (tokens, API keys)
- [ ] Production environment requires approval
- [ ] `ROLLBACK.md` documented
- [ ] Smoke tests created
- [ ] Error tracking set up (Sentry)
- [ ] Tested: push → tests run → staging deploys

---

## NEXT STEP

"CI/CD ready. Now build features. Load `pm-phase-5-building.md`."
