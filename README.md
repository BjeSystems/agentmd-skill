# AgentMD Skill (Canonical Repository) ⭐ OFFICIAL INSTALL

> **Authority:** Single canonical source for AGENTS.md bootstrap
> 
> **Official install target:** `https://github.com/BjeSystems/agentmd-skill`
> 
> **Scope:** Universal agent behavior contract system

Universal bootstrap system for AGENTS.md. Drop-in capability for any repository.

## Overview

AgentMD provides two powerful commands for managing agent behavior in your projects:

- **`/AgentMD`** — Bootstrap AGENTS.md from template
- **`/AgentCheck`** — Analyze project and auto-generate rules

## Features

- **Zero Configuration** — Clone and use immediately
- **Universal Template** — Works with any language/framework
- **Self-Learning** — Detects your stack and adapts rules
- **Safe Merging** — Append-only updates, never overwrites your edits
- **Git Integrated** — Automatic commits with descriptive messages

## Installation ⭐ OFFICIAL

**This is the only official installation source.**

### Official Method (Recommended)

```bash
# Clone official repository
git clone https://github.com/BjeSystems/agentmd-skill.git
cd agentmd-skill

# Install as Cursor skill
mkdir -p ~/.cursor/skills/agentmd
cp -r skill/* ~/.cursor/skills/agentmd/

# Verify installation
ls ~/.cursor/skills/agentmd/
# Output: agentmd.skill  analyzers/  commands/  rules/  templates/
```

### Authority Declaration

| Source | Status | Action |
|--------|--------|--------|
| `agentmd-skill` (this repo) | ✅ **OFFICIAL** | Install here |
| `agent-behavior-skill` | ⛔ **ARCHIVED** | DO NOT INSTALL |
| Any other fork | ⚠️ **Unofficial** | Use at own risk |

### Use in Any Project

```bash
cd /path/to/your-project

# Create AGENTS.md
/AgentMD

# Later: analyze and update rules
/AgentCheck
```

See [INSTALL.md](INSTALL.md) for detailed installation instructions.

## Commands

### /AgentMD

Creates AGENTS.md in project root using universal template.

**What it does:**
1. Detects project root (checks `.git/`, `package.json`, etc.)
2. Verifies no existing AGENTS.md (or suggests merge)
3. Copies template with 17 sections
4. Commits with message: `agentmd: bootstrap AGENTS.md`

**Template includes:**
- Tone Standards & Anti-Slop rules
- Documentation-First Protocol
- Decision Triggers for skill invocation
- Git Discipline (15-min commits)
- Local Checkpoints (stash-based recovery)
- Secrets Detection & Repository Visibility
- Done Criteria & Quality Gates
- AUTO-GENERATED markers for /AgentCheck updates

### /AgentCheck

Analyzes repository and appends project-specific rules.

**What it analyzes:**
- **Languages**: JavaScript, Python, Go, Rust, Ruby, etc.
- **Frameworks**: Next.js, Django, FastAPI, React, Vue, etc.
- **Tooling**: Docker, CI/CD, linters, test frameworks
- **Documentation**: README quality, API docs, contributing guides

**What it generates:**
- Framework-specific conventions
- Testing requirements
- Build commands
- Deployment constraints
- Architecture patterns

**Safety:**
- Uses `<!-- AUTO-GENERATED START/END -->` markers
- Append-only: never overwrites manual sections
- Git commit: `agentmd: project intelligence update`

## Architecture Foundation

The behavioral philosophy underlying AgentMD is documented in:

**[docs/behavior-foundation.md](docs/behavior-foundation.md)**

This document captures:
- Core philosophy (hierarchy of control, authority boundaries)
- Behavioral pillars (tone, anti-slop, documentation-first)
- Agent identity & autonomy principles
- Security & visibility doctrine
- Knowledge architecture
- Evolution history

## Backward Compatibility

**Migrating from agent-behavior-skill:**

If you previously used `agent-behavior-skill`, migrate as follows:

