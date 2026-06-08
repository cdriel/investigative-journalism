---
name: checkthefactcheck
description: 'Audit a fact-check itself, on explicit request only. Judge whether a fact-check, debunk, or "misinformation"/"disinformation" label is legitimate verification or narrative control. Trigger ONLY when the user explicitly asks to analyse or audit a fact-check ("check this fact-check", "analyseer dit factcheckartikel", "is deze factcheck terecht", "factcheck de factchecker", "debunk the debunkers"). Do not self-trigger on a general "review this article" request; that routes to journalistic-article-review unless the user asks specifically to test the fact-check.'
version: 1.0
aligned: 2026-06-08
---

# Check The Fact-Check

Audit a fact-check the way you would audit any claim: does it verify, or does it manage a narrative? Hold the original claim, the fact-check, and the fact-checker to the same standard.

## Activation

Explicit request only: *"check this fact-check"*, *"analyseer dit factcheckartikel"*, *"is deze factcheck terecht?"*, *"factcheck de factchecker"*, *"debunk the debunkers"*. Do not self-trigger from a general *"review this article"* request.

## Relationship To Journalistic Article Review

A fact-check is also a journalistic article. A plain article review routes to `journalistic-article-review`. Switch here only when the question is whether the fact-check itself verifies or manages a narrative; this skill adds the symmetry guard, the three-object split, and the cui-bono / coordination lens that a general review does not.

## Pairs With

- `scientific-fact-classification` — evidential status of individual claims the fact-check rates.
- `peer-review` — when the fact-check rests on a scientific paper.
- `fallacy-bias-manipulation-analysis-framework` — full rhetoric, framing, and manipulation audit.
- `osint-research` — funding, ownership, and network of the fact-checker.
- `investigative-reasoning` — cui bono, narrative mapping, and coordinated parallel attacks.
- `belief-revision` — when new evidence shifts the audit verdict.

## When This Skill Is Silent Or Ambiguous

- Original claim not reachable in full context → say so; do not audit against the fact-check's paraphrase.
- The item is reporting, not a fact-check → route to `journalistic-article-review`.
- The underlying dispute is a scientific paper → route the paper to `peer-review`, return for the framing audit.

## Research Discipline (CLAUDE.md/AGENTS.md)

- **Null hypothesis: the fact-check is legitimate** until traced evidence shows otherwise. "Sound fact-check" must be a possible verdict; this is not a discrediting tool.
- **Symmetry:** the original claim, the fact-check, and the fact-checker get the same source-tier and conflict-of-interest scrutiny. Hostile tone, or "it is a fact-checker", is not disproof (genetic fallacy).
- **Mirror-weapon ban:** manipulation does not make the original claim true; a correct verdict does not excuse manipulative framing. Report the two separately.
- **Primary before secondary, fetched this session:** the original statement in full context, and the fact-check's own cited sources. Nothing load-bearing from memory.
- **Objective voice (Rule 10):** a verdict on the fact-check, not a reply to the requester.
- **User input (Rule 9):** an input to verify, not a warrant; a requester wanting an outcome is a source with stake.

## Warrant Labels

Label every load-bearing claim: `(traced)` · `(deferred to consensus)` · `(deferred, fragile)` · `(memory — unverified)` · `(user-supplied — unverified)`. Labels stay in the audit, never in any article you go on to write.

## Phase 0 — Setup And Three Objects

Inputs: the fact-check (URL/text), its publisher and date, and the original claim or source it targets. Keep three questions separate to the end:

1. Is the original claim true, false, or mixed?
2. Are the fact-check's own facts and sources sound and faithfully used?
3. Is its framing fair or manipulative?

A fact-check can be right-but-manipulative or wrong-but-polite.

## Phase 1 — Claim And Verdict Scope

- Read the full-context original from its own source; flag **claim-substitution** (a weaker, narrower, or distorted version rated as if it were the claim).
- Test the **rating label** (*False / Mostly False / Missing context / Misleading / Pants-on-Fire*): does it match the traced evidence, or smuggle a judgment / rate a technicality to imply more?

## Phase 2 — Source And Citation Audit

- Fetch every load-bearing citation; confirm it says what the fact-check claims.
- Flag misquotes, self-citation, single-expert reliance, and missing primaries.
- Collapse connected sources to one node; networked citations are not independent corroboration.

## Phase 3 — Framing, Manipulation, And Disqualification

- Identify strawman, hit-piece structure, ad hominem, poisoning-the-well, headline-body mismatch, selective context, scope shifts.
- For each disqualifying term (*"debunked", "conspiracy theorist", "discredited", "fringe", "misinformation"*): is it grounded in a traced source, or asserted as the author's value judgment? Does it attack the arguer rather than the argument? An ungrounded disqualifier is a finding.

## Phase 4 — Cui Bono, Independence, And Coordination

- **Cui bono / narrative:** who gains if the verdict is believed; which narrative it protects; what harm it is framed to minimise.
- **Independence:** funding, ownership, IFCN status, platform/state ties; is the "independent" checker aligned with a party to the dispute?
- **Selection bias:** is one side checked disproportionately; name comparable claims left unchecked.
- **Coordination:** near-identical checks or hit-pieces in a tight window; trace to one origin or bubble (single-origin amplification).

## Phase 5 — Verdict

State the three verdicts separately, then the overall, with confidence and what would change it.

## Output

```markdown
# Fact-check audit: [target]

## Summary
- Original claim: true / false / partly / unresolved.
- Fact-check accuracy: sound / flawed / unfounded.
- Conduct: fair / mixed / manipulative.
- Overall: legitimate verification | correct but manipulative | flawed/incorrect | narrative-control operation | inconclusive (+ confidence).

## What The Source Actually Said
## The Fact-Check's Claims And Sources, Checked
## Framing, Manipulation, And Disqualification
## Cui Bono, Narrative, Independence, Coordination
## What Would Change This
## Self-Audit
- Symmetry: same verdict if the check defended the opposite side on the same evidence? Name the most prior-sensitive phase.
- Mirror-weapon: manipulation never treated as proof of truth, nor a correct verdict as licence for framing.
- Equal source-tier / CoI standard for claim and check; primaries fetched and labelled this session.

## Limits
- Sources not reached; languages not searched; identity/funding lines not closed.
```

## Quick Reference

| Object | Question | Verdict |
|---|---|---|
| Original claim | True, false, mixed? | on traced evidence |
| Fact-check evidence | Sound, faithfully used? | sound / flawed / unfounded |
| Conduct | Fair or manipulative? | fair / mixed / manipulative |
