# Security Audit Checklist - Token Monitor Site + Crypto Payment

## Pre-Launch Security Review

### 1. Payment System Security

#### Wallet Security
- [ ] Mnemonic seed encrypted at rest (AES-256)
- [ ] Encryption password strength verified (min 32 chars recommended)
- [ ] Mnemonic NEVER logged or transmitted
- [ ] Private keys stored encrypted (Solana)
- [ ] HD derivation path correct (BIP84 for BTC)
- [ ] Backup instructions clear and secure

#### Payment Flow
- [ ] Unique address per payment (verified)
- [ ] No address reuse vulnerability
- [ ] Payment amounts validated server-side
- [ ] No client-side price manipulation possible
- [ ] Blockchain confirmation thresholds set
- [ ] Double-spend protection in monitor

#### Admin Panel
- [ ] Admin key strength (min 32 chars, random)
- [ ] No hardcoded credentials
- [ ] Rate limiting on admin endpoints
- [ ] Brute-force protection
- [ ] Session timeout configured
- [ ] IP allowlist option available

### 2. Web Security

#### Input Validation
- [ ] Email validation (regex + sanitization)
- [ ] Product ID validation (allowlist only)
- [ ] No SQL injection vectors (using parameterized queries)
- [ ] XSS prevention (input sanitization)
- [ ] CSRF tokens on state-changing requests
- [ ] File upload restrictions (if any)

#### HTTP Security Headers
- [ ] Content-Security-Policy set
- [ ] X-Frame-Options: DENY
- [ ] X-Content-Type-Options: nosniff
- [ ] Strict-Transport-Security (HSTS)
- [ ] X-XSS-Protection enabled
- [ ] Referrer-Policy configured

#### SSL/TLS
- [ ] HTTPS enforced (redirect from HTTP)
- [ ] TLS 1.2+ only
- [ ] Strong cipher suites
- [ ] Valid SSL certificate
- [ ] No mixed content warnings
- [ ] HSTS preload eligible

### 3. API Security

#### Rate Limiting
- [ ] Payment creation endpoint: 10/min per IP
- [ ] Admin endpoints: 5/min per IP
- [ ] Status check endpoint: 60/min per IP
- [ ] Burst protection configured
- [ ] 429 responses with Retry-After

#### Authentication
- [ ] Bearer token format for admin API
- [ ] Token rotation policy
- [ ] No tokens in URLs (header-only)
- [ ] Token expiration configured
- [ ] Revocation mechanism exists

#### Data Exposure
- [ ] No sensitive data in error messages
- [ ] Stack traces disabled in production
- [ ] Payment records don't expose mnemonic/keys
- [ ] Admin responses sanitized
- [ ] CORS configured restrictively

### 4. Data Protection

#### Encryption at Rest
- [ ] Mnemonic: AES-256-GCM
- [ ] Private keys: AES-256-GCM
- [ ] Admin key: bcrypt hash (if stored)
- [ ] License keys: plain OK (sent to customer)

#### Encryption in Transit
- [ ] HTTPS for all endpoints
- [ ] Webhook callbacks use HTTPS
- [ ] Email via TLS (SMTP 587)
- [ ] No plaintext credentials transmitted

#### Data Retention
- [ ] Payment records: retention policy defined
- [ ] Logs: rotation configured
- [ ] PII handling: GDPR-aware
- [ ] Deletion mechanism available
- [ ] Backup encryption verified

### 5. Infrastructure Security

#### Server Hardening
- [ ] Firewall configured (ports 80, 443, 22 only)
- [ ] SSH key-only auth (no password)
- [ ] Non-root user for app
- [ ] Auto-updates enabled
- [ ] Fail2ban or equivalent active
- [ ] Intrusion detection configured

#### Dependencies
- [ ] npm audit run (0 high/critical)
- [ ] Dependencies up-to-date
- [ ] No known vulnerabilities
- [ ] Lockfile committed (package-lock.json)
- [ ] Minimal dependencies (reduce attack surface)

#### Monitoring
- [ ] Error logging configured
- [ ] Failed payment attempts logged
- [ ] Admin access logged
- [ ] Unusual activity alerts
- [ ] Uptime monitoring
- [ ] Disk space alerts

### 6. Operational Security

#### Access Control
- [ ] Server access restricted (SSH keys only)
- [ ] Admin panel password in 1Password
- [ ] Wallet password in 1Password
- [ ] Mnemonic backup secure (offline)
- [ ] No credentials in git

#### Incident Response
- [ ] Payment failure procedure documented
- [ ] Security breach procedure documented
- [ ] Contact info for urgent issues
- [ ] Rollback procedure tested
- [ ] Backup restoration tested

#### Deployment
- [ ] .env not committed to git
- [ ] .gitignore includes sensitive files
- [ ] Production vs dev configs separated
- [ ] Environment variables validated on start
- [ ] Health check endpoint available

### 7. Crypto-Specific Security

#### Bitcoin
- [ ] SegWit addresses (bc1...) only
- [ ] No P2PKH/legacy addresses
- [ ] Derivation path: m/84'/0'/0'/0/n
- [ ] Amount in satoshis validated
- [ ] Blockchain.info API backup plan

#### Solana
- [ ] Keypair generation secure (randomBytes)
- [ ] Private keys never logged
- [ ] RPC endpoint trusted (official)
- [ ] Amount in lamports validated
- [ ] Keypair storage encrypted

#### General
- [ ] No testnet/mainnet confusion
- [ ] Network fees documented
- [ ] Sweeping instructions clear
- [ ] Cold storage migration plan
- [ ] Multi-sig option considered (future)

### 8. Testing

#### Security Tests
- [ ] SQL injection attempts (manual)
- [ ] XSS attempts (manual)
- [ ] CSRF token bypass attempts
- [ ] Rate limit verification
- [ ] Admin brute-force test
- [ ] Payment manipulation attempts

#### Functional Tests
- [ ] Payment flow end-to-end
- [ ] Monitor detection working
- [ ] Email delivery verified
- [ ] Webhook delivery verified
- [ ] Admin unlock working
- [ ] License key generation unique

### 9. Documentation

#### Customer-Facing
- [ ] Payment instructions clear
- [ ] Refund policy stated
- [ ] Support contact visible
- [ ] Privacy policy present
- [ ] Terms of service present

#### Internal
- [ ] Deployment procedure documented
- [ ] Backup procedure documented
- [ ] Monitoring setup documented
- [ ] Incident response plan
- [ ] Architecture diagram

### 10. Compliance

#### Privacy
- [ ] GDPR: data minimization
- [ ] GDPR: right to deletion
- [ ] Email opt-out available
- [ ] No unnecessary tracking
- [ ] Cookie policy (if cookies used)

#### Legal
- [ ] Terms of service reviewed
- [ ] Refund policy clear
- [ ] Liability limitations stated
- [ ] Age restrictions if needed
- [ ] Export compliance (crypto)

---

## Pre-Launch Checklist

Before going live, ALL items above must be checked ✅

**Risk Assessment:**
- HIGH: Mnemonic exposure, admin access, payment manipulation
- MEDIUM: XSS, CSRF, rate limiting bypass
- LOW: Info disclosure, minor config issues

**Launch Criteria:**
- All HIGH risks mitigated ✅
- All MEDIUM risks addressed ✅
- LOW risks documented and accepted

**Post-Launch:**
- Security review every 30 days
- Dependency updates weekly
- Log review daily
- Penetration test after 1000 customers

---

**Auditor:** Atlas
**Date:** 2026-01-31
**Status:** Pre-launch preparation
