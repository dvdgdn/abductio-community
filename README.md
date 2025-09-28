
# ABDUCTIO™ — a BS detector that shows its work

There's too much noise. Our guts can't keep up.  
**ABDUCTIO** helps you separate signal from spin by **breaking a claim into checkable pieces**, flagging weak links, and telling you **what to verify next**. It shows its work—no vibes.

---

## Quick start (30 seconds)

You can turn **any LLM** (ChatGPT, Claude, local models, etc.) into an **ABDUCTIO reasoner** with one prompt.

1. Open the prompt and copy it:  
   **[`docs/llm_prompt.txt`](https://github.com/dvdgdn/abductio-community/blob/main/docs/llm_prompt.txt)**  
   *(Click **Raw** → copy all.)*

2. Paste it into a new chat with your LLM.

3. Run your first check by typing a claim:

```txt
claim: "Cutting meetings to 15 minutes boosts team output."
```

You'll get:

- a breakdown of the claim into small, checkable parts,
- the weakest links,
- what single fact to check next (and how),
- a simple continue / pause recommendation with reasons.

**Tip:** If you want to stay anonymous, use placeholders. ABDUCTIO evaluates the logic, not the author.

## What it does (plain English)

- **Deconstructs your claim** → makes it bite-size and testable.
- **Finds weak spots** → shows what's most likely to fail.
- **Tells you what to check next** → the smallest thing that could change the conclusion.
- **Knows when to stop** → if more digging won't change the answer, it tells you to save your time.

It's not a truth oracle. It's a disciplined way to pressure-test a claim and focus effort where it matters.

## Why trust it? (Receipts you can replay)

**Toy A/B-style demo (replayable)**  
A tiny, synthetic example where grabbing one solid fact first reduced re-work and improved first-pass approvals.  
*Takeaway: a single targeted check can pay for itself.*

**Public "coin-flip" demo (digits of π)**  
Using the digits of π as a public random source, ABDUCTIO only asks for more evidence when that could change the call—otherwise it stops. No magic, fully reproducible.  
*Takeaway: it doesn't over-collect trivia; it focuses on decisions.*

Want the details? See the open docs:

- **Prompt** (turn any LLM into an ABDUCTIO runner):  
  [`docs/llm_prompt.txt`](docs/llm_prompt.txt)

- **Community whitepaper** (plain math + design notes):  
  [`docs/whitepaper_community_version.org`](docs/whitepaper_community_version.org)

- **Open evidence pack** (reproducible demos):  
  [`docs/evidence_pack.org`](docs/evidence_pack.org)

*(Some production guardrails are private to keep the system robust; the open parts are standard and reproducible.)*

## When to use it

- Before posting a spicy take.
- Costly decisions with fuzzy inputs (product bets, hiring, vendor claims).
- Client/stakeholder memos where you want to show your logic, not just confidence.
- Triage: decide whether to dig deeper—and exactly where.

## Example

**Input**
```txt
claim: "Hiring from top schools leads to better on-the-job performance."
```

**Output (abridged)**

**Breakdown**
- A. "Top school" correlates with skills relevant to this role.
- B. Practical performance is measured consistently in your data.
- C. After controlling for role/tenure/manager, the effect still holds.

**Weak links**
- (B) Performance metrics differ across teams.
- (C) Past analyses didn't control for role or manager effects.

**What to verify next (fastest win)**
Pull last 12 months of ratings + role + tenure; run a simple matched comparison.  
If the matched difference ≥ X, the claim holds; if not, revise policy.

**Call**
Pause policy change until the matched comparison is run. More generic stats won't change the answer.

## Pro (invite-only, early access)

For heavier use and higher stakes:

- Deeper checks on bigger, messier claims
- Batch runs + shareable reports
- Private reviews with an audit trail
- Team/client workflows
- Priority help on deadlines

**Request access:** [open an issue](https://github.com/dvdgdn/abductio-community/issues/new) →  
**New Issue: Pro access**  
*(or DM "Pro" via the contact in the repo description)*

## Repo contents

- [`docs/llm_prompt.txt`](docs/llm_prompt.txt) — the prompt that turns any LLM into an ABDUCTIO reasoner (start here).
- [`docs/whitepaper_community_version.org`](docs/whitepaper_community_version.org) — background and design notes.
- [`docs/evidence_pack.org`](docs/evidence_pack.org) — reproducible demos ("receipts").

## FAQ

**Does this browse the web or call external APIs?**  
No. It runs wherever your LLM runs. If your LLM can browse, that's your model's behavior, not ABDUCTIO's.

**Is this open-source?**  
Yes, the prompt and open demos are public. Some production guardrails remain private.

**How is this different from other "BS detectors"?**  
It shows its work: clear breakdowns, concrete next checks, and a reason to stop or continue. Not just a score.

**Can I run spicy stuff?**  
Yep. For public airing, open an issue or comment with a claim. Prefer private—or want to ask if aliens built the pyramids? DM us (see repo description).

## Contributing

- Found a rough edge? Open an issue with a minimal example (your exact claim + what felt off).
- PRs welcome for docs, examples, or tests.
- Please don't submit private or identifying data.

## License

Open materials in this repo are released under the MIT License (see LICENSE).  
Trademarks and branding remain the property of their respective owners.

---

*If you think everyone's full of it except you, this isn't for you.  
If you're drowning in takes and need a clear, reproducible way to pressure-test them—welcome.*
