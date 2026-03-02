<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Idea Forge · OpenLine</title>

  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;700;800&family=JetBrains+Mono:wght@300;400;500;700&display=swap" rel="stylesheet"/>

  <style>
    *,::before,::after{box-sizing:border-box;margin:0;padding:0}

    :root{
      --bg:#050912;
      --surface:#090e1c;
      --panel:#0c1120;

      --border:rgba(56,189,248,.12);
      --border2:rgba(0,255,136,.14);

      --text:#d8e4f8;
      --muted:#8aa0c8;
      --dim:#1e2a44;

      --green:#00ff88;
      --blue:#38bdf8;
      --violet:#818cf8;
      --amber:#fbbf24;
      --red:#f87171;

      --glow-g:0 0 24px rgba(0,255,136,.22);
      --glow-b:0 0 24px rgba(56,189,248,.18);
      --glow-v:0 0 24px rgba(129,140,248,.18);

      --radius:14px;
      --mono:"JetBrains Mono",ui-monospace,Menlo,Monaco,Consolas,"Liberation Mono",monospace;
      --display:"Syne",system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif;
    }

    html{scroll-behavior:smooth}
    body{
      background:var(--bg);
      color:var(--text);
      font-family:var(--display);
      min-height:100vh;
      overflow-x:hidden;
    }

    body::before{
      content:"";
      position:fixed;inset:0;
      background-image:
        radial-gradient(ellipse 70% 60% at 20% 10%, rgba(0,255,136,.06) 0%, transparent 60%),
        radial-gradient(ellipse 50% 40% at 80% 80%, rgba(56,189,248,.05) 0%, transparent 60%),
        linear-gradient(rgba(56,189,248,.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(56,189,248,.04) 1px, transparent 1px);
      background-size:100% 100%,100% 100%,48px 48px,48px 48px;
      pointer-events:none;z-index:0;
    }

    .root{position:relative;z-index:1;max-width:1160px;margin:0 auto;padding:22px 18px 56px}

    .header{
      display:flex;align-items:flex-start;justify-content:space-between;
      gap:18px;margin-bottom:18px;
    }
    .logo{display:flex;align-items:center;gap:10px;margin-bottom:8px}
    .logo-mark{
      width:36px;height:36px;border-radius:9px;
      background:linear-gradient(135deg,var(--green),var(--blue));
      display:flex;align-items:center;justify-content:center;
      font-family:var(--mono);font-weight:800;font-size:13px;color:#050912;
      flex-shrink:0;
    }
    .logo-text{font-size:22px;font-weight:800;letter-spacing:-0.03em}
    .logo-badge{
      font-family:var(--mono);font-size:10px;color:var(--muted);
      border:1px solid var(--border);border-radius:999px;
      padding:3px 9px;margin-left:6px;
      background:rgba(255,255,255,.03);
    }
    .tagline{
      color:var(--muted);font-size:13.5px;max-width:560px;line-height:1.6;
    }
    .tagline b{color:var(--text)}
    .tagline em{color:var(--green);font-style:normal}

    .header-stats{display:flex;gap:10px;flex-shrink:0;flex-wrap:wrap;justify-content:flex-end}
    .stat-pill{
      font-family:var(--mono);font-size:11px;
      border:1px solid var(--border);border-radius:999px;
      padding:6px 12px;color:var(--muted);
      display:flex;align-items:center;gap:8px;
      background:rgba(255,255,255,.02);
    }
    .stat-pill .dot{
      width:7px;height:7px;border-radius:50%;
      background:var(--green);
      box-shadow:0 0 0 0 rgba(0,255,136,.4);
      animation:pulse 2s ease-in-out infinite;
    }
    @keyframes pulse{
      0%,100%{opacity:1;box-shadow:0 0 0 0 rgba(0,255,136,.35)}
      50%{opacity:.7;box-shadow:0 0 0 6px rgba(0,255,136,0)}
    }

    .steps-track{
      display:flex;align-items:center;gap:0;
      border:1px solid var(--border);border-radius:999px;
      padding:4px;background:var(--surface);
      width:fit-content;margin:14px 0 18px;
    }
    .step-pill{
      display:flex;align-items:center;gap:8px;
      padding:7px 16px;border-radius:999px;
      font-size:12px;font-weight:600;cursor:pointer;
      transition:all .2s ease;color:var(--muted);
      user-select:none;
      white-space:nowrap;
    }
    .step-pill .snum{
      font-family:var(--mono);font-size:10px;
      width:18px;height:18px;border-radius:50%;
      border:1px solid currentColor;
      display:flex;align-items:center;justify-content:center;
      flex-shrink:0;
    }
    .step-pill.active{
      background:linear-gradient(135deg,rgba(0,255,136,.18),rgba(56,189,248,.10));
      color:var(--green);
      border:1px solid rgba(0,255,136,.35);
    }
    .step-pill.done{color:var(--blue)}
    .step-pill.done .snum{border-color:var(--blue)}

    .main{display:grid;grid-template-columns:1fr 380px;gap:18px;align-items:start}
    @media(max-width:920px){.main{grid-template-columns:1fr}}

    .wizard, .preview-dock{
      border:1px solid var(--border);
      border-radius:var(--radius);
      background:var(--panel);
      overflow:hidden;
    }
    .wizard-inner{padding:20px}
    .dock-header{
      padding:14px 16px;border-bottom:1px solid var(--border);
      display:flex;align-items:center;justify-content:space-between;
    }
    .dock-title{font-size:13px;font-weight:800;color:var(--muted)}
    .dock-body{padding:16px}

    .step-content{display:none;animation:stepIn .25s ease}
    .step-content.active{display:block}
    @keyframes stepIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}

    .section-label{
      font-family:var(--mono);font-size:10px;color:var(--muted);
      letter-spacing:.12em;text-transform:uppercase;
      margin-bottom:12px;display:flex;align-items:center;gap:8px;
    }
    .section-label::after{content:"";flex:1;height:1px;background:var(--border)}
    .step-title{font-size:20px;font-weight:800;margin-bottom:6px}
    .step-desc{color:var(--muted);font-size:13px;line-height:1.6;margin-bottom:14px}

    .sel-grid{display:grid;gap:10px}
    .sel-grid.cols2{grid-template-columns:1fr 1fr}
    @media(max-width:700px){.sel-grid.cols2{grid-template-columns:1fr}}

    .sel-card{
      border:1px solid var(--border);
      border-radius:12px;
      background:rgba(255,255,255,.02);
      padding:14px;
      cursor:pointer;
      transition:all .18s ease;
      position:relative;overflow:hidden;
    }
    .sel-card::before{
      content:"";position:absolute;inset:0;
      background:linear-gradient(135deg,rgba(0,255,136,.06),rgba(56,189,248,.04));
      opacity:0;transition:opacity .18s;
    }
    .sel-card:hover{border-color:rgba(0,255,136,.25);transform:translateY(-1px)}
    .sel-card:hover::before{opacity:1}
    .sel-card.sel{
      border-color:rgba(0,255,136,.55);
      background:rgba(0,255,136,.06);
      box-shadow:var(--glow-g);
    }
    .sel-card.sel::before{opacity:1}
    .sel-card .check{
      position:absolute;top:10px;right:10px;
      width:18px;height:18px;border-radius:50%;
      background:var(--green);color:#050912;
      display:flex;align-items:center;justify-content:center;
      font-size:10px;opacity:0;transition:opacity .18s;
      font-family:var(--mono);font-weight:900;
    }
    .sel-card.sel .check{opacity:1}

    .card-icon{font-size:22px;margin-bottom:8px;line-height:1}
    .card-title{font-size:14px;font-weight:800;margin-bottom:4px}
    .card-meta{font-size:12px;color:var(--muted);line-height:1.5}

    .card-badge{
      display:inline-block;margin-top:8px;
      font-family:var(--mono);font-size:9px;
      padding:2px 7px;border-radius:999px;
      border:1px solid var(--border);color:var(--muted);
    }
    .card-badge.high{color:var(--red);border-color:rgba(248,113,113,.35);background:rgba(248,113,113,.06)}
    .card-badge.medium{color:var(--amber);border-color:rgba(251,191,36,.35);background:rgba(251,191,36,.06)}
    .card-badge.low{color:var(--green);border-color:rgba(0,255,136,.35);background:rgba(0,255,136,.06)}

    .proj-claim{
      font-size:11.5px;color:var(--text);line-height:1.5;
      border-left:2px solid var(--green);padding-left:9px;
      margin-top:10px;
    }
    .proj-fail{
      font-family:var(--mono);font-size:10.5px;color:var(--red);
      margin-top:8px;padding:6px 9px;
      background:rgba(248,113,113,.06);
      border-radius:8px;border:1px solid rgba(248,113,113,.18);
    }

    .nav-row{
      display:flex;align-items:center;justify-content:space-between;
      margin-top:16px;padding-top:14px;border-top:1px solid var(--border);
      gap:10px;flex-wrap:wrap;
    }
    .btn{
      display:inline-flex;align-items:center;gap:7px;
      padding:10px 16px;border-radius:10px;
      font-family:var(--display);font-size:13px;font-weight:800;
      cursor:pointer;border:1px solid var(--border);
      background:rgba(255,255,255,.04);
      color:var(--text);transition:all .18s;text-decoration:none;
      user-select:none;
    }
    .btn:hover{border-color:rgba(255,255,255,.22);background:rgba(255,255,255,.07)}
    .btn.primary{
      border-color:rgba(0,255,136,.40);
      background:linear-gradient(135deg,rgba(0,255,136,.18),rgba(56,189,248,.10));
      color:var(--green);
    }
    .btn.primary:hover{border-color:rgba(0,255,136,.65);box-shadow:var(--glow-g)}
    .btn.ghost{background:transparent;color:var(--muted)}
    .btn.ghost:hover{color:var(--text)}
    .btn.sm{padding:7px 12px;font-size:12px;font-weight:800}
    .btn:disabled{opacity:.35;pointer-events:none}

    .score-ring-wrap{display:flex;align-items:center;gap:14px;margin-bottom:14px}
    .score-ring-svg{flex-shrink:0;filter:drop-shadow(0 0 12px rgba(0,255,136,.18))}
    .score-ring-track{fill:none;stroke:rgba(255,255,255,.06);stroke-width:7}
    .score-ring-fill{
      fill:none;stroke:url(#ringGrad);stroke-width:7;stroke-linecap:round;
      transform:rotate(-90deg);transform-origin:center;
      transition:stroke-dashoffset .5s cubic-bezier(.4,0,.2,1);
    }
    .score-number{font-size:28px;font-weight:900;font-family:var(--mono)}
    .score-label{font-size:11px;color:var(--muted);margin-top:2px}
    .score-verdict{font-size:12px;font-weight:800;margin-top:6px;line-height:1.4}

    hr.fancy{border:none;border-top:1px solid var(--border);margin:14px 0}

    .block{
      border-left:2px solid var(--green);
      padding:10px 12px;
      background:rgba(0,255,136,.04);
      border-radius:0 10px 10px 0;
      margin-bottom:10px;
    }
    .block .label{
      font-family:var(--mono);font-size:9px;color:var(--green);
      text-transform:uppercase;letter-spacing:.1em;margin-bottom:4px;
    }
    .block .text{font-size:12px;line-height:1.55;color:var(--text)}

    .block.fail{
      border-left-color:var(--red);
      background:rgba(248,113,113,.04);
    }
    .block.fail .label{color:var(--red)}
    .block.fail .text{font-family:var(--mono);font-size:11px}

    .witnesses-label{
      font-family:var(--mono);font-size:9px;color:var(--muted);
      text-transform:uppercase;letter-spacing:.1em;margin:10px 0 8px;
    }
    .witness-item{
      display:flex;align-items:flex-start;gap:10px;
      padding:8px 0;border-bottom:1px solid var(--border);
    }
    .witness-item:last-child{border-bottom:none}
    .w-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:3px}
    .w-dot.hard{background:var(--red);box-shadow:0 0 6px rgba(248,113,113,.45)}
    .w-dot.soft{background:var(--amber);box-shadow:0 0 6px rgba(251,191,36,.35)}
    .w-id{font-family:var(--mono);font-size:10px;color:var(--muted);flex-shrink:0;width:92px;padding-top:1px}
    .w-text{font-size:11px;color:var(--text);line-height:1.45}
    .w-fail{font-family:var(--mono);font-size:10px;color:var(--muted);margin-top:2px;line-height:1.35}

    .tabs{display:flex;gap:2px;margin-bottom:10px;padding:4px;background:var(--surface);border-radius:10px}
    .tab{
      flex:1;padding:7px;border-radius:8px;
      font-family:var(--mono);font-size:11px;
      cursor:pointer;border:none;background:none;color:var(--muted);
      transition:all .18s;
    }
    .tab.active{background:var(--panel);color:var(--text)}

    .copy-row{display:flex;gap:8px;margin-bottom:10px;flex-wrap:wrap}
    .output-box{
      background:#030509;border:1px solid var(--border);border-radius:10px;
      padding:12px;font-family:var(--mono);font-size:11px;
      color:#a8c0e8;line-height:1.7;white-space:pre-wrap;
      overflow-wrap:anywhere;max-height:320px;overflow-y:auto;
    }
    .output-box .k{color:#7dd3fc}
    .output-box .v{color:#a7f3d0}

    .byoa{
      margin-top:12px;
      border:1px solid rgba(129,140,248,.25);
      background:rgba(129,140,248,.04);
      border-radius:12px;
      padding:12px;
    }
    .byoa h3{font-size:13px;font-weight:900;margin-bottom:8px;color:var(--text)}
    .byoa p{font-size:12px;color:var(--muted);line-height:1.5;margin-bottom:10px}
    .byoa .mini{font-family:var(--mono);font-size:11px;color:#a8c0e8;white-space:pre-wrap;overflow-wrap:anywhere}
  </style>
</head>

<body>
<div class="root">
  <div class="header">
    <div>
      <div class="logo">
        <div class="logo-mark">IF</div>
        <div class="logo-text">Idea Forge <span class="logo-badge">openline.science.v1</span></div>
      </div>
      <div class="tagline">
        A tiny, free “choose-your-own-adventure” for turning a <b>weird thought</b> into a <em>testable</em> plan.
        No logins. No keys. You leave with a GitHub Issue + YAML pack.
      </div>
    </div>
    <div class="header-stats">
      <div class="stat-pill"><span class="dot"></span> free starter kit</div>
      <div class="stat-pill">default: Agents</div>
      <div class="stat-pill">output: Issue + YAML</div>
    </div>
  </div>

  <div class="steps-track" id="stepTrack">
    <div class="step-pill active" data-step="0"><span class="snum">1</span> Topic</div>
    <div class="step-pill" data-step="1"><span class="snum">2</span> Project</div>
    <div class="step-pill" data-step="2"><span class="snum">3</span> Setup</div>
    <div class="step-pill" data-step="3"><span class="snum">4</span> Generate</div>
  </div>

  <div class="main">
    <div class="wizard">
      <div class="wizard-inner">

        <div class="step-content active" data-step="0">
          <div class="section-label">Step 1 of 4</div>
          <div class="step-title">Pick a topic</div>
          <div class="step-desc">No blanks. Pick what you care about. The missions are pre-filled and solvable.</div>
          <div class="sel-grid cols2" id="topicsGrid"></div>
          <div class="nav-row">
            <div></div>
            <button class="btn primary" id="to1">Continue</button>
          </div>
        </div>

        <div class="step-content" data-step="1">
          <div class="section-label">Step 2 of 4</div>
          <div class="step-title">Pick a project</div>
          <div class="step-desc">Each mission includes: a claim, the common shortcut, court tests, and a cheap falsifier.</div>
          <div class="sel-grid" id="projectsGrid"></div>
          <div class="nav-row">
            <button class="btn ghost" id="back0">Back</button>
            <button class="btn primary" id="to2">Continue</button>
          </div>
        </div>

        <div class="step-content" data-step="2">
          <div class="section-label">Step 3 of 4</div>
          <div class="step-title">Pick your setup</div>
          <div class="step-desc">This only changes the minimum plan and the score. The mission stays the same.</div>

          <div class="section-label" style="margin-top:14px">Who is running it?</div>
          <div class="sel-grid cols2" id="setupsGrid"></div>

          <div class="section-label" style="margin-top:16px">Time window</div>
          <div class="sel-grid cols2" id="windowsGrid"></div>

          <div class="nav-row">
            <button class="btn ghost" id="back1">Back</button>
            <button class="btn primary" id="to3">Continue</button>
          </div>
        </div>

        <div class="step-content" data-step="3">
          <div class="section-label">Step 4 of 4</div>
          <div class="step-title">Generate your pack</div>
          <div class="step-desc">Click Generate. Then copy it into a GitHub Issue. That’s the whole “public record” move.</div>

          <div class="nav-row">
            <button class="btn ghost" id="back2">Back</button>
            <div style="display:flex;gap:10px;flex-wrap:wrap">
              <button class="btn primary" id="genBtn">Generate Pack</button>
            </div>
          </div>

          <div class="byoa">
            <h3>Bring your own agent (optional)</h3>
            <p>Static page means no keys here. If you want, you can copy this tool schema into your agent so it can generate packs locally and still output the same format.</p>
            <div class="mini" id="toolSchema"></div>
          </div>
        </div>

      </div>
    </div>

    <div class="preview-dock">
      <div class="dock-header">
        <div class="dock-title">Live preview</div>
      </div>
      <div class="dock-body">

        <div class="score-ring-wrap">
          <svg class="score-ring-svg" width="80" height="80" viewBox="0 0 80 80">
            <defs>
              <linearGradient id="ringGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#00ff88"/>
                <stop offset="100%" stop-color="#38bdf8"/>
              </linearGradient>
            </defs>
            <circle class="score-ring-track" cx="40" cy="40" r="33"/>
            <circle class="score-ring-fill" id="ringFill" cx="40" cy="40" r="33"
              stroke-dasharray="207.3" stroke-dashoffset="207.3"/>
          </svg>
          <div>
            <div class="score-number" id="scoreNum">—</div>
            <div class="score-label">testability score</div>
            <div class="score-verdict" id="scoreVerdict" style="color:var(--muted)">Pick a project to score it.</div>
          </div>
        </div>

        <hr class="fancy"/>

        <div class="block" id="claimBlock" style="opacity:.35">
          <div class="label">claim</div>
          <div class="text" id="previewClaim">Choose a project.</div>
        </div>

        <div class="block fail" id="failBlock" style="opacity:.35">
          <div class="label">falsifier</div>
          <div class="text" id="previewFalsifier">—</div>
        </div>

        <div class="witnesses-label" id="wLabel" style="display:none">Court tests</div>
        <div id="witnessList"></div>

        <hr class="fancy"/>

        <div class="tabs">
          <button class="tab active" id="tabIssue">Issue body</button>
          <button class="tab" id="tabYaml">YAML spec</button>
        </div>

        <div class="copy-row">
          <button class="btn sm" id="copyBtn">Copy</button>
          <a class="btn sm primary" id="ghLink" href="#" target="_blank" rel="noopener" style="opacity:.4;pointer-events:none">Open Issue</a>
        </div>

        <div class="output-box" id="outputBox">(generate to see output)</div>
      </div>
    </div>
  </div>
</div>

<script>
  const REPO_NEW_ISSUE = "https://github.com/terryncew/openline-idea-forge/issues/new";

  const TOPICS = [
    { key:"ai-governance", icon:"🧠", title:"AI governance", meta:"Stop runaway behavior. Make drift visible.", color:"blue" },
    { key:"climate", icon:"🌱", title:"Climate & carbon", meta:"Carbon accounting, stability, durability.", color:"green" },
    { key:"cost", icon:"⚡", title:"Cost & productivity", meta:"Reduce waste. Shorten time-to-results.", color:"amber" },
    { key:"privacy", icon:"🔒", title:"Privacy & freedom", meta:"Proof without surveillance.", color:"violet" }
  ];

  const PROJECTS = {
    "ai-governance": [
      {
        id:"AG-LOOPKILL", domain:"agents",
        title:"Loop kill switch for AI agents",
        kpi:"Reduce cost-per-solved ≥30% while keeping false stops ≤2%",
        cheat_risk:"high",
        claim:"A loop governor reduces repeated-action burn by ≥30% on held-out real tasks while keeping false stops at or below 2%.",
        cheat:"It 'saves money' by stopping hard-but-solvable work early.",
        falsifier:"FAIL if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
        buyer:"Teams shipping production agents where budget + reliability both matter.",
        notes:"Lock the definition of 'solved' up front. Track cost-per-solved AND false stops simultaneously.",
        limits:[
          "Does not make the model smarter — it reduces waste and makes behavior reviewable.",
          "If 'solved' is not pre-defined, results are not meaningful.",
          "This is a guardrail + audit layer, not an evaluator."
        ],
        witnesses:[
          ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
          ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded within window","Repetition exceeds bound — looping"],
          ["W3_TESTS","stability","hard","Regression suite passes on completion","Tests fail or regressions spike"],
          ["W4_COST","cost_feasibility","soft","Cost-per-solved stays within cap","Cost-per-solved worsens beyond cap"]
        ]
      },
      {
        id:"AG-PUBLICLOG", domain:"agents",
        title:"Minimal public receipt log for AI actions",
        kpi:"Prove what happened without storing private content",
        cheat_risk:"medium",
        claim:"A minimal receipt log proves what an AI did (actions + timestamps + checks) without logging user content.",
        cheat:"It produces official-looking summaries that cannot be audited, or it leaks sensitive content.",
        falsifier:"FAIL if auditors cannot verify decisions OR if the log requires storing private content to be useful.",
        buyer:"Any org deploying AI in high-stakes workflows: support, legal, compliance.",
        notes:"Keep logs content-minimal. Require independent verification of receipts.",
        limits:[
          "Stores decision traces, not conversations.",
          "Does not prevent all misuse — it makes misuse harder to deny.",
          "If it leaks content, it fails unconditionally."
        ],
        witnesses:[
          ["W1_VERIFY","origin","hard","Independent verifier validates receipts","Receipts cannot be verified"],
          ["W2_PRIVACY","cheat_suppression","hard","No user content stored; leakage tests pass","Content leakage required or occurs"],
          ["W3_STABILITY","stability","hard","Works across multiple tools/runs","Only works in one demo setup"],
          ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"]
        ]
      }
    ],
    "climate": [
      {
        id:"CO2-HER", domain:"co2",
        title:"CO2 conversion without hydrogen cheat",
        kpi:"FE(CO) ≥90%, side reactions bounded, ≥10h time-on-stream",
        cheat_risk:"high",
        claim:"A CO2RR setup holds FE to CO ≥90% while keeping side reactions below bound for ≥10 hours continuous operation.",
        cheat:"It looks good briefly, or carbon accounting does not close.",
        falsifier:"FAIL if carbon balance does not close OR FE collapses before 10h OR side reactions dominate current.",
        buyer:"CO2 electrolysis startups and industrial R&D teams.",
        notes:"Carbon balance is non-negotiable. Stability over time matters more than peak.",
        limits:[
          "Not a full climate claim without lifecycle accounting.",
          "Peak performance is not the win — stability is.",
          "If carbon balance does not close, the result is not credible."
        ],
        witnesses:[
          ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
          ["W2_SIDE","cheat_suppression","hard","Side reactions bounded at target current","Side reaction dominates current"],
          ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay or deactivation"],
          ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable at target scale","Fast degradation or high replacement cost"]
        ]
      }
    ],
    "cost": [
      {
        id:"BAT-SEI", domain:"batteries",
        title:"Battery additive that survives real failure modes",
        kpi:"CE +1%, lower impedance growth, gas below threshold ≥100 cycles",
        cheat_risk:"medium",
        claim:"An additive improves Coulombic Efficiency by ≥1% and reduces impedance growth while keeping gas evolution below threshold over ≥100 cycles.",
        cheat:"It looks good early but parasitics dominate later, or it does not replicate across batches.",
        falsifier:"FAIL if replicate loses effect OR parasitics exceed bound OR CE gain disappears by cycle 100.",
        buyer:"Battery startups, electrolyte suppliers, OEM labs.",
        notes:"Track parasitics (gas + EIS), not just capacity. Replicate on a second batch.",
        limits:[
          "Does not generalize across chemistries without re-test.",
          "Short tests are unreliable — parasitics take time.",
          "Replication on a second batch is required."
        ],
        witnesses:[
          ["W1_ORIGIN","origin","hard","Effect replicates on separate build/batch","Effect vanishes on replicate"],
          ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS bounded","Parasitics dominate"],
          ["W3_STABILITY","stability","hard","CE and EIS within bounds ≥100 cycles","CE collapses or EIS runaway"],
          ["W4_COST","cost_feasibility","soft","Feasible and safe at scale","Prohibitive or unsafe"]
        ]
      }
    ],
    "privacy": [
      {
        id:"PRIV-RECORD", domain:"agents",
        title:"Proof without surveillance for high-stakes AI",
        kpi:"Auditable outcomes with minimal private data logging",
        cheat_risk:"medium",
        claim:"A proof log supports audits and dispute resolution without recording private user content.",
        cheat:"It stores too much (privacy failure) or too little (audit failure).",
        falsifier:"FAIL if audit cannot reconstruct the decision OR if logs include private content.",
        buyer:"Civic orgs, journalists, compliance teams, public-interest tech groups.",
        notes:"Minimize data stored. Maximize verifiability. Make disputes resolvable by outside parties.",
        limits:[
          "This is not surveillance — it is a dispute-resolving record.",
          "Too much logging fails privacy; too little fails audit.",
          "Must be verifiable by an independent outside party."
        ],
        witnesses:[
          ["W1_VERIFY","origin","hard","Outside verifier validates the record","Outside verification fails"],
          ["W2_PRIVACY","cheat_suppression","hard","Content-minimal logging passes leakage tests","Content stored or leaks"],
          ["W3_UTILITY","stability","hard","Record resolves example disputes","Record cannot settle disputes"],
          ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"]
        ]
      }
    ]
  };

  const SETUPS = [
    { key:"solo", icon:"👤", title:"Solo", meta:"You run the test alone.", note:"Do the cheapest falsifier test first. If it survives, recruit help.", score:4 },
    { key:"team", icon:"👥", title:"Small team", meta:"2–5 people split builder / skeptic / recorder.", note:"Assign one person specifically to disprove the claim.", score:9 },
    { key:"agents", icon:"🤖", title:"AI-assisted", meta:"Use Claude/GPT for research + drafting.", note:"Agents can gather evidence; the falsifier is still the judge.", score:11 },
    { key:"lab", icon:"🔬", title:"Lab/org", meta:"You have real instrumentation.", note:"Higher signal but slower loops. Match tests to instrument precision.", score:14 }
  ];

  const WINDOWS = [
    { key:"1h", icon:"⚡", title:"1 hour", meta:"Try to disprove fast.", plan:["Run the smallest test that hits Origin + Cheat suppression.","If it fails, stop. If it survives, schedule a longer run.","Log every decision."], score:4 },
    { key:"1d", icon:"📅", title:"One day", meta:"Enough to know if it’s worth a week.", plan:["Run cheap test + tighten controls.","Extend window — look for decay and parasitics.","Independent rerun on a fresh environment."], score:9 },
    { key:"weekend", icon:"🗓", title:"Weekend", meta:"Cheap → mid → independent rerun.", plan:["Cheap test: Origin + Cheat suppression.","Mid test: longer window + stricter controls.","Independent rerun on new batch or fresh environment."], score:14 }
  ];

  const $ = (id) => document.getElementById(id);

  const state = {
    step: 0,
    topic: "ai-governance",
    project: null,
    setup: "team",
    window: "weekend",
    activeTab: "issue",
    issueBody: "",
    yamlBody: "",
    ghUrl: ""
  };

  function goStep(n){
    state.step = n;
    document.querySelectorAll(".step-content").forEach(el=>{
      el.classList.toggle("active", +el.dataset.step === n);
    });
    document.querySelectorAll(".step-pill").forEach(el=>{
      const s = +el.dataset.step;
      el.classList.toggle("active", s === n);
      el.classList.toggle("done", s < n);
    });
  }

  document.querySelectorAll(".step-pill").forEach(el=>{
    el.addEventListener("click", ()=>{
      const s = +el.dataset.step;
      if (s <= state.step) goStep(s);
    });
  });

  function makeSelCard({icon,title,meta,selected,badge,badgeClass,extra,onclick}){
    const d = document.createElement("div");
    d.className = "sel-card" + (selected ? " sel" : "");
    d.innerHTML = `
      <div class="check">✓</div>
      ${icon ? `<div class="card-icon">${icon}</div>` : ""}
      <div class="card-title">${title}</div>
      <div class="card-meta">${meta}</div>
      ${badge ? `<span class="card-badge ${badgeClass||""}">${badge}</span>` : ""}
      ${extra || ""}
    `;
    d.onclick = onclick;
    return d;
  }

  function renderTopics(){
    const g = $("topicsGrid"); g.innerHTML = "";
    TOPICS.forEach(t=>{
      g.appendChild(makeSelCard({
        icon:t.icon, title:t.title, meta:t.meta,
        selected: state.topic === t.key,
        onclick(){
          state.topic = t.key;
          state.project = null;
          renderTopics();
          renderProjects();
          updatePreview();
        }
      }));
    });
  }

  function renderProjects(){
    const list = PROJECTS[state.topic] || [];
    if (!state.project && list.length) state.project = list[0];

    const g = $("projectsGrid"); g.innerHTML = "";
    list.forEach(p=>{
      const riskClass = p.cheat_risk === "high" ? "high" : (p.cheat_risk === "medium" ? "medium" : "low");
      const d = makeSelCard({
        title:p.title,
        meta:p.kpi,
        selected: state.project && state.project.id === p.id,
        badge:`cheat_risk: ${p.cheat_risk}`,
        badgeClass:riskClass,
        extra:`<div class="proj-claim">${p.claim}</div><div class="proj-fail">FAIL: ${p.falsifier}</div>`,
        onclick(){
          state.project = p;
          renderProjects();
          updatePreview();
        }
      });
      g.appendChild(d);
    });
  }

  function renderSetups(){
    const g = $("setupsGrid"); g.innerHTML = "";
    SETUPS.forEach(s=>{
      g.appendChild(makeSelCard({
        icon:s.icon,
        title:s.title,
        meta:`${s.meta}<br><span style="opacity:.75">${s.note}</span>`,
        selected: state.setup === s.key,
        onclick(){ state.setup = s.key; renderSetups(); updatePreview(); }
      }));
    });
  }

  function renderWindows(){
    const g = $("windowsGrid"); g.innerHTML = "";
    WINDOWS.forEach(w=>{
      g.appendChild(makeSelCard({
        icon:w.icon,
        title:w.title,
        meta:w.meta,
        selected: state.window === w.key,
        onclick(){ state.window = w.key; renderWindows(); updatePreview(); }
      }));
    });
  }

  function computeScore(p){
    if (!p) return 0;
    const base = 50;
    const witness = Math.min(20, (p.witnesses?.length||0)*5);
    const cheat = p.cheat_risk === "high" ? 10 : (p.cheat_risk === "medium" ? 6 : 3);
    const setup = (SETUPS.find(x=>x.key===state.setup)?.score)||0;
    const win = (WINDOWS.find(x=>x.key===state.window)?.score)||0;
    return Math.min(100, base + witness + cheat + setup + win);
  }

  function updatePreview(){
    const p = state.project;
    if (!p) return;

    const s = computeScore(p);
    $("scoreNum").textContent = s;
    const circumference = 2*Math.PI*33;
    const offset = circumference - (s/100)*circumference;
    $("ringFill").style.strokeDashoffset = offset;

    const verdict = s>=85 ? ["var(--green)","High confidence — testable this week."] :
                    s>=70 ? ["var(--blue)","Testable with tight guardrails."] :
                            ["var(--amber)","Needs stronger proof to be credible."];
    $("scoreVerdict").style.color = verdict[0];
    $("scoreVerdict").textContent = verdict[1];

    $("claimBlock").style.opacity = "1";
    $("failBlock").style.opacity = "1";
    $("previewClaim").textContent = p.claim;
    $("previewFalsifier").textContent = p.falsifier;

    const wl = $("witnessList");
    wl.innerHTML = "";
    $("wLabel").style.display = "block";
    (p.witnesses||[]).forEach(w=>{
      const item = document.createElement("div");
      item.className = "witness-item";
      item.innerHTML = `
        <div class="w-dot ${w[2]}"></div>
        <div class="w-id">${w[0]}</div>
        <div>
          <div class="w-text">PASS: ${w[3]}</div>
          <div class="w-fail">FAIL: ${w[4]}</div>
        </div>`;
      wl.appendChild(item);
    });

    const tool = {
      name: "idea_forge_pack",
      description: "Generate an Opportunity Pack (claim + court tests + falsifier) in openline.science.v1 format.",
      parameters: {
        type: "object",
        properties: {
          topic: { type: "string", enum: TOPICS.map(t=>t.key) },
          project_id: { type: "string" },
          setup: { type: "string", enum: SETUPS.map(s=>s.key) },
          time_window: { type: "string", enum: WINDOWS.map(w=>w.key) }
        },
        required: ["topic","project_id","setup","time_window"]
      }
    };
    $("toolSchema").textContent = JSON.stringify(tool, null, 2);
  }

  function esc(s){ return String(s||"").replaceAll('"','\\"'); }

  function buildArtifact(){
    const p = state.project;
    if (!p) return alert("Pick a project first.");
    const setup = SETUPS.find(x=>x.key===state.setup);
    const win = WINDOWS.find(x=>x.key===state.window);
    const score = computeScore(p);
    const id = `OP-${p.domain.toUpperCase()}-${new Date().toISOString().slice(2,10).replaceAll("-","")}`;

    const witnessLines = (p.witnesses||[]).map(w =>
      `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
    ).join("\n");

    const limitLines = (p.limits||[]).map(x => `- ${x}`).join("\n");

    state.issueBody =
`ID: ${id}
TOPIC: ${state.topic}
DOMAIN: ${p.domain}

RANKING:
- testability_score: ${score}/100
- setup: ${setup.key}
- time_window: ${win.key}

LIMITS:
${limitLines}

CLAIM:
- ${p.claim}

COMMON SHORTCUT:
- ${p.cheat}

COURT TESTS:
${witnessLines}

FALSIFIER:
- ${p.falsifier}

MINIMUM PLAN (${win.title}):
${win.plan.map((s,i)=>`- Step ${i+1}: ${s}`).join("\n")}

WHO BENEFITS IF TRUE:
- ${p.buyer}

WHY IT MATTERS:
- KPI: ${p.kpi}

NOTES:
- ${p.notes}
`;

    state.yamlBody =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
topic: "${state.topic}"
domain: "${p.domain}"
title: "${esc(p.title)}"
ranking:
  testability_score: ${score}
  setup: "${setup.key}"
  time_window: "${win.key}"
limits:
${(p.limits||[]).map(x=>`  - "${esc(x)}"`).join("\n")}
goal_kpi: "${esc(p.kpi)}"
claim: "${esc(p.claim)}"
common_shortcut: "${esc(p.cheat)}"
court_tests:
${(p.witnesses||[]).map(w=>`  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${esc(w[3])}"
    fail_condition: "${esc(w[4])}"`).join("\n")}
falsifier: "${esc(p.falsifier)}"
min_plan:
${win.plan.map((s,i)=>`  - tier: "${i===0?"cheap":i===1?"mid":"expensive"}"
    step: "${esc(s)}"`).join("\n")}
beneficiary: "${esc(p.buyer)}"
notes: "${esc(p.notes)}"
receipt_family: "openline.science.v1"
`;

    renderOutput();
    const title = `Opportunity Pack: ${p.domain.toUpperCase()} — ${p.title}`;
    state.ghUrl = `${REPO_NEW_ISSUE}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(state.issueBody)}`;
    const link = $("ghLink");
    link.href = state.ghUrl;
    link.style.opacity = "1";
    link.style.pointerEvents = "auto";

    goStep(3);
  }

  function renderOutput(){
    const box = $("outputBox");
    const txt = state.activeTab === "issue" ? state.issueBody : state.yamlBody;
    box.textContent = txt || "(generate to see output)";
  }

  function switchTab(which){
    state.activeTab = which;
    $("tabIssue").classList.toggle("active", which==="issue");
    $("tabYaml").classList.toggle("active", which==="yaml");
    renderOutput();
  }

  async function doCopy(){
    const txt = state.activeTab === "issue" ? state.issueBody : state.yamlBody;
    if (!txt) return;
    try{
      await navigator.clipboard.writeText(txt);
      const btn = $("copyBtn");
      const prev = btn.textContent;
      btn.textContent = "✓ Copied";
      setTimeout(()=>btn.textContent=prev, 1400);
    }catch(e){
      alert("Copy failed. Select text manually and copy.");
    }
  }

  $("to1").onclick = ()=>goStep(1);
  $("to2").onclick = ()=>goStep(2);
  $("to3").onclick = ()=>goStep(3);
  $("back0").onclick = ()=>goStep(0);
  $("back1").onclick = ()=>goStep(1);
  $("back2").onclick = ()=>goStep(2);

  $("genBtn").onclick = buildArtifact;

  $("tabIssue").onclick = ()=>switchTab("issue");
  $("tabYaml").onclick = ()=>switchTab("yaml");
  $("copyBtn").onclick = doCopy;

  renderTopics();
  renderProjects();
  renderSetups();
  renderWindows();
  updatePreview();
</script>
</body>
</html>
