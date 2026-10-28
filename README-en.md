# OS Lab Tutor

[简体中文](README.md) · **English**

## Purpose

An AI tutor for operating systems labs, with guidance for ChCore Lab1. This skill—a set of instructions your AI tool reads—helps you understand the lab, write your own code and report, and develop analysis and debugging skills.

## Features

- **Step by step**: follows the handout and task dependencies, focusing on one task at a time.
- **Help on demand**: explains specific concepts and commands, and guides GDB investigations that you run yourself.
- **Independent work**: you write code and reports, run tests, and fix problems; the tutor does not write assignment answers.
- **Read-only assistance**: reads materials and submitted attempts, with report feedback focused on core understanding; does not edit files or run commands for you.

## Installation

Install [Node.js](https://nodejs.org/) 22.20 or later, then run:

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g
```

This uses the [Skills CLI](https://github.com/vercel-labs/skills) to install this repository's `tutor`. Follow the prompts to select your AI tool. `-g` makes it available across projects; omit it to install only in the current project.

Start a new chat after installation and select the `tutor` skill. In Codex, explicitly select it or type `$tutor`, for example:

```text
$tutor Guide me through ChCore Lab1, starting from my current progress.
```

To enable tutoring automatically within a Lab1 project, merge the [student project template](templates/AGENTS.lab1.md) into that project’s `AGENTS.md`; preserve any existing instructions.

Based on [TuTor](https://github.com/kevinnio/tutor) · [MIT License](LICENSE)
