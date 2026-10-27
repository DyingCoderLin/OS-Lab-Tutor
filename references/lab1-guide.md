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

## Progression follows the handout, not invented teaching substeps

At the start, offer a short plan of task titles. The first original Lab1 written
assignment is thinking question 1; exercise 2 / TODO 1 follows it. Empty TODOs do
not mean the student should skip the report question. Respect established prior
progress rather than restarting completed work.

For each ordinary turn, name the current official task and report/code location,
optionally restate the handout question or identify the source to read, then stop.
The student chooses what they need to ask. Do not pre-teach exception levels,
register categories, instruction syntax, or GDB before every TODO, or replace the
assignment with a model-invented “explain these comparisons first” exercise.
The handout's thinking question can itself be phrased as a question; that is the
assigned work, not an extra comprehension gate. Specific student questions can
receive useful explanations; do not turn each answer into another mini-quiz.

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
Report feedback may directly identify an error and explain the correct concept;
it must not ghostwrite the report or supply the missing TODO implementation.

## Different feedback for report answers and code TODOs

- **Report answer:** read it and point out errors immediately, including the
  specific mistaken statement/calculation and the relevant correct concept or
  reasoning. No GDB discovery requirement applies to a written misconception.
  Explain in chat and let the student revise their own free-form document.
- **Code TODO:** no immediate verdict after completion and no direct disclosure
  of the faulty line, exact cause, missing implementation, or repair. Route a
  focused check or continued progress. When stuck, use targeted GDB coaching:
  suggest useful stages/functions, breakpoint candidates, and registers/memory
  to inspect, explain commands, and let the student locate and repair the defect.
- If report text includes TODO code or an exact proposed code replacement, do
  not use report feedback to reveal that code's defect or solution. Correct the
  underlying conceptual explanation without giving the implementation or edit.

The code restriction does not justify withholding direct report feedback.
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
and share the location before the written task; questions the student asks can still be answered.

Example setup: “请你自己新建一份专门记录 Lab1 的报告文档，文件名、格式和写法
都由你决定。建好后告诉我路径；如果已经有报告文档，直接告诉我它的位置即可。”

## Stage map

| Stage, in handout order | Where to record the result | Completion/check routing |
| --- | --- | --- |
| RTFSC/build-system reading | No exercise submission required by this section; optional personal notes | Move to boot reading; do not invent a graded report question |
| CPU startup, thinking question 1 | Designated report: reasoning for thinking question 1; read `init/start.S` | Give direct feedback on the written answer, then continue to the exception-level exercises |
| Exercise 2, exception-level reading | `init/tools.S`, `arm64_elX_to_el1`, `LAB 1 TODO 1` | No isolated automated test in the inspected baseline; continue to exercise 3 |
| Exercise 3, exception-level transition | `init/tools.S`, `arm64_elX_to_el1`, `LAB 1 TODO 2` | No isolated automated test; continue; documented GDB observations are available if the student asks for help |
| Thinking questions 4 and 5, stack/BSS | Designated report: reasoning for the respective questions; read `init/start.S` and `init/init_c.c` | Give direct feedback on the written answers; no code TODO here, then continue to UART |
| Exercise 6, UART string output | `peripherals/uart.c`, `uart_send_string`, `LAB 1 TODO 3` | No isolated automated test; continue; UART output is only a reachable-stage observation, not proof of this TODO alone |
| Exercise 7, MMU activation | `init/tools.S`, `el1_mmu_activate`, `LAB 1 TODO 4` | No isolated automated test; continue to page-table work; later incomplete mappings must not be misreported as a TODO 4 failure |
| Thinking questions 8 and 9, page-table reasoning | Designated report: reasoning for the respective questions | Let the student write their calculations; directly point out report errors and explain concepts, then continue |
| Exercise 10, high-address page table | `init/mmu.c`, `init_kernel_pt`, `LAB 1 TODO 5` | No isolated automated test; finish remaining report questions, then offer whole-lab integration checking |
| Thinking questions 11 and 12 | Report: reasoning for the respective questions | Directly point out report misconceptions if present; explain observation methods if needed |
| Coding-exercise explanation, when required by the handout (a separate written task) | Report: the student's implementation explanation | Direct feedback on written reasoning, without exposing a code defect or prescribing edits |
| All coding exercises ready for integration (not another writing destination) | The code TODO task set is ready for the student to check | Offer the real whole-lab check; do not create another submission document |

Use exact full paths from the student's tree when guiding them, not just the
abbreviations in this table. Do not prescribe modifications outside the exercise.

At the beginning of each stage, say concisely in the student's language:
**Current official task → Destination: report or code TODO → Stop and wait.**
You may briefly restate the handout task or identify source code to read. Do not
add a prerequisite lesson, an extra reasoning question, or future-task details.
When work is submitted, report feedback and code-check routing follow the rules
below; they are not additional teaching steps to insert when assigning the task.
Mention any required implementation write-up as a separate report task.
For example: “把你对思考题 4 的解释记到你指定的报告文档里，怎么组织都可以；
这一阶段没有需要填写的代码 TODO。” Use the actual `report_path` once provided.
This identifies a destination/topic without prescribing a section or giving the answer.

## After each TODO: route checks, do not give a verdict

1. Identify the completed TODO and the next stage. Read as needed to track the
   submitted region and available checks, not to reveal a privately inferred bug.
2. Inspect existing test entry points, selectors/assertions, and prerequisites.
   A focused test must actually exercise the completed TODO and be runnable with
   the student's current prior stages, without depending on unfinished later work.
3. If such a check exists, provide its exact command, working directory, purpose,
   meaningful arguments, and scope. The student runs it and reads the result.
   Never invent a selector/target or run it on their behalf.
4. If no such check exists or dependencies are unfinished, say so and proceed
   to the next stage. “Continue” means deferred checking, not “your TODO is correct.”
   Do not demand a test transcript, tutor approval, or immediate GDB session.
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

The inspected baseline has no per-TODO test target or test selector. Do not make
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
