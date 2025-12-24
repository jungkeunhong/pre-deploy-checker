# Marketplace Entry

This document contains the metadata for publishing the pre-deploy-checker plugin to Claude Code plugin marketplaces.

## Plugin Listing

### Basic Information

- **Name**: pre-deploy-checker
- **Version**: 1.0.0
- **Author**: Anthropic
- **License**: MIT

### Description (Short)

> Catch deployment errors before they hit git/Vercel. Checks for TypeScript errors, hardcoded secrets, and git issues.

### Description (Long)

> The pre-deploy-checker plugin helps developers catch deployment errors before they commit and push code to git or deploy to production. It provides comprehensive pre-deployment validation including TypeScript/build error detection, hardcoded secrets scanning (API keys, passwords, credentials), and git status verification. An autonomous agent automatically activates on deployment failures to provide concrete fixes.

### Features

- **TypeScript Error Detection**: Identifies and explains type errors before build fails
- **Security Scanning**: Detects hardcoded API keys, passwords, and credentials
- **Git Status Validation**: Checks for uncommitted changes and misconfigured `.gitignore`
- **Framework Agnostic**: Works with Next.js, React, Vue, Node.js, and any JavaScript/TypeScript project
- **Language Agnostic**: Principles apply to Python, Go, Java, and other languages
- **Autonomous Error Fixing**: Agent automatically activates on deployment errors to provide fixes
- **Educational Skills**: Comprehensive patterns for debugging and security best practices

### Categories

- Deployment
- Error Checking
- Security
- Development Tools
- Pre-commit Validation

### Tags

`deployment`, `validation`, `error-checking`, `security-scanning`, `pre-commit`, `typescript`, `secrets-detection`, `git`, `best-practices`

### Keywords

deployment, error checking, security, API keys, secrets detection, TypeScript, build errors, pre-commit, git validation, credentials, framework-agnostic

## Installation

### For Marketplace Listing

```
claude plugin add https://github.com/anthropics/pre-deploy-checker
```

### From GitHub Releases

```
claude plugin add https://github.com/anthropics/pre-deploy-checker/releases/download/v1.0.0/pre-deploy-checker-1.0.0.zip
```

### From NPM (if published)

```
claude plugin add @anthropic/pre-deploy-checker
```

## Marketplace Metadata (JSON Format)

```json
{
  "id": "pre-deploy-checker",
  "name": "Pre-Deploy Checker",
  "version": "1.0.0",
  "author": "Anthropic",
  "description": "Catch deployment errors before they hit git/Vercel. Checks for TypeScript errors, hardcoded secrets, and git issues.",
  "repository": "https://github.com/anthropics/pre-deploy-checker",
  "homepage": "https://github.com/anthropics/pre-deploy-checker",
  "documentation": "https://github.com/anthropics/pre-deploy-checker#readme",
  "license": "MIT",
  "keywords": [
    "deployment",
    "error-checking",
    "security-scanning",
    "pre-commit",
    "typescript",
    "secrets-detection",
    "git",
    "validation"
  ],
  "categories": [
    "Deployment",
    "Security",
    "Development Tools"
  ],
  "commands": [
    {
      "name": "pre-deploy-check",
      "description": "Comprehensive pre-deployment validation"
    },
    {
      "name": "quick-check",
      "description": "Fast pre-deployment validation"
    }
  ],
  "agents": [
    {
      "name": "Deployment Error Fixer",
      "description": "Autonomous error analysis and remediation"
    }
  ],
  "skills": [
    {
      "name": "TypeScript Error Detection and Debugging",
      "description": "Patterns for debugging TypeScript errors"
    },
    {
      "name": "Security Code Scanning and Secrets Detection",
      "description": "Patterns for detecting and preventing hardcoded secrets"
    }
  ],
  "iconUrl": "https://github.com/anthropics/pre-deploy-checker/raw/main/assets/icon.png",
  "thumbnailUrl": "https://github.com/anthropics/pre-deploy-checker/raw/main/assets/thumbnail.png",
  "rating": 0,
  "downloads": 0,
  "createdAt": "2025-12-24T00:00:00Z",
  "updatedAt": "2025-12-24T00:00:00Z"
}
```

