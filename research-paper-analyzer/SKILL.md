---
name: research-paper-analyzer
description: Analyzes research papers with thirteen evidence-grounded modes, including argument mapping, evidence-strength audit, comparison matrix, consensus-versus-contention map, genuine gap finding, conflict explanation, numbers extraction, claim-to-evidence tracing, action brief, next-study design, literature theming, overreach flagging, and follow-up questions. Use whenever the user shares a paper (PDF, DOI, link, pasted text, or abstract) or a set of papers and wants it critiqued, audited, tabulated, compared, synthesized, or turned into a next step, even if they only say "analyze this paper," "is this conclusion justified," "what are the real gaps," or "pull out the numbers." Adapts its evidence rubric to empirical, theoretical, computational, qualitative, and review papers. Analysis only; it does not write papers, referee reports, or rebuttals, though its output feeds them well.
---

# Research Paper Analyzer

Thirteen ways of reading a research paper critically, usable on one paper or on a set.
The modes descend from a prompt series written in reaction to the habit of asking an
LLM to "find the research gap" in one shot, which returns gaps generic enough to be
stapled onto any paper in the field. The remedy running through every mode below is the
same: anchor each output to something specific in the text (a claim, a number, a
limitation, a conflict between two papers) so that a reader can open the paper and
check it.

## When to use this

Trigger when the user supplies a paper, or several, and wants to know what it says, how
well it supports what it says, how it relates to other work, or what to do next.

Do not trigger for writing a paper, a referee report, or a rebuttal (this skill produces
analysis that can feed those, not the documents themselves); for a plain summary with no
evaluative component (just summarize); or for topical questions with no paper in hand.

## Core discipline

These seven rules apply in every mode. Each exists because its absence is how
paper analysis usually goes wrong.

1. **Ground every output in the text.** Say at the top what you actually have: full
   text, abstract only, or a summary; whether tables and figures were readable; whether
   supplementary material or code was available. Attach a location (section, page,
   table, figure, equation number) to every claim, number, and limitation you report.
   An analysis built on a skim sounds as confident as one built on a close reading;
   locations are what make the difference checkable.
2. **Keep three layers apart:** what the authors claim, what the evidence in the paper
   supports, and what you infer. Label inferences as inferences. The value of the whole
   exercise sits in the distance between the first two layers, and blending them hides it.
3. **Be specific or say nothing.** A gap, flaw, or follow-up question counts only if it
   names the finding, number, method choice, or limitation that motivates it. The test
   is whether the sentence could be pasted unchanged into a different paper in the same
   field. If it could, it is not finished.
4. **Treat "not reported" as an answer.** Never fill an empty cell with a plausible
   value. Write NR, and when the absence matters (no confidence intervals, no
   convergence test, no stated sample size) say why.
5. **Judge the argument, not the packaging.** Venue, author prestige, and citation
   counts are not evidence. Preprint or retracted status is context to report, not a
   verdict.
6. **Paraphrase, and quote only briefly.** Reproduce exact wording only for a short
   phrase where the hedge matters ("suggests" versus "demonstrates"). Long quotations
   pad the output and substitute for analysis.
7. **State what you did not check.** Image-only tables you could not read, supplementary
   material or code you did not see, sections you skimmed: say so. An analysis that is
   silent about its blind spots is read as complete.

## Intake: the ledger

Before running any mode:

1. **Locate the input.** If a file was uploaded and its content is not already in
   context, read it in full before analyzing (long PDFs section by section). If only a
   title, DOI, or link was given, try to retrieve the full text with the tools at hand.
   If that fails, say so, and either ask for the file or proceed at abstract level (see
   "Limited input").
2. **Classify each paper by type** using the rubric below. Hybrids are common (theory
   plus a numerical check); apply each rubric to the part it governs.
3. **Fix the frame.** If the user named a topic, analyze relative to it; otherwise use
   the question the paper itself poses.
4. **Build the ledger,** a working record per paper: claims (where made, how strongly
   hedged); the evidence offered for each, with location; numbers as reported, with
   units and context; stated limitations; assumptions, explicit and implicit; and the
   open questions the authors raise. Every mode reads from the ledger instead of
   re-reading the paper, so a claim keeps the same ID and the same evidence across the
   claim table, the overreach flags, and the follow-up questions. Show the ledger only
   when the user asks, or when the mode is the ledger (modes 7 and 8).

