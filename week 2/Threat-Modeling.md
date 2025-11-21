cat > Threat-Modeling.md <<'MD'
# Threat Modeling — OWASP Juice Shop (v19.1.1) — STRIDE + PASTA

## 1. App Overview
- Name: OWASP Juice Shop
- Version: 19.1.1 (example)
- Components: frontend (web UI), backend API, database, auth system, payments simulation

## 2. Assets
- User credentials and profiles
- Payment / card-like data (simulated)
- Product data and prices
- Admin functions

## 3. High-level Data Flow (short)
- User -> Web UI -> API -> Database
- Admin -> Admin UI -> API -> Database

## 4. Threat Model Methodologies
- STRIDE used to identify threats (Spoofing, Tampering, Repudiation, Info disclosure, DoS, Elevation)
- PASTA used for risk analysis & attack simulation (high-level)

## 5. STRIDE Findings (examples)
### Spoofing
- **Threat**: Credential stuffing or SQLi to bypass auth  
- **Impact**: Account takeover  
- **Controls**: parameterized queries, MFA, rate limiting, salted bcrypt passwords

### Tampering
- **Threat**: Modify price payloads (client-side)  
- **Impact**: Fraudulent orders / wrong payments  
- **Controls**: server-side validation, HMAC on sensitive request data

### Repudiation
- **Threat**: User denies performing action (no logs)  
- **Impact**: Unable to audit incidents  
- **Controls**: immutable logs, timestamps, user activity logs

### Information Disclosure
- **Threat**: XSS stealing cookies, API exposing PII  
- **Impact**: Data leak, privacy breach  
- **Controls**: output encoding, CSP, minimize data exposure, proper error handling

### DoS
- **Threat**: Flood checkout API  
- **Impact**: Unavailable service  
- **Controls**: rate limiting, WAF, resource quotas

### Elevation of Privilege
- **Threat**: IDOR allowing user to access other users’ orders  
- **Impact**: Data compromise, admin takeover  
- **Controls**: server-side authorization checks, RBAC

## 6. PASTA quick steps
1. Objectives: Protect user data & transactional integrity  
2. Scope: Login, checkout, admin API, product catalog  
3. Decomposition: (DFD sketch)  
4. Threat analysis: map STRIDE entries to components  
5. Vulnerability analysis: use OWASP Top 10 as checklist (A1–A10)  
6. Attack modeling: example attack — SQLi -> bypass login -> perform admin actions  
7. Risk & mitigation: rank by likelihood & impact; apply controls above

## 7. Prioritized Mitigations (Top 5)
1. Use parameterized queries + ORM  
2. Enforce HTTPS + Secure cookies  
3. Implement CSRF tokens + CSP  
4. Add rate limiting + logging + alerts  
5. RBAC + server-side authorization checks

---

## Evidence / Screenshots
Include lab setup screenshot: `/mnt/data/setup.png`

MD
