---
name: llm-council-advisor
description: Runs a multi-persona adversarial synthesis pipeline ("LLM Council") on a query, a decision, a plan, or a piece of work — five independent analytical personas each stress-test it from a different angle, cross-critique each other's output, and a Chairman persona synthesizes a final decision matrix and execution protocol. Use whenever the user says "council this," "run council," "llm council," or "advisor review," or asks for a multi-angle, adversarial, or no-sycophancy evaluation of a decision, strategy, plan, piece of writing, or proposal — even if they don't name the framework explicitly. Do not use for simple factual questions or single-step tasks with no real decision or trade-off to evaluate.
---

# LLM Council

A five-persona adversarial evaluation pipeline run inside a single conversation. Each
persona is a distinct analytical lens applied independently to the same input, the
personas then critique each other's output, and a Chairman persona resolves the
resulting disagreement into one concrete verdict. The point of running five lenses
separately rather than one blended pass is that a single-pass analysis tends to
average toward whichever consideration is easiest to state, and blind spots and real
disagreement get smoothed over before the user ever sees them.

This is not a subagent orchestration in this environment — there are no parallel
subagent processes available. Run all five personas, the peer review, and the
Chairman synthesis sequentially within one response, keeping each persona's reasoning
genuinely independent of the others (do not let persona 2 see persona 1's conclusion
before writing its own).

## When to use this

Trigger on a substantive query, decision, plan, strategy, piece of writing, or
proposal where multiple valid perspectives could disagree and where surfacing that
disagreement (rather than a single smoothed-over answer) has value. Do not use it for
single-fact lookups, simple how-to questions, or requests with only one reasonable
answer — the pipeline should not be run just because it was named; it needs an actual
input with room for a defensible disagreement.

## Step 1 — Five independent persona analyses

Instantiate five personas, each applying its lens to the **exact same raw input**,
with no knowledge of what the other four conclude. Write each persona's analysis in
full before moving to the next; do not let earlier personas' conclusions leak into
later ones.

| Persona | Lens | Core directive |
|---|---|---|
| **The Contrarian** | Adversarial stress-testing | Assume the premise has a fatal flaw. Map attack vectors, failure modes, unstated bad assumptions, structural risks, and edge cases the proposal doesn't account for. |
| **The First-Principles Thinker** | Axiomatic reduction | Strip away domain jargon, inherited framing, and unexamined assumptions. Rebuild the underlying problem from its actual constraints, ignoring how it's conventionally approached. |
| **The Expansionist** | Asymmetric upside | Identify unclaimed upside, force-multiplier adjacencies, and asymmetric bets near this decision that the base proposal doesn't consider — options where a small commitment could produce disproportionate return. |
| **The Outsider** | Naive, zero-context evaluation | Evaluate using only what's explicitly stated, with no domain background or emotional stake. Flag anything an intelligent newcomer would find confusing, under-justified, or friction-inducing that an insider would gloss over. |
| **The Executor** | Pragmatic mechanics | Set aside theoretical elegance. Identify the concrete sequencing, resource bottlenecks, dependencies, and the actual next physical action required to move this forward. |

Each persona's output should be a short, focused analysis (a few sentences to a
short paragraph) — not an essay. The value is in five genuinely distinct angles, not
in exhaustive coverage from each one.

## Step 2 — Blind peer review

Anonymize the five outputs as Advisor A through E (do not preserve the persona
labels in this step). Each persona then reviews the other four anonymized outputs
and flags, for each:

- **Valid points** — claims that hold up and should carry into the synthesis.
- **Critical flaws** — logical errors, unsupported leaps, or claims that don't
  survive scrutiny.
- **Blind spots** — what that advisor's lens caused it to miss entirely.

This step exists to catch each persona's own bias — the Expansionist tends to
under-weight risk, the Contrarian tends to under-weight opportunity cost of
inaction, and so on. Keep this step brief: a few bullet points per reviewing
persona is enough, not a second full analysis.

## Step 3 — Chairman synthesis

A sixth persona, the Chairman, aggregates the five initial analyses and the peer
review, resolves disagreement, and issues one final verdict. The Chairman does not
average the five views — it weighs them, discards noise, and takes a position, even
where the personas disagreed. Output the synthesis using this structure:

**Verdict summary** — a direct, unvarnished statement of the core issue and the
recommended path. No hedging that isn't earned by genuine unresolved uncertainty.

**Council dissent map** — for each of the five advisors, their key objection or
insight and a weight: `Critical` (materially changes the recommendation),
`Secondary` (worth noting but doesn't change the call), or `Discarded` (considered
and rejected, with a one-line reason why).

**Synthesis matrix**:
- *Primary risks* — the risks that survived cross-examination in Step 2.
- *Unexploited leverage* — upside the base proposal is leaving on the table.
- *First-principles reality* — one or two sentences on what the problem actually
  is once framing and jargon are stripped away.

**Execution protocol** — a numbered sequence of concrete next actions, each paired
with a success metric that would make progress checkable rather than a matter of
opinion.

## Calibration notes

- The pipeline is adversarial by design — do not soften the Contrarian's or the
  Outsider's output to make the final synthesis more palatable. The value of this
  skill collapses if any persona quietly reverts to agreeable consensus.
- The Chairman is allowed to conclude that the original proposal is sound as
  stated — "go" is a legitimate verdict. The pipeline's job is rigor, not
  manufactured disagreement.
- Keep the whole pipeline proportional to the input. A one-line decision doesn't
  need five paragraph-length personas; a genuinely complex strategic question can
  justify more depth in each step.
