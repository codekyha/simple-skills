# Claude Skills: Decision-Stress-Testing Pair

Two Claude Skills for pressure-testing an idea, decision, or piece of work before
resources are committed to it. Each implements a structured, adversarial evaluation
method rather than a single-pass opinion.

| Skill | Method | Use it for |
|---|---|---|
| [`darpa-test/`](./darpa-test) | Heilmeier Catechism (DARPA's nine-question proposal screen, since the 1970s) | A single concrete idea: a project, proposal, hire, purchase, or research direction. Nine sequential questions, ending in a forced go / fix-this-first / stop verdict. |
| [`llm-council-advisor/`](./llm-council-advisor) | Five-persona adversarial synthesis | A decision, plan, strategy, or piece of writing where multiple valid perspectives could disagree. Five independent analytical lenses, a blind cross-review pass, and a Chairman synthesis. |

Both are self-contained — one `SKILL.md` each, no external dependencies or bundled
scripts.

## Repository structure

```
.
├── README.md
├── LICENSE
├── darpa-test/
│   └── SKILL.md
└── llm-council-advisor/
    └── SKILL.md
```

## Installing

### Claude.ai (web / mobile)

Skills are added from a packaged `.skill` file via the **Save skill** button on the
file card, or from your organization's skill catalog if these have been published
there. If you only have this repository (raw `SKILL.md` files, no `.skill`
package), package a skill from its folder with the packaging script bundled in
Anthropic's `skill-creator` example skill:

```bash
python -m scripts.package_skill path/to/darpa-test
```

This produces `darpa-test.skill`, which can be uploaded through the Claude.ai skill
picker.

### Claude Code

Copy the skill folder into your skills directory — either the user-level directory
for availability across all projects, or a project's `.claude/skills/` for scope
limited to that project:

```bash
# Available in every project
cp -r darpa-test ~/.claude/skills/

# Available in one project only
cp -r llm-council-advisor /path/to/project/.claude/skills/
```

Claude Code discovers any folder containing a `SKILL.md` under those paths
automatically; no restart or registration step is required.

### Cowork / other Claude surfaces

Consult the surface's own skill-installation documentation — the loading
mechanism (folder path vs. upload vs. catalog) varies by surface, but the
`SKILL.md` files here are portable across all of them without modification.

## Using them

Neither skill needs to be invoked by name. Each `SKILL.md` frontmatter
`description` is written so Claude recognizes when the request calls for that
method — a plain request like *"is this worth building"* or *"stress-test this
plan for me"* is enough. Naming the skill explicitly (*"run the DARPA test,"*
*"council this"*) also works and is the more reliable trigger for ambiguous
requests.

- **`darpa-test`** expects one concrete idea already in hand. It is not a
  brainstorming tool — it interrogates a proposal that already exists.
- **`llm-council-advisor`** expects a decision or artifact with room for genuine,
  defensible disagreement. It is not meant for single-answer factual questions.

## Provenance

- `darpa-test` is built directly from George Heilmeier's original nine-question
  catechism (public framework, DARPA, 1970s onward), independently phrased for
  this implementation.
- `llm-council-advisor` implements a five-persona-plus-Chairman adversarial
  synthesis pipeline; the parallel-subagent dispatch described in some tool
  specifications is adapted here to a sequential single-context pipeline for
  environments without true parallel subagent execution.

## License

MIT — see [`LICENSE`](./LICENSE).
