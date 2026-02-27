---
name: /AgentCheck
description: Analyze repository and append project-specific rules to AGENTS.md
trigger: /AgentCheck
---

# /AgentCheck Command

## Purpose

Self-learning project adaptation. Analyze codebase and append project-specific rules to AGENTS.md.

## Execution Pipeline

### Stage 1 — Repository Scan

Agent MUST analyze codebase structure:

**Language Detection:**
```bash
# Check for language-specific files
[[ -f "package.json" ]] && LANG="javascript"
[[ -f "pyproject.toml" ]] && LANG="python"
[[ -f "go.mod" ]] && LANG="go"
[[ -f "Cargo.toml" ]] && LANG="rust"
[[ -f "Gemfile" ]] && LANG="ruby"
# etc.
```

**Framework Detection:**
```bash
# JavaScript/TypeScript
[[ -d "node_modules/next" ]] && FRAMEWORK="nextjs"
[[ -d "node_modules/react" ]] && FRAMEWORK="react"
[[ -d "node_modules/vue" ]] && FRAMEWORK="vue"

# Python
[[ -f "django" ]] && FRAMEWORK="django"
[[ -f "flask" ]] && FRAMEWORK="flask"
[[ -f "fastapi" ]] && FRAMEWORK="fastapi"

# Go
[[ -d "vendor" ]] && PATTERN="go-modules"
```

**Tooling Detection:**
```bash
# Build/Test
[[ -f "Dockerfile" ]] && TOOLS+="docker "
[[ -f "docker-compose.yml" ]] && TOOLS+="docker-compose "
[[ -f ".github/workflows" ]] && TOOLS+="ci-cd "
[[ -f ".eslintrc" ]] && TOOLS+="eslint "
[[ -f "Makefile" ]] && TOOLS+="make "
```

### Stage 2 — Documentation Scan

Agent MUST check documentation:

```bash
[[ -f "README.md" ]] && DOCS="README "
[[ -d "docs" ]] && DOCS+="docs-folder "
[[ -f "CONTRIBUTING.md" ]] && DOCS+="contributing "
[[ -f "API.md" ]] && DOCS+="api-docs "
```

### Stage 3 — Dependency Intelligence + Change Detection

Agent MUST infer workflow from detected frameworks:

**Detection Result Hash:**
```bash
# Generate hash of current detection
DETECTION_HASH=$(echo "$LANG $FRAMEWORK $TOOLS $ARCH" | md5sum | cut -d' ' -f1)

# Check if hash exists from previous run
if [[ -f ".agentmd/last-detection" ]]; then
    LAST_HASH=$(cat .agentmd/last-detection)
    if [[ "$DETECTION_HASH" == "$LAST_HASH" ]]; then
        echo "No structural project changes since last run — ABORT update"
        exit 0
    fi
fi

# Save current hash for next run
mkdir -p .agentmd
echo "$DETECTION_HASH" > .agentmd/last-detection
```

**Change Detection Gate:**
Agent MUST abort if no structural change since last /AgentCheck:
- Same languages detected
- Same frameworks detected  
- Same tooling detected
- No new architectural patterns

**If changes detected:** Continue to rule synthesis.

**If Next.js detected:**
```markdown
### Next.js Rules
- Server/Client separation: mark components with "use client" or "use server"
- App Router conventions for routing
- API routes in app/api/ directory
```

**If Python FastAPI detected:**
```markdown
### FastAPI Rules
- Pydantic models for request/response validation
- Dependency injection for database sessions
- Auto-generated OpenAPI docs at /docs
```

**If Docker detected:**
```markdown
### Docker Rules
- Multi-stage builds for production
- .dockerignore to exclude node_modules
- Health checks in containers
```

### Stage 4 — Rule Synthesis

Agent MUST generate project-specific section:

```markdown
<!-- AUTO-GENERATED START — IMMUTABLE GUARD — DO NOT EDIT MANUALLY -->
## Project Rules (Auto-generated)

> This section is automatically maintained by /AgentCheck.
> Manual edits will be preserved ONLY above this marker.
> To customize: add rules in manual sections or modify templates/.

Detected stack: Next.js + TypeScript + Prisma + Docker

### Framework Conventions
- Use App Router (not Pages Router)
- Server Components by default
- "use client" only for interactive components

### Database Rules (Prisma)
- Run migrations before schema changes
- Use transactions for multi-step operations
- Seed data in prisma/seed.ts

### Testing Requirements
- Jest for unit tests
- Playwright for E2E
- Coverage minimum: 80%

### Build Commands
- `npm run dev` — development
- `npm run build` — production build
- `npm run test` — test suite
- `docker-compose up` — local infrastructure

### Deployment Constraints
- Vercel for frontend
- Railway/Render for database
- Environment variables in .env.local (never commit)

<!-- AUTO-GENERATED END — IMMUTABLE GUARD — DO NOT EDIT MANUALLY -->
```

