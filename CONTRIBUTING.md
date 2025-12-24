# Contributing to Pre-Deploy Checker

Thank you for your interest in contributing! This document provides guidelines and instructions for contributing to the pre-deploy-checker plugin.

## Code of Conduct

Be respectful, inclusive, and constructive in all interactions.

## How Can You Contribute?

### Reporting Bugs

1. **Check existing issues** - Search GitHub Issues to avoid duplicates
2. **Create a detailed report** including:
   - Clear description of the bug
   - Steps to reproduce
   - Expected vs actual behavior
   - Your environment (Node version, OS, Claude Code version)
   - Error messages/stack traces
   - Project type (Next.js, React, Node.js, etc.)

### Suggesting Features

1. **Check existing discussions** - Look for similar feature requests
2. **Open a GitHub Discussion** with:
   - Clear description of the feature
   - Problem it solves
   - Use cases
   - Proposed implementation approach (if you have ideas)

### Improving Documentation

1. **Fix typos or clarity issues** - Submit a PR with corrections
2. **Add examples** - Include real-world examples in docs
3. **Improve workflows** - Suggest clearer workflow documentation
4. **Add FAQs** - Help answer common user questions

### Adding Features

#### Before You Start

- Open a GitHub Issue or Discussion first
- Discuss the feature with maintainers
- Get approval before implementing
- Understand the scope and requirements

#### Development Process

1. **Fork the repository**
   ```bash
   git clone https://github.com/your-username/pre-deploy-checker.git
   cd pre-deploy-checker
   ```

2. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   - Follow existing code style
   - Update relevant documentation
   - Add/update tests if applicable
   - Keep changes focused and minimal

4. **Test thoroughly**
   - Test with various project types
   - Test with different environments
   - Verify no regressions in existing functionality

5. **Update documentation**
   - Update README.md if user-facing changes
   - Update CHANGELOG.md with your changes
   - Add examples if needed
   - Document any new options/parameters

6. **Commit with clear messages**
   ```bash
   git commit -m "feat: Add feature description

   Explain the change and why it's needed."
   ```

7. **Push and open a Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```

## Plugin Structure

### Commands (`commands/`)
- User-initiated actions (like `/pre-deploy-check`)
- Each command is a markdown file with YAML frontmatter
- Describes what the command does and when to use it

### Agents (`agents/`)
- Autonomous subagents that can work independently
- Include clear `whenToUse` examples
- Specify exact capabilities and outputs
- Define the agent's role and expertise

### Skills (`skills/`)
- Specialized knowledge that Claude activates contextually
- Each skill in its own directory with `SKILL.md`
- Teach patterns, best practices, and debugging approaches
- Organized by topic (TypeScript, Security, etc.)

### Manifest (`.claude-plugin/plugin.json`)
- Defines plugin metadata
- Lists name, version, author, description
- Configure custom paths if needed

## Adding a New Skill

1. **Create directory**: `skills/skill-name/`
2. **Create SKILL.md** with:
   ```markdown
   ---
   name: Skill Name
   description: When to use this skill and what it teaches
   version: 1.0.0
   ---

   # Skill content here...
   ```
3. **Organize content**:
   - Use clear headings (H2, H3)
   - Include practical examples
   - Add code samples with before/after
   - Include prevention/best practices
4. **Test activation**: Trigger the skill with relevant questions
5. **Update README.md** to mention the new skill

## Adding a New Command

1. **Create file**: `commands/command-name.md`
2. **Add YAML frontmatter**:
   ```markdown
   ---
   name: command-name
   description: Clear description of what it does
   argument-hint: 'Optional: project-path'
   allowed-tools: [Bash, Read, Grep, Glob]
   ---

   # Command documentation...
   ```
3. **Document clearly**:
   - What it checks
   - When to use it
   - Expected output
   - Common issues
4. **Test thoroughly**: Run the command on test projects
5. **Update README.md** with usage examples

## Adding a New Agent

1. **Create file**: `agents/agent-name.md`
2. **Add YAML frontmatter**:
   ```markdown
   ---
   description: What the agent does
   whenToUse:
     - description: Scenario 1
       examples:
         - "Example trigger 1"
         - "Example trigger 2"
   capabilities:
     - Capability 1
     - Capability 2
   model: claude-opus-4-1-20250805
   color: "#1e3a8a"
   ---
   ```
3. **Include examples**: Show expected interactions
4. **Test activation**: Trigger with provided examples
5. **Update README.md** with agent description

## Code Style Guide

### Markdown Files
- Use consistent heading hierarchy (H1 → H2 → H3)
- Use code blocks with syntax highlighting
- Use tables for structured information
- Use lists instead of paragraphs when possible
- Add clear examples with before/after code

### YAML Frontmatter
- Use consistent indentation (2 spaces)
- Keep field values concise but clear
- Use arrays for multiple items
- Quote strings with special characters

### Documentation
- Use clear, conversational language
- Target mid-level developers (not too simple, not too advanced)
- Include real-world examples
- Explain not just "what" but "why"

## Testing Guidelines

### Before Submitting PR

1. **Test commands**: Run on 2-3 different project types
2. **Test agents**: Trigger with all provided examples
3. **Test skills**: Ask relevant questions to activate
4. **Check documentation**: Read all changes for clarity
5. **Verify links**: Ensure all references work
6. **Check formatting**: Run on mobile viewport for docs changes

### Test Checklist

- [ ] All components load without errors
- [ ] Commands produce expected output
- [ ] Agents activate on specified triggers
- [ ] Skills activate on relevant questions
- [ ] Documentation is clear and complete
- [ ] No hardcoded secrets or sensitive data
- [ ] YAML frontmatter is valid
- [ ] Markdown formatting is correct
- [ ] Examples work as described

## Review Process

1. **Automated checks**: GitHub Actions validates structure
2. **Maintainer review**: We'll review code and documentation
3. **Feedback loop**: We may suggest changes
4. **Approval**: Once approved, we'll merge your PR
5. **Release**: Your contribution will be in the next version

## Release Process

1. Update version in `plugin.json`
2. Update `CHANGELOG.md` with changes
3. Create a Git tag matching version
4. Push to GitHub (triggers release workflow)
5. Announce in GitHub Releases

## Questions?

- Open a GitHub Discussion
- Check existing Issues and Discussions
- Email: hello@anthropic.com

## Thank You!

Your contributions make this plugin better for everyone. We appreciate your time and effort!
