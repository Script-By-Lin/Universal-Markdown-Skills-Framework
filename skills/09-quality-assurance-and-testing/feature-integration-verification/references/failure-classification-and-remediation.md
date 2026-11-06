# Failure Classification and Remediation Guide (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `feature-integration-verification`  
> Domain: 09 — Quality Assurance & Testing  

---

## 1. Overview
This reference asset codifies the canonical 11-category failure taxonomy for feature integration breakdowns. It provides concrete examples, root-cause diagnostics, reproduction templates, and targeted surgical remediation strategies for each failure class.

---

## 2. The 11 Canonical Failure Categories

| Code | Failure Class | Typical Root Cause | Impact Scope |
|---|---|---|---|
| `CONNECTION_FAILURE` | Service / Endpoint Unreachable | Wrong port, DNS misconfiguration, CORS header rejection, offline daemon. | Complete service breakdown. |
| `API_CONTRACT_MISMATCH` | Request/Response Schema Discrepancy | Mismatched field names, wrong casing (`userId` vs `user_id`), unexpected wrapper object. | Broken UI rendering or HTTP 400/422. |
| `DATA_INCONSISTENCY` | Database vs In-Memory Mismatch | Unsaved state, non-atomic updates, missing transaction rollback, unsynchronized cache. | Corrupted state or stale data. |
| `AUTHENTICATION_FAILURE` | Credential / Token Extraction Failure | Expired JWT, missing cookie attributes (`SameSite=None`), omitted `Authorization` header. | HTTP 401 Unauthorized loops. |
| `AUTHORIZATION_FAILURE` | Permission / Tenant Boundary Breach | Missing RBAC check, object-level authorization omission (BOLA/IDOR), tenant leak. | HTTP 403 or data leakage. |
| `BUSINESS_LOGIC_FAILURE` | Flawed Domain Rule Execution | Calculation error, wrong state transition, unhandled business constraint. | Invalid business output. |
| `STATE_SYNCHRONIZATION_FAILURE` | Frontend Cache / Store Out of Sync | Missing cache invalidation, unobserved reactivity, stale optimistic update. | UI displays old state after save. |
| `DEPENDENCY_FAILURE` | Missing or Broken Upstream Service | Downstream API timeout, unseeded database lookup table, missing environment variable. | HTTP 500 / 502 / 504 errors. |
| `ERROR_HANDLING_FAILURE` | Uncaught Exception / Blank Screen | Missing try/catch, unhandled Promise rejection, undefined object access in UI template. | Crashed UI or silent server exit. |
| `REGRESSION` | Pre-existing Functionality Broken | Side-effect in shared component or table schema modification breaking older feature. | Pre-existing tests fail. |
| `UNVERIFIED_INTEGRATION` | Untested / Assumed Working Boundary | Implementation claims completion without running end-to-end integration tests. | Unknown operational reliability. |

---

## 3. Detailed Failure Profiles & Surgical Remediation

### 3.1 `API_CONTRACT_MISMATCH`
- **Symptom**: Frontend displays empty list or `undefined` for fields; backend logs indicate schema validation error (HTTP 422).
- **Reproduction**:
  1. Inspect network tab / HTTP payload: Frontend sends `{ filterType: "active" }`.
  2. Backend validator expects: `{ type: "active" }`.
- **Surgical Remediation**:
  1. Determine authoritative contract source (OpenAPI spec or backend Zod/Pydantic schema).
  2. Align client API request model to match server contract.
  3. Author contract integration test verifying serializer and deserializer compatibility.

---

### 3.2 `STATE_SYNCHRONIZATION_FAILURE`
- **Symptom**: User updates a profile name, backend saves to DB successfully (HTTP 200), but UI continues displaying old profile name until a hard browser refresh.
- **Reproduction**:
  1. Trigger mutation via UI.
  2. Verify DB query reflects updated value.
  3. Inspect frontend store: query cache was not invalidated or optimistic update was overwritten with stale local cache.
- **Surgical Remediation**:
  1. Add explicit cache invalidation trigger (e.g. `queryClient.invalidateQueries(['userProfile'])`).
  2. Ensure mutation response payload is written directly into local store state.
  3. Author end-to-end component test asserting UI re-render upon successful mutation response.

---

### 3.3 `DATA_INCONSISTENCY`
- **Symptom**: Payment succeeds at external gateway, but order status remains `pending_payment` in application database.
- **Reproduction**:
  1. Simulate webhook from payment provider with payload `status: "succeeded"`.
  2. Backend webhook endpoint returns HTTP 200, but database record is unchanged due to an unhandled exception in post-payment email dispatch.
- **Surgical Remediation**:
  1. Separate payment state persistence from non-critical notifications (email, analytics).
  2. Wrap database status transition in an isolated atomic transaction.
  3. Author integration test verifying order state transitions to `paid` even if secondary notifications fail.

---

### 3.4 `CONNECTION_FAILURE` (CORS or Transport Rejection)
- **Symptom**: Browser console logs `Access to fetch at 'http://localhost:4000/api' has been blocked by CORS policy`.
- **Reproduction**: Inspect pre-flight `OPTIONS` request; backend does not return `Access-Control-Allow-Origin: http://localhost:3000`.
- **Surgical Remediation**:
  1. Configure CORS middleware with explicit allowed origin whitelist.
  2. Do NOT use `Access-Control-Allow-Origin: *` if credentials/cookies are included.
  3. Test pre-flight request with curl: `curl -I -X OPTIONS http://localhost:4000/api -H "Origin: http://localhost:3000"`.

