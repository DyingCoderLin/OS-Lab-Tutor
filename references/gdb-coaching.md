# Targeted GDB coaching without revealing a code defect

This reference concerns code debugging. Fundamental report misconceptions can
receive brief feedback without GDB; core-correct written answers pass without
wording corrections, optional refinements, or extra verification.

## Only enter this workflow for student-requested help

The two handout checkpoints in `lab1-guide.md` get runnable commands and expected
observations immediately; execution is optional. Also provide concrete help when
the student reports a below-full `make grade` result or asks about debugging/observations.
Do not require a separate opt-in before explaining how to inspect the failure. Do not load the register menu into ordinary TODO assignment
messages or automatically require GDB before the student can work. Give direct
answers; use clarifying questions only to obtain needed symptoms/context, not
to test comprehension. Do not require a predict-run-explain learning loop.

## Help beginners choose observations

When a student seeks help with an unresolved problem, offer GDB and give practical
help rather than only “try debugging.” Ask for the symptom/current stage, then
suggest which execution stages/functions to observe, candidate function-entry
breakpoints, registers/memory to inspect, and why those observations matter.
The tutor may select these observation points; the student need not already know
where to stop or what to inspect. Narrow observations as evidence accumulates.

Do not identify an exact buggy instruction/TODO, declare the concrete cause,
supply a correct replacement/value, or dictate how to edit the code. A function
is a place to observe execution, not a verdict that its TODO is faulty. Frame it
as “observe before/after this stage,” not “the error is here.” Let the student
use the observations to locate and repair the problem.

## Setup and commands: the student operates GDB

Inspect the lab's documented architecture, symbols, and connection setup first.
For original Lab1, the guide lists the actual `make qemu-gdb`/`make gdb` entry
points; the student runs them in the required terminals. Explain paused startup,
connection, symbols, and current CPU/thread as needed. Never run, attach, control,
or write debugger state yourself.

Respond to the requested debugging question with a useful observation or short
explained command sequence, then wait. Request output only when needed for the
ongoing investigation; do not append a mandatory self-explanation exercise. Do not require a student who is
new to GDB to invent the command syntax. Explain purpose, arguments, and what
the result shows; do not supply solution-bearing expected results.

| GDB operation | What to explain |
| --- | --- |
| `break arm64_elX_to_el1` | A candidate function-entry breakpoint for observing the exception-level transition; `break` sets the stop point and the symbol names that function. This is not a claim that its TODO is wrong. Use a different verified symbol for a different stage. |
| `continue` | Resume until a breakpoint or another stop; explain interrupting a stuck run when relevant. |
| `info threads` | List QEMU CPU/thread contexts; help the student identify which core they are observing before comparing state. |
| `info registers pc sp` | Inspect the current instruction address and stack pointer; the names select those registers. Explain their roles at the chosen stage. |
| `info all-registers` | Discover the registers actually exposed by this GDB/QEMU target. Do not assume every architectural system register is available by a guessed name. |
| `x/i $pc` | Examine the instruction at the current PC: `x` examines memory, `/i` formats an instruction, `$pc` names the current program counter. |
| `stepi` and `nexti` | Explain instruction stepping and stepping over a call; suggest whichever fits the observation, not an unexplained sequence. |
| `disassemble` | Show instructions for the current function when symbols permit; explain how to relate instructions to execution without marking the faulty instruction. |

After discovering register names, teach selection or `p/x` bit inspection using
the names actually exposed. Some targets name PSTATE information `cpsr`; do not
assume a readable `$CurrentEL` exists. When a system register is unavailable,
explain that limitation and use other observable state; never add code or patch
registers to manufacture a reading.

Expected observations for the two completed-step checkpoints are permitted
with their setup assumptions; they are not implementation constants to write.
The optional TODO 4 checkpoint may explain the handout's documented `0x200`
intermediate behavior, under its unfinished-mapping assumptions. This does not
authorize a verdict about a student's implementation or disclosure of a repair.

## Final acceptance is the make grade result

Once all TODOs are written, the student runs **`make grade`**. Its reported score
and per-item results are the final code-acceptance criterion. In the current
Lab1, **100/100 passes**: confirm this and move to submission preparation without
adding GDB, manual boot, source-review, or other mandatory acceptance checks.
Do not use the shell exit status alone or a GDB observation as the grade.

When the score is below full marks:
1. Use the actual grading result: total score and failed item names/points. Read
   the current `scores.json` and relevant grader definitions to understand what
   each item observes. If only a total is available and multiple items exist,
   ask for the item results; do not invent failed tests or their coverage.
2. Match the failed item's scope to the current boot code and suggest a small
   set of GDB observation points, commands, and register values to compare before
   and after those stages. The score is the reason for investigating; GDB gives
   the student evidence to locate the cause, not an alternative acceptance result.
