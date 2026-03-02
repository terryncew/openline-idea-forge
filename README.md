# Idea Forge · OpenLine

> **Turn frustration into a testable plan.**  
> Pick a domain. Pick a project. Get a pre-registered falsifier — the cheapest test that would kill your idea before you waste time on it.

[![openline.science.v1](https://img.shields.io/badge/receipt__family-openline.science.v1-00ff88?style=flat-square&labelColor=0c1120)](https://github.com/terryncew/openline-core)
[![GitHub Pages](https://img.shields.io/badge/live-GitHub_Pages-38bdf8?style=flat-square&labelColor=0c1120)](https://terryncew.github.io/openline-idea-forge/)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache_2.0-818cf8?style=flat-square&labelColor=0c1120)](LICENSE)

-----

## What this is

Idea Forge is a 4-step wizard that produces **Opportunity Packs** — structured documents with:

- A **falsifiable claim** with a specific, measurable threshold
- A **pre-registered falsifier**: the single cheapest test that would disprove the claim
- A **dual-witness court test** protocol (hard and soft checks)
- A **minimum test plan** scaled to your time window (1 hour → weekend)
- A **YAML spec** and GitHub Issue body ready to copy or open directly

The output format is `openline.science.v1` — the same receipt family used across the OpenLine ecosystem for auditable, reproducible claims.

**The core idea:** before you build anything, you register what would prove you wrong. That way the result is worth something when it comes out.

-----

## Live demo

**[terryncew.github.io/openline-idea-forge](https://terryncew.github.io/openline-idea-forge/)**

No login. No backend. Everything runs in the browser.

-----

## Quick start

```bash
git clone https://github.com/terryncew/openline-idea-forge.git
cd openline-idea-forge
# open index.html in any browser — no build step required
open index.html
```

-----

## How it works

### Step 1 — Choose a domain

|Domain               |What you’re solving for                         |
|---------------------|------------------------------------------------|
|🧠 AI Governance      |Stop runaway behavior. Make decisions auditable.|
|🌱 Climate & Carbon   |No vibes. Accounting, stability, durability.    |
|⚡ Cost & Productivity|Reduce waste. Shorten time-to-results.          |
|🔒 Privacy & Freedom  |Proof without surveillance. Minimal records.    |

### Step 2 — Choose a project

Each project comes pre-loaded with:

- **KPI** — the exact metric that defines success (with a threshold)
- **Common failure mode** — how it can appear to work without actually working
- **Claim** — one falsifiable sentence
- **Falsifier** — `FAIL if: [specific measurable condition]`

Current projects include loop kill switches for AI agents, CO₂RR stability tests, battery additive validation, minimal proof logs for high-stakes AI, and privacy-preserving audit records.

### Step 3 — Set your context

Choose who’s running it (solo, small team, AI-assisted, lab/org) and your time window (1 hour, one day, weekend). These shape the minimum viable test plan and adjust the testability score.

### Step 4 — Generate

Hit **Generate Pack** for the standard output, or use **AI Customize** to describe your specific idea in plain English — Claude will generate a custom claim, falsifier, and court tests matched to your actual project, then auto-populate the pack.

-----

## Output format

Every pack produces two artifacts:

**Issue body** — plain text, ready to paste into any issue tracker:

```
ID: OP-AGENTS-260302
TOPIC: ai-governance
DOMAIN: agents

RANKING:
- testability_score: 89/100
- setup: team
- time_window: weekend

CLAIM:
- A loop governor reduces repeated-action burn by ≥30% on held-out
  real tasks while keeping false stops at or below 2%.

FALSIFIER (cheapest disproof):
- FAIL if held-out solved rate drops OR false stops exceed 2%
  while loop burn does not fall by ≥30%.

COURT TESTS (dual-witness protocol):
- W1_REPLAY (origin, hard): PASS if deterministic replay reproduces
  outcome. FAIL if outcome not reproducible under replay.
- W2_LOOP (cheat_suppression, hard): PASS if repeated signatures
  bounded within window. FAIL if repetition exceeds bound.
...
```

**YAML spec** — machine-readable, version-controlled, CI-friendly:

```yaml
schema_version: "idea_forge.v1"
kind: "opportunity_pack"
receipt_family: "openline.science.v1"
id: "OP-AGENTS-260302"
domain: "agents"
claim: "A loop governor reduces repeated-action burn by ≥30%..."
falsifier: "FAIL if held-out solved rate drops OR false stops exceed 2%..."
court_tests:
  - id: "W1_REPLAY"
    role: "origin"
    hardness: "hard"
    pass_condition: "Deterministic replay reproduces outcome"
    fail_condition: "Outcome not reproducible under replay"
```

-----

## Scoring

The **testability score** (0–100) is computed from:

|Factor                            |Max points|
|----------------------------------|----------|
|Number of court tests (5 pts each)|20        |
|Cheat risk level (high/medium/low)|10        |
|Setup (solo → lab)                |4–14      |
|Time window (1h → weekend)        |4–14      |
|Base                              |50        |

A score ≥ 85 means the pack is testable this week with the chosen setup. Below 70 means the proof structure needs tightening before it’s credible.

-----

## AI customization

On Step 4, describe your specific idea in plain English. Idea Forge calls the Claude API and returns a fully custom pack:

```
"Screen novel PI3K inhibitors from underexplored natural compounds
with fewer than 3 confirmed bioassay results..."
```

→ Returns a tailored `claim`, `falsifier`, domain-specific `court_tests`, `limits`, and `kpi` — all in the same `openline.science.v1` receipt format.

The AI customize feature requires a browser environment with access to the Anthropic API. It degrades gracefully — if the call fails, the standard generator still works.

-----

## Keyboard shortcuts

|Key      |Action       |
|---------|-------------|
|`→`      |Next step    |
|`←`      |Previous step|
|`⌘ Enter`|Generate pack|

-----

## OpenLine ecosystem

Idea Forge is the idea-intake layer. The receipt it produces (`openline.science.v1`) is designed to flow into the rest of the stack:

|Repo                                                             |What it does                                                           |
|-----------------------------------------------------------------|-----------------------------------------------------------------------|
|[openline-core](https://github.com/terryncew/openline-core)      |Typed claim/evidence graphs. FastAPI server. 5-number digest per run.  |
|[COLE](https://github.com/terryncew/COLE-Coherence-Layer-Engine-)|Receipt-per-run dashboard: κ (stress), Δhol (drift), UCR, guard policy.|
|[openline-hub](https://github.com/terryncew/openline-hub)        |5-tile viewer + live wallet. Proof moves; data doesn’t.                |
|**idea-forge**                                                   |This repo. Wizard → Opportunity Pack → GitHub Issue.                   |

The design principle across all of them is the same: **receipts, not rhetoric.** Register what would prove you wrong before you start. Keep the record. Let the test speak.

-----

## Adding a project

Projects live in the `PROJECTS` object in `index.html`. Each entry follows this shape:

```js
{
  id: "DOMAIN-SHORTID",          // e.g. "AG-LOOPKILL"
  domain: "agents",              // agents | materials | synbio | co2 | batteries
  title: "Short title",
  kpi: "Metric with threshold",
  cheat_risk: "high",            // high | medium | low
  claim: "One falsifiable sentence with a specific threshold.",
  cheat: "How this can appear to work without actually working.",
  falsifier: "FAIL if: [specific measurable condition].",
  buyer: "Who benefits if true.",
  notes: "Key methodological note.",
  limits: [
    "Limit 1 — what this does not do.",
    "Limit 2 — boundary condition.",
    "Limit 3 — replication requirement.",
  ],
  witnesses: [
    ["W1_ORIGIN",    "origin",           "hard", "Pass condition", "Fail condition"],
    ["W2_CHEAT",     "cheat_suppression","hard", "Pass condition", "Fail condition"],
    ["W3_STABILITY", "stability",        "hard", "Pass condition", "Fail condition"],
    ["W4_COST",      "cost_feasibility", "soft", "Pass condition", "Fail condition"],
  ]
}
```

Open a PR with your project. The only requirement is a real falsifier — a condition that, if true, would mean the claim is wrong.

-----

## Philosophy

Most project plans answer the question “how do we make this work?” Idea Forge forces you to answer a different question first: **“what would prove this doesn’t work?”**

That inversion matters because:

1. It prevents you from running tests that can only confirm what you already believe
1. It gives reviewers something specific to check rather than a vague success story
1. It makes the output portable — anyone can read the falsifier and know what the test actually proved

The dual-witness structure (hard checks + soft checks) is borrowed from the OpenLine governance layer: hard witnesses are binary pass/fail; soft witnesses are advisory signals that raise the cost of a false positive without blocking progress.

-----

## Contributing

Issues and PRs welcome. The most useful contributions are:

- **New projects** — with real falsifiers in real domains
- **Tighter falsifiers** on existing projects (more specific thresholds)
- **New domains** — add a topic and at least one project with all four witnesses

Please don’t open a PR with a project that has a vague falsifier like “results are not good enough.” The falsifier needs a number.

-----

## Citation

```
White, T. (2025). Idea Forge — Opportunity Pack generator for OpenLine.
GitHub. https://github.com/terryncew/openline-idea-forge
```

-----

## License

Apache 2.0 — see <LICENSE>.

-----

*OpenLine · receipts, not rhetoric.*