```bash
# Remove old skill (optional)
rm -rf ~/.cursor/skills/agent-behavior

# Install new skill
git clone https://github.com/BjeSystems/agentmd-skill.git
cp -r agentmd-skill/skill/* ~/.cursor/skills/agentmd/

# In your project:
cd /path/to/project-with-old-AGENTS.md
/AgentCheck   # Updates to new format with project-specific rules
```

**Key differences:**
- Old: Static template → New: `/AgentMD` + `/AgentCheck` commands
- Old: Manual customization → New: Auto-detection and rule synthesis
- Old: 16 sections → New: 17 sections + AUTO-GENERATED project rules

The old repository is now deprecated and archived:
https://github.com/BjeSystems/agent-behavior-skill

## Project Structure

```
agentmd-skill/
├── skill/
│   ├── agentmd.skill           # Skill registration
│   ├── commands/
│   │   ├── agentmd.command.md      # /AgentMD implementation
│   │   └── agentcheck.command.md   # /AgentCheck implementation
│   ├── templates/
│   │   └── AGENTS.template.md      # Universal template (17 sections)
│   ├── analyzers/
│   │   └── project_scan.md         # Detection algorithms
│   └── rules/
│       └── merge_policy.md         # Safe merge rules
├── docs/
│   └── behavior-foundation.md    # Philosophical foundation
├── README.md                     # This file
├── INSTALL.md                    # Detailed installation guide
└── LICENSE                       # MIT License
```

## Template Sections

Universal AGENTS.template.md covers:

1. **Tone Standards** — Concise communication
2. **Anti-Slop Constraints** — No filler, no tutorial text
3. **Decision Triggers** — Auto-invoke skills
4. **Documentation-First** — Read before coding
5. **Code Documentation** — Create docs after coding
6. **MCP Context7** — Documentation source
7. **Done Criteria** — Completion checklist
8. **Landing Polish** — Quality gates
9. **External Knowledge** — Allowed/prohibited sources
10. **Recurring Tasks** — Scheduled maintenance
11. **Conflict Detection** — Rule override prevention
12. **Repo Visibility** — Private-by-default
13. **Secrets Detection** — Auto-scan before push
14. **Agent Autonomy** — Freedom and boundaries
15. **Identity & Scope** — Role definition
16. **Git Discipline** — 15-min commits + change-based
17. **Local Checkpoints** — Stash-based recovery

Plus AUTO-GENERATED section for project-specific rules.

## Language/Framework Support

### Detected Languages
- JavaScript/TypeScript
- Python
- Go
- Rust
- Ruby
- Java
- And more...

### Detected Frameworks
- Next.js (App Router & Pages Router)
- React, Vue, Angular
- Django, FastAPI, Flask
- Ruby on Rails
- And more...

### Detected Tooling
- Docker & docker-compose
- GitHub Actions, CI/CD
- ESLint, Prettier, Black
- Jest, Pytest, Go test
- And more...

## Customization

After running `/AgentMD`, edit AGENTS.md:

1. **Section 3** — Replace generic skill names with your actual skills
2. **Section 6** — Update MCP source if not using Context7
3. **Section 7** — Adjust Done Criteria for your workflow
4. **Section 16** — Modify commit frequency if needed

Then run `/AgentCheck` to detect your stack and add project rules.

## Safety Guarantees

- Never modifies workflow files
- Never overwrites user-written sections
- Append-only via AUTO-GENERATED markers
- All changes committed with descriptive messages
- Rollback via git history

## Examples

### Next.js Project

```bash
/AgentMD
# Creates AGENTS.md

/AgentCheck
# Detects: Next.js 14, TypeScript, Prisma, Docker
# Adds: App Router rules, server/client separation, API conventions
```

### Python API

```bash
/AgentMD
# Creates AGENTS.md

/AgentCheck
# Detects: FastAPI, SQLAlchemy, Alembic
# Adds: Pydantic validation, migration workflow, async handlers
```

## Version

1.0.0 — Initial release with /AgentMD and /AgentCheck

## License

MIT — See [LICENSE](LICENSE) file

## Contributing

1. Fork repository
2. Create feature branch
3. Make changes
4. Submit pull request

All contributions must follow:
- Safety constraints (append-only, no overwrites)
- Git discipline rules
- Documentation-first protocol
