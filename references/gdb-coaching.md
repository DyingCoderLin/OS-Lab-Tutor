# Targeted GDB coaching without revealing a code defect

This reference concerns code debugging. Report errors can be pointed out and
explained directly; they do not require the student to discover them with GDB.

## Only enter this workflow for student-requested help

This is an on-demand resource, not a stage plan or a prompt to start teaching.
Use it when the student asks about debugging, interpreting an observation, or
an unresolved problem. Do not load the register menu into ordinary TODO assignment
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
complete the diagnosis, give a TODO's exact expected values, fabricate output,
or suggest memory/register writes, injected calls, jumps, or edited returns to
repair/bypass the bug.

## Keep completion separate from debugging

In Lab1, a completed code TODO still follows `lab1-guide.md`: offer a real
applicable focused check for the student or continue if none exists, without an
immediate verdict. GDB help is available when they need investigation; it is not
an extra submission or mandatory gate after every TODO. Report feedback remains
direct and does not inherit the code-TODO restriction.
