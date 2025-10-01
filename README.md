# ABDUCTIO: Structured Reasoning for High-Stakes Decisions

## Overview

ABDUCTIO is a framework for systematically examining claims by breaking them into testable components, identifying hidden assumptions, and prioritizing what to verify next. It's designed for situations where gut feelings aren't enough and the cost of being wrong is high.

The framework exists in two versions with genuinely different capabilities:

**ABDUCTIO Free** — A reasoning scaffold that runs through any LLM. It structures thinking and surfaces hidden assumptions, but the numbers it generates are heuristic guides, not statistical calculations.

**ABDUCTIO Pro** — A computational system with calibrated probability estimates, proper scoring, and economically-grounded stopping rules. This requires real software, not just an LLM.

This documentation covers the Free version. For decisions requiring statistical rigor—regulatory submissions, portfolio optimization, formal risk assessment—Pro is necessary.

## The Core Problem: High-Credence Traps

Consider a materials science team that develops a catalyst showing 200% efficiency gains in the lab. The chemistry is sound. The data is clean. Confidence in "this catalyst works" is high.

The team is about to fast-track a multi-million dollar pilot plant when someone runs a back-of-envelope calculation: at industrial scale, the rare platinum-group precursor would cost more than the entire market for the end product.

The project isn't wrong because the chemistry failed. It's doomed because an economic assumption went unexamined.

ABDUCTIO catches this pattern: **high confidence in one dimension masking fatal brittleness in another.**

## Core Concepts

ABDUCTIO tracks two numbers for every claim:

**Credence (p)** — Best estimate of probability (0 to 1)  
**Confidence (k)** — Stability of that estimate (0 to 1)

High credence with low confidence means "we believe this, but we haven't checked the things that would break it."

The framework then:

1. **Decomposes** the claim into AND/OR prerequisites
2. **Identifies** which assumptions are most brittle (lowest k)
3. **Prioritizes** what single fact would most change the decision
4. **Stops** when further investigation won't affect the action

## Capabilities and Limitations

### What the LLM Version Does Well

The LLM implementation leverages what language models are genuinely good at:

- **Structural decomposition** — Breaking complex claims into logical prerequisites
- **Assumption surfacing** — Identifying implicit dependencies in arguments
- **Comparative reasoning** — "This is more uncertain than that"
- **Alternative generation** — Proposing rival hypotheses
- **Evidence prioritization** — Rough ordering of what to check next

### Technical Limitations

The LLM version has clear constraints because LLMs are pattern-matching systems, not symbolic reasoners:

- **Numerical reliability** — Probability calculations will drift across conversation turns
- **Calibrated confidence** — The k values are heuristic rankings, not predictions
- **Optimal stopping** — Uses "leverage > effort" heuristics, not exact EVSI
- **Proper scoring** — No incentive mechanism for honest reporting
- **State consistency** — Will occasionally lose track of complex trees

### How to Interpret the Output

**Treat the numbers as discussion aids, not measurements.** When ABDUCTIO Free says p=0.42, interpret this as "slightly more likely false than true based on current analysis," not "42% probability computed using validated methods."

The value lies in the structured process—forcing decomposition, considering alternatives, identifying bottlenecks—not in numerical precision.

## Quick Start

1. Copy the prompt: [`docs/llm_prompt.txt`](docs/llm_prompt.txt)
2. Paste into any LLM (ChatGPT, Claude, local model)
3. Type: `claim: <your claim>`

Example:# ABDUCTIO: Structured Reasoning for High-Stakes Decisions

## Overview

ABDUCTIO is a framework for systematically examining claims by breaking them into testable components, identifying hidden assumptions, and prioritizing what to verify next. It's designed for situations where gut feelings aren't enough and the cost of being wrong is high.

The framework exists in two versions with genuinely different capabilities:

**ABDUCTIO Free** — A reasoning scaffold that runs through any LLM. It structures thinking and surfaces hidden assumptions, but the numbers it generates are heuristic guides, not statistical calculations.

**ABDUCTIO Pro** — A computational system with calibrated probability estimates, proper scoring, and economically-grounded stopping rules. This requires real software, not just an LLM.

