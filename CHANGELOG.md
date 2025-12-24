# Changelog

All notable changes to the pre-deploy-checker plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-24

### Added

#### Commands
- **`/pre-deploy-check`** - Comprehensive pre-deployment validation
  - TypeScript/build error detection
  - Hardcoded secrets and credentials scanning
  - Git status and history verification
  - `.gitignore` configuration validation

- **`/quick-check`** - Fast pre-deployment validation
  - Quick hardcoded secrets scanning
  - Build compilation check
  - Optimized for frequent use during development

#### Agents
- **Deployment Error Fixer** - Autonomous error analysis and remediation
  - Automatically activates on deployment failures and build errors
  - Provides root cause analysis with code examples
  - Generates step-by-step fix guidance
  - Explains prevention strategies

#### Skills
- **TypeScript Error Detection and Debugging**
  - 5 common error categories with patterns
  - Debugging workflow (6-step process)
  - Error code reference table
  - Type assertion best practices
  - CI/CD integration guidance

- **Security Code Scanning and Secrets Detection**
  - API keys and tokens scanning
  - Database credentials detection
  - Private keys and certificates
  - Automated scanning techniques (grep patterns)
  - Language-specific scanning (JS/TS, Python, Go, Java)
  - Emergency remediation guide
  - `.gitignore` security template

#### Documentation
- Comprehensive README.md with features, workflows, and FAQ
- Detailed skill documentation (TypeScript + Security)
- Command usage guides with examples
- Agent trigger conditions and examples
- Security best practices throughout

### Features

- **Framework Agnostic** - Works with Next.js, React, Vue, Node.js, and any JavaScript/TypeScript project
- **Language Agnostic** - Principles apply across Python, Go, Java, and other languages
- **Security-First** - Focuses on preventing credential leaks and hardcoded secrets
- **Educational** - Skills teach debugging patterns and best practices
- **Autonomous** - Agent automatically activates and provides guidance
- **Fast & Comprehensive** - Both quick checks and thorough validation options

### Security

- Detects hardcoded API keys, tokens, and credentials
- Identifies database passwords and private keys
- Provides `.gitignore` best practices
- Includes emergency remediation guide for exposed secrets
- No hardcoded credentials in plugin code or examples

### Known Limitations

- Focuses on JavaScript/TypeScript and general principles
- Does not perform runtime security analysis
- Does not check code logic vulnerabilities
- Does not scan dependencies for vulnerabilities (separate tools recommended)

---

## Future Roadmap

### [1.1.0] - Planned

- [ ] Language-specific detection (Python type hints, Go, Java)
- [ ] Pre-commit hook integration
- [ ] Custom scanning rules configuration
- [ ] Integration with git-secrets and TruffleHog
- [ ] Performance metrics and reporting
- [ ] Slack/Discord notifications

### [1.2.0] - Planned

- [ ] API endpoint security scanning
- [ ] Dependency vulnerability checks
- [ ] Code quality metrics reporting
- [ ] Automated remediation for common issues
- [ ] Multi-language support expansion
- [ ] CI/CD pipeline integration

### [2.0.0] - Future

- [ ] Machine learning-based anomaly detection
- [ ] Cross-project security scanning
- [ ] Team collaboration features
- [ ] Advanced audit logging
- [ ] Custom rule engine

---

## How to Contribute

We welcome contributions! See CONTRIBUTING.md for guidelines.

### Reporting Issues

Found a bug? Report it on GitHub Issues with:
- Clear description of the problem
- Steps to reproduce
- Your environment (Node version, OS, project type)
- Error messages/logs

### Suggesting Features

Have an idea? Open a GitHub Discussion or Issue with:
- Description of the feature
- Use case/problem it solves
- How you'd like to use it

### Contributing Code

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

---

## Support

- **Documentation**: See README.md and skills
- **Issues**: GitHub Issues
- **Discussions**: GitHub Discussions
- **Email**: hello@anthropic.com

---

## License

This project is licensed under the MIT License - see LICENSE file for details.
