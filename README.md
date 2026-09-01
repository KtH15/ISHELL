# ISHELL — The Most Advanced Interactive Python Shell

An advanced interactive terminal shell, built entirely with the Python 3
standard library (zero third-party dependencies), tuned to run well on
**Termux (Android)** and also Linux/macOS.

## Install (Termux or Linux)

```bash
cd ishell
bash install.sh
```

Then launch it with:

```bash
ishell
```

Or run it directly without installing:

```bash
python3 main.py
```

## Features

### 1. Full persistent memory
- Every command you run is stored in a SQLite database (`~/.ishell/state.db`)
- Full interactive history with search: `history search_term`
- Real usage statistics: `stats` — shows most-used commands, failure rate, total time

### 2. Local intelligence (works fully offline)
- **Typo correction**: type `grpe` instead of `grep`, and it asks "did you mean grep?"
- **Natural-language -> command**: `? show me disk space` -> suggests `df -h`
- **Command explanations**: `explain rm -rf test` -> explains what each part does
- **Optional real AI**: if you export `ANTHROPIC_API_KEY`, the `ask <question>` command connects to a real Claude model

### 3. Full job control
- Run any command in the background: `sleep 100 &`
- List all jobs: `jobs`
- Kill a job: `kill %1`
- The prompt itself shows how many jobs are currently running

### 4. Aliases & bookmarks
- Define a permanent alias: `alias gp=git push`
- Save a directory under a short name: `bookmark work`, then `go work` from anywhere
- All of this persists across sessions

### 5. Rich visual interface
- Colored, aligned tables for all output
- Live system info panel: `sysinfo` (CPU load, disk space, colored progress bars)
- 3 ready-made themes: `theme default` / `theme midnight` / `theme mono`
- Smart prompt showing: current path, current Git branch, job count, and the exit code if the last command failed

### 6. Full integration with the real shell
- All normal bash commands work as-is: pipes (`|`), `&&`, `||`, redirections
- Tab-completion for paths, commands, and aliases
- Readline command history persists across sessions, works with up/down arrows

## Built-in commands

| Command | What it does |
|---|---|
| `cd <dir>` | Change directory |
| `pwd` / `whoami` | Current path / current username |
| `clear` / `cls` | Clear the screen |
| `sysinfo` | System info panel |
| `stats` | Your usage statistics |
| `history [query]` | Show / search history |
| `alias name=cmd` | Define a permanent alias |
| `unalias name` | Remove an alias |
| `cmd &` | Run in the background |
| `jobs` | List running jobs |
| `kill %N` | Terminate a job |
| `bookmark name` | Save the current directory |
| `go name` | Jump to a saved bookmark |
| `bookmarks` | List all bookmarks |
| `explain <cmd>` | Explain a command |
| `? question` | Translate a question into a shell command |
| `ask <question>` | Real AI (requires an API key) |
| `theme [name]` | Change theme |
| `exit` / `quit` | Quit |

## Files

```
ishell/
├── main.py     # Main REPL loop and all built-in commands
├── core.py     # Config, themes, persistent database
├── intel.py    # Local intelligence: typo correction, suggestions, explanations
├── jobs.py     # Background job control
├── ui.py       # UI elements: tables, progress bars, system panel
└── install.sh  # Installer script for Termux/Linux
```

## Enabling real AI (optional)

```bash
export ANTHROPIC_API_KEY="sk-ant-..."
ishell
```

Without this key, the shell runs at full power but uses only local
intelligence (typo correction and built-in suggestions) — no internet
connection required.
