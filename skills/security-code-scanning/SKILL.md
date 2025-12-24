---
name: Security Code Scanning and Secrets Detection
description: This skill activates when checking for hardcoded credentials, API keys, database passwords, and other secrets in source code. Provides patterns to detect leaks, scanning strategies, and best practices for secret management across all languages.
version: 1.0.0
---

# Security Code Scanning and Secrets Detection

Before deploying, you must catch hardcoded secrets that could expose credentials, API keys, database passwords, and sensitive data.

## Critical: Never Commit Secrets to Git

**Once committed, secrets are in git history FOREVER.** Anyone with repo access has them. You must:
1. Never hardcode secrets in source
2. Always use environment variables
3. Scan before every commit
4. Regenerate exposed credentials immediately

---

## Common Secrets You Must Find

### API Keys and Tokens

**Patterns to search for:**

```javascript
// ❌ EXPOSED: Hardcoded API key
const apiKey = "sk-proj-abc123def456ghi789"
const token = "ghp_1234567890abcdefghijklmnopqrstuvwxyz"

// ❌ EXPOSED: In string literals
const url = "https://api.example.com/data?key=sk-abc123"

// ❌ EXPOSED: In config objects
const config = {
  apiKey: "sk-123456",
  endpoint: "https://api.example.com"
}

// ✅ SAFE: Use environment variables
const apiKey = process.env.API_KEY
const token = process.env.GITHUB_TOKEN
```

**Where to look:**
- `.js`, `.ts`, `.jsx`, `.tsx` files
- `.env` (should be in `.gitignore`)
- `.json` config files
- `.py`, `.go`, `.java` source files
- `.env.example` (should have dummy values!)

---

### Database Credentials

**Patterns to search for:**

```javascript
// ❌ EXPOSED: Hardcoded DB password
const db = new Database({
  host: "db.example.com",
  user: "admin",
  password: "MySecurePassword123!"  // ❌ EXPOSED!
})

// ❌ EXPOSED: In connection string
const connectionString = "postgresql://user:password@localhost:5432/mydb"

// ❌ EXPOSED: In AWS SDK
const credentials = {
  accessKeyId: "AKIAIOSFODNN7EXAMPLE",
  secretAccessKey: "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
}

// ✅ SAFE: Use environment variables
const db = new Database({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD
})
```

---

### Private Keys and Certificates

**Patterns to search for:**

```
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQC...
-----END PRIVATE KEY-----

-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEA2Z3qX2BTLS/4nJlxyYUOAhk7tN4A8p3FN6m...
-----END RSA PRIVATE KEY-----
```

**Where to look:**
- `.pem`, `.key`, `.p12` files (should not be in repo!)
- `.json` files with embedded keys
- Comments mentioning credentials
- Documentation files with examples

---

## Automated Scanning Techniques

### Technique 1: Grep-Based Search

Search for common secret patterns in your codebase:

```bash
# Search for API keys
grep -r "api[_-]?key" --include="*.js" --include="*.ts" .

# Search for passwords
grep -r "password\s*=" --include="*.js" --include="*.ts" .

# Search for AWS credentials
grep -r "AKIA" --include="*.js" --include="*.json" .

# Search for private keys
grep -r "BEGIN PRIVATE KEY" --include="*.pem" --include="*.key" .

# Search for GitHub tokens
grep -r "ghp_" --include="*.js" --include="*.md" .

# Search for .env files
find . -name ".env" -o -name ".env.local" -o -name ".env.*.local"
```

### Technique 2: Pattern-Based Detection

Common secret patterns:

| Type | Pattern | Example |
|------|---------|---------|
| AWS Access Key | `AKIA[0-9A-Z]{16}` | `AKIAIOSFODNN7EXAMPLE` |
| AWS Secret Key | Long base64-like string | `wJalrXUtnFEMI/K7MDENG/...` |
| GitHub Token | `ghp_` | `ghp_1234567890abc...` |
| API Key | `sk-` prefix | `sk-proj-abc123...` |
| Private Key | `BEGIN PRIVATE KEY` | In `.pem` files |
| Password Assignment | `password\s*=` | Various languages |

---

## Code Review Checklist for Secrets

Before pushing code, verify:

- [ ] No hardcoded API keys (search for `apiKey`, `api_key`, `API_KEY`)
- [ ] No hardcoded passwords (search for `password`, `passwd`, `pwd`)
- [ ] No database credentials (search for `DB_PASS`, `DB_PASSWORD`)
- [ ] No AWS credentials (search for `AKIA`, `aws_secret`)
- [ ] No GitHub tokens (search for `ghp_`, `github_token`)
- [ ] No private keys (search for `BEGIN PRIVATE KEY`, `.pem`, `.key`)
- [ ] No hardcoded URLs with credentials (search for `://user:pass@`)
- [ ] `.env.local` is in `.gitignore`
- [ ] `.env` file is in `.gitignore`
- [ ] All credentials use `process.env.VARIABLE_NAME`

---

## `.gitignore` Security Requirements

**Minimum `.gitignore` for secrets:**

