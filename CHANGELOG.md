# Changelog

All notable changes to this project will be documented in this file.

## [1.0.0] - 2026-10-18

### 🚀 Initial Public Release

The complete **9-Skill Spec-Driven Multi-Agent Pipeline** for autonomous software engineering, architecture, testing, and compliance.

#### Included Skills
- **`product-specifier`**: Translates greenfield ideas into granular, ID-indexed `specs/PRD.md` with Gherkin acceptance criteria and non-functional budgets.
- **`system-architect`**: Produces `specs/ARCHITECTURE.md`, `specs/DATABASE.md`, and `specs/SECURITY.md` with polyglot support (TypeScript/Python), health observability contracts, and AI/LLM boundaries.
- **`design-and-standards-lead`**: Generates `specs/DESIGN_SYSTEM.md`, `specs/CODE_STYLE.md`, and `specs/TESTING.md` enforcing UI states, anti-gaming rules, and strict linting.
- **`task-decomposer`**: Converts all 7 specification files into a dependency-ordered, atomic task graph in `specs/TASKS.md` (Greenfield and Delta Modes).
- **`senior-software-engineer`**: Executes unblocked tasks using strict Red-Green-Refactor TDD, an automated 3-strike retry cap, and atomic git commits.
- **`spec-compliance-auditor`**: Independently audits completed tasks `[-]` against all 7 specs, verifying anti-gaming compliance and promoting to `[x]`.
- **`devops-infrastructure-engineer`**: Provisions containerization, CI/CD GitHub workflows, and environment configurations.
- **`change-and-triage-lead`**: Manages Day-2 changes (P0 production hotfixes, bug reproductions, refactor tests, and `[SUPERSEDES]` spec patches).
- **`brownfield-reverse-specifier`**: Reverse-engineers un-spec'd codebases into the complete 7-spec suite without altering production code.

#### Distribution & Installation
- Full compatibility with the **skills.sh** open standard (`npx skills@latest add nizaalkhot/skills`).
- Multi-agent compatibility across **Cursor**, **Claude Code**, **GitHub Copilot**, **Codex**, **Windsurf**, **OpenCode**, and **Gemini CLI**.
- Automated release workflow with Changesets and GitHub Releases.
