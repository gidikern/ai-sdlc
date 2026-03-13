# Security Review Checklist

## Authentication

### Password Handling
- [ ] Passwords hashed with bcrypt/argon2 (not MD5/SHA1)
- [ ] No plaintext passwords in logs/errors
- [ ] Password requirements enforced
- [ ] Account lockout after failed attempts

### Session Management
- [ ] Session tokens are random and unpredictable
- [ ] Sessions expire appropriately
- [ ] Session invalidated on logout
- [ ] Secure cookie flags set (HttpOnly, Secure, SameSite)

### JWT (if used)
- [ ] Strong secret or RS256 algorithm
- [ ] Appropriate expiration time
- [ ] Sensitive data not in payload
- [ ] Token validation on every request

## Authorization

- [ ] Authorization checked on every endpoint
- [ ] No reliance on client-side checks only
- [ ] Proper role/permission verification
- [ ] Resource ownership verified (user can only access their data)
- [ ] Admin functions protected

## Input Validation

### General
- [ ] All input validated server-side
- [ ] Type checking enforced
- [ ] Length limits applied
- [ ] Allowed characters restricted where appropriate

### Injection Prevention
- [ ] SQL queries parameterized (no string concatenation)
- [ ] NoSQL queries use proper drivers
- [ ] Command execution avoided or sanitized
- [ ] LDAP queries escaped

### XSS Prevention
- [ ] Output encoded for context (HTML, JS, URL)
- [ ] Content-Security-Policy headers set
- [ ] User content sanitized before display
- [ ] React/Vue auto-escaping not bypassed unnecessarily

## Data Protection

### Sensitive Data
- [ ] PII encrypted at rest
- [ ] Sensitive fields masked in logs
- [ ] Credit card data handled per PCI standards
- [ ] Health data handled per HIPAA (if applicable)

### Transmission
- [ ] HTTPS enforced
- [ ] HSTS header present
- [ ] TLS 1.2+ required
- [ ] Certificate validation not disabled

### Storage
- [ ] Secrets in environment/vault (not code)
- [ ] Database credentials rotated
- [ ] Encryption keys managed properly
- [ ] Backups encrypted

## API Security

### Rate Limiting
- [ ] Rate limits on authentication endpoints
- [ ] Rate limits on expensive operations
- [ ] Rate limits on public APIs

### Request Validation
- [ ] Request size limits
- [ ] File upload validation (type, size)
- [ ] CORS configured properly
- [ ] CSRF tokens for state-changing operations

### Response Security
- [ ] No sensitive data in error messages
- [ ] Consistent error responses (don't leak info)
- [ ] Security headers set (X-Frame-Options, etc.)

## Common Vulnerabilities

### OWASP Top 10 Quick Check

| Vulnerability | What to Look For |
|--------------|------------------|
| Injection | String concatenation in queries |
| Broken Auth | Weak session management |
| Sensitive Data | Unencrypted storage/transmission |
| XXE | XML parsing of untrusted input |
| Broken Access | Missing authorization checks |
| Misconfiguration | Debug mode, default creds |
| XSS | Unescaped user input in output |
| Deserialization | Deserializing untrusted data |
| Components | Outdated dependencies |
| Logging | Sensitive data in logs |

## Security Red Flags

Immediately flag these:

```typescript
// 🔴 SQL Injection
db.query(`SELECT * FROM users WHERE id = ${userId}`);

// 🔴 Command Injection
exec(`ls ${userInput}`);

// 🔴 Hardcoded Secret
const API_KEY = "sk-123456789";

// 🔴 Weak Crypto
const hash = md5(password);

// 🔴 Missing Auth Check
app.get('/admin/users', (req, res) => {
  // No auth check!
  return db.getAllUsers();
});

// 🔴 Sensitive Data in Logs
logger.info(`User login: ${email} with password ${password}`);

// 🔴 XSS via dangerouslySetInnerHTML
<div dangerouslySetInnerHTML={{ __html: userContent }} />
```

## Health App Specific

For digital health applications, additional checks:

### HIPAA Considerations
- [ ] PHI access logged (audit trail)
- [ ] Minimum necessary data accessed
- [ ] Data retention policies enforced
- [ ] BAA in place with third parties

### Health Data Security
- [ ] Health metrics encrypted
- [ ] User consent captured
- [ ] Data export/deletion available
- [ ] Third-party sharing disclosed
