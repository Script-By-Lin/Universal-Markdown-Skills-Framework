---
name: canary-watch
description: Use this skill to monitor and verify a deployed URL after releases — checks HTTP endpoints, SSE streams, static assets, console errors, and performance regressions after deploys, merges, or dependency upgrades. Smoke / canary / post-deploy verification.
metadata:
  origin: ECC
version: 1.7.0
---

# Skill: Canary & Post-Deploy Health Verification

> Canonical UMSF Domain Skill Specification adhering to the standard schema.  
> Category: Domain 11 — Reliability & Operations  
> Status: Level 1 MVP-First Active Specification  

---

## 1. Metadata
- **Identifier**: `canary-watch`
- **Category**: Reliability & Operations (Domain 11)
- **Authority**: UMSF Canonical Skill Library (Precedence Level 6)
- **Maintainer**: Universal Markdown Skills Framework
- **Level 3 References**:
  - None (self-contained Level 1 & Level 2 guidance)

---

## 2. MVP Summary (Level 1 Execution Contract)

- **Purpose**: Monitor and verify deployed URLs, HTTP endpoints, SSE streams, and static assets after releases, merges, or upgrades.
- **When to Use**: Smoke testing post-deployment environments, verifying production releases, or validating canary traffic.
- **Essential Invariants**:
  1. Canary verification must check status codes, response times, and console error telemetry.
  2. Automated rollback trigger must be defined if error rates exceed error budget threshold.
  3. Verify both static asset availability (HTTP 200, non-zero bytes) and dynamic API health.
- **Minimal Workflow**:
  1. Execute probe against core deployment endpoints (/healthz, /ready, /api/status).
  2. Verify static bundle integrity, CDN caching headers, and SSL certificate validity.
  3. Inspect error logs and latency histograms during canary traffic ramp.
  4. Render structured Canary Verification Report with pass/fail release verdict.
- **Expected Deliverables**: Canary deployment health report with explicit release approval or rollback recommendation.
- **Critical Restrictions**: Never approve a production release if canary probes return 5xx errors or elevated latency.

> ℹ️ **Progressive Context Loading**:
> For standard engineering tasks, this **Level 1 MVP Summary** provides the complete operational contract.
> If deep procedures, edge case handling, or comprehensive checklists are required, proceed to **Level 2 — Core Instructions** below.

---

## Level 2 — Core Instructions & Deep Procedures

### When to Use

- After deploying to production or staging
- After merging a risky PR
- When you want to verify a fix actually fixed it
- Continuous monitoring during a launch window
- After dependency upgrades

### How It Works

Monitors a deployed URL for regressions. Runs in a loop until stopped or until the watch window expires.

### What It Watches

```
1. HTTP Status — is the page returning 200?
2. Console Errors — new errors that weren't there before?
3. Network Failures — failed API calls, 5xx responses?
4. Performance — LCP/CLS/INP regression vs baseline?
5. Content — did key elements disappear? (h1, nav, footer, CTA)
6. API Health — are critical endpoints responding within SLA?
7. Static Assets — are JS, CSS, image, and font requests returning 2xx/3xx with expected content types?
8. SSE Streams — do event-stream endpoints connect and receive an initial event or heartbeat?
```

### Watch Modes

**Quick check** (default): single pass, report results
```
/canary-watch https://myapp.com
```

**Sustained watch**: check every N minutes for M hours
```
/canary-watch https://myapp.com --interval 5m --duration 2h
```

**Diff mode**: compare staging vs production
```
/canary-watch --compare https://staging.myapp.com https://myapp.com
```

### Alert Thresholds

```yaml
critical:  # immediate alert
  - HTTP status != 200
  - Console error count > 5 (new errors only)
  - LCP > 4s
  - API endpoint returns 5xx
  - Static asset returns 4xx/5xx
  - SSE endpoint cannot connect or drops before first heartbeat

warning:   # flag in report
  - LCP increased > 500ms from baseline
  - CLS > 0.1
  - New console warnings
  - Response time > 2x baseline
  - Static asset content type changed unexpectedly
  - SSE heartbeat latency > 2x baseline

info:      # log only
  - Minor performance variance
  - New network requests (third-party scripts added?)
```

### Notifications

When a critical threshold is crossed:
- Desktop notification (macOS/Linux)
- Optional: Slack/Discord webhook
- Log to `~/.claude/canary-watch.log`

### Output

```markdown
### Canary Report — myapp.com — 2026-03-23 03:15 PST

### Status: HEALTHY ✓

| Check | Result | Baseline | Delta |
|-------|--------|----------|-------|
| HTTP | 200 ✓ | 200 | — |
| Console errors | 0 ✓ | 0 | — |
| LCP | 1.8s ✓ | 1.6s | +200ms |
| CLS | 0.01 ✓ | 0.01 | — |
| API /health | 145ms ✓ | 120ms | +25ms |
| Static assets | 42/42 ✓ | 42/42 | — |
| SSE /events | connected ✓ | connected | +80ms heartbeat |

### No regressions detected. Deploy is clean.
```

### Integration

Pair with:
- `/browser-qa` for pre-deploy verification
- Hooks: add as a PostToolUse hook on `git push` to auto-check after deploys
- CI: run in GitHub Actions after deploy step

---

## Level 3 — Optional References & Supplementary Assets
  - None (self-contained Level 1 & Level 2 guidance)
