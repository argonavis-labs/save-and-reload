---
name: list-skills
description: List all saved skills. Use when the user says "list my saved skills", "show my skills", "what skills do I have", or wants to see available saved skills.
---

# List Skills

You are helping the user see all their saved skills from `~/.claude/.saved/skills/`.

## Process

### Step 1: Check for Skills Directory

First, check if the skills directory exists and has files:
```bash
ls ~/.claude/.saved/skills/*.md 2>/dev/null
```

### Step 2: Handle Empty/Missing Directory

If no skills exist, display:
```
No saved skills found.

To save a skill:
1. Complete a task with Claude
2. Say "save this" to capture it as a reusable skill

Your skills will be stored in ~/.claude/.saved/skills/
```

### Step 3: Read All Skills

For each `.md` file in the directory, read the YAML frontmatter to extract:
- `name`: The skill identifier
- `description`: One-line summary
- `created`: When it was saved (optional, for sorting)
- `complexity`: simple/medium/complex (optional)
- `tags`: Categories (optional)

Use this bash command to list all skill files:
```bash
for f in ~/.claude/.saved/skills/*.md; do
  [ -f "$f" ] && head -20 "$f"
  echo "---FILE_SEPARATOR---"
done
```

### Step 4: Display as Table

Present the skills in a clean, simple table format:

```
Saved Skills
════════════════════════════════════════════════════════════════
Name                │ Description
════════════════════════════════════════════════════════════════
add-auth-flow       │ Add JWT authentication to an Express API
create-component    │ Create a React component with tests
setup-ci            │ Configure GitHub Actions CI pipeline
════════════════════════════════════════════════════════════════
3 skills saved

To reload a skill: "reload skill [name]"
```

### Step 5: Keep It Simple

- Just show name and description
- Sort alphabetically by name
- Show total count at the bottom
- Include the hint on how to reload

## Table Formatting

Use box-drawing characters for a clean look:
- `═` for horizontal lines
- `│` for vertical separator
- Keep name column ~20 chars, truncate if needed
- Description can be longer but truncate at ~50 chars if needed

## Example Output

```
Saved Skills
════════════════════════════════════════════════════════════════
Name                │ Description
════════════════════════════════════════════════════════════════
api-endpoint        │ Create a new REST API endpoint with validation
component-gen       │ Generate React component with TypeScript
db-migration        │ Create and run a database migration
docker-setup        │ Add Docker configuration to a project
test-suite          │ Set up Jest testing with coverage
════════════════════════════════════════════════════════════════
5 skills saved

To reload: "reload skill [name]"
To save new: complete a task, then "save this"
```

## Important Guidelines

1. **Be concise**: This is just a listing, not detailed info
2. **Consistent formatting**: Use the same table format every time
3. **Helpful hints**: Always include how to reload and save
4. **Handle edge cases**: Empty directory, permission issues, malformed files
