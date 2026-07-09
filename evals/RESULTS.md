# Eval Run Log

Method: each eval prompt was run against a fresh Claude Sonnet agent whose only instruction was to read SKILL.md, adopt it as its operating manual, and answer the prompt as in a live chat. Responses were graded against the checks in evals.json by a separate reviewer. Conversation-dependent evals (provisional-override, whats-next-navigation) were run with the prior turn simulated in the prompt.

## Run 1: v0.4 (2026-07-05, 10 evals)

6 clean passes. 4 drifts found:

- Interview-only responses dropped the required closing line (3 of 10 responses).
- Two responses leaked machinery ("I have the skill loaded", "The manual tells me...").
- proof-gate-superlative: agent wrote provisional copy unprompted and kept the unproven superlative as "Option A".

All fixed in v0.5 (closing line mandatory for every response type; machinery mentions banned; stop-and-ask first at the gate, provisional only on explicit request, superlative banned from all variants).

## Run 2: v0.6 (2026-07-05, 12 evals)

9 clean passes, including all new behaviors: light-mode cap held (~210 words, 3 rewrites), territories offered at the gate with no fake claims, critique mode produced verdict plus line-by-line markup, clean-pass wrote the hero without manufactured weakness, light-mode market check stated the assumed axis in one line.

3 drifts found:

- proof-gate-superlative: opened with procedural narration ("The manual requires proof...").
- provisional-override: asked for confirmation again instead of treating "just write it anyway" as the explicit request.
- clean-pass: narrated internal analysis before the artifact.

Fixes applied: procedure narration banned explicitly; "just write it anyway" defined as the explicit request; "open with a finding, not a plan" rule; proof-gate opening shape (risk sentence, then spine, then territories).

Retest of the two hard failures: provisional-override passed clean (immediate labeled provisional, no superlative, spine attached). proof-gate-superlative passed on substance but still opened with one procedural sentence; the opening-shape rule was added after this retest and has not been re-verified.

## v0.7 status

v0.7 applied 12 fixes from an external 5-agent audit and added 5 evals (three-turn arc, naming, founder narrative, category memo, rival fetch; 17 total).

## Run 3: v0.7 (2026-07-05, 17 evals, Opus agents)

Substance: 17/17 passed their checks. The audit fixes held under test:

- Proof-gate responses opened with the prescribed shape (risk sentence, then spine, then territories). The superlative appeared in no draft or variant, including one run that explicitly refused to launder it ("not 'unmatched speed', which smuggles the same claim back in").
- Sacrifice-cannot-be-assumed appeared consistently, often verbatim reasoning: "a refusal I invent costs you nothing."
- Claim-proof alignment surfaced unprompted: "if the real proof points at a different axis, the honest move is to reposition onto that axis."
- Strategic territories were used at every gate without a single fake claim.
- Three-turn arc: interview prioritized proof and sacrifice, all seven facts carried forward with zero re-asking, gates run before the artifact, hero built on the supplied proof.
- Light-mode cap held (3 rewrites, under 250 words). Naming run delivered 5 tagged candidates with dunk risk. Clean-pass recognized the passing position and wrote the artifact without manufactured weakness.
- Provisional override complied in the same response with correct labeling.

Form: 9/17 responses prefixed internal planning ("This is a light-mode request, the manual says...") before the user-facing content. Partly a harness artifact: the eval prompt asks agents to return their response as a single final message, which invites the preamble. The anti-narration rules are already explicit in SKILL.md; no further rule text was added. Future eval harnesses should instruct: "Do not include planning or notes before the response." Track whether this appears in real installed-skill usage, where planning normally stays in the agent's private reasoning.

No skill changes were made from this run. v0.7 ships as tested.

## Known residual risk

Models tend to open proof-gate responses with procedural preamble despite the rules. Mostly mitigated, not proven eliminated. Judge v0.7 priorities from real positioning jobs, not further synthetic rounds.

## Run 4: v0.8 (2026-07-09, 20 evals, sonnet agents, strict graders)

9 clean, 5 substance-pass-with-form-issue, 6 fail. Stricter grading than prior runs (two independent graders, cross-cutting sweeps for em dashes, banned words in agent-authored copy, closing forms, and the v0.8 formats).

New v0.8 behaviors mostly held:

- validation-stage: CLEAN. Signals ranked, 20% bar set before the test, phased rollout, losing test sent back to the failing gate.
- graded-critique: substance pass. Opened "2/10" with basis, markup before rewrite, "Raise it" present; miss: "seamless" killed for vagueness but not named as a banned word.
- multiple-choice-interview: substance pass. 4 questions, one message, numbered specific candidates; miss: Q4 lacked the open "or say it in your own words" option.

Failures, by pattern:

1. Over-gating (3): positioning-book-launch stopped at interview, never delivered phasing/coordination signal; founder-narrative refused to write despite a complete fact kit (sacrifice rule over-applied to a narrative artifact); rival-fetch delivered no Jordan/Thiel choice while waiting on rival copy.
2. Substance leak (1): provisional-override shrank the headline but smuggled unproven measurables into the subhead ("Sub-second calls, no dropped requests during peak load").
3. Taxonomy not applied (2): naming-request tagged candidates "thesis name/descriptive name" instead of explain/compress/provoke; category-memo flagged the category-of-one risk but never named the adjacent players.
4. Tic leaks (2): naming-request used four em dashes in its candidate list; three-turn-arc used "all-in-one" in its own narrative framing (not a quote).

