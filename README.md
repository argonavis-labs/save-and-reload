# save-and-reload

```
╔═══════╗ ███████╗ █████╗ ██╗   ██╗███████╗
║░░░░░░░║ ██╔════╝██╔══██╗██║   ██║██╔════╝
║       ║ ███████╗███████║██║   ██║█████╗
║ ╔═══╗ ║ ╚════██║██╔══██║╚██╗ ██╔╝██╔══╝
║ ╚═══╝ ║ ███████║██║  ██║ ╚████╔╝ ███████╗
╚═══════╝ ╚══════╝╚═╝  ╚═╝  ╚═══╝  ╚══════╝

 █████╗ ███╗   ██╗██████╗     ██████╗ ███████╗██╗      ██████╗  █████╗ ██████╗
██╔══██╗████╗  ██║██╔══██╗    ██╔══██╗██╔════╝██║     ██╔═══██╗██╔══██╗██╔══██╗
███████║██╔██╗ ██║██║  ██║    ██████╔╝█████╗  ██║     ██║   ██║███████║██║  ██║
██╔══██║██║╚██╗██║██║  ██║    ██╔══██╗██╔══╝  ██║     ██║   ██║██╔══██║██║  ██║
██║  ██║██║ ╚████║██████╔╝    ██║  ██║███████╗███████╗╚██████╔╝██║  ██║██████╔╝
╚═╝  ╚═╝╚═╝  ╚═══╝╚═════╝     ╚═╝  ╚═╝╚══════╝╚══════╝ ╚═════╝ ╚═╝  ╚═╝╚═════╝
```

Save your Claude Code sessions as reusable skills. Reload them anytime.

## Install

```bash
claude /install https://github.com/argonavis-labs/save-and-reload
```

## Usage

- **"save this"** - Save your current session as a reusable skill
- **"reload skill [name]"** - Re-run a saved skill in your current project
- **"list my saved skills"** - See all your saved skills

---

Skills are stored in `~/.claude/.saved/skills/` as markdown files.