## Choosing a mode

| # | Mode | Input | Answers |
|---|---|---|---|
| 1 | Argument Map | one paper | What is the argument, and where is it logically weak? |
| 2 | Evidence Strength Audit | one or more papers | How good is the evidence behind each paper's headline claim? |
| 3 | Comparison Matrix | two or more | How do these studies line up side by side? |
| 4 | Consensus vs Contention | three or more | What is settled, and what is actively disputed? |
| 5 | Real Gap Finder | one or more (best after 3, 4, 6) | Which genuine gaps do these papers leave? |
| 6 | Conflict Explainer | two or more that disagree | Is the disagreement real, or an artifact of definitions and methods? |
| 7 | Numbers Extractor | one paper | What are the important quantities, and do they agree with each other? |
| 8 | Claim-to-Evidence Tracer | one paper | For each claim, where exactly is the support? |
| 9 | Action Brief | one or more | What follows for practice, policy, or the next decision? |
| 10 | Next Study Designer | a gap from mode 5 or the user | What study would close it? |
| 11 | Literature Themer | four or more | How does this body of work organize into themes? |
| 12 | Overreach Flag | one paper | Which conclusions exceed the evidence? |
| 13 | Follow-up Questions | one paper | What three specific questions does this paper leave open? |
| - | Single-paper pass | one paper | Compact default: claims and evidence, unresolved questions, overreach flags, three follow-ups |

Routing rules:

- A mode named by number or by name runs as named.
- A goal stated in plain words maps to the closest mode; say which mode you chose when
  the mapping is not obvious.
- "Analyze this paper" with nothing more runs the single-paper pass.
- Several papers and no instruction: run mode 3, then mode 2, and offer 4, 6, 11, and 5
  as next steps.
- Multi-mode requests run in dependency order, extracting once. For a set of papers:
  `3 -> 2 -> 4 -> 6 -> 11 -> 5 -> 10 -> 9`. For one paper: `8 -> 7 -> 12 -> 13`. Later
  modes lean on earlier ones (gaps come from limitations and conflicts, study designs
  from gaps, briefs from everything), so skipping ahead makes the later mode redo the
  earlier work badly.

## Evidence rubric by paper type

Prompts of this kind are usually written with social-science papers in mind (sample
size, p-values, effect sizes). Many papers have none of those, so judge evidence by what
the paper's type actually offers.

- **Empirical or quantitative** (experiments, trials, observational studies, surveys).
  Evidence is measured data under a described design. Check the design (randomized,
  quasi-experimental, observational); how the sample was chosen and whether it is large
  enough for the effect claimed; measurement validity; effect sizes with intervals, not
  only p-values; multiple comparisons and analytic flexibility; preregistration;
  attrition and missing data; confounding; external validity; replication status.
- **Theoretical or analytical** (mathematical physics, formal models, theory papers).
  Evidence is derivation. Check that the stated assumptions are the ones actually used;
  that no derivation step is skipped or merely asserted; that limiting and special cases
  are recovered; the regime of validity; whether invariances and symmetries are
  respected; internal consistency of units, dimensions, signs, and conventions;
  dependence on unproven conjectures; whether results are exact or approximate and how
  the approximation error is controlled; and whether the paper yields a testable
  prediction.
- **Computational or numerical** (simulation, machine learning, numerical methods).
  Evidence is runs. Check convergence and resolution studies; validation against known
  solutions; baselines and ablations; seeds and variance across runs; data leakage and
  tuning on test data; benchmark saturation; compute and parameter disclosure; code and
  data availability.
- **Qualitative or mixed-methods.** Evidence is interpretive data. Check sampling
  logic; saturation; coding procedure and inter-rater reliability; reflexivity;
  triangulation; and whether transferability claims go beyond the cases studied.
- **Reviews and meta-analyses.** Evidence is the literature as sampled. Check search
  strategy and databases; inclusion criteria; risk-of-bias assessment; heterogeneity;
  publication bias. For narrative reviews, check selectivity: what would a different
  reasonable search have surfaced?

### Evidence tiers

