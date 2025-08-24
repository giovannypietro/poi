# Contributing to Proof-of-Intent (PoI)

Thank you for your interest in contributing to the Proof-of-Intent project! This document provides guidelines and information for contributors.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [What We're Building](#what-were-building)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Code Standards](#code-standards)
- [Documentation](#documentation)
- [Testing](#testing)
- [Submitting Changes](#submitting-changes)
- [Community](#community)
- [Questions or Need Help?](#questions-or-need-help)
- [Thank You!](#thank-you)

## Code of Conduct

This project is committed to providing a welcoming and inclusive environment for all contributors. By participating, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md).

The Code of Conduct ensures that:
- All participants feel safe and welcome
- Disagreements are handled respectfully
- Harassment and inappropriate behavior are not tolerated
- Community standards are clearly defined and enforced

Please read the full [Code of Conduct](CODE_OF_CONDUCT.md) for complete details on our community standards and enforcement procedures.

## What We're Building

Proof-of-Intent (PoI) is a cryptographic approach to AI agent security that moves beyond traditional IAM from "who can do what" to "why are they doing it, right now, on whose behalf, and with what justification?"

Our goal is to create:
- **Tamper-evident receipts** for AI agent actions
- **Cryptographic binding** between capabilities and agent lineage
- **Provable accountability** at machine speed
- **Auditable trust** in autonomous systems

## How Can I Contribute?

### 🐛 Report Issues
- **Bug reports**: Found a problem? Let us know!
- **Feature requests**: Have ideas for improvements?
- **Documentation**: Something unclear or missing?

### 💡 Improve Documentation
- **README updates**: Make the project easier to understand
- **Schema documentation**: Improve field descriptions and examples
- **Tutorials**: Help others learn how to use PoI
- **Translation**: Help make PoI accessible in more languages

### 🔧 Contribute Code
- **Bug fixes**: Help resolve reported issues
- **New features**: Implement requested capabilities
- **Tests**: Improve test coverage and quality
- **Examples**: Create sample implementations

### 🗣️ Community Support
- **Answer questions**: Help others in discussions
- **Share use cases**: Show how PoI solves real problems
- **Feedback**: Provide input on design decisions
- **Promotion**: Help spread awareness of the project

## Getting Started

### Prerequisites
- Basic understanding of IAM and security concepts
- Familiarity with JSON and API design
- Interest in AI agent security
- Git and GitHub experience (helpful but not required)

### Setup
1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/poi.git
   cd poi
   ```
3. **Add the upstream remote**:
   ```bash
   git remote add upstream https://github.com/giovannypietro/poi.git
   ```

### First Contribution
- Start with something small like documentation improvements
- Check the Issues page for "good first issue" labels
- Join GitHub Discussions to get familiar with the community

## Development Workflow

### Branch Strategy
- **Main branch**: Stable, production-ready code
- **Feature branches**: `feature/description-of-feature`
- **Bug fix branches**: `fix/description-of-bug`
- **Documentation branches**: `docs/description-of-changes`

### Workflow Steps
1. **Create a branch** from main:
   ```bash
   git checkout -b feature/your-feature-name
   ```
2. **Make your changes** and commit them:
   ```bash
   git add .
   git commit -m "Add feature: description of what you added"
   ```
3. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
4. **Create a Pull Request** on GitHub

### Commit Messages
Use clear, descriptive commit messages:
- **Format**: `type: description of changes`
- **Types**: `feat:`, `fix:`, `docs:`, `style:`, `refactor:`, `test:`, `chore:`
- **Examples**:
  - `feat: add support for custom capability scopes`
  - `fix: resolve timestamp validation issue`
  - `docs: improve schema field descriptions`

## Code Standards

### General Principles
- **Readability**: Code should be easy to understand
- **Consistency**: Follow established patterns
- **Documentation**: Comment complex logic
- **Testing**: Include tests for new functionality

### Style Guidelines
- Use clear, descriptive variable and function names
- Keep functions focused and single-purpose
- Add comments for complex business logic
- Follow the existing code style in the project

### Security Considerations
- **Input validation**: Always validate and sanitize inputs
- **Cryptographic operations**: Use established, secure libraries
- **Error handling**: Don't expose sensitive information in errors
- **Access control**: Implement proper authorization checks

## Documentation

### What to Document
- **New features**: How they work and how to use them
- **API changes**: Updated endpoints and parameters
- **Configuration**: New options and their effects
- **Examples**: Real-world usage scenarios

### Documentation Standards
- Use clear, concise language
- Include practical examples
- Keep information up-to-date
- Use consistent formatting and structure

### Where to Document
- **README.md**: High-level project overview
- **SCHEMA.md**: Detailed field definitions and validation
- **Code comments**: Inline documentation for complex logic
- **Examples**: Sample implementations and use cases

## Testing

### Test Types
- **Unit tests**: Test individual functions and components
- **Integration tests**: Test how components work together
- **Schema validation**: Ensure JSON receipts are valid
- **Security tests**: Verify cryptographic operations

### Running Tests
```bash
# Run all tests
npm test

# Run specific test files
npm test -- --grep "schema validation"

# Run tests in watch mode
npm run test:watch
```

### Writing Tests
- Test both valid and invalid inputs
- Include edge cases and error conditions
- Use descriptive test names
- Keep tests focused and independent

## Submitting Changes

### Pull Request Process
1. **Ensure your code follows** the project's standards
2. **Include tests** for new functionality
3. **Update documentation** as needed
4. **Describe your changes** clearly in the PR description
5. **Link related issues** if applicable

### Pull Request Template
```markdown
## Description
Brief description of what this PR accomplishes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Other (please describe)

## Testing
- [ ] Tests pass locally
- [ ] Added tests for new functionality
- [ ] Updated existing tests as needed

## Documentation
- [ ] Updated relevant documentation
- [ ] Added inline comments where appropriate

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review of my code
- [ ] I have commented my code where necessary
- [ ] My changes generate no new warnings
```

### Review Process
- At least one maintainer must approve your PR
- Address any feedback or requested changes
- Maintainers may request additional tests or documentation
- Once approved, your changes will be merged

## Community

### Communication Channels
- **GitHub Issues**: Bug reports and feature requests
- **GitHub Discussions**: General questions and community chat
- **Pull Requests**: Code review and collaboration
- **Email**: For security-sensitive issues

### Getting Help
- Check existing Issues and Discussions
- Search the documentation for answers
- Ask questions in GitHub Discussions
- Be specific about what you're trying to accomplish

### Recognition
- Contributors are listed in the [AUTHORS](AUTHORS) file
- Significant contributions are acknowledged in release notes
- Community members are recognized for their ongoing support

## Questions or Need Help?

- **GitHub Discussions**: Start a discussion
- **Issues**: Report a problem
- **Security**: Email for sensitive security issues
- **General**: Join the community conversation

## Thank You!

Your contributions help make Proof-of-Intent a reality. Whether you're fixing bugs, improving documentation, or sharing ideas, every contribution makes a difference in building more trustworthy AI systems.

---

**Ready to contribute?** Start by forking the repository or joining a discussion!
