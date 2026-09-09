---
name: darpa-test
description: Stress-tests a project idea, research proposal, product concept, hire, purchase, or any other undertaking before resources are committed to it, using the Heilmeier Catechism (the nine-question framework DARPA directors have used since the 1970s to decide which projects get funded). Use this skill whenever the user asks to "run the DARPA test," "Heilmeier Catechism," "stress-test my idea," "validate this project," "poke holes in this plan," "is this worth building," or wants a rigorous pre-mortem / go-no-go assessment of a proposal before money, time, or headcount is spent on it — even if they only describe the idea and don't name the framework explicitly.
---

# The DARPA Test (Heilmeier Catechism)

A structured interrogation of a single idea, run as one continuous conversation. The
method is adversarial by design: it is meant to surface the question the idea's owner
cannot answer without changing the subject, before the idea consumes a budget or a
calendar quarter. There is no jargon requirement and no domain restriction — the same
nine questions work on a research proposal, a new product line, a hire, a purchase, or
a side project.

## When to use this

Trigger on requests to validate, stress-test, sanity-check, or get a go/no-go read on
a specific proposed undertaking — not on requests for open-ended brainstorming, and
not on requests to *generate* new ideas. This skill needs one concrete idea already in
hand.

## The nine questions

These originate from George Heilmeier's catechism, written while he was DARPA
director in the 1970s and still used by the agency to screen proposals:

1. What is the objective? State it with no specialized vocabulary.
2. How is this problem addressed today, and what are the limits of current practice?
3. What is new in the proposed approach, and why is success plausible now?
4. Who is affected if this works, specifically?
5. If it succeeds, what changes for them?
6. What are the risks?
7. What will it cost — in money, time, and attention?
8. How long will it take to reach a first real result?
9. What are the interim and final checkpoints that would prove success or failure?

Questions 4 and 5 are one line in DARPA's original phrasing ("who cares, and if you
succeed, what difference will it make"). Splitting them matters in practice: an idea
can have an interested party and still change nothing for anyone on a given Monday —
those are two separate failure modes worth testing separately.

## How to run it

Run this as a single sequential pass through one conversation, all seven stages
against the same idea, so each stage can build on what the previous one exposed.
Work through the stages below **in order**, giving the user a moment to respond to
substantial gaps (see "Where to push back") before advancing when working
interactively — but if the user has supplied a full, detailed description of the idea
up front and asked for the complete test, run all stages in one pass rather than
stopping after each.

There is no numeric pass mark. The output that matters is: which question, if any,
could not be answered without dodging it — that question names the actual risk in the
idea.

### Stage 1 — Plain-language restatement

Restate the idea with no specialized vocabulary, at a level a bright non-specialist
would follow. Then flag which parts of the user's original phrasing were doing the
work of hiding an undecided detail — jargon is frequently a substitute for a decision
not yet made. If the plain-language version sounds thin, say so; that thinness is
information, not a failure of the rewrite.

### Stage 2 — Current practice and its limits

Enumerate every way this problem is currently being handled — including the
null option (doing nothing), the cheapest available workaround, and the actual
current best alternative, not a straw-man one. For each, state its real cost to the
person who bears it and precisely where it breaks down. Doing nothing is the
default competitor and it is free; most ideas lose to it, so it deserves the same
rigor as any named competitor.

### Stage 3 — What is actually novel

Separate what is genuinely new in this approach from what is simply this person's
version of something that already exists — a different implementation is not
automatically an advantage. Then argue the opposing case directly: give the
strongest reason the new approach could fail for the same underlying reason the
existing options fail. If nothing distinct survives that adversarial pass, the idea
reflects a preference, not an advantage, and that should be stated plainly.

### Stage 4 — Who is affected, and what changes

Name a specific role, organization type, or person, and the specific moment they
encounter this problem — a generic beneficiary class ("researchers," "small
businesses," "students") is not a sufficient answer. Then state concretely what is
different for that person immediately after success, in near-term, checkable terms
rather than an eventual, diffuse benefit. If the honest answer is "not much
changes," say that directly rather than softening it.

### Stage 5 — Risk, ranked by probability

List everything that could kill the project, ranked by likelihood of actually
occurring — not by how alarming it sounds; the dramatic risks draw attention while
the mundane, probable ones are what actually end projects. For the three most
likely, propose the cheapest test that could be run within a week to determine
whether each is real.

### Stage 6 — The full cost

State the real cost in money, hours, and attention required to reach a first
working result, including the costs that are typically omitted: the owner's own
time, post-launch maintenance, and — critically — what the owner will have to stop
doing to make room for this. That displaced activity is often the cost that
actually decides whether the project is worth doing.

### Stage 7 — Checkpoints with teeth

Define a mid-point checkpoint and a final checkpoint, each with a date, a specific
number, and a decision bound to that number in advance. Write the failure
condition so specifically that it cannot be argued away after the fact — the
number that defines failure should be fixed now, not renegotiated once the data is
in. State what should happen if the mid-point checkpoint is missed.

### Verdict

After all seven stages are complete, synthesize a verdict in the same conversation:

- Score each stage's answer out of 5 on honesty and specificity — not on how
  persuasive or polished it reads.
- Name the single weakest answer.
- State what a motivated skeptic, actively trying to kill this idea, would attack
  first.
- Close with exactly one of three words — **go**, **fix-this-first**, or
  **stop** — followed by a one-sentence reason.

A verdict of "go" authorizes running the cheapest test identified in Stage 5's risk
list — it is not authorization to build the full project.

## Where to push back

The method fails silently if answers are accepted at face value. When running this
interactively:

- If Stage 4's affected party is a category rather than a named role and moment,
  ask for the specific instance before proceeding.
- If Stage 5's risks are listed by severity rather than probability, re-sort them
  and say so.
- If Stage 7's checkpoint lacks a number or a date, do not let it pass as written —
  a checkpoint without both is not falsifiable.
- If any stage's answer restates the idea's appeal rather than answering the
  question asked, name that gap explicitly rather than moving on.

## Output format

For a single-pass run, structure the response as one stage per section, in order,
followed by the verdict. Keep each stage's analysis focused — this is meant to be a
diagnostic pass, not an exhaustive report. Do not pad stages where the honest
answer is short; a two-sentence answer that concedes a real weakness is more useful
here than an elaborated one that avoids it.
