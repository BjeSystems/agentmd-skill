# AgentMD Skill

Universal bootstrap system for agent behavior contracts. Drop-in capability for any repository.

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

## Quick Start

### 1. Clone Repository

```bash
git clone https://github.com/<username>/agentmd-skill.git
cd agentmd-skill
```

### 2. Import as Cursor Skill

```bash
# Copy to Cursor skills directory
mkdir -p ~/.cursor/skills/agentmd
cp -r skill/* ~/.cursor/skills/agentmd/
```

### 3. Use in Any Project

```bash
cd /path/to/your-project

# Create AGENTS.md
/AgentMD

# Later: analyze and update rules
/AgentCheck
```

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

## Project Structure

```
agentmd-skill/
├── skill/
│   ├── agentmd.skill           # Skill registration
│   ├── commands/
│   │   ├── agentmd.command.md      # /AgentMD logic
│   │   └── agentcheck.command.md   # /AgentCheck logic
│   ├── templates/
│   │   └── AGENTS.template.md      # Universal template (17 sections)
│   ├── analyzers/
│   │   └── project_scan.md         # Detection algorithms
│   └── rules/
│       └── merge_policy.md         # Safe merge rules
├── README.md                   # This file
├── INSTALL.md                  # Detailed installation guide
└── LICENSE                     # MIT License
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
