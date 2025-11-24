# Contributing to Dependency Scanner Microservices

Thank you for your interest in contributing to the Dependency Scanner platform! This document provides guidelines and instructions for contributing to this project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Environment Setup](#development-environment-setup)
- [Project Structure](#project-structure)
- [How to Contribute](#how-to-contribute)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Pull Request Process](#pull-request-process)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Enhancements](#suggesting-enhancements)

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to the project maintainers.

## Getting Started

1. Fork the repository
2. Clone your fork: `git clone https://github.com/YOUR_USERNAME/scalable-microservice.git`
3. Add upstream remote: `git remote add upstream https://github.com/Dependency-Scanner/web-app-service.git`
4. Create a new branch: `git checkout -b feature/your-feature-name`

## Development Environment Setup

### Prerequisites

- **Python 3.11+** (recommended: 3.11 or 3.13)
- **Docker** and **Docker Compose** (for containerized development)
- **Redis** (for caching)
- **Git** (for version control)

### Setting Up Individual Services

Each microservice can be set up independently:

#### Web App Service

```bash
cd web-app-service
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

#### Auth Service

```bash
cd auth-service
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

#### Dependency Scanner Service

```bash
cd dependency-scanner-service
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

#### Integration Service

```bash
cd Integration-Service
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Environment Variables

Each service requires specific environment variables. Create a `.env` file in each service directory based on the following templates:

**Auth Service:**
```env
JWT_SECRET_KEY=your-secret-key
JWT_ALGORITHM=HS256
JWT_ACCESS_TOKEN_EXPIRE_MINUTES=30
SCANNER_SERVICE_URL=http://localhost:8082
INTEGRATION_SERVICE_URL=http://localhost:8083
```

**Scanner Service:**
```env
JWT_SECRET_KEY=your-secret-key
JWT_ALGORITHM=HS256
REDIS_HOST=localhost
REDIS_PORT=6379
NVD_API_KEY=your-nvd-api-key
GITHUB_TOKEN=your-github-token
```

**Integration Service:**
```env
JWT_SECRET_KEY=your-secret-key
JIRA_URL=your-jira-url
JIRA_EMAIL=your-email
JIRA_API_TOKEN=your-token
GITHUB_TOKEN=your-github-token
```

**Web App Service:**
```env
AUTH_SERVICE_URL=http://localhost:8081
SCANNER_SERVICE_URL=http://localhost:8082
INTEGRATION_SERVICE_URL=http://localhost:8083
REDIS_HOST=localhost
REDIS_PORT=6379
```

## Project Structure

```
scalable-microservice/
├── auth-service/           # Authentication & orchestration service
├── dependency-scanner-service/  # Vulnerability scanning service
├── Integration-Service/    # JIRA & GitHub integration service
├── web-app-service/       # Web UI & BFF service
├── mcp-service/           # Model Context Protocol service
├── scrapper-service/      # Web scraping service
└── logs/                  # Service logs and PIDs
```

## How to Contribute

### Types of Contributions

We welcome various types of contributions:

- **Bug fixes**: Fix issues in the codebase
- **New features**: Add new functionality to services
- **Documentation**: Improve or add documentation
- **Tests**: Add or improve test coverage
- **Performance improvements**: Optimize code performance
- **Code refactoring**: Improve code quality and maintainability

### Finding Issues to Work On

- Check the [Issues](https://github.com/Dependency-Scanner/web-app-service/issues) page
- Look for issues labeled `good first issue` or `help wanted`
- Comment on the issue to let others know you're working on it

## Coding Standards

### Python Style Guide

We follow [PEP 8](https://pep8.org/) with some modifications:

- **Line length**: Maximum 100 characters (not 79)
- **Indentation**: 4 spaces (no tabs)
- **Imports**: Group imports (standard library, third-party, local)
- **Type hints**: Use type hints for function parameters and return values
- **Docstrings**: Use Google-style docstrings

### Code Formatting

Use the following tools to maintain code quality:

```bash
# Install development dependencies
pip install black flake8 mypy pylint isort

# Format code with Black
black .

# Sort imports
isort .

# Lint with flake8
flake8 .

# Type checking with mypy
mypy .
```

## Testing Guidelines

### Writing Tests

- Write unit tests for all new functionality
- Aim for at least 80% code coverage
- Use `pytest` for testing
- Mock external service calls

### Running Tests

```bash
# Run tests for a specific service
cd web-app-service
pytest

# Run with coverage report
pytest --cov=app --cov-report=html

# Run specific test file
pytest tests/test_services.py

# Run tests in verbose mode
pytest -v
```

## Commit Message Guidelines

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:


### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, missing semicolons, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `ci`: CI/CD changes


## Pull Request Process

1. **Update your fork**: Sync with upstream before creating a PR
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Create a descriptive PR title**: Follow the commit message format

3. **Fill out the PR template**: Provide context about your changes

4. **Ensure all tests pass**: Run tests locally before submitting

5. **Update documentation**: Update relevant documentation if needed

6. **Request review**: Tag relevant maintainers for review

7. **Address feedback**: Respond to review comments promptly

8. **Squash commits**: Squash commits if requested before merging

### PR Checklist

- [ ] Code follows the project's style guidelines
- [ ] Self-review of code completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] Tests added/updated and passing
- [ ] No new warnings generated
- [ ] Dependent changes merged and published

## Reporting Bugs

### Before Submitting a Bug Report

- Check the [existing issues](https://github.com/Dependency-Scanner/web-app-service/issues) to avoid duplicates
- Verify the bug with the latest version of the code
- Collect relevant information (logs, error messages, environment details)

### Bug Report Template

```markdown
**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Set up service with '...'
2. Send request to '....'
3. See error

**Expected behavior**
A clear description of what you expected to happen.

**Actual behavior**
What actually happened.

**Screenshots/Logs**
If applicable, add screenshots or log output.

**Environment:**
- OS: [e.g., macOS, Ubuntu 22.04]
- Python version: [e.g., 3.11.5]
- Service version: [e.g., 1.2.0]
- Docker version (if applicable): [e.g., 24.0.5]

**Additional context**
Add any other context about the problem here.
```

## Suggesting Enhancements

### Enhancement Request Template

```markdown
**Is your feature request related to a problem?**
A clear description of what the problem is.

**Describe the solution you'd like**
A clear description of what you want to happen.

**Describe alternatives you've considered**
Alternative solutions or features you've considered.

**Additional context**
Add any other context, mockups, or examples.

**Which service(s) does this affect?**
- [ ] auth-service
- [ ] dependency-scanner-service
- [ ] Integration-Service
- [ ] web-app-service
- [ ] Other (specify)
```

## Questions?

If you have questions about contributing, feel free to:

- Open a [Discussion](https://github.com/Dependency-Scanner/web-app-service/discussions)
- Contact the maintainers
- Join our community chat 

---

Thank you for contributing to the Dependency Scanner project! 🎉
