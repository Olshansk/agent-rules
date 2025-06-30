# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

Agent Rules is a collection of reusable rules and knowledge documents for AI coding assistants. The repository contains two main types of content:

- **project-rules/**: Actionable `.mdc` files that define workflows and commands for AI assistants
- **docs/**: Reference documentation and knowledge bases for various technologies

## Core Architecture

### Rule System Structure
- Rules use `.mdc` (Markdown with Configuration) format
- Each rule provides specific commands (e.g., `/commit`, `/check`, `/implement-task`)
- Rules are designed to work across different project types and languages
- Support for both Cursor and Claude Code through unified format

### Key Command Categories

#### Development Workflow
- `/commit` - Create structured commits with conventional format and emoji prefixes
- `/commit-fast` - Auto-generate and use first commit message suggestion
- `/implement-task` - Methodical task implementation with planning phases
- `/context-prime` - Load comprehensive project understanding (README, structure, configs)

#### Code Quality & Analysis
- `/check` - Run comprehensive quality checks (linting, type checking, security)
- `/clean` - Fix all formatting and linting issues across the codebase
- `/code-analysis` - Advanced multi-faceted code analysis with various inspection options
- `/pr-review` - Multi-perspective PR review (PM, Dev, QA, Security, DevOps, UX)

#### Documentation & Communication
- `/create-docs` - Generate comprehensive documentation for components
- `/add-to-changelog` - Update CHANGELOG.md with structured entries
- `/mermaid` - Create Mermaid diagrams for visualizing code structure
- `/analyze-issue` - Fetch GitHub issue details and create implementation specs

## Common Development Commands

### Installation
```bash
# Install project rules globally
./install-project-rules.sh

# Customize MCP servers and rules
./tweak-claude.sh
```

### Multi-Language Support Patterns

The rules automatically detect and use appropriate tools for different languages:

**Python:**
```bash
black .
isort .
flake8 . --extend-ignore=E203
mypy .
```

**JavaScript/TypeScript:**
```bash
npx prettier --write .
npx eslint . --fix
npx tsc --noEmit
```

**Swift:**
```bash
swift-format --in-place .
swiftlint --fix
```

**Go:**
```bash
go vet ./...
golint ./...
```

### Git Workflow Integration
- All commands respect git staging and workflow
- Conventional commit format: `type(scope): description`
- Emoji prefixes: ✨ feat, 🐛 fix, 📝 docs, ♻️ refactor
- Pre-commit hooks respected unless `--no-verify` specified

## Project Structure Understanding

### Essential Files
- `README.md` - Main project documentation and usage instructions
- `install-project-rules.sh` - Global installation script for Claude Code
- `tweak-claude.sh` - Interactive configuration tool for MCP servers and rules
- `project-rules/*.mdc` - Individual rule definitions
- `docs/*.mdc` - Reference documentation for Swift, MCP, and other technologies

### Global Rules Integration
Files in `global-rules/` are designed for `~/.claude/CLAUDE.md`:
- GitHub issue creation automation
- MCP server setup (Peekaboo, GitHub, Firecrawl)
- Terminal title management
- Cross-project rule synchronization

## Development Best Practices

### Context Loading Strategy
1. Read README.md and CLAUDE.md
2. List project structure (`git ls-files | head -50`)
3. Review configuration files (package.json, Cargo.toml, etc.)
4. Understand development workflow

### Quality Gates
- Run `/check` before commits
- Fix issues incrementally: build errors → tests → linting → warnings
- No commits during active quality check processes
- Use `/clean` to fix all formatting issues automatically

### Documentation Standards
- Reference specific functions with `file_path:line_number` format
- Generate LLM-optimized documentation with file references
- Follow Keep a Changelog format for changelog updates
- Include table of contents for longer documentation

## MCP Integration

The repository includes setup for several MCP servers:
- **Peekaboo**: Screenshot capture with AI analysis
- **GitHub**: API access for issue and PR management
- **Firecrawl**: Web scraping capabilities

API keys are managed through `~/.zshrc` environment variables and extracted securely by setup scripts.