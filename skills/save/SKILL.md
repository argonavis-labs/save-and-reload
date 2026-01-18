---
name: save
description: Save the current chat session as a reusable skill. Use when the user says "save this", "save this skill", "save this session", or wants to capture what was accomplished for future reuse.
---

# Save Skill

You are helping the user save their current chat session as a reusable skill that can be replayed later.

## Storage Location

All saved skills go to: `~/.claude/.saved/skills/`

First, ensure this directory exists:
```bash
mkdir -p ~/.claude/.saved/skills
```

## Process

### Step 1: Acknowledge and Analyze

Acknowledge the save request and analyze what was accomplished in this session. Look for:
- What task was completed
- What files were created or modified
- What tools/commands were used
- What decisions were made and why

### Step 2: Ask Clarifying Questions

Ask the user 5-8 questions to capture the essence of this skill. Ask them ALL AT ONCE in a numbered list so the user can respond to all of them together. Include questions like:

1. **Goal**: "What was the primary goal of this task? (I'll suggest: [your analysis])"
2. **Success Criteria**: "How would you know this was done correctly? What should the end result look like?"
3. **Parameters**: "What parts of this should be customizable for future use? (e.g., filenames, component names, API endpoints)"
4. **Prerequisites**: "What needs to exist before running this skill? (e.g., specific files, dependencies, project structure)"
5. **Scope**: "Should I exclude any steps from the saved skill? Or is there anything I missed that should be included?"
6. **Context**: "Is this specific to a particular framework/language, or should it be more generic?"
7. **Tags**: "What categories or tags would help you find this later? (e.g., auth, testing, deployment)"
8. **Name**: "I suggest naming this skill `[your-suggested-name]`. Would you like a different name?"

Tailor these questions based on what actually happened in the session. Skip irrelevant questions.

### Step 3: Generate the Skill File

After receiving answers, create a markdown file with this exact format:

```markdown
---
name: "[skill-name]"
description: "[one-line description]"
created: "[ISO 8601 timestamp]"
tags: ["tag1", "tag2"]
complexity: "[simple|medium|complex]"
parameters:
  - name: "[param-name]"
    description: "[what this parameter is for]"
    default: "[default value if any]"
---

# [Skill Title]

## Goal
[Clear statement of what this skill accomplishes]

## Prerequisites
- [What must exist before running]
- [Required dependencies]
- [Expected project structure]

## Parameters
| Parameter | Description | Default |
|-----------|-------------|---------|
| `{{param-name}}` | [description] | [default] |

## Steps

### 1. [First Step Title]
[Detailed instructions for this step]

### 2. [Second Step Title]
[Detailed instructions for this step]

[Continue for all steps...]

## Success Criteria
- [ ] [How to verify step 1 worked]
- [ ] [How to verify step 2 worked]
- [ ] [Overall success indicator]

## Notes
[Any important context, gotchas, or tips]
```

### Step 4: Determine Complexity

Set complexity based on:
- **simple**: 1-2 parameters, 1-4 steps, straightforward task
- **medium**: 3-4 parameters, 5-7 steps, some decision points
- **complex**: 5+ parameters, 8+ steps, multiple decision points or conditional logic

### Step 5: Save the File

Save the skill to `~/.claude/.saved/skills/[skill-name].md`

Use the Bash tool to write the file:
```bash
cat > ~/.claude/.saved/skills/[skill-name].md << 'SKILL_EOF'
[full markdown content here]
SKILL_EOF
```

### Step 6: Confirm

Tell the user:
- The skill has been saved
- The full file path
- How to use it: "Say 'reload skill [skill-name]' or 'list my saved skills' to see all your skills"

## Parameter Placeholder Syntax

Use `{{parameter-name}}` for any customizable values. Examples:
- `{{component-name}}` - Name of a component to create
- `{{api-endpoint}}` - API endpoint URL
- `{{filename}}` - Target filename
- `{{project-path}}` - Project directory path

## Important Guidelines

1. **Be specific**: Write steps that can be followed without the original session context
2. **Be complete**: Include all necessary commands, code patterns, and file paths
3. **Be generic where appropriate**: Replace project-specific values with parameters
4. **Capture the "why"**: Include reasoning for decisions, not just the "what"
5. **Make it actionable**: Each step should be concrete and executable
