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