Used by modes 2, 8, 9, and the single-paper pass. Assign a tier per claim, with a
one-line reason.

- **Strong.** Demonstrated in this paper by a method suited to the claim, with
  uncertainty quantified (or the derivation complete and checked in limiting cases), and
  the main alternative explanations addressed.
- **Moderate.** Demonstrated, but a limitation leaves a live alternative explanation or
  restricts the regime; or the evidence is indirect yet convergent.
- **Weak.** Suggestive: small or unrepresentative sample, uncontrolled confounds, a
  single unvalidated run, an unproven step, or reliance on an analysis that is not shown.
- **Unsupported.** Nothing in the paper bears on the claim, or the evidence cuts against
  it.
- **Inherited.** The claim rests on cited prior work rather than on anything shown here.
  Its strength is that of the cited work; say whose evidence it is.

Tiers are ordinal judgments. Do not turn them into scores or average them.

## The modes

### Single-paper pass (default)

The compact form of the flagship request: tabulate claims, evidence, and unresolved
questions; flag conclusions that exceed the evidence; propose three follow-up questions
tied to specific findings. Output, in this order, about one page unless asked for more:

1. **Snapshot** (three or four lines): paper type, the question it poses, design or
   scope, and what you were able to read.
2. **Claims and evidence:** table with columns ID | Claim | Evidence offered | Location
   | Tier.
3. **Unresolved questions,** split into those the authors acknowledge and those they do
   not but that follow from the design or the data.
4. **Overreach flags** in the mode 12 format, or "none found" with what you checked.
5. **Three follow-up questions** in the mode 13 format.

### 1. Argument Map

Method. State the central thesis in one sentence. Decompose it into sub-claims. For each
sub-claim list the evidence offered and the warrant, meaning the reasoning step that
licenses moving from that evidence to that claim; mark each warrant as stated or
implicit. Then look for the standard failures: a missing premise, equivocation on a key
term, circularity, a non sequitur, a hidden assumption, and scope shift (something
established for one setting and then applied to another). Finish by identifying the
load-bearing assumptions: those whose failure would bring down the thesis rather than a
single sub-claim.

Output. An indented outline (thesis, sub-claims S1 to Sn, evidence, warrant) with each
logical gap flagged at the step where it occurs and located in the paper, followed by a
ranked list of load-bearing assumptions. Offer a diagram only if the user wants one and
the environment can render it; the outline carries the content.

### 2. Evidence Strength Audit

Method. Classify each paper, apply its rubric, and assign a tier to its headline claim.

Output. Table: Paper | Type | Scope (sample size, regime, or cases) | Method quality
(one line) | Main limitation | Tier of headline claim. Then rank the papers by
confidence in their headline claims, with one line of reasons each. Rank within
comparable types only: a derivation and a randomized trial do not sit on one scale, so
across types give a combined view of confidence in the shared question instead. When
the user is deciding how far to trust a paper and web access is available, also check
for retractions, corrections, and failed replications, and report what you found or did
not find.

### 3. Comparison Matrix

Output. One row per paper, columns Paper | Research question | Sample | Method |
Variables | Findings | Limitations. For theoretical papers read Sample as the regime or
class of systems treated and Variables as the key quantities and parameters, and say
which reading you used above the table. Every cell is specific or NR; findings carry
their numbers when the paper gives them. After the table, add three to five lines on
patterns visible only in the matrix (for example, all positive results come from one
method, or sample sizes are uniformly small). That comparison is the reason to build a
matrix.

### 4. Consensus vs Contention

Method. Sort claims into three groups. **Settled:** supported by several independent
lines of evidence; give the number of lines and the papers. **Contested:** state the
question, the positions, which papers hold each, the evidence each side uses, and what
would resolve it. **Open:** no adequate evidence in the set. Count independent lines of
evidence, not papers; papers that share data, authors, or a method count once.
Everything is relative to the papers supplied unless you searched, so say which. If the
set looks one-sided, say that too: consensus within a curated set is weak evidence of
consensus in the field. With fewer than three papers this mode cannot establish
consensus; report the positions, and either search for more or stop there.

### 5. Real Gap Finder

