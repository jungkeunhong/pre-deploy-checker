---
name: quick-check
description: Fast pre-deployment validation that scans for hardcoded secrets and runs a quick build check without full git status verification. Use when you need quick feedback.
argument-hint: 'Optional: project-path (defaults to current directory)'
allowed-tools: [Bash, Read, Grep, Glob]
---

# Quick Pre-Deployment Check

Fast validation for when you need quick feedback before committing. Skips comprehensive git checks to save time.

## What This Check Does

1. **Secret/Credential Scanning** (FAST): Quick search for hardcoded API keys, passwords
2. **Quick Build Check** (FAST): Runs build command and reports errors
3. **Skips**: Full git status, environment variable verification, detailed analysis

## Usage

```
/quick-check
/quick-check /path/to/project
```

## What Gets Checked

✓ Hardcoded API keys and tokens
✓ Hardcoded passwords and credentials
✓ Build/TypeScript compilation
✓ Private keys and certificates

## What Gets SKIPPED (for speed)

⊘ Detailed git status
⊘ `.gitignore` verification
⊘ Environment variable checks
⊘ Full codebase analysis

## Output Format

Reports issues found:
- **Type**: What kind of issue (secret, build error, etc.)
- **Location**: File and line number
- **Severity**: Critical/Warning
- **Fix**: Quick remediation steps

## When to Use This

✓ Quick pre-commit validation
✓ When you're confident about changes
✓ For frequent checks during development
✓ When you need feedback in seconds

✗ Don't use before pushing to main branch (use `/pre-deploy-check` instead)
✗ Don't use as sole validation before production deploy

## Speed Expectations

- Typical project: 2-5 seconds
- Large project: 5-15 seconds
- Comprehensive check (`/pre-deploy-check`): 15-30 seconds

## Common Outputs

### No Issues Found
```
✓ No hardcoded secrets detected
✓ Build successful
→ Safe to commit!
```

### Issues Found
```
⚠ API key found in src/config.js:12
→ Move to .env.local before committing

⚠ Database password in src/db.ts:45
→ Use process.env.DB_PASSWORD instead
```

## Next Steps After Quick Check

- Fix any issues found
- For push to main: Run `/pre-deploy-check` for comprehensive validation
- For local commit: This quick check is usually sufficient
