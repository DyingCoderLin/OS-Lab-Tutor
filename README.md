# OS Lab Tutor

**English** · [Español](README-es.md)

An **agent skill** (a folder of instructions your AI tool loads when it's relevant) that turns it into a learning tutor. TuTor gives a brief plan, assigns the current handout task, and waits. It explains concepts or debugging when you ask, without completing the assignment for you.

Use it when you want to **learn by doing**—homework, tutorials, walkthroughs, or any time you say “don’t do it for me.”

## Objective

TuTor helps **teachers and students** use AI as a coach, not a cheat sheet. Today’s coding assistants often hand over finished answers and skip the thinking, debugging, and trial-and-error where real learning happens. This skill redirects that power toward **learning by doing**: the learner writes the code and runs the commands; the agent explains concepts and tools and identifies deliverable locations; for Lab1 it routes checks or continued progress while the student performs tests, debugging, and repairs—without doing the work for them. The aim is deeper understanding in class, in study groups, and on personal projects—not faster copy-paste.


## What it does

| Behavior | Detail |
|----------|--------|
| **Original tutor rhythm** | First introduce the lab and collaboration, then a title-only plan and complete current task requirements with report/code destination; then wait. Thinking question 1 precedes TODO 1. Explanations are available on request; no added prerequisite quizzes or mini-lessons. |
| **Your report document** | Create a dedicated report document yourself and tell the tutor its path. Choose any readable format and organization; no required template, headings, or layout. The tutor reads it but never writes it for you. |
| **Context and task order** | Thinking questions include a labelled source section/local reading range for their premises. Read that context yourself. Page-table order: question 8 → exercise 10 / TODO 5 → question 9 → 11/12; question 9 uses your implementation. |
| **Lab1 stages and destinations** | The tutor recognizes the current Lab1 handout and gives each active task one destination: a topic in your report or a specific code TODO. Any required write-up is a separate report task. Question numbers are topic references, not required headings. |
| **Lab1 completion** | No immediate TODO verdict. Use a real applicable focused check or continue; after TODO 1/4, get runnable GDB steps and expected observations immediately, with an optional skip path. No extra opt-in is needed. Whole-lab grading stays separate. |
| **Hints without answers** | No TODO implementations, defective lines, root causes, correct values, or repair recipes, including in prose. |
| **No assignment answers** | Requests to directly complete a thinking question, provide reference report text, or walk through the whole solution are refused. You can ask about a specific confusing instruction/concept. |
| **Report feedback** | Core understanding is enough: an adequate answer passes and you move on. No wording polish or optional improvements. Only fundamental errors or missing central requirements receive brief feedback; the tutor never writes the answer. |
| **GDB coaching** | When make grade is below full marks or you ask for debugging help, get relevant stages/functions, breakpoint candidates, registers/memory, and explained commands. You run, locate, and repair the problem; the tutor never names the code defect or fix. |
| **Tool gate** | Read-only inspection supports your question; the tutor reviews submitted work but never edits files or runs builds, programs, tests, or debuggers. |
| **Command teaching** | Every suggested command explains its goal, arguments, and the kind of evidence it yields; no solution-bearing expected output. |

Optional deep dives live in [`references/`](references/):

- [`references/example-flow.md`](references/example-flow.md) — OS lab review and debugging without revealing repairs
- [`references/tool-gate.md`](references/tool-gate.md) — which shell commands are allowed
- [`references/gdb-coaching.md`](references/gdb-coaching.md) — student-led debugger investigation
- [`references/lab1-guide.md`](references/lab1-guide.md) — ChCore Lab1 stage/report/TODO map and source-backed check inventory

## Lab1 submissions

Submit three parts: the authentic AI conversation record, your dedicated report
document, and your modified Lab1 files containing the TODO implementations.
Keep/export the real conversation using your tool's supported method. Stage tasks
write to either the report or a code TODO; testing/debugging supports those tasks
and does not add another mandatory submission. Only fundamental report errors need brief
feedback; adequate answers pass without polishing; code TODOs keep the check-or-continue and no-defect-disclosure policy.

## Project instructions for plain Lab1 prompts

The global skill is manual-only in Codex. To use it directly, select it or write
`$tutor`; “help me with Lab1” alone does not ensure the skill is loaded.

If a student Lab1 workspace should always preserve these learning boundaries,
copy [templates/AGENTS.lab1.md](templates/AGENTS.lab1.md) to that workspace as
`AGENTS.md`, or merge it into existing project instructions. Do not overwrite
an existing file or copy this repository's maintainer `AGENTS.md` there.
The student template stands on its own: ordinary requests follow the report/code
boundaries even without invoking the skill. Open Codex in that Lab1 directory;
after installing/changing the file, restart the run or explicitly reread it in
an existing chat. This option affects that project, not global skill activation.

## Install

This fork is based on [TuTor](https://github.com/kevinnio/tutor). Its **0.7.7-dev** rules are unreleased; remote installs include them only after these changes are published. In Codex, explicitly select the skill or invoke `$tutor`; automatic invocation is disabled. Other tools may select skills differently.

**Repository:** [github.com/DyingCoderLin/OS-Lab-Tutor](https://github.com/DyingCoderLin/OS-Lab-Tutor)

TuTor is a folder with `SKILL.md` (the instructions) plus `references/` (extra reading). Keep the folder named `tutor`. Some tools refuse to load a skill if the folder name doesn't match the name inside `SKILL.md`.

### Install with Skills CLI (recommended)

The [Skills CLI](https://github.com/vercel-labs/skills) ([skills.sh](https://skills.sh)) is a small installer. It looks for the AI tools on your computer and puts the skill in the right folder for each, so you don't need to know the paths.

**User-wide (all projects)** — recommended for your first install:

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g -y
```

**This project only** (share with a class or team via git):

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -y
```

**Pick specific tools** (skip the menu):

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g -a opencode -a github-copilot -a gemini-cli -y
```

| Flag | Meaning |
|------|---------|
| `-g`, `--global` | User-wide install (`~/…/skills/`) |
| (no `-g`) | Install into the current project only |
| `-a`, `--agent` | Which tools to install for, e.g. `opencode`, `github-copilot`, `gemini-cli`, `cursor`, `claude-code`, `codex` |
| `-y`, `--yes` | Non-interactive |

Preview before installing: `npx skills add DyingCoderLin/OS-Lab-Tutor --list`. Every supported tool: [vercel-labs/skills](https://github.com/vercel-labs/skills#supported-agents).

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
REPO=https://github.com/DyingCoderLin/OS-Lab-Tutor.git
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
ln -sf "$SKILL_ROOT/agents" "$TARGET/agents"
```

### Install TuTor via TuTor

As a fun exercise, have TuTor install itself with you—you run every command; it explains concepts and helps you decide how to check your work. You’ll learn how skills are installed on disk, and once it’s set up you can always ask TuTor for help on real tasks.

Paste this into an AI tool that can open links (start a new chat).

**Trust note:** this prompt asks your AI tool to fetch instructions from the internet (`raw.githubusercontent.com`), from the development branch `master` (which can change). Only run it from a source you trust — a skill you install can influence what your AI tool does in future sessions. Prefer the manual install steps above if you don't want remote instructions fetched.

```text
TuTor, install yourself with me—I run every command; you tutor.

Read and follow for this entire session:

- SKILL.md: https://raw.githubusercontent.com/DyingCoderLin/OS-Lab-Tutor/master/SKILL.md
- README Install section: https://raw.githubusercontent.com/DyingCoderLin/OS-Lab-Tutor/master/README.md

Follow TuTor’s rules: brief plan, current handout task, then wait; explain when I ask, without extra quizzes. Use command breakdowns and the active lab's completion policy. For Lab1, ask me to create/designate a report document and share its path, accept my free-form layout, name each report/code destination, and route "done" to a student-run focused check or the next stage, without an immediate correctness verdict. Never reveal repairs.
Never install for me (no writing skill files, no git clone, no npx on my behalf)—refuse "just do it."

First, ask me which AI tool I use (e.g. OpenCode, GitHub Copilot, Gemini CLI, Cursor, Claude Code)
and whether I want a user-wide install or project-local. Use the correct skills path for that tool.

Goal: `tutor` skill installed on my machine.
Teach `npx skills add DyingCoderLin/OS-Lab-Tutor -g -y` unless I want manual git clone.

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

This fork's `0.7.7-dev` rules do not yet have a release tag. The old `v0.6` version lacks these changes. After a release is published, use its actual tag in `git clone --branch <release-tag>` and inspect the revision with `git describe --tags --always`. Do not assume a development version has a published tag.

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

Help me investigate this failing test with GDB. Suggest useful stages, breakpoints, and registers with explained commands; do not reveal the faulty code or fix.
```

3. **Attempt the current handout task yourself.** Ask for help when needed, then reply when done. The tutor does not insert extra questions before you may start a TODO.
4. **In Lab1, designate your report:** create a dedicated document yourself (or use one you already created), then tell the tutor its path. Write however you like, as long as the tutor can understand it. Thinking answers go there; coding tasks go in the named TODO; any required implementation explanation is a separate report task. The tutor accepts core-correct report work without polishing and only flags fundamental errors, but cannot write a full answer, fill missing reasoning, or directly identify a code defect or repair. After each TODO, run a genuine focused check if one is available now; otherwise continue without a tutor verdict. The original five-TODO version has integrated `make grade` rather than isolated automated tests, plus optional manual GDB observations after TODO 1/4. The tutor gives the actual commands and observations up front; executing them is optional. Final acceptance is the make grade score: full marks passes; otherwise get GDB locations/register changes based on failed scoring items, revise your code, and rerun make grade. No additional acceptance checks are imposed. Other lab workflows can still use source-review feedback.
5. If the tutor jumps to a Lab1 verdict or fix, remind it: *“Tell me where this stage's result belongs. Give me an existing focused check to run, or let me continue if there is none. I will investigate observed failures with GDB.”*

## Repository layout

```text
tutor/
├── SKILL.md              # The skill itself (required)
├── references/           # Extra reading the tool loads on demand
│   ├── example-flow.md
│   ├── gdb-coaching.md
│   ├── lab1-guide.md
│   └── tool-gate.md
├── agents/               # Optional modes and Codex invocation policy
│   ├── openai.yaml
│   ├── opencode/tutor.md
│   └── claude/tutor.md
├── templates/
│   └── AGENTS.lab1.md
├── README.md
├── README-es.md
├── AGENTS.md             # Instructions for agents editing this repo
├── AUTHORS.md            # Contributors (names and GitHub handles)
└── LICENSE               # MIT
```

The version lives in `SKILL.md`, in the `metadata.version` line near the top (currently **0.7.7-dev**). This is an unreleased development version; release tags are created separately when publishing is requested.

## Contribute

We welcome feedback and collaboration.

- **Bug reports and feature requests** — [open a GitHub issue](https://github.com/DyingCoderLin/OS-Lab-Tutor/issues/new). Describe what you expected, what happened, and which agent you use.
- **Code and docs** — send a [pull request](https://github.com/DyingCoderLin/OS-Lab-Tutor/compare). Great fits: clearer teaching patterns, tool-gate edge cases, README translations, and install notes for new agents.

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

<a href="https://github.com/DyingCoderLin/OS-Lab-Tutor/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=DyingCoderLin/OS-Lab-Tutor&columns=3" alt="Contributors" />
</a>

Avatars are generated from [GitHub contributors](https://github.com/DyingCoderLin/OS-Lab-Tutor/graphs/contributors) via [contrib.rocks](https://contrib.rocks) (contributors-img). Names and handles: [AUTHORS.md](AUTHORS.md).

## Donations

If TuTor helps you learn, you can buy me a coffee via PayPal:

**[paypal.me/kevindperezm](https://paypal.me/kevindperezm?locale.x=es_XC&country.x=MX)**

Donations are optional and not required to use or contribute to this project.

## License

[MIT](LICENSE) — Copyright (c) 2026 Kevin Perez