Method. Produce up to five gaps, fewer if fewer survive; never pad to reach five. Each
must pass four tests. **Anchored:** tied to a named limitation, contradiction, or
untested boundary in specific papers, with location. **Non-generic:** passes the paste
test from the core discipline. **Answerable:** some feasible method or derivation could
address it. **Consequential:** closing it would change a conclusion, a decision, or an
estimate rather than add one more data point.

Output. Table: Gap | Anchor (paper and location) | Why it remains open (methodological
barrier, scarce data, neglected regime or population, conceptual ambiguity) | What
closing it would change | Novelty status. Novelty status is "unverified" unless you
searched: a gap relative to the papers supplied is not evidence that no one has done the
work. If the user will rely on novelty (a grant, an introduction, a thesis), search for
each gap and report the closest prior work found.

### 6. Conflict Explainer

Method. For each conflict, state Finding A and Finding B with locations, then compare
them along the dimensions that usually explain disagreement: how key terms are defined
and operationalized; population or regime; method and measurement; analysis choices
(models, controls, thresholds, approximations); data source, period, or resolution; and
power or precision. Rule out definitional and contextual differences before calling
anything a contradiction, since many apparent conflicts are two true statements about
different things.

Output. A comparison table per conflict, then a verdict: **genuine contradiction** (same
question, comparable methods, incompatible results); **apparent conflict** (explained
by definitions, methods, or context, so both can hold); or **unresolved with the
information at hand** (say what is missing). Close with the decisive test: the single
analysis or experiment that would discriminate between the accounts.

### 7. Numbers Extractor

Method. Extract every quantity a reader would need to judge the work: sample sizes,
effect sizes, test statistics, p-values, confidence intervals and error bars, fit
parameters, key constants and parameter ranges, validity bounds, resolutions and
tolerances, and the headline numbers in the abstract.

Output. Table: # | Quantity | Value as reported | Unit or scale | What it measures, and
for which group, condition, or regime | Location | Reported or derived. Do not round,
convert, or normalize silently. Then run consistency checks, in code when code
execution is available and carefully by hand otherwise (say which): counts against
percentages, subgroup sizes against the total, confidence intervals against reported
p-values, degrees of freedom against sample size, units and dimensions between text and
tables, and abstract numbers against results numbers. Report each discrepancy with both
locations, or "no discrepancies among N checks" when clean. Finish with what is missing
that should be present (no effect size, no interval, no convergence or resolution
test).

### 8. Claim-to-Evidence Tracer

Output. Table: ID | Claim (paraphrased) | Where claimed (abstract, introduction,
results, discussion) | Supporting evidence | Where (section, table, figure, equation) |
Link (direct, indirect, inherited, none) | Note. Then list four kinds of mismatch:
orphan claims (stated with no traceable support), orphan evidence (shown but never tied
to a claim), claims whose strength changes between abstract and body, and evidence that
does not say what the paper says it says. A location is precise enough when the user
can open the paper and find the evidence in under a minute.

### 9. Action Brief

Write for a reader who will act, not review. Structure: bottom line (two sentences at
most); what the evidence establishes, with tiers; what remains uncertain; implications
by audience (practitioners, policymakers, researchers, as relevant), each tagged with
the tier it depends on; next steps, concrete and ordered; and what not to conclude,
meaning the most tempting over-reading. Implications must not outrank the evidence: a
weak-tier finding supports "worth investigating," not "implement." Keep it to one page.
If the user wants something to circulate and the environment offers document tools,
produce it as a document; otherwise answer inline.

### 10. Next Study Designer

Method. Start from gaps found in mode 5 or named by the user. If there are several,
choose the single best study and justify the choice, then sketch the others more
briefly. For each study give: the question and hypothesis (for theoretical work, the
target result); the design type and why it fits; the sample and sampling (or regime,
parameter range, and assumptions to relax); the variables and measures (independent,
dependent, controls; or the quantities and observables); the analysis plan, including
the comparison that would count as success; precision or power considerations (or error
control and the limiting cases that must be recovered); threats to validity and how the
design handles them; the result that would falsify the hypothesis; and feasibility in
data, time, tools, and expertise. Flag where a pilot is needed before the main study.
One page per study.

### 11. Literature Themer

