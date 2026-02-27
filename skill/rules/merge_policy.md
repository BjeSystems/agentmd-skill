# Merge Policy

Safe append-only merging for /AgentCheck command.

## Core Principle

**Append-only updates.** Never overwrite user-written content.

## AUTO-GENERATED Markers

Required format:

```markdown
<!-- AUTO-GENERATED START -->
## Project Rules (Auto-generated)

... generated content ...

<!-- AUTO-GENERATED END -->
```

## Merge Algorithm

### Case 1: Markers Exist

When AGENTS.md already has AUTO-GENERATED markers:

```python
def merge_with_markers(existing, new_content):
    # Find START marker position
    start_pos = existing.find("<!-- AUTO-GENERATED START -->")
    end_pos = existing.find("<!-- AUTO-GENERATED END -->")
    
    if start_pos == -1 or end_pos == -1:
        return None  # Markers not found
    
    # Extract manual content (before markers)
    manual_content = existing[:start_pos]
    
    # Build new file
    result = manual_content
    result += "<!-- AUTO-GENERATED START -->\n"
    result += new_content
    result += "\n<!-- AUTO-GENERATED END -->\n"
    
    return result
```

### Case 2: No Markers

When AGENTS.md exists but has no markers:

```python
def merge_new_markers(existing, new_content):
    # Check if markers exist
    if "<!-- AUTO-GENERATED" in existing:
        return None  # Should use Case 1
    
    # Append markers at end
    result = existing.rstrip()  # Remove trailing whitespace
    result += "\n\n---\n\n"
    result += "<!-- AUTO-GENERATED START -->\n"
    result += "## Project Rules (Auto-generated)\n\n"
    result += new_content
    result += "\n<!-- AUTO-GENERATED END -->\n"
    
    return result
```

### Case 3: First Run

When /AgentCheck runs after /AgentMD:

```python
def merge_first_run(existing):
    # Template should already have markers
    # Just replace content between them
    return merge_with_markers(existing, generate_rules())
```

## Safety Rules

### DO
- Append new rules after existing ones
- Preserve all manual sections
- Update timestamp in markers (optional)
- Add comments explaining auto-generation

### DO NOT
- Modify text above START marker
- Delete user-written rules
- Reorder existing sections
- Edit workflow rules
- Change formatting style

## Conflict Resolution

When auto-generated rules conflict with manual:

| Scenario | Resolution |
|----------|------------|
| Duplicate rule | Keep manual, ignore auto |
| Contradictory rules | Manual wins, log warning |
| Manual more specific | Keep manual |
| Auto more specific | Append auto, note in comments |

## Verification

After merge, verify:

```bash
# Check markers present
grep -q "<!-- AUTO-GENERATED START -->" AGENTS.md
grep -q "<!-- AUTO-GENERATED END -->" AGENTS.md

# Check manual content preserved
wc -l AGENTS.md  # Compare with before

# Check no deletions
diff <(echo "$ORIGINAL_MANUAL") <(head -n $START_LINE AGENTS.md)
```

## Rollback

If merge corrupts file:

```bash
# Restore from git
git checkout HEAD -- AGENTS.md

# Or from backup
cp AGENTS.md.bak AGENTS.md
```

## Example Merge

### Before
```markdown
## 16. Git Discipline

... rules ...

---

**Compliance:** This document...
```

### After Merge
```markdown
## 16. Git Discipline

... rules ...

---

<!-- AUTO-GENERATED START -->
## Project Rules (Auto-generated)

Detected: Next.js + TypeScript

### Framework Rules
- Use App Router
- Server Components by default

<!-- AUTO-GENERATED END -->

---

**Compliance:** This document...
```

## User Override

Users can prevent auto-updates:

```markdown
<!-- AUTO-GENERATED DISABLED -->
## Project Rules (Manual)

... user maintains this section ...

<!-- AUTO-GENERATED END -->
```

When /AgentCheck sees DISABLED, it skips updates and notifies user.
