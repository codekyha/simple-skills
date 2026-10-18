# simple-skills

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Claude Skills for structured, adversarial evaluation of ideas, decisions, and research
papers. Each skill is a single `SKILL.md` that Claude loads when a request matches its
description, with no dependencies and no bundled scripts. Each replaces a single-pass
opinion with a written, repeatable method.

## Skills at a glance

| Skill | Method | Needs | Produces |
|---|---|---|---|
| [`darpa-test`](./darpa-test) | Heilmeier Catechism: DARPA's nine-question proposal screen, run as seven stages | One concrete idea already in hand | A stage-by-stage interrogation ending in a one-word verdict: go, fix-this-first, or stop |
| [`llm-council-advisor`](./llm-council-advisor) | Five independent personas, a blind peer review, and a Chairman synthesis | A decision, plan, strategy, or draft with room for defensible disagreement | Verdict summary, dissent map, synthesis matrix, and an execution protocol with success metrics |
| [`research-paper-analyzer`](./research-paper-analyzer) | Thirteen evidence-grounded modes on a shared claim-and-evidence ledger | One paper or a set of papers (full text gives the best results) | Mode-specific tables, for example claims against evidence, overreach flags, genuine gaps, or a study design |

## Quick start

1. Get the files: `git clone https://github.com/codekyha/simple-skills.git`, or download
   the repository as a ZIP from GitHub's **Code** menu.
