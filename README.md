# Spec-Driven Multi-Agent Skills

[![skills.sh](https://skills.sh/b/spec-driven/skills)](https://skills.sh)

A complete, production-grade **9-Skill Spec-Driven Pipeline** to design, architect, implement, test, and audit software using AI coding agents with granular ID traceability, test-first execution, and independent spec auditing.

Compatible with **Cursor, Claude Code, GitHub Copilot, Codex, Windsurf, OpenCode, Devin, Gemini CLI**, and any tool supporting the open Agent Skills standard.

---

## ⚡ Installation & Quickstart (30-second setup)

You can install all 9 skills directly into your project or AI agent using the standard npm/npx installer or your agent's plugin manager.

### Method 1: Using `npx skills` (Recommended for all agents)

Install all skills into your current workspace:
```bash
npx skills@latest add <owner>/<repo>
```

Install a specific skill only (e.g. `system-architect`):
```bash
npx skills@latest add <owner>/<repo> --skill=system-architect
```

Target a specific agent directly (`-a` flag):
```bash
npx skills@latest add <owner>/<repo> -a cursor    # cursor, claude-code, copilot, windsurf, opencode, devin
```

To update installed skills at any time:
```bash
npx skills@latest update
```

---

### Method 2: Agent-Specific Plugins

<details>
<summary><strong>Claude Code</strong></summary>

Install directly from GitHub via plugin:
```bash
claude plugin marketplace add <owner>/<repo>
claude plugin install spec-driven-skills@<owner>
```
</details>

<details>
<summary><strong>Codex</strong></summary>

```bash
codex plugin marketplace add <owner>/<repo>
codex plugin add spec-driven-skills@<owner>
```
Updates itself on startup.
</details>

<details>
<summary><strong>GitHub Copilot (CLI & VS Code)</strong></summary>

```bash
copilot plugin marketplace add <owner>/<repo>
copilot plugin install spec-driven-skills@<owner>
```

In VS Code: Open command palette, select **Chat: Install Plugin From Source**, and enter `https://github.com/<owner>/<repo>`.
</details>

<details>
<summary><strong>Gemini CLI</strong></summary>

```bash
gemini skills install https://github.com/<owner>/<repo>.git --path skills
```
Re-run command to update.
</details>

---

## 📂 The `specs/` Directory Structure

Every requirement, table, endpoint, security rule, and UI component is assigned a granular ID (e.g., `PRD-AC-1a`, `DB-TBL-1`, `ARCH-API-1`, `SEC-VAL-1a`) so tasks only load the specific sections they touch. Specifications evolve safely on Day-2 through versioned `[SUPERSEDES]` patches managed by `change-and-triage-lead`.

```text
specs/
├── PRD.md             # [PRD-US-*, PRD-AC-*, PRD-UI-*, PRD-NFR-*] Stories, Gherkin criteria & NFR budgets
├── ARCHITECTURE.md    # [ARCH-SYS-*, ARCH-API-*, ARCH-HLT-*, ARCH-INT-*, ARCH-LLM-*] APIs, health & AI contracts
├── DATABASE.md        # [DB-CFG-*, DB-TBL-*, DB-MIG-*] Schemas, indexes, cascades & migration commands
├── SECURITY.md        # [SEC-AUTH-*, SEC-RBAC-*, SEC-VAL-*, SEC-ENV-*] Auth, tenant RBAC, rate limits & secrets
├── DESIGN_SYSTEM.md   # [DS-TOK-*, DS-TYP-*, DS-CMP-*, DS-A11Y-*, DS-CLI-*] UI tokens, 6 states & CLI ergonomics
├── CODE_STYLE.md      # [CS-DIR-*, CS-NAM-*, CS-TYP-*, CS-ERR-*] Folder tree, strict typing & lint CLI commands
├── TESTING.md         # [TST-CFG-*, TST-DB-*, TST-MCK-*, TST-EVAL-*, TST-MAP-*] Runners, anti-gaming & AI evals
└── TASKS.md           # Dependency-ordered task graph ([ ] Pending -> [-] Awaiting Audit -> [x] Audited)
```

---

## 🛠️ The 9 Agent Skills Overview

| # | Skill Name | Role | Reads (Inputs) | Writes / Updates (Outputs) |
| :- | :--- | :--- | :--- | :--- |
| **1** | [`product-specifier`](./skills/product-specifier/SKILL.md) | Product Manager | User Idea Prompt | `specs/PRD.md` |
| **2** | [`system-architect`](./skills/system-architect/SKILL.md) | Principal System & Security Architect | `specs/PRD.md` | `specs/ARCHITECTURE.md`<br>`specs/DATABASE.md`<br>`specs/SECURITY.md` |
| **3** | [`design-and-standards-lead`](./skills/design-and-standards-lead/SKILL.md) | Staff Frontend & Quality Lead | `PRD.md`, `ARCHITECTURE.md`, `DATABASE.md`, `SECURITY.md` | `specs/DESIGN_SYSTEM.md`<br>`specs/CODE_STYLE.md`<br>`specs/TESTING.md` |
| **4** | [`task-decomposer`](./skills/task-decomposer/SKILL.md) | Agile Delivery Lead | All 7 `specs/*.md` files | `specs/TASKS.md` (Greenfield or Delta Mode) |
| **5** | [`senior-software-engineer`](./skills/senior-software-engineer/SKILL.md) | Senior Full-Stack Engineer | `specs/TASKS.md` + Referenced Spec IDs | Code + Tests + Atomic Git Commit (`[ ]` $\rightarrow$ `[-]`) |
| **6** | [`spec-compliance-auditor`](./skills/spec-compliance-auditor/SKILL.md) | Independent QA & Security Reviewer | `[-]` tasks in `TASKS.md` + Referenced Spec IDs | Audits code/tests (`[-]` $\rightarrow$ `[x]` or rejects to `[ ]`) |
| **7** | [`devops-infrastructure-engineer`](./skills/devops-infrastructure-engineer/SKILL.md) | Principal DevOps Engineer | Tracked Infra Tasks in `TASKS.md` + Specs | `.env.example`, `.github/workflows/ci.yml`, `Dockerfile` |
| **8** | [`change-and-triage-lead`](./skills/change-and-triage-lead/SKILL.md) | Day-2 Release & Triage Architect | Hotfix / Bug / Refactor / Feature Request | Patches `specs/*.md` (`[SUPERSEDES]`) + Appends to `TASKS.md` |
| **9** | [`brownfield-reverse-specifier`](./skills/brownfield-reverse-specifier/SKILL.md) | Staff Systems Archaeologist | Existing Repo without `specs/` | Reverse-engineers all 7 `specs/*.md` + baseline `TASKS.md` |

---

## 🚀 Workflow 1: Greenfield Build (New Repository)

Each specification skill includes an **Overwrite Guard** (refusing to clobber existing specs) and a **Clarification Gate** with tailored defaults. Reply **`Use defaults`** or override specific items.

1. **Product Scope (`product-specifier`):**
   > `Use product-specifier to spec out [your product idea].` $\rightarrow$ Generates `specs/PRD.md`.
2. **Architecture, DB & Security (`system-architect`):**
   > `Use system-architect to generate our architecture, database, and security specs.` $\rightarrow$ Generates `ARCHITECTURE.md`, `DATABASE.md`, and `SECURITY.md` (supports TypeScript, Python/FastAPI, or Polyglot + LLM/Agent contracts).
3. **Design, Code Style & Testing (`design-and-standards-lead`):**
   > `Use design-and-standards-lead to create our design system, code style, and testing specs.` $\rightarrow$ Generates `DESIGN_SYSTEM.md`, `CODE_STYLE.md`, and `TESTING.md`.
4. **Task Graph (`task-decomposer`):**
   > `Use task-decomposer to build specs/TASKS.md from all 7 spec files.` $\rightarrow$ Verifies 100% `PRD-AC-*` coverage and generates `Phase 0` (scaffolding + early CI), Vertical Feature Slices split into atomic $\le 3$-file tasks, and final production containerization tasks.
5. **Implementation & Audit Loop (`senior-software-engineer` + `devops-infrastructure-engineer` + `spec-compliance-auditor`):**
   - Run `senior-software-engineer` (or `devops-infrastructure-engineer` for `Task 0.3` / `Task Final.1`) to implement the next `- [ ]` task via Red-Green-Refactor TDD, transition it to `- [-]`, and create an atomic git commit.
   - Run `spec-compliance-auditor` after each task (or at the end of each Phase) to independently verify compliance and promote `- [-]` tasks to `- [x]`.

---

## 🏛️ Workflow 2: Onboarding an Existing Repo (Brownfield)

If you have an existing codebase without a `specs/` directory:
> `Use brownfield-reverse-specifier to document this repository into specs/.`
- Inspects your existing routes, schemas, auth, UI, and tests without modifying code, generating all 7 `specs/*.md` files and a baseline `specs/TASKS.md` with completed features marked `[x]`.

---

## 🔄 Workflow 3: Day-2 Iterations (Hotfixes, Bugs, Refactors & New Features)

Always route post-MVP changes through **`change-and-triage-lead`**:

- **TYPE 0 (P0 Production Hotfix):** Adds a `[PRIORITY: P0-HOTFIX]` task to `specs/TASKS.md`. `senior-software-engineer` automatically preempts pending feature tasks to execute `P0-HOTFIX` tasks first.
- **TYPE 1 (Bug Fix):** Appends a `Task Fix-X.Y` item requiring the engineer to write a failing reproduction test before applying the fix.
- **TYPE 2 (Refactor):** Appends a `Task Refactor-X.Y` item requiring characterization tests before internal code restructuring.
- **TYPE 3 (New Feature / Schema Change):** Asks 1–4 targeted questions, patches only impacted specs using sequential IDs or `[v2 — SUPERSEDES v1]` blocks, and appends the new feature phase to `specs/TASKS.md` (directly for $\le 3$ tasks, or via `task-decomposer` in **Delta Mode** for larger features).
- **Mixed Requests:** Automatically splits bug fixes (Track 1, high priority) from new features (Track 2) so fixes never wait behind feature work.

---

## 🛡️ Guardrails Enforced by the Pack

- **3-Strike Retry Cap:** If `senior-software-engineer` fails to resolve the same test/type/lint error after 3 attempts, it halts and outputs an escalation report instead of looping infinitely.
- **Anti-Gaming Ban:** `.skip`, `.only`, weakened assertions, `any`, `@ts-ignore`, `# type: ignore`, `eslint-disable`, and `# noqa` are strictly banned and checked by `spec-compliance-auditor`.
- **Two-Key Verification (`[ ]` $\rightarrow$ `[-]` $\rightarrow$ `[x]`):** The engineer marks completed tasks `[-]`; the independent auditor promotes them to `[x]`.

---

## 📄 License

MIT