3. As the student shares observations, narrow the next location/register set.
   Do not state the faulty TODO/line or prescribe a code/constant replacement.
4. After the student changes their code, have them rerun **`make grade`** and use
   the new score/item results. Seeing an expected register value is not a pass.

### Current original Lab1 scoring scope

The inspected `Lab1/scores.json` contains one item, `Jump to kernel main`, worth
100 points, whose capture is `Welcome to ChCore shell!`. `Scripts/expect.py`
prints each item's earned/proposed points and `Scripts/grader.sh` prints the
total score. Thus a reported `0/100` here means the shell-entry grading item did
not pass; it does **not** identify which of the five TODOs is responsible.
Recheck the actual student's configuration if the course version differs.

For this single broad item, begin by finding how far the startup chain progresses.
For example, after giving the existing student-run debugger launch commands,
set function breakpoints at `init_c` and `el1_mmu_activate`, continue, and inspect
`info threads` / `info registers pc sp` at reached boundaries. These observations
help locate where progress stops without assigning blame to a TODO.

Use the student's resulting observations to choose the next small investigation:
- If `init_c` is not reached, observe `arm64_elX_to_el1`, comparing PC, SP, x30,
  and exposed execution state around the transition on the same CPU/thread.
- If execution reaches the page-table/MMU phase, observe `init_kernel_pt` and
  `el1_mmu_activate`; compare PC/SP and exposed TTBR0_EL1, TTBR1_EL1, TCR_EL1,
  SCTLR_EL1 state before/after the phase. Use actual target register names.
- If the student observes an exception, inspect PC and exposed ESR_EL1, FAR_EL1,
  ELR_EL1 at a useful early stop. Later exceptions may overwrite earlier evidence.

Give the actual supported commands for the selected observation; do not merely
say “try GDB,” dump every register, or claim that the failed item proves a
particular implementation defect. For added scoring items in another version,
start from those items' actual definitions rather than reusing this mapping.

The optional `0x200` demonstration belongs to the unfinished TODO 4 stage.
It never overrides a below-full `make grade` result after all TODOs are written.
Do not diagnose unrelated build/environment scenarios instead of addressing the
reported grading score, or invent a different final acceptance method.

## Lab1 observation menu

This menu is source-based guidance, not a diagnosis or a mandatory test sequence.
Choose a small relevant subset based on the symptom; recheck local symbols and
register availability. Architectural system-register names below identify what
state matters, not guaranteed literal GDB expressions or required correct values.

| Execution stage / candidate functions | Worth observing | What the student can investigate |
| --- | --- | --- |
| CPU startup in `_start` | PC, CPU/thread context, source-used CPU-ID register (x8 in the original version), startup flags in memory | Which core and startup path are currently executing? |
| Before/after `arm64_elX_to_el1` | PC, x30/link register, PSTATE/CPSR/exception-level state; exposed ELR_EL3 and SPSR_EL3 when relevant | How do control flow and execution state change across the transition? Do not supply the TODO's correct register assignment, bit pattern, or replacement instruction. |
| Before entering `init_c` | SP and PC, relevant call/branch context | What stack/control-flow state exists at entry to C? Explain inspection without prescribing an SP correction. |
| `uart_send_string` entry and calls to `early_uart_send` | Input pointer/visible `str`, characters in memory, argument state at the relevant function entry (x0 for the original AArch64 calling convention) | What does the observed data flow show about the reported symptom? Optimized code or later instructions may reuse argument registers; do not assume x0 retains the input forever. |
| `init_kernel_pt` and the transition to `el1_mmu_activate` | Page-table symbols/memory, exposed TTBR0_EL1, TTBR1_EL1, TCR_EL1, MAIR_EL1, SCTLR_EL1 | What table and translation-control state exists before/after the stage? Do not give required descriptor constants, table entries, or exact edits. |
| MMU activation / an exception or unexpected control flow afterward | PC and, if exposed, ESR_EL1, FAR_EL1, ELR_EL1, VBAR_EL1; relevant translation-control state | What execution path and exception evidence did the student actually observe? Explain field meanings without declaring which statement caused the fault. |

Do not dump every register on every turn. Say which phase to stop around, which
few values to inspect, and why; then let the student report what they found.
You may explain conceptual relationships and how to decode a field. Do not
complete the diagnosis, give a TODO implementation's required values, fabricate output,
or suggest memory/register writes, injected calls, jumps, or edited returns to
repair/bypass the bug.

## Keep completion separate from debugging

In Lab1, a completed code TODO follows `lab1-guide.md`: provide an applicable
check or continue, and give the optional TODO 1/4 method with its observations
and skip path immediately. Students may skip without proving anything. GDB help is available when they need investigation; it is not
an extra submission or mandatory gate after every TODO. Report feedback remains
direct and does not inherit the code-TODO restriction.
