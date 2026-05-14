# Contributing to Computer Graphics Algorithms

Thank you for considering contributing to this project! This document provides guidelines for contributing.

## Code of Conduct

This project adheres to the Contributor Covenant Code of Conduct. By participating, you are expected to uphold this code.

## How to Contribute

### Reporting Bugs

Before creating a bug report, check the issue list to avoid duplicates.

**When filing a bug report, include:**
- Clear, descriptive title
- Exact steps to reproduce
- Specific examples
- Current behavior vs. expected behavior
- Environment (OS, compiler, OpenGL version)
- Relevant code or screenshots

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues.

**Before creating an enhancement suggestion, check:**
- If it's already been suggested
- If it aligns with project scope

**Enhancement suggestions should include:**
- Clear, descriptive title
- Detailed description of proposed enhancement
- Current behavior vs. desired behavior
- Implementation approach (if applicable)

### Pull Requests

**Process:**
1. Fork the repository
2. Create a branch (`git checkout -b feature/descriptive-name`)
3. Make your changes with clear, documented code
4. Test thoroughly
5. Commit with clear messages
6. Push to your fork
7. Submit a pull request

**PR Requirements:**
- Clear description of changes
- Reference related issues
- Updated documentation if needed
- Code comments for complex logic
- Consistent formatting with existing code

## Development Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/Computer_Graphics.git
cd Computer_Graphics

# Create a development branch
git checkout -b develop

# Make your changes
# Test locally
# Commit and push
```

## Coding Standards

- **Language**: C++11/14 standard
- **Style**: Follow existing code patterns
- **Comments**: Write clear, meaningful comments
- **Naming**: Use descriptive variable/function names
- **Functions**: Keep functions focused and modular

## Testing

- Test your code locally before submitting
- Ensure existing programs still compile and run
- Add test cases for new features

## Documentation

- Update README if adding new algorithms
- Document algorithm complexity and approach
- Add inline comments for complex logic
- Include usage examples

## Commit Messages

Use clear, descriptive commit messages:
```
fix(bresenham): correct circle rendering at edges
feat(clipping): add Cohen-Sutherland line clipping
docs(readme): add algorithm explanation section
refactor(dda): optimize floating point calculations
```

## Review Process

- At least one maintainer review required
- Feedback will be provided constructively
- Changes may be requested before merging
- All tests must pass

## Recognized Contributors

Contributors will be recognized in the project documentation.

Thank you for contributing!
