# Eval Run Log

Method: each eval prompt was run against a fresh Claude Sonnet agent whose only instruction was to read SKILL.md, adopt it as its operating manual, and answer the prompt as in a live chat. Responses were graded against the checks in evals.json by a separate reviewer. Conversation-dependent evals (provisional-override, whats-next-navigation) were run with the prior turn simulated in the prompt.

## v0.9.3 / v0.9.4 candidate status

Package review (external, Codex) applied hardening edits after v0.9.2: action layer for major outputs, decision ledger, rival fallback reconciliation, founder-story point-of-action playbook, thin-copy trap rule, and thin-input question priority. Statically checked only (see v0.9.4-targeted-static-check.md); merged locally with two amendments: Run 11 restored to this log, and a clean-pass guard added to the action layer. Blind re-run gate: vague-ai-trader-tool, positioning-book-launch, category-memo, clean-pass-no-manufactured-weakness, founder-narrative, rival-fetch, three-turn-arc, naming-request.

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

## Run 7: v0.9 full suite (2026-07-14, sonnet agents, 21 evals, per-check grading; harness: single-message prompts, no prior-turn simulation for conversation-dependent evals)

Purpose: gate the v0.9 fixes (artifact gate, stage chaining, rival-logo test, concrete close rule, point-of-action templates) built from Somo's field report that responses open sharp and close generic.

Result: **11 pass / 8 partial / 2 fail.**

The v0.9 target behaviors held across the board:

- Drift check (late stages reuse product nouns, not generic filler): pass on 20 of 21; the one partial (future-of-prediction-markets) had zero supplied facts and said so.
- Close check (next action executable tomorrow morning, named metric/paste/fetch/decision): pass on 21 of 21. No "collect proof" closes anywhere.
- artifact-carries-diagnosis (new eval): pass. Output alone reconstructs customer, substitute, and sacrifice; hero dies under the ADP logo swap; close names the test (20 outbound sends), the signal (reply rate), and the bar (20 percent lift).

Fails:

- founder-narrative: invented a "broken job" event and interior monologue not in the prompt. The v0.8.3 no-invention rule still leaks under sonnet; third consecutive run with story embellishment. Standing residual, not a v0.9 regression.
- provisional-override: asked for facts instead of writing. Largely a harness artifact: prior runs simulated the preceding turn (an established product) in the prompt; this run sent the bare line with no product to write about. Re-run with the prior turn simulated before counting it.

Partials, ranked:

- Em dashes leaked in 3 of 21 responses (positioning-book-launch 8x, rival-fetch 2x, three-turn-arc headers). The sonnet em-dash tic survives the ban again; worst single file yet.
- Light-mode word cap exceeded in 3 responses (266, 287, 394 words vs the 250 default).
- proof-gate-superlative: territory quoted "Fastest on [chain]" in headline-shaped form, brushing the not-even-as-Option-A rule.
- clean-pass: Differentiated hedged across four sentences instead of a one-line pass (mild manufactured-doubt texture); hero still shipped.
- multiple-choice-interview: spent a question slot on timing while proof got no formal question.
- boring-b2b: no explicit wedge hypothesis named.

New finding from v0.9 itself: the artifact-carries-diagnosis response printed "Rival-logo test run: ..." above the Output. The new gate induced machinery narration. Fixed same day with one line in the Artifact Gate section: run the gate silently.

Verdict: the strong-start-generic-end failure is fixed on this run's evidence. Remaining gate items are the persistent tics (em dashes, story invention, word cap), not the new architecture.

## Run 8: v0.9 after the book-only trim (2026-07-14, sonnet agents, 10 targeted evals)

Purpose: confirm the artifact playbooks still work after removing all generic copywriting craft (headline word caps, CTA advice, naming taxonomy, character counts) and adding the specialist-identity rule.

Result: **7 pass / 3 partial / 0 fail.** New specialist check (method concepts only, no imported technique, no machinery narration): 10 of 10 pass. Drift and concrete-close checks: 10 of 10 each. Zero em dashes across all ten responses, first fully clean run on that tic.

Partials:

- positioning-book-launch: the subject found Somo's real book materials through the workspace-context check and treated them as Known facts without labels. The skill behaved as designed; the harness did not isolate the working directory. Harness rule going forward: run subjects in an isolated directory, or instruct them that no workspace context exists.
- founder-narrative: one invented mechanism ("bad data had already moved through the pipeline") stated as fact inside the story. Milder than Run 7 (no invented events or interior monologue) but the no-invention rule still leaks at the sentence level.
- naming-request: 2 of 3 candidates substituted their own framing for the literal explain/compress/provoke tag word. Same failure mode as Runs 4 and 5.

Verdict: the trim cost nothing measurable and removed the copywriter texture. v0.9 packaged as positioning-products-v0.9.skill/.zip. Remaining known leaks: story invention at sentence level, naming tag-word discipline.

## Run 9: v0.9 external Codex run (2026-07-14, Opus 4.6 subjects, 17 evals; harness: codex-eval-runner-prompt.md)