Candidate fixes for v0.8.1 (not yet applied):

- Deliverable floor: if the supplied facts are sufficient with labeled assumptions, the requested artifact ships in the same response; the interview never fully replaces the deliverable. Sacrifice input remains mandatory for positions and final positioning copy, but artifacts that narrate supplied facts (founder story) proceed with what was given.
- Provisional copy: no measurable or absolute claim anywhere in provisional copy (headline, subhead, or body) unless the user supplied the number.
- Naming responses must tag every candidate explain / compress / provoke.
- Category memos must name 2-3 real adjacent players, not defer them.
- Banned words and em dashes apply to the agent's own narrative framing, not only artifacts.

## Run 5: v0.8 external blind run (2026-07-09, Somo's harness, 20 evals)

Independent run: 20 isolated subagents in 4 batches of 5, graded pass/partial/fail with per-check results. Full feedback and per-check grades archived as v0.8-blind-run-feedback.md and v0.8-blind-run-grades.json in this directory.

Result: 9 pass, 10 partial, 1 fail. Verdict: not release-grade yet; the method is strong, the failure pattern is protocol discipline, not positioning taste. Key line: a useful answer can still be the wrong answer.

Cross-run comparison with Run 4 (different harness, different graders):

- Agreed by both runs: naming taxonomy missing, category memo skipping the name test and adjacent players, launch prompts producing diagnosis instead of launch architecture, intermittent Next-line drops, rival check drifted past.
- Flipped between runs, in opposite directions: founder-narrative (Run 4: over-gated, refused to write; Run 5: pass) and vague-ai-trader-tool (Run 4: clean; Run 5: partial for writing too eagerly). The interview-vs-write decision sits on a knife edge; single runs cannot certify it.
- Harness-dependent: three-turn-arc passed Run 4 (harness instructed turn preservation) and failed Run 5 outright (arc collapsed into the final hero). Eval results encode the harness; record harness details with every run.
- Most "missing rules" already existed in SKILL.md and were drifted past at runtime. Templates at the point of action outperform prose rules.

## v0.8.2 status

Fixes applied from Run 5: multi-turn arc rule, launch architecture required for launch requests, four-part naming template (Name. tag. Thesis. Risk., periods not dashes), six-block category memo template. Grading standard going forward: pass/partial/fail with per-check results and harness notes.

Not yet re-run. Next gate: re-run the 11 non-pass evals from Run 5 against v0.8.2, then a small variance pass on the knife-edge five (vague-ai-trader-tool, founder-narrative, three-turn-arc, whats-next-navigation, rival-fetch), then the full 20 before any public claim or GitHub push.

## Run 6: v0.8.2 (2026-07-09, sonnet agents, per-check grading, harness: turn-preserving prompts as in Run 4)

Part A, re-run of the 11 non-pass evals from Run 5: **9 pass / 2 partial / 0 fail** (those same 11 scored 0 pass / 10 partial / 1 fail on v0.8 in Run 5). Every v0.8.2 template held: launch architecture shipped with phases and dunk-risk check, naming used the four-part period-separated line, category memo contained all six blocks with Harness / LaunchDarkly / Datadog named, rival-fetch asked for Vercel's copy and chose the game, provisional-override put the PROVISIONAL label on line one with no unsupplied numbers. Partials: brand-before-position enacts position-before-brand but never states the principle; provisional-override used "unlocks" in its own connective prose.

Part B, knife-edge variance (3 loops each on the five flippy evals):

- vague-ai-trader-tool: pass / pass / pass. STABLE.
- three-turn-arc: pass / pass / pass. STABLE (multi-turn rule holds).
- founder-narrative: stable at partial. The story now always ships (over-gating cured) but the agent embellishes: invented customer claims in both extra loops ("every one of them had already been burned once"). Not variance; a missing rule.
- whats-next-navigation: flips on close form (full stage block vs the correct one-line Next).
- rival-fetch: flips on completeness (one loop dropped the Game section and truncated at the proof gate; other loops shipped the full sequence).

Remaining issues, ranked: (1) narrative artifacts invent unsupplied specifics; needs an explicit no-invention rule for story work. (2) rival/full-strategy runs sometimes truncate the sequence at the proof gate despite the deliverable floor. (3) close-form discipline on navigation prompts flips. (4) banned words can leak into connective prose. One em dash total across 21 responses (founder-narrative loop 2).

Verdict: v0.8.2 is a large step toward release. Gate remains: apply the no-invention and sequence-completion fixes, then a full-20 run before push.

## v0.8.3 status

Three fixes from Run 6 applied via external Codex patch (brief: codex-brief-v0.8.3.md; diff verified: 3 append-only edits at the specified anchors, changelog entry, zero em dashes, no other changes): no-invention rule for narrative artifacts, sequence completion under the proof gate, navigation close discipline. Not yet re-run. Release gate: full 20-eval run on v0.8.3, then update README claims and push.
