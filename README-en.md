# OS Lab Tutor

[简体中文](README.md) · **English**

## Purpose

An AI tutor for operating systems labs, with guidance for ChCore Lab1, Lab2 and Lab3. This skill—a set of instructions your AI tool reads—helps you understand the lab, write your own code and report, and develop analysis and debugging skills.

## Features

- **Step by step**: follows the handout and task dependencies, focusing on one task at a time.
- **Help on demand**: explains specific concepts and commands, and guides GDB investigations that you run yourself.
- **Independent work**: you write code and reports and fix problems, with explanations and guidance on demand.
- **Lab1 assistance**: reads materials and submitted attempts while you run commands and debug.
- **Lab2 implementation guidance**: ask for a TODO function's implementation idea, necessary steps, and what each step does and why. The tutor may explain current interfaces and data structures, but does not provide code, pseudocode or a statement-by-statement prose implementation, or directly locate and repair bugs in your code.
- **Lab2 execution support**: the tutor may run existing builds/tests, explain output, export authentic logs and package submissions. You write the core TODOs and code changes, and operate GDB. The revised Lab2 retains `split_chunk` and `merge_chunk` in exercise 1, `query_in_pgtbl` in exercise 4, and the three blanks in `handle_trans_fault` in exercise 10: four functions and six blanks. Exercise 9 (`find_vmr_for_va`) is instructor-provided. Questions 5 and 6 and challenges 7 and 11 are not assigned; the other related code is provided. Completion means 100 points on the existing basic grading items. Submit code and authentic dialogue; no lab report is required. Environment installation and repair follow the existing course requirements.
- **Lab3 execution support**: the tutor may explain implementation approaches, run existing builds and tests, explain their output, export authentic logs and package submissions. You complete the TODOs, edit the code and operate GDB. In exercise 1, initialize the capability group and handle initialization failures in `sys_create_cap_group`. In exercise 2, set ELF segment mapping permissions in `create_root_thread`. In exercise 3, initialize the thread context in `init_thread_ctx`. In exercise 5, fill in the exception vector table `el1_vector`. In exercise 6, save and restore general-purpose registers in `exception_enter` and `exception_exit`. There is one blank in each of three C functions, one vector table and two assembly macros. Completion requires 100 points across five items worth 20 points each. Submit your modified code and authentic AI conversation. No lab report is required. Environment installation and repair follow the existing course requirements.

The current development version is **0.7.19-dev** and has no release tag yet.

## Installation

Install [Node.js](https://nodejs.org/) 22.20 or later, then run:

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g
```

This uses the [Skills CLI](https://github.com/vercel-labs/skills) to install this repository's `tutor`. Follow the prompts to select your AI tool. `-g` makes it available across projects; omit it to install only in the current project.

Start a new chat after installation and select the `tutor` skill. In Codex, explicitly select it or type `$tutor`, for example:

```text
$tutor Guide me through ChCore Lab2, starting from my current progress.
```

Based on [TuTor](https://github.com/kevinnio/tutor) · [MIT License](LICENSE)

## Course project setup

Lab1 uses `templates/AGENTS.lab1.md` and `templates/CLAUDE.lab1.md`. Lab2 uses `templates/AGENTS.lab2.md` and `templates/CLAUDE.lab2.md`. Course maintainers place each pair in the matching lab directory as `AGENTS.md` and `CLAUDE.md`. The entrypoints require loading the full skill and the matching lab guide.

Lab2 requires a skill copy containing `references/lab2-guide.md`. For a course-provided local update, its entrypoint supports directly reading the sibling `DyingCoderLin_OS-Lab-Tutor` repository. Remote installation commands retrieve remote content, so local changes must reach that remote before they become available through those commands.

For Lab3, use `templates/AGENTS.lab3.md` and `templates/CLAUDE.lab3.md` with [the Lab3 guide](references/lab3-guide.md).