## Screenshots/Demo

### Command: `/pre-deploy-check`
- Shows comprehensive error checking output
- Displays TypeScript errors with line numbers
- Reports hardcoded secrets with context
- Shows git status validation results

### Command: `/quick-check`
- Shows fast validation running
- Displays secrets found (or none)
- Quick build check results

### Agent: Deployment Error Fixer
- Shows activation on error keywords
- Displays root cause analysis
- Provides step-by-step fixes with code
- Shows prevention strategies

## Setup Instructions for Users

### Installation

1. **Install the plugin**:
   ```bash
   claude plugin add https://github.com/anthropics/pre-deploy-checker
   ```

2. **Verify installation**:
   ```bash
   /help | grep pre-deploy
   ```

3. **Try it out**:
   ```bash
   /quick-check /your/project/path
   ```

### First Use

1. Navigate to your project directory
2. Run `/quick-check` for a fast validation
3. Run `/pre-deploy-check` before pushing to main branch
4. If deployment fails, share the error with Claude - the agent activates automatically

## Support & Documentation

- **README**: Full documentation with workflows and FAQ
- **GitHub Issues**: Report bugs and request features
- **GitHub Discussions**: Ask questions and share ideas
- **Contributing Guide**: Contribute improvements
- **Changelog**: See what's new in each version

## Requirements

- Claude Code (latest version)
- Node.js/npm (for JavaScript/TypeScript projects) - optional
- Python (for Python projects) - optional
- Git (for git status validation)

No additional dependencies required for the plugin itself.

## Compatibility

- **Operating Systems**: macOS, Linux, Windows
- **Node.js**: 16.0.0 or higher (for JS/TS projects)
- **Python**: 3.7+ (for Python project scanning)
- **Claude Code**: Latest version recommended

## Pricing

**Free** - Open source MIT licensed plugin

## Support Tiers

- **Community**: GitHub Issues and Discussions (free)
- **Priority**: GitHub Issues with priority label (free/paid options available)

## Analytics

When published, track:
- Total downloads
- Active users
- Error reports
- Feature requests
- Community contributions

## Roadmap

### Version 1.1.0 (Q1 2025)
- Language-specific detection (Python, Go, Java)
- Pre-commit hook integration
- Custom scanning rules
- git-secrets integration

### Version 1.2.0 (Q2 2025)
- Dependency vulnerability checks
- Code quality metrics
- CI/CD pipeline integration
- Team collaboration features

### Version 2.0.0 (Q3 2025+)
- ML-based anomaly detection
- Cross-project security scanning
- Advanced audit logging
- Custom rule engine

## Legal

- **License**: MIT (permissive open source license)
- **Attribution**: Required - must credit Anthropic
- **Modification**: Allowed - can modify and redistribute
- **Commercial Use**: Allowed - can be used commercially
- **Patent**: No patent claims

## Marketplace Guidelines Compliance

✓ No spyware, malware, or unethical code
✓ Clear documentation and usage instructions
✓ Respects user privacy (no telemetry without consent)
✓ No hardcoded credentials or secrets
✓ Active maintenance and support
✓ Clear license terms
✓ Follows marketplace community guidelines

## Distribution Channels

### Primary
- Claude Code Official Plugin Marketplace

### Secondary
- GitHub Releases
- NPM Registry (if published)
- Community Plugin Collections

### Future
- Anthropic Plugin Hub
- Third-party Claude integrations

## Contact & Questions

- **Author Email**: hello@anthropic.com
- **GitHub**: https://github.com/anthropics/pre-deploy-checker
- **Issues**: https://github.com/anthropics/pre-deploy-checker/issues
- **Discussions**: https://github.com/anthropics/pre-deploy-checker/discussions

---

**Ready for marketplace publication** ✅