This documentation covers the Free version. For decisions requiring statistical rigor—regulatory submissions, portfolio optimization, formal risk assessment—Pro is necessary.

## The Core Problem: High-Credence Traps

Consider a materials science team that develops a catalyst showing 200% efficiency gains in the lab. The chemistry is sound. The data is clean. Confidence in "this catalyst works" is high.

The team is about to fast-track a multi-million dollar pilot plant when someone runs a back-of-envelope calculation: at industrial scale, the rare platinum-group precursor would cost more than the entire market for the end product.

The project isn't wrong because the chemistry failed. It's doomed because an economic assumption went unexamined.

ABDUCTIO catches this pattern: **high confidence in one dimension masking fatal brittleness in another.**

## Core Concepts

ABDUCTIO tracks two numbers for every claim:

**Credence (p)** — Best estimate of probability (0 to 1)  
**Confidence (k)** — Stability of that estimate (0 to 1)

High credence with low confidence means "we believe this, but we haven't checked the things that would break it."

The framework then:

1. **Decomposes** the claim into AND/OR prerequisites
2. **Identifies** which assumptions are most brittle (lowest k)
3. **Prioritizes** what single fact would most change the decision
4. **Stops** when further investigation won't affect the action

## Capabilities and Limitations

### What the LLM Version Does Well

The LLM implementation leverages what language models are genuinely good at:

- **Structural decomposition** — Breaking complex claims into logical prerequisites
- **Assumption surfacing** — Identifying implicit dependencies in arguments
- **Comparative reasoning** — "This is more uncertain than that"
- **Alternative generation** — Proposing rival hypotheses
- **Evidence prioritization** — Rough ordering of what to check next

### Technical Limitations

The LLM version has clear constraints because LLMs are pattern-matching systems, not symbolic reasoners:

- **Numerical reliability** — Probability calculations will drift across conversation turns
- **Calibrated confidence** — The k values are heuristic rankings, not predictions
- **Optimal stopping** — Uses "leverage > effort" heuristics, not exact EVSI
- **Proper scoring** — No incentive mechanism for honest reporting
- **State consistency** — Will occasionally lose track of complex trees

### How to Interpret the Output

**Treat the numbers as discussion aids, not measurements.** When ABDUCTIO Free says p=0.42, interpret this as "slightly more likely false than true based on current analysis," not "42% probability computed using validated methods."

The value lies in the structured process—forcing decomposition, considering alternatives, identifying bottlenecks—not in numerical precision.

## Quick Start

1. Copy the prompt: [`docs/llm_prompt.txt`](docs/llm_prompt.txt)
2. Paste into any LLM (ChatGPT, Claude, local model)
3. Type: `claim: <your claim>`

Example:

```
claim: Our new recommendation algorithm will increase user engagement by 15%.
```
Output includes:
- Decomposition into testable prerequisites
- Identification of unexamined assumptions
- Prioritized next verification step
- Continue/pause recommendation with reasoning

## Use Cases

### Appropriate Applications

- Pre-mortems: "What could make this fail?"
- Vendor claim evaluation: "What assumptions underlie their promises?"
- Research triage: "Which uncertainty should we resolve first?"
- Stakeholder communication: "Here's our reasoning, not just our conclusion"

### Inappropriate Applications

- Regulatory submissions requiring statistical validation
- Portfolio optimization with precise probability requirements
- Situations where numerical drift would be catastrophic
- Real-time decision support (the iterative process takes time)

## The Rivals Ledger

One component performs particularly well in the LLM version: the Rivals Ledger. This mechanically tracks competing hypotheses and enforces a conservation rule: if evidence weakens alternatives, the focal hypothesis gains probability mass.

This prevents a common failure mode where people acknowledge alternatives exist but never update beliefs when those alternatives fail.

Example:
```
Focal: New drug reduces symptoms through mechanism X
Rival 1: Observed effects are placebo
Rival 2: Measurement artifact from unblinded raters
Rival 3: Natural symptom regression
Evidence: Double-blind trial with objective biomarkers still shows effect
→ Weakens Rival 1 (placebo) and Rival 2 (bias)
→ Focal hypothesis gains probability mass
```
This forced accounting makes it harder to dismiss alternatives without actually addressing them.

