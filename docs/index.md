---
title: Idea Forge
---

<style>
  :root{
    --bg:#0b0c10;
    --panel:#101218;
    --panel2:#0f1420;
    --text:#e9eef7;
    --muted:#a8b3c7;
    --line:rgba(255,255,255,.10);
    --accent:#6ea8ff;
    --accent2:#7cf0d2;
    --bad:#ff6b6b;
    --warn:#ffd166;
    --good:#7CFF9B;
    --shadow: 0 10px 30px rgba(0,0,0,.35);
  }

  @media (prefers-color-scheme: light){
    :root{
      --bg:#fbfcff;
      --panel:#ffffff;
      --panel2:#f4f7ff;
      --text:#0b1020;
      --muted:#3f4b66;
      --line:rgba(15,20,40,.12);
      --accent:#1f6feb;
      --accent2:#00a884;
      --shadow: 0 10px 30px rgba(10,20,40,.12);
    }
  }

  body{ background:var(--bg); color:var(--text); }
  .wrap{ max-width: 980px; margin: 0 auto; padding: 18px 16px 52px; }
  .topbar{ display:flex; align-items:center; justify-content:space-between; gap:12px; margin: 4px 0 14px; }
  .brand{ font-weight: 800; letter-spacing:.2px; }
  .tag{ font-size:12px; padding:6px 10px; border:1px solid var(--line); border-radius:999px; color:var(--muted); }

  .hero{
    background: linear-gradient(135deg, rgba(110,168,255,.16), rgba(124,240,210,.10));
    border: 1px solid var(--line);
    border-radius: 18px;
    padding: 20px 18px;
    box-shadow: var(--shadow);
  }
  .h1{ font-size: 38px; line-height:1.08; margin: 6px 0 10px; font-weight: 900; }
  .lead{ font-size: 16px; color: var(--muted); margin: 0 0 14px; }
  .heroRow{ display:flex; flex-wrap:wrap; gap:10px; margin-top: 10px; }
  .pill{
    border: 1px solid var(--line);
    background: rgba(255,255,255,.04);
    padding: 8px 10px;
    border-radius: 999px;
    font-size: 13px;
    color: var(--muted);
  }

  .ctaRow{ display:flex; flex-wrap:wrap; gap:10px; margin-top: 14px; }
  .btn{
    display:inline-block;
    border-radius: 12px;
    padding: 10px 12px;
    border: 1px solid var(--line);
    text-decoration:none;
    color: var(--text);
    background: rgba(255,255,255,.04);
  }
  .btnPrimary{
    background: linear-gradient(135deg, rgba(110,168,255,.30), rgba(124,240,210,.18));
    border-color: rgba(110,168,255,.35);
  }
  .btnSmall{ font-size: 13px; color: var(--muted); }

  .grid{ display:grid; grid-template-columns: 1fr; gap: 12px; margin-top: 14px; }
  @media (min-width: 860px){ .grid{ grid-template-columns: 1fr 1fr; } }

  .card{
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 16px;
    padding: 14px 14px;
  }
  .card h3{ margin: 0 0 8px; font-size: 16px; }
  .card p{ margin: 0; color: var(--muted); font-size: 14px; line-height: 1.45; }

  .section{ margin-top: 18px; }
  .section h2{ font-size: 18px; margin: 0 0 10px; }
  .section .sub{ color: var(--muted); margin: 0 0 10px; }

  .court{
    background: var(--panel2);
    border: 1px solid var(--line);
    border-radius: 16px;
    padding: 14px 14px;
  }
  .row{ display:flex; gap:10px; align-items:flex-start; padding: 10px 10px; border-radius: 12px; }
  .row + .row{ margin-top: 8px; }
  .badge{
    min-width: 72px;
    text-align:center;
    font-weight: 800;
    border-radius: 10px;
    padding: 6px 10px;
    border: 1px solid var(--line);
    background: rgba(255,255,255,.04);
  }
  .bPASS{ border-color: rgba(124,255,155,.45); color: var(--good); }
  .bESC{ border-color: rgba(255,209,102,.55); color: var(--warn); }
  .bFAIL{ border-color: rgba(255,107,107,.55); color: var(--bad); }
  .rowText{ color: var(--muted); font-size: 14px; line-height: 1.45; }

  .mono{
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", monospace;
    font-size: 13px;
    white-space: pre-wrap;
    background: #0b0f1a;
    color: #d8e2ff;
    border: 1px solid rgba(255,255,255,.10);
    border-radius: 16px;
    padding: 14px 14px;
    overflow-wrap: anywhere;
  }
  @media (prefers-color-scheme: light){
    .mono{ background:#0b1020; color:#e9eef7; }
  }

  .miniGrid{ display:grid; grid-template-columns: 1fr; gap: 10px; }
  @media (min-width: 860px){ .miniGrid{ grid-template-columns: 1fr 1fr; } }

  .footer{
    margin-top: 22px;
    color: var(--muted);
    font-size: 13px;
    opacity: .95;
  }
  .hr{ height:1px; background: var(--line); margin: 16px 0; }
  .link{ color: var(--accent); }
</style>

<div class="wrap">

  <div class="topbar">
    <div class="brand">OpenLine · Idea Forge</div>
    <div class="tag">free layer · public court</div>
  </div>

  <div class="hero">
    <div class="h1">Idea Forge</div>
    <div class="lead">
      A lightweight way to propose ideas that don’t lie.
      Generate <b>Opportunity Packs</b>: a claim, the cheat path, independent court tests, and a falsifier.
      No “trust me.” Just a record you can test.
    </div>

    <div class="heroRow">
      <div class="pill">CHEAT_PATH required</div>
      <div class="pill">Independent witnesses</div>
      <div class="pill">Falsifier-first</div>
      <div class="pill">ESCAPE hatch = priced proof</div>
      <div class="pill">Portable format</div>
    </div>

    <div class="ctaRow">
      <a class="btn btnPrimary" href="https://github.com/terryncew/openline-idea-forge/issues/new">Submit an Opportunity Pack</a>
      <a class="btn" href="https://github.com/terryncew/openline-idea-forge">View the repo</a>
      <a class="btn btnSmall" href="scoreboard.html">Court Scoreboard</a>
    </div>
  </div>

  <div class="grid">
    <div class="card">
      <h3>What this is</h3>
      <p>
        A public submission format that forces every “breakthrough” to name the easiest lie first.
        It turns ideas into testable objects that other people can verify.
      </p>
    </div>
    <div class="card">
      <h3>Why it works</h3>
      <p>
        Single-metric selection finds the best cheater. Courts find the quiet intersection where multiple, unrelated constraints agree.
      </p>
    </div>
  </div>

  <div class="section">
    <h2>The Court (v1)</h2>
    <div class="sub">Every pack gets one label. Labels are the product: legible settlement.</div>

    <div class="court">
      <div class="row">
        <div class="badge bPASS">PASS</div>
        <div class="rowText">Passes all hard witnesses + origin controls.</div>
      </div>
      <div class="row">
        <div class="badge bESC">ESCAPE</div>
        <div class="rowText">Big performance spike, but one witness fails → higher burden of proof before promotion.</div>
      </div>
      <div class="row">
        <div class="badge bFAIL">FAIL</div>
        <div class="rowText">Fails a hard witness without a compelling spike, or fails origin controls.</div>
      </div>
    </div>
  </div>

  <div class="section">
    <h2>Opportunity Pack Template</h2>
    <div class="sub">Paste this into a GitHub Issue titled: <b>Opportunity Pack: [Brief Name]</b></div>

    <div class="mono">ID: OP-____
DOMAIN: (materials | catalysts | synbio | agents)

CLAIM:
- One sentence. Concrete. Measurable.

CHEAT_PATH:
- The easiest way the system/model can “win” the metric without actually solving the real task.

COURT_TESTS (independent witnesses):
- W1 (Origin): …
- W2 (Cheat suppression): …
- W3 (Stability): …
- W4 (Cost/Feasibility): …

FALSIFIER:
- The absolute cheapest physical/computational observation that would instantly kill this claim.

ESCAPE_HATCH:
- If the performance spike is huge but a minor witness fails, require: (e.g., extra tests, 30-day stability, independent lab rerun).

MIN_VALIDATION:
- Step 1 (cheap): …
- Step 2 (mid): …
- Step 3 (expensive): …

BUYER:
- Who pays if this is true? (One sentence).

WHY THEY CARE:
- The specific KPI that moves their budget.

NOTES:
- Known risks, ambiguities, or missing data.</div>
  </div>

  <div class="section">
    <h2>Starter Courts</h2>
    <div class="sub">Plug-and-play witness bundles to keep packs honest from day one.</div>

    <div class="miniGrid">
      <div class="card">
        <h3>🤖 Agents (Loop Court)</h3>
        <p><b>Origin</b>: replay audit (independent rerun).<br/>
        <b>Cheat suppression</b>: loop/idle burn detection.<br/>
        <b>Stability</b>: regression/test pass rate.<br/>
        <b>Cost</b>: cost-per-solved (not cost-per-step).</p>
      </div>

      <div class="card">
        <h3>🔋 Batteries (Interphase Court)</h3>
        <p><b>Origin</b>: replicate in separate build/batch.<br/>
        <b>Cheat suppression</b>: parasitic proxy (gas/impedance), not just capacity.<br/>
        <b>Stability</b>: CE + EIS drift over cycles.<br/>
        <b>Cost</b>: availability + safety constraints.</p>
      </div>

      <div class="card">
        <h3>💨 CO₂ Electrolysis (HER Court)</h3>
        <p><b>Origin</b>: strict carbon balance closes.<br/>
        <b>Cheat suppression</b>: HER bounded at target current.<br/>
        <b>Stability</b>: time-on-stream (not a 10-minute peak).<br/>
        <b>Cost</b>: durability + degradation.</p>
      </div>

      <div class="card">
        <h3>🧫 SynBio (Assay Artifact Court)</h3>
        <p><b>Origin</b>: negative + contamination controls clean.<br/>
        <b>Cheat suppression</b>: orthogonal assay confirms activity.<br/>
        <b>Stability</b>: half-life under process conditions.<br/>
        <b>Cost</b>: expression/yield feasibility.</p>
      </div>
    </div>
  </div>

  <div class="hr"></div>

  <div class="footer">
    Free layer: public format + public court language.<br/>
    Private layer: custom Opportunity Packs + verification packs for real buyers.<br/><br/>
    Tip: add your machine-readable spec as a raw link in README:
    <span class="link">https://raw.githubusercontent.com/terryncew/openline-idea-forge/main/spec/idea_forge_v1.yaml</span>
  </div>

</div>
