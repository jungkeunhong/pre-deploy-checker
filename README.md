# Pre-Deploy Checker Plugin

Catch deployment errors before they hit git/Vercel. Comprehensive error detection for TypeScript/build errors, hardcoded secrets, and git issues.

## Features

- **TypeScript Error Detection**: Identifies and explains type errors before build fails
- **Security Scanning**: Detects hardcoded API keys, passwords, and credentials
- **Git Status Validation**: Checks for uncommitted changes and misconfigured `.gitignore`
- **Framework Agnostic**: Works with any JavaScript/TypeScript project (Next.js, React, Node.js, etc.)
- **Language Agnostic**: Principles apply to Python, Go, Java, and other languages
- **Autonomous Error Fixing**: Agent automatically activates on deployment errors to provide fixes

## Components

### Commands

#### `/pre-deploy-check` - Comprehensive Check
Full validation before pushing to main or deploying to production.

**Checks:**
- TypeScript/build errors
- Hardcoded secrets (API keys, passwords, credentials)
- Git status and uncommitted changes
- `.gitignore` configuration

**Usage:**
```bash
/pre-deploy-check
/pre-deploy-check /path/to/project
```

#### `/quick-check` - Fast Check
Quick validation for frequent checks during development. Skips git verification for speed.

**Checks:**
- Hardcoded secrets (quick scan)
- Build compilation

**Usage:**
```bash
/quick-check
/quick-check /path/to/project
```

### Agents

#### Deployment Error Fixer
Automatically activates when you mention deployment problems, build errors, or any "won't deploy" situations.

**Triggers:**
- "My build failed"
- "Got a Vercel deployment error"
- "TypeScript error"
- "This won't deploy"
- Error messages from console/logs

**Provides:**
- Root cause analysis
- Step-by-step fixes with code examples
- Prevention strategies

### Skills

#### TypeScript Error Detection
Comprehensive patterns for debugging TypeScript errors, type mismatches, and build failures.

**Covers:**
- Type mismatch errors
- Missing type annotations
- Component props issues
- Union type errors
- Array type issues
- Build error debugging workflow

#### Security Code Scanning
Detailed guidance on detecting and preventing hardcoded secrets and credentials.

**Covers:**
- API keys and tokens
- Database credentials
- Private keys and certificates
- Automated scanning techniques
- `.gitignore` best practices
- Remediation if secrets are exposed

## Quick Start

1. **Install the plugin:**
   ```bash
   claude plugin install https://github.com/jungkeunhong/pre-deploy-checker
   ```

2. **Before committing:**
   ```bash
   /quick-check
   ```

3. **Before pushing to main or deploying:**
   ```bash
   /pre-deploy-check
   ```

4. **If deployment fails:**
   - Share the error message
   - The Deployment Error Fixer agent activates automatically
   - Follow the step-by-step fixes provided

## Common Workflows

### Workflow 1: Pre-Commit (Local)
```
1. Make code changes
2. Run /quick-check
3. Fix any issues found
4. git commit
5. Ready for local testing
```

### Workflow 2: Pre-Push to Main
```
1. Code changes committed locally
2. Run /pre-deploy-check
3. Fix any issues found
4. git push origin main
5. Monitor deployment
```

### Workflow 3: Deployment Failure
```
1. Deployment fails with error
2. Share error message with Claude
3. Deployment Error Fixer activates
4. Follow provided fixes
5. Run /pre-deploy-check to verify
6. Deploy again
```

### Workflow 4: Team Development
```
1. Onboard new developer
2. Show them /quick-check before committing
3. Show them /pre-deploy-check before pushing
4. Reduce deployment-time surprises
5. Consistent quality across team
```

## Security Considerations

### Critical: Never Commit Secrets

This plugin helps detect hardcoded secrets before they leak to git, but:

1. **Once committed to git, secrets are exposed forever** (even if deleted later)
2. **You MUST regenerate any exposed credentials** (API keys, passwords, tokens)
3. **Always use `.env.local`** for local development credentials
4. **Always add to `.gitignore`**: `.env`, `.env.local`, `*.pem`, `*.key`

### What This Plugin Checks For

✓ API keys (OpenAI, GitHub, etc.)
✓ Database passwords
✓ AWS/Azure credentials
✓ Private keys and certificates
✓ GitHub tokens
✓ Hardcoded environment variables

### What This Plugin DOESN'T Check For

⊘ Business logic vulnerabilities
⊘ SQL injection risks
⊘ XSS vulnerabilities
⊘ Insecure dependencies
⊘ Misconfigured CORS/headers

(Use dedicated security tools for those)

## For Different Frameworks

### Next.js
```bash
/pre-deploy-check
```
Checks: `npm run build` output, `.env.local`, secrets

### React + TypeScript
```bash
/quick-check  # During development
/pre-deploy-check  # Before deploying to Vercel
```

### Node.js Backend
```bash
/pre-deploy-check  # Before deploying to production
```

### Python Project
```bash
/quick-check  # Before committing
```
Principles apply, but you may need additional Python-specific checks

## FAQ

**Q: Will this commit my changes?**
A: No. This plugin only identifies issues. You have full control over commits and pushes.

**Q: Can it fix issues automatically?**
A: The Deployment Error Fixer agent provides step-by-step fixes you apply manually, ensuring you understand the changes.

**Q: What if I accidentally commit secrets?**
A: Run git rm --cached [file] and regenerate all exposed credentials immediately. See the Security Code Scanning skill for detailed remediation.

**Q: Do I need both commands?**
A: `/quick-check` is for frequent, fast validation. `/pre-deploy-check` is for thorough validation before critical operations.

**Q: Works with my framework?**
A: Yes! The plugin is framework agnostic and works with any JavaScript, TypeScript, Python, Go, or Java project.

**Q: What's the performance impact?**
A: Minimal. Checks run in 2-15 seconds depending on project size.

## Support & Contributing

Report issues or contribute improvements:
- GitHub: https://github.com/jungkeunhong/pre-deploy-checker
- Issues: https://github.com/jungkeunhong/pre-deploy-checker/issues
- Documentation: https://github.com/jungkeunhong/pre-deploy-checker#readme

## License

MIT License - See LICENSE file for details