```
# Environment variables
.env
.env.local
.env.*.local
.env.production.local
.env.development.local

# Private keys and certificates
*.pem
*.key
*.p12
*.pfx

# AWS credentials
~/.aws/credentials
~/.aws/config

# IDE secrets
.idea/
.vscode/settings.json

# Database credentials
config/database.yml
config/secrets.yml

# OS files
.DS_Store
Thumbs.db
```

**Critical:** Verify `.env.local` is in `.gitignore` before committing!

```bash
# Check if .env.local is already in git
git ls-files | grep -E "\.env|\.key|\.pem"

# If you find files that shouldn't be there, remove them:
git rm --cached .env.local
echo ".env.local" >> .gitignore
git add .gitignore
git commit -m "Remove secrets from git history"
```

---

## If You Accidentally Commit Secrets

**IMMEDIATE ACTIONS (within hours):**

1. **Remove from git history** (required):
   ```bash
   git rm --cached .env.local
   ```

2. **Add to .gitignore**:
   ```bash
   echo ".env.local" >> .gitignore
   git add .gitignore
   git commit -m "Remove secrets from git history"
   ```

3. **Regenerate ALL exposed credentials**:
   - New API keys
   - New database passwords
   - New authentication tokens
   - New private keys
   - Update GitHub, AWS, databases with new credentials

4. **For published/pushed repos**, consider using `git filter-branch` or BFG Repo-Cleaner:
   ```bash
   # WARNING: This rewrites history and affects all collaborators
   bfg --delete-files .env.local
   # Or
   git filter-branch --tree-filter 'rm -f .env.local' HEAD
   ```

5. **Notify your team** - they'll need to pull the updated history

---

## Best Practices for Secret Management

### Development (.env.local)

```bash
# ✅ CORRECT: .env.local (NEVER committed)
DB_PASSWORD=localpassword123
API_KEY=dev-key-abc123
```

```bash
# ✅ CORRECT: .env.example (dummy values for reference)
DB_PASSWORD=your-password-here
API_KEY=your-api-key-here
```

**Rules:**
- `.env.local` stays local only
- `.env.example` shows structure without secrets
- Both should be in `.gitignore`

### Production (Environment Variables)

**Use platform environment variables:**

```bash
# On Vercel
# Settings → Environment Variables
DB_PASSWORD=prod-secure-password
API_KEY=prod-api-key-xyz

# On GitHub Actions
# Settings → Secrets and variables → Actions
PRODUCTION_API_KEY=xxx
PRODUCTION_DB_PASSWORD=xxx

# On Heroku
heroku config:set API_KEY=xxx
```

**Rules:**
- Never in code
- Never in git
- Set via platform UI or CLI
- Rotate regularly

---

## Pre-Commit Scanning Automation

**Add to your git workflow:**

```bash
#!/bin/bash
# .git/hooks/pre-commit (make executable: chmod +x)

# Scan for secrets before commit
echo "Scanning for hardcoded secrets..."

# Check for common patterns
PATTERNS=(
  "password\s*="
  "api[_-]?key"
  "secret"
  "AKIA"
  "ghp_"
  "BEGIN PRIVATE KEY"
)

for pattern in "${PATTERNS[@]}"; do
  if grep -r "$pattern" --include="*.js" --include="*.ts" . 2>/dev/null; then
    echo "⚠️ WARNING: Potential secret detected! Review before committing."
    exit 1
  fi
done

echo "✓ No obvious secrets detected"
exit 0
```

---

## Language-Specific Scanning

### JavaScript/TypeScript
```bash
grep -r "api[_-]?key\|password\|secret" --include="*.js" --include="*.ts" src/
```

### Python
```bash
grep -r "api_key\|password\|secret" --include="*.py" .
```

### Go
```bash
grep -r "apiKey\|password\|secret" --include="*.go" .
```

### Java
```bash
grep -r "apiKey\|password\|secret" --include="*.java" .
```

---

## Red Flags in Code Review

Reject PRs containing:
- ❌ Hardcoded API keys, tokens, or passwords
- ❌ Database credentials in source
- ❌ Private keys or certificates
- ❌ AWS access keys or secrets
- ❌ `.env` or `.env.local` files
- ❌ Comments with example credentials (even fake ones)
- ❌ URLs with embedded credentials (`user:pass@host`)

---

## Tools for Detection

**Open Source Tools:**
- `truffleHog` - Searches git history for secrets
- `git-secrets` - Prevents committing secrets
- `detect-secrets` - Secret scanning for Python
- `TruffleHog` - Finds secrets in git repos

**SaaS Tools:**
- GitHub Secret Scanning (free for public repos)
- GitLab Secret Detection
- Snyk Secret Scanner

---

## Summary: Pre-Deployment Checklist

✓ No hardcoded API keys
✓ No hardcoded passwords
✓ No database credentials in code
✓ No AWS/Azure credentials
✓ No private keys or certs
✓ `.env.local` in `.gitignore`
✓ `.env` in `.gitignore`
✓ All secrets use environment variables
✓ Ran secret scanner (grep patterns above)
✓ Verified `.gitignore` is in repo
