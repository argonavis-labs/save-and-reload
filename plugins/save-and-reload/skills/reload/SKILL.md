---
name: reload
description: Reload and execute a previously saved skill. Use when the user says "do this again", "reload skill [name]", "reload our skill on [name]", "run the [name] skill", or wants to re-execute a saved skill.
---

# Reload Skill

You are helping the user reload and execute a previously saved skill from `~/.claude/.saved/skills/`.

## Process

### Step 1: Identify the Skill

Parse the user's request to find the skill name. They might say:
- "do this again" - needs clarification, list skills and ask which one
- "reload skill add-auth" - skill name is "add-auth"
- "reload our skill on component-creator" - skill name is "component-creator"
- "run the testing skill" - skill name is "testing"

If no skill name is clear, list available skills:
```bash
ls ~/.claude/.saved/skills/*.md 2>/dev/null | xargs -I {} basename {} .md
```

Then ask: "Which skill would you like to reload?"

### Step 2: Read the Skill File

First, display this message:
```
💽 Loading skill from disk...
```

Then read the skill from `~/.claude/.saved/skills/[skill-name].md`:
```bash
cat ~/.claude/.saved/skills/[skill-name].md
```

If the file doesn't exist, inform the user and list available skills.

### Step 3: Parse and Display

Parse the skill file to extract:
- Name and description from frontmatter
- Complexity level
- Parameters (if any)
- Steps overview

Display a summary to the user:
```
Skill: [name]
Description: [description]
Complexity: [simple/medium/complex]
Parameters: [list or "none"]

Steps:
1. [step 1 title]
2. [step 2 title]
...
```

### Step 4: Get Approval and Parameters

**For simple skills (complexity: simple OR fewer than 3 parameters AND fewer than 5 steps):**
Ask: "Ready to proceed? (yes/no)"

**For complex skills (complexity: medium/complex OR 3+ parameters OR 5+ steps):**
1. Show the parameters with their defaults
2. Ask: "Would you like to customize any parameters, or proceed with defaults?"
3. If they want to customize, ask for each parameter value
4. Confirm the final parameter values before proceeding

### Step 5: Execute the Skill

Once approved, execute the skill step by step:

1. Read the current repository/folder context to understand where you are
2. For each step in the skill:
   - Announce the step with: `▶️ Step X: [step title]...`
   - Replace any `{{parameter}}` placeholders with actual values
   - Execute the step (create files, run commands, etc.)
   - Confirm completion before moving to the next step
3. If a step fails, stop and ask the user how to proceed

### Step 6: Verify Success

After completing all steps, go through the Success Criteria:
- Check each criterion
- Report which ones pass/fail
- If any fail, offer to help fix them

### Step 7: Report Completion

Display the completion message in this format:
```
✅ Skill executed successfully!

Summary:
- Skill: [name]
- Steps completed: X/X
- Files modified: [list of files]
```

Include details about what was created/modified and any parameters that were used.

## Parameter Substitution

When you see `{{parameter-name}}` in the skill:
1. Check if the user provided a value
2. If not, use the default from the skill's frontmatter
3. If no default exists, ask the user for a value

Example:
- Skill says: `Create file {{component-name}}.tsx`
- User provided: `component-name = "UserProfile"`
- Execute: `Create file UserProfile.tsx`

## Handling Missing Skills

If the skill file doesn't exist:
```
I couldn't find a skill named "[name]".

Available skills:
- skill-one: Description of skill one
- skill-two: Description of skill two

Would you like to reload one of these instead?
```

## Handling Empty Skills Directory

If `~/.claude/.saved/skills/` is empty or doesn't exist:
```
You don't have any saved skills yet.

To save a skill, complete a task and then say "save this" to capture it for future reuse.
```

## Important Guidelines

1. **Always show before doing**: Display the plan before executing
2. **Respect the user's context**: Adapt file paths and commands to the current project
3. **Be interactive**: Ask for confirmation at key decision points
4. **Handle errors gracefully**: If something fails, explain what happened and offer alternatives
5. **Preserve intent**: The goal is to replicate the original outcome, not necessarily the exact steps