Method. Tag each paper from the ledger with its question, method, and main finding.
Cluster by the question being answered, not by shared keywords, and name each theme as
a claim or question rather than a topic. Use five to eight themes for a large set and
fewer for a small one. A theme needs at least two papers; the rest go in an orphan bin
rather than being forced into a theme.

Output, per theme: name; papers; where they agree; where they disagree; typical
methods; common limitations; one line on the state of the theme. End with the orphans
and three lines of cross-theme observation (which themes are method-bound, which have
stalled, which depend on a single dataset or group).

### 12. Overreach Flag

Method. For each conclusion in the title, abstract, discussion, and conclusion, compare
its strength and scope with what the results support. Check these patterns:

- causal language from a correlational or observational design;
- generalization beyond the sample, population, regime, or parameter range actually
  tested;
- extrapolation outside the tested range, or a claim about a limit never approached;
- statistical significance presented as practical or physical importance, or
  non-significance presented as no effect;
- a mechanism asserted without a test that separates it from alternatives;
- subgroup or post hoc findings presented as confirmatory;
- "consistent with" or "suggests" hardened into "shows" or "demonstrates" between body
  and abstract;
- novelty or priority claims ("first," "no prior work") with no stated search;
- comparison against weak, outdated, or untuned baselines;
- conclusions undercut by the paper's own limitations section;
- results valid under a stated approximation or idealization presented as
  unconditional.

Output, per flagged item: Where stated | What is claimed | What the evidence supports |
Pattern | Severity (minor: wording; moderate: scope; major: the conclusion is not
supported) | Defensible rewording. Flag only real gaps. "No overreach found," with what
you checked, is a legitimate result, and manufactured flags drown real ones. This mode
judges the claim's relation to the evidence; flaws in the evidence itself belong to
modes 2 and 8.

### 13. Follow-up Questions

Produce three questions unless asked for another number. Each must be anchored in a
specific finding (with location), tied to a method that could answer it, and not
answerable from the paper itself. Aim for variety: one about mechanism (why does this
happen), one about boundaries (where does it stop holding), and one about robustness
(does it survive a different dataset, method, or regime).

Output. Table: Question | Anchoring finding (location) | Why the paper cannot answer it
| Method that would.

## Verification before returning

- Every number in the output appears in the source at the cited location, or is marked
  derived with its arithmetic checked.
- Every claim, flag, gap, and question carries a location or an explicit NR.
- Authors' claims, supported conclusions, and your inferences are kept apart and labeled.
- Every gap and follow-up question passes the paste test.
- Every overreach flag has a defensible rewording and rests on the evidence, not on tone.
- Tiers have one-line reasons and are not averaged.
- The limits of what you could read are stated.

## Limited input

- **Abstract only.** Run the single-paper pass at abstract level (claims, hedging,
  visible overreach), say plainly that the evidence cannot be audited, and offer to
  continue with the full text. Do not run modes 2, 7, or 8 on invented detail.
- **Scanned or image-only material.** Read it with the tools available and mark values
  taken from images as such.
- **Non-English papers.** Analyze in the original language, reply in the user's, and
  keep technical terms in both where they differ.
- **Long papers and books.** Process in sections, build the ledger incrementally, and
  say which parts were read.
- **Large sets (more than about fifteen papers).** Extract ledger rows for all of them
  first, then run the mode, and report coverage.
- **Preprints.** Same standard as published work; note the status.

## Calibration

- **Match the reader.** For a specialist, skip definitions of standard methods; for a
  non-specialist, define a term once. Take the cue from how the request is written.
- **Scale to the request.** The single-paper pass is about a page. Tables may run long
  when a paper has many claims, but the prose around them stays short.
- **Do not hunt for flaws.** A strong paper deserves a strong tier. A report in which
  every claim is weak is as uninformative as one in which every claim is strong; tiers
  are useful only if they discriminate.
- **Evaluate speculation as speculation.** When a paper is openly speculative, ask
  whether the argument is internally coherent and what would test it, instead of
  penalizing it for data it never claimed to have.

## Provenance

The thirteen modes adapt a prompt series for analyzing research papers by Hamidullah
Khan, PhD (@iamkhanphd) on Threads
(https://www.threads.com/@iamkhanphd/post/DemET4pEUvB). The ledger, the paper-type
rubric, the evidence tiers, the pipeline ordering, and the verification checklist are
additions.
