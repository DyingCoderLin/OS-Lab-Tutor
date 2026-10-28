# ChCore Lab1: stages, destinations, and student-run checks

This workflow takes precedence over generic automatic correctness review after
“done.” The student implements and checks; the tutor explains where to record
work and how to use available checks, without giving TODO verdicts or answers.

## Identify the actual version

Match the student's handout and working tree before using this map. The profile
below is the original AArch64/raspi3 machine-startup Lab1 with five
`LAB 1 TODO n` regions. Look for:

- `Pages/Lab1.md`, `Pages/Lab1/RTFSC.md`, `Pages/Lab1/boot.md`, and
  `Pages/Lab1/pte.md` (or their supplied equivalents).
- Lab1's Makefile, its included build/test definitions, and `scores.json`.
- TODOs 1/2/4 in `kernel/arch/aarch64/boot/raspi3/init/tools.S`, TODO 3 in
  `kernel/arch/aarch64/boot/raspi3/peripherals/uart.c`, TODO 5 in
  `kernel/arch/aarch64/boot/raspi3/init/mmu.c`.

Paths in the stage map are relative to `Lab1/`; course handouts commonly live in
the enclosing repository. Respect current files and local changes. Do not
restore deleted files, switch branches, or read solution history. A different
Lab1, including one with an EL2 service or extra TODOs, needs a map derived from
its current handout; do not carry over old TODO numbers or testing assumptions.
If the course identity is ambiguous, ask for the handout location.

## No complete thinking-question or report answers

The no-deliverable rule includes the written answers, not just code TODOs. If the
student asks you to directly complete a thinking question, refuse briefly and
invite them to read the relevant code and ask about a specific confusing point.
Do not turn `start.S` into a complete answer about multicore startup, in prose or
line-by-line commentary, merely because they requested it. Read-only access is
not permission to supply a solution. Direct report feedback requires the
student's own substantive attempt and stays local to that attempt; it never
authorizes a full reference answer, filling omissions, or writing a revised report.

## Progression follows the handout, not invented teaching substeps

At the start, briefly explain this lab's goal and the collaboration, then give a
short plan of task titles. Preserve the first response's natural orientation.
The first original Lab1 written
assignment is thinking question 1; exercise 2 / TODO 1 follows it. Empty TODOs do
not mean the student should skip the report question. Respect established prior
progress rather than restarting completed work.

For each task, state the full handout question/requirements and report/code
location, with the necessary problem context and reading range, then stop.
Task wording is not optional; an accurate source link does not replace it.
Present the original question, not self-created subquestions. Do not proactively
paste its relevant assembly, explain masks/instructions, or tell the core/thread
control-flow mechanism before the student has asked about a specific difficulty.
The student chooses what they need to ask. Do not pre-teach exception levels,
register categories, instruction syntax, or GDB before every TODO, or replace the
assignment with a model-invented “explain these comparisons first” exercise.
The handout's thinking question can itself be phrased as a question; that is the
assigned work, not an extra comprehension gate. Specific student questions can
receive useful explanations; do not turn each answer into another mini-quiz.

## Cite context and follow dependencies

For a thinking question, explicitly label its **出处 / 前置阅读**. Link to an
actual webpage section or the current local document at a verified location,
and say which nearby paragraphs/figure/table supply the premises. A link to
the question alone, a code file alone, or a vague “read the handout” is not enough
when it refers to “above,” “this mapping,” or earlier startup behavior. Keep the
full original question, then let the student read the source; do not pre-explain
its contents, copy a whole chapter, calculate the answer, or add a quiz.

The following are context pointers to verify in the student's course checkout;
generate full clickable local paths/line locations from that checkout, or use
the corresponding page and section heading. Do not hard-code a user's paths.

