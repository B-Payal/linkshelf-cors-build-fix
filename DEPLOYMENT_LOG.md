# Deployment Checklist

**Application:** <Application Name>  
**Platform:** <Render / Railway / Vercel / etc.>  
**Live URL:** https://<your-live-url>  
**Checklist Completed:** 30 June 2026  
**Engineer:** Payal

| # | Item | Status | Evidence |
|---|------|--------|----------|
| 01 | Environment variables configured on platform | ✅ PASS | `screenshots/01-env-vars-platform.png` |
| 02 | Build passes locally | ✅ PASS | `npm run build` completed successfully (`screenshots/02-local-build.png`) |
| 03 | Build passes in CI | ✅ PASS / ⏭️ SKIP | GitHub Actions run (`screenshots/03-ci-build.png`) or explain why CI is not configured |
| 04 | Database migrations executed | ✅ PASS | Deployment logs showing `prisma migrate deploy` (`screenshots/04-migration-log.png`) |
| 05 | CORS verified | ✅ PASS | Browser Network tab showing successful API requests (`screenshots/05-cors-network-tab.png`) |
| 06 | API base URL correct in production | ✅ PASS | `VITE_API_URL` points to production backend (`screenshots/06-api-url.png`) |
| 07 | Authentication flow tested in production | ✅ PASS | Successful login and protected route (`screenshots/07-auth-production.png`) |
| 08 | Health endpoint responding | ✅ PASS | `GET /health` returned `200 OK` (`screenshots/08-health-endpoint.png`) |
| 09 | No secrets committed to Git | ✅ PASS | `git log` returned no `.env` history and `.gitignore` contains `.env` (`screenshots/09-no-secrets-git.png`) |
| 10 | `.env.example` committed | ✅ PASS | `.env.example` present in repository (`screenshots/10-env-example.png`) |
| 11 | Node version pinned | ✅ PASS | `package.json` contains `engines` field and deployment platform uses same version (`screenshots/11-node-version.png`) |
| 12 | Docker image builds locally | ⏭️ SKIP | Project deployed directly from GitHub to Render. No Dockerfile is used. |

---

## Evidence Summary

### 01. Environment Variables
Verified all required environment variables were configured on the deployment platform.

**Evidence:** `screenshots/01-env-vars-platform.png`

---

### 02. Local Production Build
Executed the production build locally.

```bash
npm run build
```

The build completed successfully without errors.

**Evidence:** `screenshots/02-local-build.png`

---

### 03. Continuous Integration

GitHub Actions successfully built the project.

**Evidence:** `screenshots/03-ci-build.png`

> If CI is not configured, change this item to **SKIP** and explain why.

---

### 04. Database Migration

Production database migrations executed successfully during deployment.

**Evidence:** `screenshots/04-migration-log.png`

---

### 05. CORS Verification

Verified API requests from the deployed frontend completed successfully without CORS errors.

**Evidence:** `screenshots/05-cors-network-tab.png`

---

### 06. Production API URL

Confirmed the frontend communicates with the deployed backend rather than localhost.

**Evidence:** `screenshots/06-api-url.png`

---

### 07. Authentication Flow

Successfully logged into the production application and accessed protected routes.

**Evidence:** `screenshots/07-auth-production.png`

---

### 08. Health Endpoint

Verified the health endpoint returns a successful response.

Example:

```bash
curl https://<your-live-url>/health
```

Response:

```json
{
  "status": "ok",
  "timestamp": "2026-06-30T12:34:56.000Z"
}
```

**Evidence:** `screenshots/08-health-endpoint.png`

---

### 09. Secrets Audit

Executed:

```bash
git log --all --oneline -- .env
git log --all -S "SECRET" --oneline
git log --all -S "API_KEY" --oneline
grep .env .gitignore
```

Verified no secrets have been committed and `.env` is ignored.

**Evidence:** `screenshots/09-no-secrets-git.png`

---

### 10. Environment Example File

Confirmed that `.env.example` exists and documents all required environment variables using placeholder values.

**Evidence:** `screenshots/10-env-example.png`

---

### 11. Node Version

Verified the Node.js version is pinned in `package.json` and matches the deployment environment.

Example:

```json
"engines": {
  "node": ">=18.0.0"
}
```

**Evidence:** `screenshots/11-node-version.png`

---

### 12. Docker

**Status:** SKIP

**Reason:**

This project is deployed directly from GitHub to Render. It does not include a Dockerfile, and the hosting platform manages the build and runtime environment.

---

# Follow-up Tasks

- [ ] Configure GitHub Actions if CI has not been set up.
- [ ] Continue monitoring deployment logs after future releases.
- [ ] Re-run this checklist before every production deployment.

---

# Deployment Summary

- ✅ PASS: 11
- ❌ FAIL: 0
- ⏭️ SKIP: 1

The deployment was successfully verified using the deployment checklist. Environment variables, production build, authentication, CORS, API connectivity, database migrations, health endpoint, Git security, and Node.js configuration were all validated. Docker was intentionally skipped because the application is deployed directly from GitHub to Render without containerization.