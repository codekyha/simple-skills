# Claude Skills: Structured Evaluation Toolkit

Three Claude Skills for pressure-testing an idea, a decision, or a research paper before
resources are committed to it or its conclusions are trusted. Each implements a
structured, adversarial evaluation method rather than a single-pass opinion.

| Skill | Method | Use it for |
|---|---|---|
| [`darpa-test/`](./darpa-test) | Heilmeier Catechism (DARPA's nine-question proposal screen, since the 1970s) | A single concrete idea: a project, proposal, hire, purchase, or research direction. Nine sequential questions, ending in a forced go / fix-this-first / stop verdict. |
| [`llm-council-advisor/`](./llm-council-advisor) | Five-persona adversarial synthesis | A decision, plan, strategy, or piece of writing where multiple valid perspectives could disagree. Five independent analytical lenses, a blind cross-review pass, and a Chairman synthesis. |
| [`research-paper-analyzer/`](./research-paper-analyzer) | Thirteen evidence-grounded analysis modes (argument map, evidence audit, overreach flags, gap finding, next-study design, and more) built on a shared claim-and-evidence ledger | One paper or a set of papers: critique it, audit its evidence, tabulate its claims and numbers, compare studies, find genuine gaps, or design the follow-up. The evidence rubric adapts to empirical, theoretical, computational, qualitative, and review papers. |

All three are self-contained — one `SKILL.md` each, no external dependencies or bundled
scripts.

## Repository structure

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

## Installing

Clone the repository once; the commands below run from its root.

```bash
git clone https://github.com/codekyha/simple-skills.git
cd simple-skills
```

The examples use `research-paper-analyzer`; substitute `darpa-test` or
`llm-council-advisor` to install either of the others. A skill's folder name must equal
the `name` in its `SKILL.md` frontmatter.

### Claude.ai (web / mobile)

Skills need a Pro, Max, Team, or Enterprise plan with code execution enabled
(Enterprise owners must first enable skills in Admin settings → Capabilities).

1. Open Settings → Capabilities and turn on **Code execution and file creation**.
2. Build a ZIP whose top-level entry is the skill folder. Any ZIP tool works; this
   one is cross-platform (Python 3):

   ```bash
   python -m zipfile -c research-paper-analyzer.zip research-paper-analyzer
   ```

3. In Settings → Capabilities → Skills, choose **Upload skill**, select the ZIP, and
   switch the skill on.

Some documentation labels the settings page *Features* rather than *Capabilities*.
Uploaded skills are private to your account, so each team member uploads separately;
a skill uploaded here is not available through the Claude API, which has its own upload.

If a `.skill` file is presented in a Claude conversation, its file card offers a
**Save skill** button (where your organization allows skill creation) that installs it
without the steps above. The packaging script
bundled with Anthropic's `skill-creator` example skill produces the same kind of file (a
ZIP archive) and validates the frontmatter first; run it from the `skill-creator`
directory:

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
current session without a restart. The main exception is a top-level skills directory that did not
exist when the session started; run `/reload-skills` in that case. Invoke the skill
directly with `/research-paper-analyzer`, or make a request that matches its description
and Claude loads it on its own.

### Cowork / other Claude surfaces

Consult the surface's own skill-installation documentation — the loading
mechanism (folder path vs. upload vs. catalog) varies by surface, but the
`SKILL.md` files here are portable across all of them without modification.

## Using them

None of the skills needs to be invoked by name. Each `SKILL.md` frontmatter
`description` is written so Claude recognizes when the request calls for that
method — a plain request like *"is this worth building"*, *"stress-test this
plan for me"*, or *"is this paper's conclusion justified"* is enough. Naming the skill
explicitly (*"run the DARPA test,"* *"council this,"* *"run the overreach flag on this
paper"*) also works and is the more reliable trigger for ambiguous requests.

- **`darpa-test`** expects one concrete idea already in hand. It is not a
  brainstorming tool — it interrogates a proposal that already exists.
- **`llm-council-advisor`** expects a decision or artifact with room for genuine,
  defensible disagreement. It is not meant for single-answer factual questions.
- **`research-paper-analyzer`** expects a paper (PDF, link, or pasted text) or a set of
  papers. A bare *"analyze this paper"* runs a compact single-paper pass: a
  claims-and-evidence table, unresolved questions, overreach flags, and three follow-up
  questions. For a specific analysis, ask by name or number — *"build a comparison
  matrix for these five papers,"* *"mode 5: find the real gaps,"* *"extract every number
  and check them against each other."* It does not write papers, referee reports, or
  rebuttals; its output is suitable raw material for them.

### Modes of `research-paper-analyzer`

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
  (@iamkhanphd; [lead post](https://www.threads.com/@iamkhanphd/post/DemET4pEUvB)). The prompt
  texts were reconstructed from the series and are not reproduced verbatim. The
  shared ledger, the paper-type evidence rubric, the evidence tiers, the pipeline
  ordering, and the verification checklist are additions made here.

## License

MIT — see [`LICENSE`](./LICENSE).