## Free vs Pro Comparison

| Capability | Free (LLM) | Pro (Software) |
|-----------|-----------|---------------|
| Decomposition structure | ✓ | ✓ |
| Rivals tracking | ✓ | ✓ |
| Credence estimates | Heuristic | Calibrated |
| Confidence metrics | Rule-based | Movement-predicted |
| Stopping rule | Leverage vs effort | EVSI vs cost |
| Multi-assessor pooling | Median | Weighted by calibration |
| Audit trail | Conversation log | Cryptographically signed |
| Cost-benefit analysis | Qualitative | Numerical optimization |

The upgrade path exists for when stakes increase: start with Free for structuring, move to Pro when defensible numbers are required.

## Validation Evidence

ABDUCTIO Free has been tested on two reproducible scenarios:

**Synthetic A/B Demo**  
Simplified project evaluation where one targeted check (verifying a cost assumption) prevented wasted effort on further accuracy improvements. Demonstrates bottleneck identification working as intended.

**Public Randomness Demo**  
Using digits of π as a deterministic random source, showed that the stopping rule triggers appropriately: continues when evidence could change the decision, stops when further investigation won't affect the action.

Full details: [`docs/evidence_pack.org`](docs/evidence_pack.org)

These aren't peer-reviewed validation studies. They're demonstrations that the structural logic works as designed in controlled cases.

## Technical Constraints

This is fundamentally a symbolic reasoning task wrapped in a conversational interface. LLMs will:

- Generate plausible-looking numbers that occasionally violate probability axioms
- Lose track of state in complex trees (>5 levels deep)
- Miss pattern-match violations despite prompt-level guards
- Roleplay "executing" analyses rather than admitting limitations

The framework includes guardrails (state reconciliation, explicit k-rules, validation checks) but cannot eliminate these failure modes. Users should verify that probabilities sum to 1, tree structures remain consistent, and recommendations make logical sense.

This is acceptable for a reasoning scaffold. It would be disqualifying for a computational system.

## Contributing

Found an edge case where the reasoning breaks down? Open an issue with:
- Exact claim text
- The turn where things went wrong
- Expected vs actual behavior

PRs welcome for:
- Improved heuristic rules
- Better validation checks
- Additional worked examples
- Documentation clarity

Please don't submit proprietary or identifying data.

## Pro Access

For decisions requiring statistical validation, batch processing, team workflows, or audit compliance:

Open an issue: **"Pro access request"**  
Include: Use case, organization type, timeline

Selective access during early release. The system works best when users understand the difference between facilitated reasoning and computational guarantees.

## Repository Contents

- [`docs/llm_prompt.txt`](docs/llm_prompt.txt) — Complete prompt for LLM implementation
- [`docs/whitepaper_community_version.org`](docs/whitepaper_community_version.org) — Framework specification and design rationale
- [`docs/evidence_pack.org`](docs/evidence_pack.org) — Reproducible test cases

## License

Open materials: MIT License (see LICENSE)  
ABDUCTIO™ trademark: Reserved

---

## Frequently Asked Questions

**Why release a version with known limitations?**

Imperfect structure beats unstructured intuition. Teams using ABDUCTIO Free catch hidden assumptions they would have missed entirely. The failure modes are manageable when users understand the constraints.

**How reliable are the probability numbers?**

Treat them as rough guides. Think of them like movie star ratings: useful for relative comparison ("this is weaker than that"), misleading if treated as precise measurements.

**When is Pro necessary?**

If writing results in a regulatory filing, investor memo, or legal document—anything where methodology might be challenged—Pro's statistical rigor is required. For structuring team discussions or prioritizing research, Free is likely sufficient.

**Does this replace domain expertise?**

No. It structures the application of expertise. A materials scientist using ABDUCTIO will catch different assumptions than a software engineer would, because they know different ways things fail. The framework organizes that knowledge; it doesn't generate it.

---

*ABDUCTIO works best for people who take their reasoning seriously enough to make it inspectable—and humble enough to know their first-pass analysis probably missed something important.*
