# Installation Guide

## Prerequisites

- Git installed
- Cursor IDE (for skill import)
- GitHub account (for cloning)

## Method 1: As Cursor Skill (Recommended)

### Step 1: Clone Repository

```bash
git clone https://github.com/<username>/agentmd-skill.git
cd agentmd-skill
```

### Step 2: Install Skill

```bash
# Create skill directory
mkdir -p ~/.cursor/skills/agentmd

# Copy skill files
cp -r skill/* ~/.cursor/skills/agentmd/

# Verify installation
ls ~/.cursor/skills/agentmd/
# Output: agentmd.skill  analyzers/  commands/  rules/  templates/
```

### Step 3: Verify in Cursor

1. Open Cursor
2. Start new chat
3. Type `/AgentMD` — should be recognized
4. Type `/AgentCheck` — should be recognized

### Step 4: Use in Projects

```bash
cd /path/to/your-project

# In Cursor chat:
/AgentMD

# Later, after coding:
/AgentCheck
```

## Method 2: Direct File Copy

If you don't want to install as skill:

```bash
# Clone repository
git clone https://github.com/<username>/agentmd-skill.git

# Copy template directly to project
cp agentmd-skill/skill/templates/AGENTS.template.md \
   /path/to/your-project/AGENTS.md

# Manually edit AGENTS.md for your project
```

## Method 3: Submodule (Advanced)

For teams wanting version-controlled skill:

```bash
cd /path/to/your-project

# Add as submodule
git submodule add https://github.com/<username>/agentmd-skill.git .agentmd

# Use commands via submodule
.agentmd/skill/templates/AGENTS.template.md
```

## Post-Installation Setup

### First Run Checklist

1. **Create AGENTS.md in test project:**
   ```bash
   cd ~/projects/test-project
   /AgentMD
   ```

2. **Verify file created:**
   ```bash
   ls -la AGENTS.md
   git log --oneline -1
   # Should show: agentmd: bootstrap AGENTS.md
   ```

3. **Review template:**
   - Open AGENTS.md
   - Check all 17 sections present
   - Verify AUTO-GENERATED markers at end

4. **Run AgentCheck:**
   ```
   /AgentCheck
   ```
   
5. **Verify project rules added:**
   ```bash
   grep -A 5 "AUTO-GENERATED START" AGENTS.md
   ```

## Troubleshooting

### Command Not Recognized

**Problem:** `/AgentMD` not recognized in Cursor

**Solution:**
1. Check skill directory exists:
   ```bash
   ls ~/.cursor/skills/agentmd/
   ```
2. Verify `agentmd.skill` file present
3. Restart Cursor
4. Try again

### Permission Denied

**Problem:** Cannot copy files to `~/.cursor/skills/`

**Solution:**
```bash
# Create directory with proper permissions
mkdir -p ~/.cursor/skills/agentmd
chmod 755 ~/.cursor/skills/agentmd

# Copy files
cp -r skill/* ~/.cursor/skills/agentmd/
```

### AGENTS.md Already Exists

**Problem:** Running `/AgentMD` in project with existing AGENTS.md

**Solution:**
- Use `/AgentCheck` instead to update rules
- Or manually rename existing file:
  ```bash
  mv AGENTS.md AGENTS.md.backup
  /AgentMD
  ```

### Git Commit Fails

**Problem:** `git commit` fails after creating AGENTS.md

**Solution:**
1. Check git config:
   ```bash
   git config user.email
   git config user.name
   ```
2. Stage manually if needed:
   ```bash
   git add AGENTS.md
   git commit -m "agentmd: bootstrap AGENTS.md"
   ```

## Uninstallation

### Remove Skill

```bash
rm -rf ~/.cursor/skills/agentmd/
```

### Remove from Project

```bash
cd /path/to/project
git rm AGENTS.md
git commit -m "Remove AGENTS.md"
```

## Verification

### Test Installation

```bash
# Create test project
mkdir -p ~/test-agentmd
cd ~/test-agentmd
git init

# Run command
/AgentMD

# Verify
[[ -f AGENTS.md ]] && echo "✓ AGENTS.md created"
git log --oneline | grep -q "agentmd" && echo "✓ Committed"
```

### Expected Output

```
✓ Project root detected: /home/user/test-agentmd
✓ No existing AGENTS.md
✓ Template copied (17 sections)
✓ File created: AGENTS.md
✓ Committed: agentmd: bootstrap AGENTS.md

Next steps:
  1. Review AGENTS.md
  2. Customize Decision Triggers (Section 3)
  3. Run /AgentCheck after coding
```

## Updates

### Update Skill

```bash
cd /path/to/agentmd-skill
git pull origin main

# Reinstall
cp -r skill/* ~/.cursor/skills/agentmd/
```

### Check Version

```bash
grep "version:" ~/.cursor/skills/agentmd/agentmd.skill
```

## Support

- Issues: GitHub Issues
- Discussions: GitHub Discussions
- Documentation: README.md, this file
