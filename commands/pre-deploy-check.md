---
name: pre-deploy-check
description: Comprehensive pre-deployment validation checking TypeScript/build errors, hardcoded secrets (API keys, passwords, credentials), and git status before committing and pushing.
argument-hint: 'Optional: project-path (defaults to current directory)'
allowed-tools: [Bash, Read, Grep, Glob]
---

# Pre-Deployment Comprehensive Check

Run this command before committing and pushing code to catch errors early.

## What This Check Does

1. **TypeScript/Build Errors**: Runs build command and analyzes errors
2. **Secret/Credential Scanning**: Searches for hardcoded API keys, passwords, database credentials
3. **Git Status Validation**: Checks for uncommitted changes and pending commits
4. **Environment Variables**: Verifies `.env.local` is in `.gitignore`

## Usage

```
/pre-deploy-check
/pre-deploy-check /path/to/project
```

## What Happens

The check will:
- Scan source files for hardcoded secrets
- Attempt to run build commands (npm run build, etc.)
- Check git status and history
- Verify `.gitignore` configuration
- Report all issues found with recommended fixes

## Output Format

For each issue found:
1. **What was found** (specific file and line)
2. **Why it's a problem** (security/build impact)
3. **How to fix it** (exact steps)

## Common Issues and Fixes

### Build Errors
If TypeScript errors are found, you'll get:
- Error type (TS2339, TS2345, etc.)
- File and line number
- Suggested fix based on error pattern

### Secrets Found
If secrets are detected, you'll get:
- Secret type (API key, password, etc.)
- File location
- Step-by-step remediation guide

### Git Issues
If git status shows problems, you'll get:
- List of uncommitted files
- Files that should be ignored
- Changes to `.gitignore` needed

## When to Use This

✓ Before `git commit`
✓ Before `git push`
✓ Before deploying to production
✓ After big refactoring changes
✓ When onboarding new team members

## What This Does NOT Check

⚠️ Does not commit changes (you do that manually)
⚠️ Does not run tests (use `/quick-check` for faster validation)
⚠️ Does not check code quality/linting (separate concern)
⚠️ Does not validate business logic (manual review needed)
