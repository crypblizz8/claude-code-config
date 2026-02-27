# Claude Code Config

my personal claude code configuration - mostly not created by me, but sourced from many talented people in the community.

## Installation

### Option 1: Copy-Paste into Claude Code (No Git Required)

Copy the prompt from [INSTALL.md](INSTALL.md) and paste it into Claude Code. Claude will fetch and install all config files automatically.

### Option 2: Git Clone

```bash
git clone https://github.com/crypblizz8/claude-code-config.git ~/.claude
```

### Option 3: Selective Install

```bash
# Clone elsewhere first
git clone https://github.com/crypblizz8/claude-code-config.git /tmp/claude-config

# Copy what you need
cp -r /tmp/claude-config/rules/* ~/.claude/rules/
cp -r /tmp/claude-config/skills/* ~/.claude/skills/
cp -r /tmp/claude-config/agents/* ~/.claude/agents/
```

## Contents

### Rules (`.claude/rules/`)

Path-scoped instructions loaded automatically when working with matching files.

| File | Scope | Description |
|------|-------|-------------|
| `typescript.md` | `**/*.{ts,tsx}` | TypeScript conventions |
| `testing.md` | `**/*.{test,spec}.ts` | Testing patterns |
| `comments.md` | All files | Comment policy |
| `forge.md` | `**/*.sol` | Foundry/ZKsync rules |

### Skills (`.claude/skills/`)

Model-invoked capabilities Claude applies automatically.

| Skill | Description |
|-------|-------------|
| `planning-with-files` | Persistent markdown planning for multi-step work, research, and progress tracking |
| `react-useeffect` | React useEffect best practices, including when to avoid Effects |
| `rigorous-coding` | Rigorous implementation and review standards for correctness and reliability |
| `screen-recording-frame-assessment` | Analyze app screen recordings into timeline-based UX findings and prioritized UI improvements |
| `vercel-react-best-practices` | Vercel React/Next.js performance patterns for rendering, data, and bundling |
| `web-design-guidelines` | UI/UX and accessibility review checklist for web interfaces |
| `web3` | Consolidated web3 core skill for Next.js/Vercel dApps, auth, Solidity patterns, security, audit, and EIP references |

### Agents (`.claude/agents/`)

Custom subagents for specialized tasks.

| Agent | Description |
|-------|-------------|
| `codebase-search` | Find files and implementations |
| `media-interpreter` | Extract info from PDFs/images |
| `open-source-librarian` | Research OSS with citations |
| `tech-docs-writer` | Create technical documentation |

### Commands (`.claude/commands/`)

Custom slash commands.

| Command | Description |
|---------|-------------|
| `interview` | Interactive planning/spec fleshing |

### Hooks (`.claude/hooks/`)

Scripts triggered by Claude Code events.

| Hook | Event | Description |
|------|-------|-------------|
| `keyword-detector.py` | UserPromptSubmit | Detects keywords in prompts |
| `skill-reminder.sh` | UserPromptSubmit | Reminds the model to invoke relevant skills before coding |
| `check-comments.py` | PostToolUse (Write/Edit) | Validates comment policy |
| `todo-enforcer.sh` | Stop | Ensures todos are tracked |

### CLAUDE.md

Personal global instructions loaded into every session.

## Credits

- Web3 skill content in `skills/web3` is adapted from [0xinit/web3-godmode-config](https://github.com/0xinit/web3-godmode-config).

## Recommended Plugins

Plugins I use alongside this config. Install via CLI:

### Official Plugins

```bash
claude plugin install frontend-design
claude plugin install code-review
claude plugin install typescript-lsp
claude plugin install plugin-dev
claude plugin install ralph-loop
```

### claude-hud (status line)

Add the marketplace first, then install:

```bash
claude plugin marketplace add jarrodwatts/claude-hud
claude plugin install claude-hud@claude-hud
```