2. Install one skill (full steps under [Installing](#installing)):
   - **Claude.ai:** ZIP the skill's folder and upload it under Settings → Capabilities →
     Skills.
   - **Claude Code:** copy the skill's folder into `~/.claude/skills/`.
3. Ask for it in plain words, or by name:

   > Run the DARPA test on this idea: ...
   >
   > Council this: should we ...
   >
   > Analyze this paper for [topic]. (attach the PDF)

## The skills

### `darpa-test`

A structured interrogation of one idea (a project, proposal, product, hire, or purchase)
that surfaces the question its owner cannot answer without changing the subject. The
nine Heilmeier questions run as seven stages: plain-language restatement; current
practice and its limits; what is actually novel; who is affected and what changes; risk
ranked by probability; the full cost; and checkpoints that each carry a date, a number,
and a decision fixed in advance.

A verdict closes the run. Each stage is scored out of 5 on honesty and specificity, not
polish; the weakest answer is named; the first thing a motivated skeptic would attack is
stated; and the answer ends in exactly one of **go**, **fix-this-first**, or **stop**
with a one-sentence reason. A "go" authorizes only the cheapest test from the risk
list, not the full build.

Built-in push-back rules reject vague answers: a beneficiary category in place of a named
role and moment, risks sorted by drama instead of likelihood, and a checkpoint without a
number or a date.

- *Try:* "run the DARPA test on this," "poke holes in this plan," "is this worth
  building."
- *Not for:* brainstorming. The skill interrogates a proposal that already exists.

### `llm-council-advisor`

Five personas analyze the same raw input independently: the **Contrarian** (attack
vectors and failure modes), the **First-Principles Thinker** (rebuild the problem from
its actual constraints), the **Expansionist** (asymmetric upside), the **Outsider**
(zero-context reading), and the **Executor** (sequencing and the next physical action).
Their outputs are anonymized as Advisors A to E, and each persona reviews the other four
for valid points, critical flaws, and blind spots.

A Chairman then weighs the views instead of averaging them and issues a verdict summary;
a dissent map that rates each objection **Critical**, **Secondary**, or **Discarded**; a
synthesis matrix (surviving risks, unexploited leverage, first-principles reality); and a
numbered execution protocol with a success metric per step. The run is sequential inside
one response, and "the proposal is sound as stated" is a legitimate verdict: the aim is
rigor, not manufactured disagreement.

- *Try:* "council this," "run an advisor review on this strategy," "give me a
  no-sycophancy evaluation of this proposal."
- *Not for:* single-fact lookups or questions with one reasonable answer.

### `research-paper-analyzer`

Thirteen ways of reading a research paper critically, on one paper or a set. Every output
is anchored to something specific in the text (a claim, a number, a limitation, a
conflict between papers) with a location, so a reader can open the paper and check it.
Work starts from a shared ledger of claims, evidence, numbers, limitations, and
assumptions, so a claim keeps one ID across modes. Evidence is judged by what the paper's
type actually offers (empirical, theoretical, computational, qualitative, or review), and
each claim receives a tier with a one-line reason: **Strong**, **Moderate**, **Weak**,
**Unsupported**, or **Inherited** (resting on cited work rather than shown here).

A bare "analyze this paper" runs a compact single-paper pass, with a table of this shape
followed by unresolved questions, overreach flags, and three follow-up questions:

```
| ID | Claim | Evidence offered | Location | Tier |
```

For a specific analysis, ask by name or number:

| # | Mode | Input | Produces |
|---|---|---|---|
| 1 | Argument Map | one paper | Thesis, sub-claims, warrants, logical gaps, load-bearing assumptions |
| 2 | Evidence Strength Audit | one or more | Evidence tier for each paper's headline claim, with a ranking |
| 3 | Comparison Matrix | two or more | Side-by-side table of question, sample, method, variables, findings, limitations |
| 4 | Consensus vs Contention | three or more | Settled, contested, and open questions, counted by independent evidence |
| 5 | Real Gap Finder | one or more | Up to five anchored, non-generic gaps with their novelty status |
| 6 | Conflict Explainer | two or more | Verdict on whether conflicting findings are genuine or definitional or methodological, plus a decisive test |
| 7 | Numbers Extractor | one paper | Every key quantity with its location, plus consistency checks |
| 8 | Claim-to-Evidence Tracer | one paper | Each claim mapped to its evidence and location; orphan claims and orphan evidence |
| 9 | Action Brief | one or more | One-page brief whose implications are tied to evidence tier |
| 10 | Next Study Designer | a gap | Study design sketch with a falsification criterion |
| 11 | Literature Themer | four or more | Five to eight themes with agreements, disagreements, methods, limits |
| 12 | Overreach Flag | one paper | Conclusions that exceed the evidence, with severity and a defensible rewording |
| 13 | Follow-up Questions | one paper | Three questions tied to specific findings and methods |

Modes chain in dependency order: `3 -> 2 -> 4 -> 6 -> 11 -> 5 -> 10 -> 9` for a set of
papers, `8 -> 7 -> 12 -> 13` for deep reading of one paper.

- *Try:* "is this conclusion justified," "build a comparison matrix for these five
  papers," "mode 5: find the real gaps," "extract every number and check them against
  each other."
- *Limits:* given only an abstract, it runs the single-paper pass at abstract level and
  says plainly that the evidence cannot be audited. It is analysis only; it does not write
  papers, referee reports, or rebuttals, though its output is suitable raw material.

## Using the skills

Claude keeps each installed skill's `description` in context and loads the full
instructions only when a request matches. A plain request is usually enough; naming the
skill is the more reliable trigger for ambiguous requests. In Claude Code every skill is
also a slash command, for example `/research-paper-analyzer`.

## Installing

The examples use `research-paper-analyzer`; substitute `darpa-test` or
`llm-council-advisor` for either of the others. Commands run from the repository root. A
skill's folder name must equal the `name` in its `SKILL.md` frontmatter, as it does here.

### Claude.ai

Skills need a Pro, Max, Team, or Enterprise plan with code execution enabled (Enterprise
owners must first enable skills in Admin settings → Capabilities).

1. Open Settings → Capabilities and turn on **Code execution and file creation**.
2. Build a ZIP whose top-level entry is the skill folder, not the whole repository. Any
   ZIP tool works; this command is cross-platform (Python 3):

   ```bash
   python -m zipfile -c research-paper-analyzer.zip research-paper-analyzer
   ```

3. In Settings → Capabilities → Skills, choose **Upload skill**, select the ZIP, and
   switch the skill on.

Some documentation labels the settings page *Features* rather than *Capabilities*.
Uploaded skills are private to your account, so each team member uploads separately; a
skill uploaded here is not available through the Claude API, which has its own upload.

If a `.skill` file is presented in a Claude conversation, its file card offers a
**Save skill** button (where your organization allows skill creation) that installs it
without the steps above. The packaging script bundled with Anthropic's `skill-creator`
example skill produces the same kind of file (a ZIP archive) and validates the
frontmatter first; run it from the `skill-creator` directory:

```bash
python -m scripts.package_skill path/to/research-paper-analyzer
```

### Claude Code

Skills are read from the filesystem, so nothing is uploaded. Copy the folder into the
personal directory for availability in every project, or into a project's
`.claude/skills/` to limit it to that repository (commit it there to share it with
collaborators):

```bash
# Available in every project
mkdir -p ~/.claude/skills
cp -r research-paper-analyzer ~/.claude/skills/

# Available in one project only
mkdir -p /path/to/project/.claude/skills
cp -r research-paper-analyzer /path/to/project/.claude/skills/
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse .\research-paper-analyzer "$HOME\.claude\skills\"
```

Claude Code watches these directories, so adding or editing a skill takes effect in the
current session without a restart. The main exception is a top-level skills directory
that did not exist when the session started; run `/reload-skills` in that case.

### Cowork and other Claude surfaces

Consult the surface's own skill-installation documentation; the loading mechanism
(folder path, upload, or catalog) varies by surface, but the `SKILL.md` files here are
portable without modification. Claude Code's documentation also lists skills enabled on
your claude.ai account as loading in Cowork, cloud, and signed-in terminal sessions, so a
Claude.ai upload may already cover those.

### Troubleshooting

- **Skills are greyed out in Claude.ai:** code execution or skills may be disabled by an
  organization owner, or code execution may be off in your own settings.
- **Upload fails:** the usual causes are a folder name that does not match the skill's
  `name`, a missing `SKILL.md`, invalid characters in the name or description, and a ZIP
  over the size limit.
- **Claude Code does not see a new skill:** run `/reload-skills` if `~/.claude/skills/`
  was created after the session started.
- **The skill does not trigger on its own:** name it explicitly in the request, or call it
  as a slash command in Claude Code.

## Repository layout

```
.
├── README.md
├── LICENSE
├── darpa-test/
│   └── SKILL.md
├── llm-council-advisor/
│   └── SKILL.md
└── research-paper-analyzer/
    └── SKILL.md
```

## Adding a skill to this repository

1. Create `<skill-name>/SKILL.md`. The folder name must equal the `name` field.
2. Frontmatter: `name` is at most 64 characters, lowercase letters, digits, and hyphens,
   and must not contain the reserved words "anthropic" or "claude". `description` is
   non-empty, at most 1024 characters, free of angle brackets, and states both what the
   skill does and when to use it.
3. Use only the frontmatter keys that claude.ai and the API accept on upload: `name`,
   `description`, `license`, `compatibility`, `metadata`, and `allowed-tools`.
4. Keep `SKILL.md` under about 500 lines, and keep exactly one `SKILL.md` per skill
   folder; the `skill-creator` validator rejects extras because claude.ai and the API do
   on upload.
5. Validate before committing, from the `skill-creator` directory:

   ```bash
   python -m scripts.quick_validate path/to/skill-folder
   ```

6. Add the skill to the tables, the layout tree, and the provenance list in this README.

Built `.skill` packages are git-ignored; they are release artifacts, not source.

## Provenance

- `darpa-test` is built directly from George Heilmeier's original nine-question
  catechism (public framework, DARPA, 1970s onward), independently phrased for
  this implementation.
- `llm-council-advisor` implements a five-persona-plus-Chairman adversarial
  synthesis pipeline; the parallel-subagent dispatch described in some tool
  specifications is adapted here to a sequential single-context pipeline for
  environments without true parallel subagent execution.
- `research-paper-analyzer` adapts a series of prompts for analyzing research papers
  posted on Threads by Hamidullah Khan, PhD
  (@iamkhanphd; [lead post](https://www.threads.com/@iamkhanphd/post/DemET4pEUvB)). The
  prompt texts were reconstructed from the series and are not reproduced verbatim. The
  shared ledger, the paper-type evidence rubric, the evidence tiers, the pipeline
  ordering, and the verification checklist are additions made here.

## License

MIT — see [`LICENSE`](./LICENSE).