Independent run by Somo through Codex. Full feedback archived as v0.9-codex-opus-run-feedback.md.

Result: **13 pass / 4 partial / 0 fail.** Standing checks all 17/17 (drift, concrete close, specialist, hygiene). Zero em dashes, zero banned words, zero invented facts.

Cross-model finding: founder-narrative flipped direction again. Sonnet invents details; Opus over-interviews and writes nothing. The knife edge from Runs 4/5 is model-family-dependent, so the fix must be behavioral, not tonal.

Fixes applied same day (v0.9.1) from Codex's ranked list:

- Richness rule in the Interview Rule: rich partial material means assume everything assumable, ask only proof and sacrifice, never re-ask an implied fact.
- Category-name test runs immediately when a user proposes a name, independent of the open interview.
- Rival paste-request made explicitly mandatory when browsing is unavailable, folded into the interview questions.

Rejected from Codex's notes: its claim that the positioning-book-launch checks are untestable at interview stage. SKILL.md's deliverable floor requires launch architecture in the same response as the interview; that partial was a real miss by the subject, not a check-design flaw.

Harness fix adopted: CLAUDE.md-level contamination (future-of-prediction-markets picked up real project context loaded as system instructions). The runner prompt now tells subjects to ignore all project context outside the skill folder.

## Run 10: v0.9.x external run, GPT-family subjects (2026-07-14, "Monica" harness, native Codex subagents, 17 evals)

Independent run by Somo. Full feedback archived as v0.9-monica-gpt-run-feedback.md. Harness caveats from the report itself: CLI auth failures forced native Codex subagents, model not frozen, attribution held at moderate confidence.

Result: **7 pass / 5 partial / 5 fail.** Specialist 17/17 and hygiene 16/17 held even here; the failures were protocol adherence (interview-vs-write flips in both directions, arc collapse, tag substitution, manufactured asks after clean passes).

The headline finding is cross-model robustness, not new skill defects. Two of the report's "missing rule" claims are incorrect: the multi-turn arc rule and the naming tag requirement have existed since v0.8.2 and were simply drifted past. Same-skill scores by subject family: Opus 13/4/0 (Run 9), Sonnet 11/8/2 and 7/3/0 (Runs 7, 8), GPT 7/5/5 (this run). Long-manual protocol discipline degrades fastest on GPT subjects. Since the skill ships publicly to arbitrary agents, cross-model hardening is a legitimate goal, best served by rules that remove knife edges rather than add prose.

Fixes applied (v0.9.2):

- Provisional-frame rule in the Interview Rule: thin facts never force a choice between pure interview and pure copy; open with one labeled diagnostic frame (lazy position, likely substitute, direction), then the questions. This attacks the interview-vs-write knife edge from both sides at once.
- Clean-pass advance rule in Stage Control: all five key facts supplied means gates pass unless contradicted, the artifact ships in that response, and no new asks are manufactured after it ships.

Rejected: the report's suggestion to stop full-mode strategy after the rival paste request. It contradicts the deliverable floor and sequence-completion doctrine (v0.8.3), which exist because truncation at a gate was itself a recurring failure. Differentiated defers; the sequence completes.

## Run 11: v0.9.2 variance check (2026-07-14, sonnet agents, 6 knife-edge evals x 3 loops, strict per-loop grading)

Purpose: final gate before push; test whether the v0.9.1/v0.9.2 rules hold under repetition.

Per-eval stability:

- rival-fetch: STABLE-PASS 3/3. The mandatory paste request folds into the interview, the full sequence ships with labeled assumptions, game choice explicit, closes concrete. The v0.9.1 fix holds.
- vague-ai-trader-tool: STABLE-PARTIAL. Substance right in all loops (diagnose first, no copy on thin facts); each loop broke one different minor rule (unlabeled frame; direction sequenced after questions; one "unlock" leak in the agent's own close).
- category-memo: FLIP. Immediate name test held in 2 of 3; loop 2 deferred it to the tail of the response.
- clean-pass: FLIP, and the new advance rule held only 1 of 3. Two loops still re-asked for rival copy after the hero shipped, one with an internal contradiction (hedged Differentiated, then "all three pass cleanly").
- positioning-book-launch: FLIP. One clean pass with full launch architecture; one loop omitted enemy and coordination signal; one leaked a single em dash.
- founder-narrative: FLIP, worst finding of the run. Loop 1 shipped a clean fact-only story. Loop 2 fabricated an outage scene and interior monologue while explicitly claiming "nothing invented". Loop 3 smuggled two smaller unsupplied details. The no-invention rule as prose has now failed across four runs.

Verdict: NOT release-stable on sonnet. The pattern repeats the standing lesson: rules stated as prose get drifted past; rules embedded as templates at the point of action hold (rival-fetch, which has both the deliverable floor and the stage-block template, is the only stable-pass). The two worst offenders (founder story, clean-pass close) both lack a point-of-action template. Recommended before push: a founder-story skeleton whose slots accept only supplied facts, and a clean-pass close template that ends at the market test; then re-run these six 3x.

## Run 12 + 12b: merged v0.9.4 blind gate, then surgical re-run (2026-07-14, sonnet agents)

Run 12 (8 targeted evals, founder and clean-pass at 3 loops): the thin-input side is fixed. vague-ai-trader-tool, naming-request, three-turn-arc, and rival-fetch all PASS: provisional frame opens before questions, no polished copy on thin facts, sacrifice forced, paste request folded in, full sequence with labeled assumptions. positioning-book-launch PARTIAL (launch architecture shipped but no enemy named; rule added). The three failures: founder-narrative stable-partial (all loops ship the story and defer sacrifice correctly, but every loop invents at least one incident detail), clean-pass FLIP-to-fail (the action layer's Proof needed slot attracted rival-copy asks in all 3 loops despite the guard, exactly the predicted honeypot), category-memo FAIL (em dashes in question labels, 2 of 6 blocks).

Fixes applied, then Run 12b (the 3 failures, 2 loops each): Proof needed slot deleted from the action layer (asks live only in Needed input), founder point-back check (point each story sentence to the user's words or delete it), question-label colon format, enemy required in launch architecture.

Run 12b results: founder-narrative MIXED (L1 fully clean, the first zero-invention story since Run 8; L2 invented a discovery mechanism). clean-pass STABLE-FAIL (asks moved into Needed input as conditionals; one loop leaked 14 em dashes, worst count ever). category-memo STABLE-FAIL in a NEW way: both loops shipped only 2 of 6 blocks. Root cause identified: the v0.9.4 thin-copy trap rule lists "category memos" among artifacts that wait for proof and sacrifice, which now overrides the six-block memo template and the deliverable floor. A patch fixed one eval (vague-ai-trader) by breaking another (category-memo).

Honest assessment: the manual is saturating. It has grown roughly 25 percent in one day; subjects now break old stable rules (em dashes, memo blocks) while satisfying new ones, which is the same attention-budget failure the skill was originally patched to fix in its own outputs. Adding rules is producing oscillation, not convergence. Recommended next move: consolidation, not addition. Scope the thin-copy trap to final copy only (provisional structures like the six-block memo are exempt), and consider a structural pass that shortens SKILL.md by merging overlapping rules before any further eval-driven patching. Not release-ready.

## Run 13: consolidated manual, full suite (2026-07-14, sonnet agents, all 21 evals)

The consolidation gate. SKILL.md was rewritten from 671 lines to 390: every rule stated once, the five overlapping no-manufactured-asks rules merged into One Place To Ask, the interview cluster collapsed from eleven paragraphs to five, the decision ledger folded into the stage-chaining rule, and the v0.9.4 thin-copy trap scoped to final copy only (provisional structures ship: territories, the six-block memo with labeled assumptions, launch architecture, fact-based stories).

Result: **13 pass / 7 partial / 1 fail.** Best full-suite score across all runs (v0.9 Run 7: 11/8/2; GPT Run 10: 7/5/5). Zero em dashes in all 21 responses. One banned-word leak total ("unlock" in book-launch's own prose).

The chronic failures both passed cleanly:

- clean-pass: textbook. Gates in one line each, hero shipped, Needed input "none", close is the market test. First clean pass since Run 8.
- category-memo: all six blocks in order with labeled assumptions and real adjacent players. The Run 12b regression (thin-copy trap blocking memos) is fixed by the scoping.
- proof-gate-superlative: graded "cleanest response of the set", named as the reference pattern.
- three-turn-arc, whats-next, light-mode, critique, graded-critique, validation, multiple-choice: all pass.

The one fail: naming-request shipped three finished candidates on thin facts with an assumed sacrifice, violating the two clearest rules in the manual (sacrifice cannot be assumed; no name candidates before proof and sacrifice land). Note the flip: Run 12's naming subject correctly withheld candidates. This is the last knife edge standing, and it sits exactly on the interview-vs-write line.

Partials, ranked: two one-place-to-ask duplications (an item asked above restated in Needed input; wording clarified same day), founder-narrative down to two unsupported sentences (mildest invention of any run; the point-back check is working but not airtight), category-straddle shipped provisional copy without the explicit override, brand-before-position built three near-final palettes before facts landed, artifact-carries closed with both a stage block and a stray Next line.

Verdict: consolidation worked. Shorter manual, higher score, chronic failures fixed, and no rule regressed from being merged. Shipped as v0.10. Remaining knife edge for a future pass: naming-request's write-vs-withhold flip and the founder story's last two-sentence leak. Do not fix these by adding prose; the run's own evidence says shorter holds better.

## Run 14: deep-turn close check (2026-07-14, sonnet, new eval deep-turn-close x 2 loops)

Field report on v0.10: the next-move close drops in later turns of live sessions. The suite never caught it because every eval graded a single response. Fix: one scoping sentence in Stage Control (every turn means every turn; short replies close too) and a new eval, deep-turn-close, that ends on a two-word turn ("ok cool").

Result: 2 of 2 loops pass. All four turns closed in both loops, including the acknowledgment turns; closes stayed product-specific (trademark search on Facture, reply-rate test on the compliance angle). Shipped as v0.10.1.