### Stage 5 — Safe Merge (Hard Boundary Enforcement)

Agent MUST enforce hard boundary — ONLY content between markers:

**Hard Boundary Rules:**
1. Extract START marker line number: `grep -n "AUTO-GENERATED START" AGENTS.md`
2. Extract END marker line number: `grep -n "AUTO-GENERATED END" AGENTS.md`
3. Modify ONLY lines between START+1 and END-1
4. Content above START line: READ-ONLY (never touched)
5. Content below END line: READ-ONLY (never touched)
6. START/END marker lines themselves: READ-ONLY (never modified)

**Boundary Violation Detection:**
```bash
# Before any write, verify boundaries
if sed -n "1,${START_LINE}p" AGENTS.md | diff -q - <(echo "$ORIGINAL_HEAD"); then
    echo "ERROR: Head section modified — ABORT"
    exit 1
fi
```

**Duplication Prevention:**
```bash
# Before append, check if rule already exists
if grep -q "Detected framework: $FRAMEWORK" AGENTS.md; then
    echo "Rule exists: $FRAMEWORK — skipping duplicate"
    continue
fi
```

**Merge Algorithm (Boundary-Strict):**
```bash
# Read original
START_LINE=$(grep -n "AUTO-GENERATED START" AGENTS.md | head -1 | cut -d: -f1)
END_LINE=$(grep -n "AUTO-GENERATED END" AGENTS.md | tail -1 | cut -d: -f1)

# Extract untouchable sections
HEAD_SECTION=$(sed -n "1,${START_LINE}p" AGENTS.md)
TAIL_SECTION=$(sed -n "${END_LINE},\$p" AGENTS.md)

# Build new file
NEW_CONTENT=$(cat <<EOF
${HEAD_SECTION}
<!-- AUTO-GENERATED START — IMMUTABLE GUARD — DO NOT EDIT MANUALLY -->
## Project Rules (Auto-generated)

> This section is automatically maintained by /AgentCheck.
> Manual edits will be overwritten. Add custom rules in manual sections above.

$(generate_rules_with_dedup)
<!-- AUTO-GENERATED END — IMMUTABLE GUARD — DO NOT EDIT MANUALLY -->
${TAIL_SECTION#*END —>}
EOF
)

# Atomic replace
mv AGENTS.md AGENTS.md.bak
echo "$NEW_CONTENT" > AGENTS.md
```

**Protection Level:**
- User sections: Sacred, untouchable, cryptographically sealed
- AUTO-GENERATED sections: Agent-maintained ONLY
- Markers: Immutable boundaries, never crossed

### Stage 6 — Git Commit

Agent MUST commit changes:

```bash
git add AGENTS.md
git commit -m "agentmd: project intelligence update

Added project-specific rules based on codebase analysis:
- Detected frameworks: [list]
- Tooling: [list]
- Testing requirements
- Build commands

Generated by /AgentCheck command."
```

## Safety Constraints

### Hard Boundary Enforcement
Agent MUST modify ONLY content between AUTO-GENERATED markers. Any attempt to touch content outside markers = ABORT.

### Change Detection Gate
Agent MUST abort update if no structural project change detected:
```bash
# Compare current detection with previous state
if [[ "$CURRENT_DETECTED" == "$PREVIOUS_DETECTED" ]]; then
    echo "No structural changes detected — skipping update"
    exit 0
fi
```

### Duplication Prevention
Agent MUST check for existing rules before append:
```bash
# Hash-based deduplication
current_hash=$(md5sum <<< "$RULE_CONTENT")
if grep -q "$current_hash" .agentmd/checksums; then
    echo "Rule already exists — skipping"
    exit 0
fi
```

### Recursion Safety
Agent MUST NOT:
- Modify workflow files (.cursor/rules/)
- Override user-written sections (above AUTO-GENERATED markers)
- Remove existing rules
- Hallucinate frameworks not present in codebase
- Edit source code files
- Update AGENTS.md if no project structure change since last run

## Success Criteria

- [ ] Repository scanned (languages, frameworks, tooling)
- [ ] Project-specific rules generated
- [ ] Safe merge performed (append-only)
- [ ] AUTO-GENERATED markers present
- [ ] Committed with descriptive message

## Error Handling

| Scenario | Action |
|----------|--------|
| AGENTS.md not found | Suggest running /AgentMD first |
| Cannot detect frameworks | Add generic placeholder rules |
| No changes detected | Report "no new rules to add" |
| Git commit fails | Stage only, report to user |

## Output

On success:
```
✓ Repository analyzed: [languages]
✓ Frameworks detected: [list]
✓ Project rules generated: [count] rules
✓ Safe merge: AUTO-GENERATED section updated
✓ Committed: agentmd: project intelligence update

Detected patterns:
  - Language: TypeScript/JavaScript
  - Framework: Next.js 14 (App Router)
  - Database: Prisma + PostgreSQL
  - Testing: Jest + Playwright
  - Deployment: Docker + Vercel
```
