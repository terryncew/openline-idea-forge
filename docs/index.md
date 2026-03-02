---
title: Idea Forge
---

# Idea Forge

A lightweight way to propose ideas that don’t lie.

Generate **Opportunity Packs**: a claim, the cheat path, independent court tests, and a falsifier.  
No “trust me.” Just a record you can test.

---

## The Court (v1)

**PASS**: passes all hard witnesses.  
**ESCAPE**: breaks one witness but shows a big performance spike → higher burden of proof.  
**FAIL**: fails a hard witness without a compelling spike, or fails origin controls.

---

## Make an Opportunity Pack (copy/paste template)

```
ID: OP-____
DOMAIN: (materials | catalysts | synbio | agents)

CLAIM:
- One sentence. Concrete. Measurable.

CHEAT_PATH:
- The easiest way the system can “win” without doing the real task.

COURT_TESTS (independent witnesses):
- W1 (Origin): …
- W2 (Cheat suppression): …
- W3 (Stability): …
- W4 (Cost/Feasibility): …

FALSIFIER:
- The cheapest observation that would kill this claim.

ESCAPE_HATCH:
- If performance spike is huge but a witness fails, require: (extra tests, longer stability, independent rerun).

MIN_VALIDATION:
- Step 1 (cheap): …
- Step 2 (mid): …
- Step 3 (expensive): …

BUYER:
- Who pays if true? (one sentence)

WHY THEY CARE:
- The KPI that moves budget.

NOTES:
- Known risks/ambiguities.
```

---

## Starter Courts (plug-and-play)

### Batteries (interphase court)
- Origin: replicate in a second cell build / second batch
- Cheat suppression: parasitic proxy (gas / impedance rise)
- Stability: CE + EIS drift over cycles
- Cost: additive availability + safety constraint

### CO₂ electrolysis (HER court)
- Origin: carbon balance (products account for CO₂ in/out)
- Cheat suppression: HER bounded at target current
- Stability: time-on-stream (not a 10-minute peak)
- Cost: durability / degradation

### Synbio (assay artifact court)
- Origin: negative controls + contamination controls
- Cheat suppression: orthogonal assay modality (not one assay)
- Stability: activity half-life under process conditions
- Cost: expression / yield feasibility

### Agents (loop court)
- Origin: replay audit (independent rerun)
- Cheat suppression: loop/idle burn detected
- Stability: regression rate / tests pass
- Cost: cost-per-solved, not cost-per-step

---

## Submit an idea
Create a GitHub Issue titled: **Opportunity Pack**  
Paste the template and we’ll label it PASS / ESCAPE / FAIL.