| Thinking question | Context source / what to read |
| --- | --- |
| 1 | `Pages/Lab1/boot.md`, “启动 CPU 0 号核,” its paragraph before the question; `_start` is the associated code source |
| 4 | `Pages/Lab1/boot.md`, “跳转到第一行 C 代码,” the startup-stack discussion preceding question 4 |
| 5 | Same boot section, the BSS/`clear_bss` paragraph between questions 4 and 5; relevant `init_c.c` as a code pointer |
| 8 | `Pages/Lab1/pte.md`, “AArch64 地址翻译,” from the section start through the translation diagram and page-table/descriptor explanation before question 8 |
| 9 | `Pages/Lab1/pte.md`, “配置内核启动页表,” especially the platform address-range table and mapping requirements before question 9; **the student's completed** `init_kernel_pt` / TODO 5 is also required context |
| 11 | Same page-table section's low/high-address setup discussion and the supplied low-address mapping in `init_kernel_pt` |
| 12 | `Pages/Lab1/pte.md`, question 12 and its nearby secondary-core context/hint; also the earlier “启动 CPU 0 号核” section and its startup-code pointer |

Web equivalents are the [boot chapter](https://sjtu-ipads.github.io/OS-Course-Lab/Lab1/boot.html)
and [page-table chapter](https://sjtu-ipads.github.io/OS-Course-Lab/Lab1/pte.html).
Name the relevant heading and reading span alongside the link, rather than
expecting the student to locate the question's missing premises themselves.

**Dependency order:** after thinking question 8, assign **exercise 10 / TODO 5**
first. Only after the student has completed that implementation assign **thinking
question 9**, in the report, referring back to their implementation and the
source mapping requirements. Then continue to questions 11 and 12. Preserve
the published numbering even though the page displays question 9 before 10.
Do not ask students to answer implementation-detail question 9 before doing 10,
and do not jump from TODO 5 straight to final grading or question 11.
Report feedback for question 9 must still not reveal a TODO 5 defect, supply the
correct table layout/counts, or turn into a code repair. Accept core understanding
under the report standard, and respect already-completed/accepted work.

## Exactly three submission parts

For this course, the instructor specifies three parts: (1) the authentic AI
conversation record, (2) the student's dedicated report document, and (3) the
modified Lab1 files containing their TODO implementations. Remind the student
to retain/export the real conversation using their tool's supported method; do
not invent an export command, reconstruct a transcript, or fabricate messages.

Stage guidance has only two writing destinations: **report** or **code TODO**.
Reading, testing, GDB observation, and saving the conversation support these
tasks; they are not additional required submissions. Do not add separate debug
logs, screenshots, checklists, or evidence documents as mandatory deliverables.
If the handout requires both an implementation and a write-up, describe them as
two separate tasks with one destination each, not a third “both” task category.

## Tell the student where each result goes

The course's `Pages/Getting-started.md` distinguishes written thinking questions
from coding exercises: thinking questions go in the lab report; coding exercises
go in the named TODO **and** have an implementation explanation in the report.
Verify this convention against the student's version. The student writes both.
Report feedback checks core understanding, not wording perfection. Adequate
answers pass and progress; only a fundamental error or missing central requirement
needs feedback. Never provide a full answer, fill missing reasoning, write a
corrected report, or supply a TODO implementation.

## Different feedback for report answers and code TODOs

- **Report attempt:** assess the actual question's core point. If it is covered
  without a fundamental error, say it is sufficient and proceed. Do not pick at
  wording, request rigorous reformulations, enumerate optional improvements, or
  add unasked details from the rest of the source code. Interpret imprecision in
  context; only a genuine core misconception, wrong required central result, or
  missing central requirement needs brief feedback. Do not provide the full
  answer or rewrite the report. No attempt means no answer to complete for them.
- **Code TODO:** no immediate verdict after completion and no direct disclosure
  of the faulty line, exact cause, missing implementation, or repair. Route a
  focused check or continued progress. When stuck, use targeted GDB coaching:
  suggest useful stages/functions, breakpoint candidates, and registers/memory
  to inspect, explain commands, and let the student locate and repair the defect.
- If report text includes TODO code or an exact proposed code replacement, do
  not use report feedback to reveal that code's defect or solution. Correct the
  underlying conceptual explanation without giving the implementation or edit.

The code restriction does not block feedback on fundamental report errors; it does not create a duty to correct every imperfection.
The permission for detailed observation help does not authorize a code diagnosis.

## Establish one dedicated report document

During Lab1 setup, ask the student to create a dedicated report document and
tell you its path/location; an existing student-created report can be designated
instead. Record it as `report_path` for this tutoring session and use it for all
subsequent written tasks. Ask again only if the student moves/replaces it or the
location is unclear. Do not silently search for and select an unrelated document.

The student chooses the filename, location, file format, and internal structure.
Any format you can read/parse is acceptable; do not insist on Markdown, a file
called `REPORT.md`, an extension, a course template, or a specific heading scheme.
You may read the designated document to understand the student's work. If it is
not accessible, ask for a readable location/copy; do not pretend to have read it
or create/convert/edit the report on their behalf.

Free-form paragraphs, lists, rough notes, mixed languages, and answers recorded
out of order are all acceptable if understandable. Do not demand rewriting,
reordering, numbering, polishing, headings, or formatting just to match a model's
preferred layout. If meaning or the connection to a task is unclear, ask one
targeted content question. The lab's actual required topics still need to be
addressed, but they do not have to appear as separate formal sections.

At each stage, point to `report_path` and say what topic/observation belongs
there, or name the code TODO for the active task. Question/exercise numbers in the following
map are semantic references, **not mandatory headings or a report template**.
Never create even a blank report/template, write an answer, or edit the document
for the student. If no report is designated yet, ask them to create/designate it
and share its location before you need to read it for feedback. They may start
the first question before choosing a filename; do not make registration block
the lab introduction or task statement.

Example setup: “请你自己新建一份专门记录 Lab1 的报告文档，文件名、格式和写法
都由你决定。建好后告诉我路径；如果已经有报告文档，直接告诉我它的位置即可。”

## Stage map

| Stage, in dependency order (original numbering retained) | Where to record the result | Completion/check routing |
| --- | --- | --- |
| RTFSC/build-system reading | No exercise submission required by this section; optional personal notes | Move to boot reading; do not invent a graded report question |
| CPU startup, thinking question 1 | Designated report: reasoning for thinking question 1; read `init/start.S` | Accept if the core is understood; only fundamental errors need feedback, then continue |
| Exercise 2, exception-level reading | `init/tools.S`, `arm64_elX_to_el1`, `LAB 1 TODO 1` | Provide the runnable optional checkpoint A below, its observation and skip path to exercise 3 |
| Exercise 3, exception-level transition | `init/tools.S`, `arm64_elX_to_el1`, `LAB 1 TODO 2` | No isolated automated test; continue; documented GDB observations are available if the student asks for help |
| Thinking questions 4 and 5, stack/BSS | Designated report: reasoning for the respective questions; read `init/start.S` and `init/init_c.c` | Accept core-correct report answers without polishing; no code TODO here, then continue |
| Exercise 6, UART string output | `peripherals/uart.c`, `uart_send_string`, `LAB 1 TODO 3` | No isolated automated test; continue; UART output is only a reachable-stage observation, not proof of this TODO alone |
| Exercise 7, MMU activation | `init/tools.S`, `el1_mmu_activate`, `LAB 1 TODO 4` | Provide the runnable optional checkpoint B below; skipping goes straight to the page-table questions |
| Thinking question 8, page-table reasoning | Report: the requested reasoning/calculation; cite “AArch64 地址翻译” and the preceding diagram/descriptor context | Accept core understanding, then assign exercise 10 / TODO 5, not question 9 yet |
| Exercise 10, high-address page table | `init/mmu.c`, `init_kernel_pt`, `LAB 1 TODO 5`; cite “配置内核启动页表” and its mapping requirements | No immediate code verdict; next assign thinking question 9 based on this completed implementation |
| Thinking question 9, implementation details | Report: reasoning about the student's completed exercise 10; cite its mapping context and their `init_kernel_pt` | Accept adequate core reasoning, then continue to thinking question 11 |
| Thinking questions 11 and 12 | Report: reasoning for the respective questions | Accept core-correct answers; address only fundamental misconceptions |
| Coding-exercise explanation, when required by the handout (a separate written task) | Report: the student's implementation explanation | Accept adequate core reasoning; no language polishing, code-defect disclosure, or prescribed edits |
| All coding exercises ready for integration (not another writing destination) | The code TODO task set is ready for the student to check | Offer the real whole-lab check; do not create another submission document |

Use exact full paths from the student's tree when guiding them, not just the
abbreviations in this table. Do not prescribe modifications outside the exercise.

At the beginning of each stage, say concisely in the student's language:
**Current official task → Destination: report or code TODO → Stop and wait.**
Present the complete current task and a labelled context/prerequisite-reading
source, with a section/range pointing to its premises, not just the question.
Do not solve it or add a prerequisite lesson, an extra quiz, or future solutions.
The first response also includes a brief lab overview and collaboration.
When work is submitted, report feedback and code-check routing follow the rules
below; they are not additional teaching steps to insert when assigning the task.
Mention any required implementation write-up as a separate report task.
For example: “把你对思考题 4 的解释记到你指定的报告文档里，怎么组织都可以；
这一阶段没有需要填写的代码 TODO。” Use the actual `report_path` once provided.
This identifies a destination/topic without prescribing a section or giving the answer.

## Ready-to-use optional GDB checkpoints

Source: [Lab1 boot handout](https://sjtu-ipads.github.io/OS-Course-Lab/Lab1/boot.html),
exercise 2's hint and “启用 MMU.” These are manual observations, not automated grades.

After TODO 1/4, give a compact guide **immediately**: working directory/environment,
launch commands, observation commands, what should be visible and under which
assumptions, then “可选；不想调试可以直接继续……” with the next handout task.
Do not merely advertise that a check exists or wait for an opt-in before showing
how. Do not introduce it by quoting skill rules or reciting why no verdict is given.
If the student already declined, skip the guide and proceed. No logs/screenshots,
extra report, successful observation, or tutor approval are required to advance.

### Shared launch, when not already connected

Use the current course environment/toolchain; both terminals work from `Lab1/`.
Terminal 1: `make qemu-gdb` builds and starts QEMU paused for the debugger.
Terminal 2: `make gdb` starts the project's GDB setup and connects to that QEMU.
Verify these targets/config locally before presenting them; adapt to the student's
existing container/editor setup. If already connected, start at the observation
steps. Do not run any of these commands yourself.

### A — after TODO 1, inspect the exception-level read

For a fresh run paused at startup, the current scaffold supports:

```gdb
break arm64_elX_to_el1
continue
x/i $pc
stepi
info registers x9
```

Explain briefly: stop at the function, inspect the student's first instruction,
execute it once, then read the register used by the following comparison (`x9`
in the original scaffold; recheck local source). Do not supply the instruction
that belongs in the TODO. Check that execution is at the intended TODO before
stepping rather than advancing unrelated instructions into unfinished later work.

Observation: in the handout's fresh QEMU `raspi3b` EL3 startup, the raw CurrentEL
encoding is `0xc` (the level field encodes 3). This is a runtime observation for
the already-completed step, not a constant to hard-code or proof of implementation
correctness. Other entry levels/targets differ; do not label a TODO wrong from a
single mismatch. TODO 2 need not be completed to observe this local step.

End with the optional skip path to exercise 3 / TODO 2, without a compulsory question.

### B — after TODO 4, inspect the documented intermediate state

This applies while page-table work is unfinished, under the handout's setup.
Use the shared launch for a fresh run, then in GDB:

```gdb
continue
```

After output stops, the student presses **Ctrl-C in the GDB terminal**, then runs:

```gdb
info registers pc
x/i $pc
```

The handout describes repeated execution at `0x200` in this intermediate state,
with unfinished mappings and an unset exception vector base. Explain this as the
documented stage phenomenon, not a code verdict. Do not insist on it if the
student's setup differs or the mappings are already completed; do not undo work
to reproduce it. End with the optional skip path to thinking question 8.

### Once all TODOs are complete

The student runs `make grade`; its score/test-item results are the sole final
code-acceptance criterion. Full marks passes without extra required checks.
Below full marks, read the failed scoring item's actual definition and use the
grade-based branch in `gdb-coaching.md` to suggest locations/register changes for
student investigation. After the student revises the code, they rerun `make grade`.
Do not replace the score with a manual-boot/GDB verdict or dismiss a low grade
because `0x200` was expected during an earlier unfinished stage.

## After each TODO: route checks, do not give a verdict

1. Identify the completed TODO and the next stage. Read as needed to track the
   submitted region and available checks, not to reveal a privately inferred bug.
2. Inspect existing test entry points, selectors/assertions, and prerequisites.
   A focused test must actually exercise the completed TODO and be runnable with
   the student's current prior stages, without depending on unfinished later work.
3. If such a check exists, provide its exact command, working directory, purpose,
   meaningful arguments, and scope. The student runs it and reads the result.
   Never invent a selector/target or run it on their behalf.
4. If no such automated check exists or dependencies are unfinished, continue
   to the next stage. At TODO 1/4, give the ready-to-use optional manual guide
   above unless declined; lack of automated tests does not erase those
   handout observations. “Continue” is not a correctness verdict. Do not require
   a test transcript, tutor approval, or immediate GDB session.
5. Do not announce correct/incorrect/partial after each TODO, including through
   an unsolicited hint that reveals the tutor found a defect. If the student
   seeks help interpreting a failure or asks how to investigate, answer that
   request using conceptual explanations/GDB observations without a concrete fix.
   Do not append an invented reasoning exercise to ordinary task progression.

This Lab1 policy overrides generic source-review rules in `SKILL.md`, agent
wrappers, and other references. Do not bypass it by calling a verdict a “hint.”

## Check inventory for the inspected original version

These are source-inspected entry points, not commands the tutor has executed.
Recheck local definitions before recommending them. The student's working
directory for the following commands is `Lab1/`.

| Command/entry point | Actual scope and timing |
| --- | --- |
| `make grade` | Whole-lab integration. Lab1's Makefile includes `Scripts/lab.mk`, which includes `Scripts/kernel.mk`. The target rebuilds and runs the score configuration; the inspected `scores.json` checks for entry into the ChCore shell. Offer after all five TODOs, never as an isolated test after TODO 1–4. A shell score does not prove every report answer or exercise independently correct. |
| `make build` | Compiles/builds the kernel. Can expose build errors; it is not a behavioral correctness test for a TODO. Student runs it only when useful. |
| `make qemu` | Builds and boots the current kernel. Observations depend on all executed earlier steps and may stop on unfinished later work; not an isolated TODO test. |
| `make qemu-gdb`, then `make gdb` in another terminal | The first command builds and starts QEMU paused; the second starts the supplied GDB connection/symbol setup. Offer as separate student actions for stage observation or debugging, not as a pass/fail TODO test. Confirm local setup/environment first. |

The inspected baseline has no per-TODO automated target/selector, but does have
the optional manual observations above. Do not make
up `make test-todo1`, `make grade TODO=1`, or isolated scores. If a student's
version adds genuine focused tests, use those after verifying their scope and
dependencies; this inventory must not prevent using real new tests.

The handout suggests GDB observation around early boot and MMU/page-table stages.
When students cannot resolve a problem, suggest relevant execution phases,
function breakpoints, and registers/memory to inspect, with explained GDB commands.
Use `gdb-coaching.md` for concrete Lab1 guidance. Do not directly name the faulty
statement, exact cause, required replacement/value, or repair. A later boot hang
with unfinished TODOs is not evidence that the just-finished TODO is wrong.

## Source anchors to recheck

- `Pages/Getting-started.md`: report versus coding deliverables.
- `Pages/Lab1.md` and `Pages/Lab1/RTFSC.md`: stage order and reading-only section.
- `Pages/Lab1/boot.md`: questions 1/4/5, exercises 2/3/6/7, early GDB observations.
- `Pages/Lab1/pte.md`: questions 8/9/11/12, exercise 10, final integrated grading.
- `Lab1/Makefile`, `Scripts/lab.mk`, `Scripts/kernel.mk`, `Lab1/scores.json`:
  command definitions and test scope.
- `Scripts/gdb/gdbinit` and `Pages/Appendix/kernel-debugging.md`: debugger setup.

These are paths to inspect in the student's course checkout, not files bundled
with this skill. Do not treat a stale profile as proof of their current setup.
