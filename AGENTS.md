# AGENTS.md — TuTor repository

Instructions for AI coding agents working **on this repo** (not for end users learning with the TuTor skill).

## Project

**TuTor** is an [Agent Skills](https://agentskills.io)-style package: a tutor skill that teaches step-by-step without completing the user's task. It ships as `SKILL.md` plus optional `references/` for deeper agent-only docs.

| File / directory | Purpose |
|----------------|---------|
| `SKILL.md` | **Source of truth** for tutor behavior. YAML frontmatter (`name`, `description`, `metadata.version`) must stay valid for Cursor, Claude Code, OpenCode, and `.agents/skills`. |
| `references/` | Long examples and rules loaded on demand (e.g. `example-flow.md`, `tool-gate.md`). Keep `SKILL.md` lean; add detail here. |
| `agents/` | Agent-mode wrappers (`opencode/tutor.md`, `claude/tutor.md`). Frontmatter pins the harness tools to read-only and points the agent at the skill. A new harness means one more file, no generator; keep the wrapper bodies identical. |
| `README.md` | Default user-facing docs (Chinese): purpose, features, and installation. |
| `README-en.md` | English version of `README.md`; keep both versions aligned. |
| `AGENTS.md` | This file — repo conventions for agents. |
| `AUTHORS.md` | Contributor list — keep in sync with README Contributors section. |
| `LICENSE` | MIT — keep in sync with README license sections. |
| `playground/` | Local experiments (gitignored). Do not commit. |

**Skill identity:** folder name and frontmatter `name` must both be `tutor`.

**Current version:** see `metadata.version` in `SKILL.md` (bump when behavior or compatibility meaningfully changes).

**Tool-gate declaration:** `SKILL.md` frontmatter uses only Agent Skills standard fields — the body defines the inspection-only boundary; `allowed-tools` (experimental in the spec) pre-approves read-only inspection tools; reviewing submitted TODOs is allowed, but revealing repairs is not. There is no standard field to *deny* tools, so the tool gate is prose-enforced via `SKILL.md` + `references/tool-gate.md` (the agent must refuse forbidden commands). Do not add platform-specific frontmatter keys (`disallowed-tools`, `context`, `agent`, etc.) — keep the skill cross-platform.

## No full thinking/report answers

“Never produce their deliverable” includes thinking-question/report answers, not
just code. Requests for a direct answer, reference write-up, or full walkthrough
receive a short refusal, relevant source pointer, and invitation for a specific
question, without the solution. Report feedback requires an actual student attempt
and stays local; it does not authorize writing a corrected/full answer or filling
missing reasoning. Check this boundary in all references/wrappers and examples.

## Project-level student guard

`templates/AGENTS.lab1.md` is a deployable student-project instruction file,
distinct from this maintainer `AGENTS.md`. It must explicitly require loading
the installed tutor SKILL.md and Lab1 guide for Lab1 learning requests even when
the student omits `$tutor`. Its core rules are a fallback, not a substitute for
loading an installed skill. Never install the maintainer file into coursework.
Merge rather than overwrite existing student instructions. If the designated
OS Lab Tutor skill is missing, the student template must authorize installing it
from this repository using the current agent's available installer or Git,
verifying and reading it before tutoring; this is the only installation exception
to the lesson's read-only rule. Resolve native paths/loaders for Codex, Claude
Code, OpenCode, and DSH instead of assuming Codex. The Claude import template
is `templates/CLAUDE.lab1.md`; preserve existing project entrypoints. Keep global
client settings unchanged; the project supplies standing activation.

## Preserve the upstream interaction rhythm

Keep the entrypoint close to the upstream plan → current assignment → wait
workflow. First introduce the lab/collaboration and preserve complete task
wording; concise progression does not mean omitting requirements. Lab1 tasks
follow the handout, starting with thinking question 1 before
exercise 2 / TODO 1 when not already completed. Brief task wording/source pointers
are allowed; do not substitute model-created comprehension questions, mini-lessons,
or prediction exercises for the assigned work. Concepts/GDB help are on demand.
Keep this rule consistent in examples, wrappers, and both READMEs. Thinking
questions get labelled context-source links and reading spans, not just a bare
question/code pointer. Lab1's dependency order is 8 → 10 / TODO 5 → 9 → 11/12;
retain original numbering even though the handout visually lists 9 before 10.

## Lab-specific completion policies

Keep `SKILL.md`, references, optional agent wrappers, and both READMEs consistent.
ChCore Lab1 uses `references/lab1-guide.md`: identify the actual version, name
report/code destinations at every stage, and route each completed TODO to a real
applicable student-run focused check or continued progress, without an immediate
correctness verdict. At TODO 1/4, immediately give the optional method's runnable
commands, observation and assumptions, then the skip path; no extra opt-in or
policy recital. Final code acceptance is the make grade score/item results:
full marks passes; otherwise map failed scoring items to GDB locations and
before/after register observations, without identifying faulty code or repairs.
Student reruns of make grade decide acceptance, not manual boot/GDB observations.
Declining continues without evidence/report demands. Keep these manual activities
distinct from automated tests. This overrides generic source review. Never mislabel a build,
GDB observation, or whole-lab grade as an isolated TODO test. Other labs can keep
generic source review without repairs. Report review checks core understanding:
accept an adequate answer and continue without polishing, optional refinements,
or another revision request. Only a fundamental misconception, wrong central
required result, or missing central requirement warrants brief feedback. Interpret
loose wording in context. Do not edit/ghostwrite or launder code answers through
report review. If students are stuck on code, provide concrete GDB stages/functions,
breakpoint candidates, registers/memory, and explained commands. Observation
guidance is allowed; directly revealing a code defect, cause, or fix is not.
Students own debugger execution, localization, and repair.
Lab1 submissions are exactly the authentic AI conversation, dedicated report,
and modified Lab1 files. Each stage task writes either to the report or a code
TODO; do not invent further mandatory artifacts. Report tasks are the formal
thinking questions only. Code and authentic conversation evidence implementation;
never add per-exercise/catch-up coding write-ups from the generic Getting-started
sentence. This is an explicit local adaptation, not a claim that the original
course wording changed. Question 9 remains a thinking-question report task.
Students create/designate their own dedicated report document and share its
path. Track that location, accept any readable free-form organization, and never
create, write, reformat, or impose a template on the report. Question numbers in
the guide identify topics, not required headings.
Codex invocation remains explicit-only in `agents/openai.yaml`.

## Editing conventions

1. **Behavior changes** → edit `SKILL.md` and/or `references/`. Prefer `references/` for long walkthroughs or tables.
2. **User-visible docs** → update `README.md` and `README-en.md` when relevant (see below).
3. **Minimal diffs** — match existing tone and structure; do not refactor unrelated files.
4. **No secrets** — never commit `.env`, tokens, or personal machine paths as examples.
5. **Do not commit** `playground/`, `.cursor/`, `.opencode/`, `.agents/` (see `.gitignore`).

## Write the READMEs for beginners

The READMEs are read by students who may never have used an AI coding tool, an agent mode, or a skill. Assume none of that vocabulary:

- Explain a term the first time it appears, in plain words. A *skill* is a folder of instructions the tool loads when it's relevant.
- Say *AI tool* or the tool's name instead of *harness*; *mode* instead of *subagent*; *the folder it reads* instead of *frontmatter* where the exact key doesn't matter.
- Keep commands, paths, flags, filenames, and product names literal — never translate or soften them.
- Keep the technical version when it is the point of the step (a flag name, a file to edit), and add one sentence saying what it is for.
- Sections that only make sense to people already in the ecosystem belong under an "advanced" or "local development" heading, not in the install path.

## Keep README and README-en in sync

When you change something that affects how people **install, upgrade, use, or contribute** to TuTor, update **both** `README.md` and `README-en.md` in the same change.

| Update both READMEs when… | Examples |
|---------------------------|----------|
| Install or upgrade paths change | New agent platform, renamed directories |
| Version bump | `metadata.version` in `SKILL.md` — update the version line in both READMEs |
| New user-facing feature | New section in docs (e.g. upgrade flow) |
| Repository layout changes | New top-level files agents/users should know about |
| Contribution workflow changes | PR checklist, testing expectations |

| README sync not required when… | Examples |
|----------------------------------|----------|
| Only tutor runtime behavior in `SKILL.md` / `references/` | Wording of refusals, internal tool-gate edge cases |
| Typos or clarity inside skill text with no user doc impact | — |

**Chinese and English README rules:**

- Translate prose; keep commands, paths, flags, and code **literal** (same as TuTor teaches learners).
- Preserve the language switcher at the top: Chinese README links to `README-en.md`; English links to `README.md`.
- Keep section structure parallel so diffs between languages stay easy to review.

## Version bumps

When bumping `metadata.version` in `SKILL.md`:

1. Increment the version string in frontmatter.
2. Update the “currently **X.Y**” (or equivalent) line in **both** READMEs.
3. For development versions such as `0.7-dev`, mark both READMEs as unreleased and do not invent a release tag. Keep installation examples honest about the branch they use.
4. Only when the user explicitly requests a release, create/push the actual release tag and update pinned examples in both READMEs. A version bump alone does not authorize commits, tags, or publishing.
5. Mention the version in the commit message if the user asked for commits.

## Commits

Group related changes logically (e.g. skill + reference in one commit; README pair in another) unless the user asks for a single commit.

Do not create commits unless the user explicitly requests them.

## Testing changes

- Install the skill from this repo into one target path (e.g. `~/.cursor/skills/tutor` via clone or symlink).
- Run a short “teach me X, don’t do it for me” session and confirm the short plan/current-assignment/wait rhythm, thinking question 1 before TODO 1, no added comprehension gates, report/TODO feedback boundaries, and student-requested GDB guidance.
- For doc-only changes, skim both READMEs for broken links and mismatched version numbers.
- CI (`.github/workflows/security.yml`) runs on every PR: gitleaks gates on leaked secrets; SkillSpector uploads static findings to the Security tab as advisory. Treat a new HIGH/CRITICAL finding as a blocker even though the job stays green.

## Links

- Chinese docs (default): [README.md](README.md)
- English docs: [README-en.md](README-en.md)
- Skill entrypoint: [SKILL.md](SKILL.md)
