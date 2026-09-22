# TuTor

**English** · [Español](README-es.md)

An **agent skill** (a folder of instructions your AI tool loads when it's relevant) that turns it into a learning tutor. TuTor plans work in small steps, explains every command, verifies your progress with read-only checks, and refuses to complete the assignment for you.

Use it when you want to **learn by doing**—homework, tutorials, walkthroughs, or any time you say “don’t do it for me.”

## Objective

TuTor helps **teachers and students** use AI as a coach, not a cheat sheet. Today’s coding assistants often hand over finished answers and skip the thinking, debugging, and trial-and-error where real learning happens. This skill redirects that power toward **learning by doing**: the learner writes the code and runs the commands; the agent plans steps, explains tools, and verifies progress—without doing the work for them. The aim is deeper understanding in class, in study groups, and on personal projects—not faster copy-paste.


## What it does

| Behavior | Detail |
|----------|--------|
| **Step-by-step** | Outlines a numbered plan up front; gives **one** action per turn (no full solution). |
| **Verification** | After you say you’re done, the tool checks with read-only commands (`Read`, `ls`, `cat`, `git status`, `git diff`, tests you ran). |
| **Tool gate** | The tool may inspect your work but must **not** create, edit, or run commands that build your deliverable for you. |
| **Command teaching** | Every shell command includes a breakdown: goal, pieces, and what success looks like. |

Optional deep dives live in [`references/`](references/):

- [`references/example-flow.md`](references/example-flow.md) — greenfield app walkthrough
- [`references/tool-gate.md`](references/tool-gate.md) — which shell commands are allowed

## Install

**Repository:** [github.com/kevinnio/tutor](https://github.com/kevinnio/tutor)

TuTor is a folder with `SKILL.md` (the instructions) plus `references/` (extra reading). Keep the folder named `tutor`. Some tools refuse to load a skill if the folder name doesn't match the name inside `SKILL.md`.

### Install with Skills CLI (recommended)

The [Skills CLI](https://github.com/vercel-labs/skills) ([skills.sh](https://skills.sh)) is a small installer. It looks for the AI tools on your computer and puts the skill in the right folder for each, so you don't need to know the paths.

**User-wide (all projects)** — recommended for your first install:

```bash
npx skills add kevinnio/tutor -g -y
```

**This project only** (share with a class or team via git):

```bash
npx skills add kevinnio/tutor -y
```

**Pick specific tools** (skip the menu):

```bash
npx skills add kevinnio/tutor -g -a opencode -a github-copilot -a gemini-cli -y
```

| Flag | Meaning |
|------|---------|
| `-g`, `--global` | User-wide install (`~/…/skills/`) |
| (no `-g`) | Install into the current project only |
| `-a`, `--agent` | Which tools to install for, e.g. `opencode`, `github-copilot`, `gemini-cli`, `cursor`, `claude-code`, `codex` |
| `-y`, `--yes` | Non-interactive |

Preview before installing: `npx skills add kevinnio/tutor --list`. Every supported tool: [vercel-labs/skills](https://github.com/vercel-labs/skills#supported-agents).

After installing, start a **new chat** (or reopen the tool) so it notices the skill.

### Which tool to start with

Any of these works. If you're picking a first one, **OpenCode** is free and open source, and you can connect it to a free model, including one that runs on your own computer. **GitHub Copilot** and **Gemini CLI** are free for verified students ([Student Developer Pack](https://education.github.com/pack), [Google AI for students](https://gemini.google/students/)). Cursor and Claude Code need a paid plan unless your school provides one.

### How to use TuTor in each tool

- **OpenCode** — Describe what you want to learn; OpenCode loads the skill when it's relevant. [OpenCode skills](https://opencode.ai/docs/skills/).
- **GitHub Copilot** — In VS Code, type `/tutor` in the chat, or describe what you want to learn. [Copilot skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills).
- **Gemini CLI** — Describe what you want to learn; Gemini CLI loads the skill when it's relevant. [Gemini CLI skills](https://geminicli.com/docs/cli/skills/).
- **Cursor** — Ask to learn something (e.g. “Teach me to build a todo app—don’t write it for me”) or use `/tutor` if available. [Cursor skills](https://cursor.com/docs/context/skills).
- **Claude Code** — Run `/tutor` or describe what you want to learn. [Claude Code skills](https://code.claude.com/docs/en/skills).

### Optional: make TuTor a mode you can switch to

Normally the skill loads on its own when it's relevant. If you'd rather pick TuTor from a menu, the way you pick Plan or Build in OpenCode, add one small extra file. It also stops the tool from editing your files, so TuTor can only read.

| Tool | File | Put it in | How to switch |
|------|------|-----------|---------------|
| [OpenCode](https://opencode.ai) | `agents/opencode/tutor.md` | `~/.config/opencode/agents/` | press `Tab` to switch to **tutor** |
| [Claude Code](https://code.claude.com) | `agents/claude/tutor.md` | `~/.claude/agents/` | `claude --agent tutor`, or `@tutor` in a chat |
| [GitHub Copilot](https://code.visualstudio.com/docs/agent-customization/custom-agents) (VS Code) | `agents/claude/tutor.md` | `~/.claude/agents/` | pick **tutor** in the agents menu |

```bash
SKILL_DIR=~/.claude/skills/tutor   # wherever the tutor skill is installed

mkdir -p ~/.config/opencode/agents ~/.claude/agents
ln -sf "$SKILL_DIR/agents/opencode/tutor.md" ~/.config/opencode/agents/tutor.md
ln -sf "$SKILL_DIR/agents/claude/tutor.md"   ~/.claude/agents/tutor.md
```

VS Code Copilot reads the Claude folder too, so one file covers Copilot and Claude Code.

On macOS and Linux these are shortcuts, so updating TuTor (`npx skills update`) updates the mode as well. On Windows, Git Bash may copy the file instead, so run the commands again after updating.

Install the skill first. Both files tell the tool to follow it. A skill can only ask the tool not to edit your files; these files make the tool refuse.

Each tool expects its own format, which is why there is one file per tool. Cursor removed its custom modes in 2.1, so there you use the skill only.

### Manual install (git clone)

If you'd rather not use the installer, clone this project into the folder your tool reads. The folder depends on the tool:

| Tool | For all your projects | Only this project |
|------|----------------------|-------------------|
| [Cursor](https://cursor.com) | `~/.cursor/skills/tutor` | `.cursor/skills/tutor` or `.agents/skills/tutor` |
| [Claude Code](https://code.claude.com) | `~/.claude/skills/tutor` | `.claude/skills/tutor` |
| [OpenCode](https://opencode.ai) | `~/.config/opencode/skills/tutor` | `.opencode/skills/tutor` |
| [GitHub Copilot](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills) | `~/.copilot/skills/tutor` | `.github/skills/tutor` |
| [Gemini CLI](https://geminicli.com/docs/cli/skills/) | `~/.gemini/skills/tutor` | `.gemini/skills/tutor` |

```bash
REPO=https://github.com/kevinnio/tutor.git
TARGET=~/.cursor/skills/tutor   # user-wide example

mkdir -p "$(dirname "$TARGET")"
git clone "$REPO" "$TARGET"
```

Don't install inside `~/.cursor/skills-cursor/`. Cursor keeps its own skills there. If `TARGET` already exists, remove it or use [Upgrade](#upgrade) instead of cloning again.

### Symlink for local development

```bash
SKILL_ROOT="$HOME/code/tutor"
TARGET="$HOME/.cursor/skills/tutor"

mkdir -p "$TARGET"
ln -sf "$SKILL_ROOT/SKILL.md" "$TARGET/SKILL.md"
ln -sf "$SKILL_ROOT/references" "$TARGET/references"
```

### Install TuTor via TuTor

As a fun exercise, have TuTor install itself with you—you run every command; it coaches and checks your work. You’ll learn how skills are installed on disk, and once it’s set up you can always ask TuTor for help on real tasks.

Paste this into an AI tool that can open links (start a new chat).

**Trust note:** this prompt asks your AI tool to fetch instructions from the internet (`raw.githubusercontent.com`), pinned to release tag `v0.6` (immutable). Only run it from a source you trust — a skill you install can influence what your AI tool does in future sessions. Prefer the manual install steps above if you don't want remote instructions fetched.

```text
TuTor, install yourself with me—I run every command; you tutor.

Read and follow for this entire session:

- SKILL.md: https://raw.githubusercontent.com/kevinnio/tutor/v0.6/SKILL.md
- README Install section: https://raw.githubusercontent.com/kevinnio/tutor/v0.6/README.md

Follow TuTor’s rules: one step at a time, command breakdowns, verify after I say "done".
Never install for me (no writing skill files, no git clone, no npx on my behalf)—refuse "just do it."

First, ask me which AI tool I use (e.g. OpenCode, GitHub Copilot, Gemini CLI, Cursor, Claude Code)
and whether I want a user-wide install or project-local. Use the correct skills path for that tool.

Goal: `tutor` skill installed on my machine.
Teach `npx skills add kevinnio/tutor -g -y` unless I want manual git clone.

After I answer, give a short numbered plan for my tool and scope, then Step 1 and stop.
```

## Upgrade

### Skills CLI (recommended)

```bash
npx skills update tutor -g -y    # user-wide
npx skills update tutor -y       # this project only
```

List installed copies: `npx skills list | grep tutor`

### Manual git clone

```bash
cd ~/.cursor/skills/tutor   # your install path
git pull origin master
```

For a **git submodule**: `git submodule update --remote path/to/tutor`

### Pin to a release tag (reproducible install)

Release tags are immutable. To install an exact audited version instead of `master`:

```bash
# fresh clone
git clone --branch v0.6 https://github.com/kevinnio/tutor.git "$TARGET"
# or, inside an existing clone
git fetch --tags && git checkout v0.6
```

Verify the pinned version: `git describe --tags`

### Check your installed version

```bash
grep '^  version:' ~/.cursor/skills/tutor/SKILL.md
# path varies — use npx skills list to find installs
```

Compare with `metadata.version` in [SKILL.md](SKILL.md) on GitHub.

### After upgrading

1. **Reopen your AI tool** (or start a new chat) so it reloads the skill.
2. **Confirm the version** with the `grep` command above.
3. If behavior is unchanged, run `npx skills list` and update every scope (user-wide vs project) where `tutor` is installed.

## How to use

1. **Install** the skill (see above) and open your project in the tool.
2. **Say what you want to learn**, and that the tool should tutor you, not do the work for you.

Example prompts:

```text
I want to learn how to add tests to this repo. Walk me through it step by step; don't edit files for me.

Enséñame a crear un API REST con Express. No hagas el código por mí.

Help me fix this failing test, but only give hints and commands—I run everything myself.
```

3. **Do each step** the tutor assigns, then reply when done (e.g. “done”, “listo”).
4. The tutor **verifies** before moving on. If something is wrong, it tells you what’s missing—no skipping ahead.
5. If the tool tries to do your work, remind it: *“Follow the tutor skill—verify only, I run the commands.”*

## Repository layout

```text
tutor/
├── SKILL.md              # The skill itself (required)
├── references/           # Extra reading the tool loads on demand
│   ├── example-flow.md
│   └── tool-gate.md
├── agents/               # Optional modes (read-only)
│   ├── opencode/tutor.md
│   └── claude/tutor.md
├── README.md
├── README-es.md
├── AGENTS.md             # Instructions for agents editing this repo
├── AUTHORS.md            # Contributors (names and GitHub handles)
└── LICENSE               # MIT
```

The version lives in `SKILL.md`, in the `metadata.version` line near the top (currently **0.6**). Releases are tagged `v<version>` (e.g. `v0.6`); pin to a tag for a reproducible install.

## Contribute

We welcome feedback and collaboration.

- **Bug reports and feature requests** — [open a GitHub issue](https://github.com/kevinnio/tutor/issues/new). Describe what you expected, what happened, and which agent you use.
- **Code and docs** — send a [pull request](https://github.com/kevinnio/tutor/compare). Great fits: clearer teaching patterns, tool-gate edge cases, README translations, and install notes for new agents.

### Pull request workflow

1. **Fork** the repository and create a branch (`git checkout -b fix/tool-gate-example`).
2. **Change** `SKILL.md` and/or files under `references/`. Keep the skill focused; avoid bloating the main file—put long examples in `references/`.
3. **Test** by installing your branch into one agent (Cursor, Claude Code, or OpenCode) and running through a short learning task.
4. **Open a pull request** with:
   - What behavior changed and why
   - Which agent(s) you tested
   - Any breaking change to install paths or skill name (`tutor` must match the folder name for OpenCode)

Please do not commit secrets, personal paths, or generated `node_modules` / playground artifacts.

## Contributors

<a href="https://github.com/kevinnio/tutor/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=kevinnio/tutor&columns=3" alt="Contributors" />
</a>

Avatars are generated from [GitHub contributors](https://github.com/kevinnio/tutor/graphs/contributors) via [contrib.rocks](https://contrib.rocks) (contributors-img). Names and handles: [AUTHORS.md](AUTHORS.md).

## Donations

If TuTor helps you learn, you can buy me a coffee via PayPal:

**[paypal.me/kevindperezm](https://paypal.me/kevindperezm?locale.x=es_XC&country.x=MX)**

Donations are optional and not required to use or contribute to this project.

## License

[MIT](LICENSE) — Copyright (c) 2026 Kevin Perez
