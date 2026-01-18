# save-and-reload

```
  ╔══════════════════════════════════════════════════════╗
  ║                                                      ║
  ║     ┌────────────────────┐                           ║
  ║     │  ┌──────────────┐  │                           ║
  ║     │  │ ░░░░░░░░░░░░ │  │    SAVE & RELOAD          ║
  ║     │  │ ░░░░░░░░░░░░ │  │                           ║
  ║     │  └──────────────┘  │    Save your sessions.    ║
  ║     │   ┌────────────┐   │    Reload them anytime.   ║
  ║     │   │  ▪▪▪▪▪▪▪▪  │   │                           ║
  ║     │   └────────────┘   │    Claude Code Plugin     ║
  ║     └────────────────────┘                           ║
  ║                                                      ║
  ╚══════════════════════════════════════════════════════╝
```

Save your Claude Code sessions as reusable skills. Reload them anytime.

## Install

```bash
claude /plugin install github:your-username/save-and-reload
```

## Usage

- **"save this"** - Save your current session as a reusable skill
- **"reload skill [name]"** - Re-run a saved skill in your current project
- **"list my saved skills"** - See all your saved skills

---

Skills are stored in `~/.claude/.saved/skills/` as markdown files.
