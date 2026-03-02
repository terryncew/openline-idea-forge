<!doctype html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Idea Forge · OpenLine</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;700;800&family=JetBrains+Mono:wght@300;400;500;700&display=swap" rel="stylesheet"/>
<style>
/* ── Reset + Variables ───────────────────────────────────────────────────── */
*,::before,::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:       #050912;
  --surface:  #090e1c;
  --panel:    #0c1120;
  --border:   rgba(56,189,248,.12);
  --border2:  rgba(0,255,136,.14);
  --text:     #d8e4f8;
  --muted:    #4a5a7a;
  --dim:      #1e2a44;

–green:    #00ff88;
–green2:   #00c96a;
–blue:     #38bdf8;
–violet:   #818cf8;
–amber:    #fbbf24;
–red:      #f87171;

–glow-g:   0 0 24px rgba(0,255,136,.25);
–glow-b:   0 0 24px rgba(56,189,248,.20);
–glow-v:   0 0 24px rgba(129,140,248,.20);

–radius:   14px;
–mono:     ‘JetBrains Mono’, ui-monospace, monospace;
–display:  ‘Syne’, system-ui, sans-serif;
}

html{scroll-behavior:smooth}
body{
background:var(–bg);
color:var(–text);
font-family:var(–display);
min-height:100vh;
overflow-x:hidden;
}

/* ── Background grid + noise ─────────────────────────────────────────────── */
body::before{
content:’’;
position:fixed;inset:0;
background-image:
radial-gradient(ellipse 70% 60% at 20% 10%, rgba(0,255,136,.06) 0%, transparent 60%),
radial-gradient(ellipse 50% 40% at 80% 80%, rgba(56,189,248,.05) 0%, transparent 60%),
linear-gradient(rgba(56,189,248,.04) 1px, transparent 1px),
linear-gradient(90deg, rgba(56,189,248,.04) 1px, transparent 1px);
background-size:100% 100%, 100% 100%, 48px 48px, 48px 48px;
pointer-events:none;z-index:0;
}

/* ── Layout ──────────────────────────────────────────────────────────────── */
.root{position:relative;z-index:1;max-width:1160px;margin:0 auto;padding:24px 20px 60px}

/* ── Header ──────────────────────────────────────────────────────────────── */
.header{
display:flex;align-items:flex-start;justify-content:space-between;
margin-bottom:32px;gap:20px;
}
.header-left{}
.logo{
display:flex;align-items:center;gap:10px;margin-bottom:10px;
}
.logo-mark{
width:36px;height:36px;border-radius:9px;
background:linear-gradient(135deg,var(–green),var(–blue));
display:flex;align-items:center;justify-content:center;
font-family:var(–mono);font-weight:700;font-size:13px;color:#050912;
flex-shrink:0;
}
.logo-text{font-size:22px;font-weight:800;letter-spacing:-0.03em}
.logo-badge{
font-family:var(–mono);font-size:10px;color:var(–muted);
border:1px solid var(–border);border-radius:99px;padding:3px 9px;
margin-left:6px;
}
.tagline{color:var(–muted);font-size:13.5px;max-width:500px;line-height:1.6}
.tagline em{color:var(–green);font-style:normal}

.header-stats{
display:flex;gap:10px;flex-shrink:0;
}
.stat-pill{
font-family:var(–mono);font-size:11px;
border:1px solid var(–border);border-radius:99px;
padding:5px 12px;color:var(–muted);
display:flex;align-items:center;gap:6px;
}
.stat-pill .dot{
width:6px;height:6px;border-radius:50%;
background:var(–green);
animation:pulse-dot 2s ease-in-out infinite;
}
@keyframes pulse-dot{0%,100%{opacity:1;box-shadow:0 0 0 0 rgba(0,255,136,.4)}50%{opacity:.7;box-shadow:0 0 0 5px rgba(0,255,136,0)}}

/* ── Step pills ──────────────────────────────────────────────────────────── */
.steps-track{
display:flex;align-items:center;gap:0;margin-bottom:28px;
border:1px solid var(–border);border-radius:99px;
padding:4px;background:var(–surface);
width:fit-content;
}
.step-pill{
display:flex;align-items:center;gap:7px;
padding:7px 18px;border-radius:99px;
font-size:12px;font-weight:500;cursor:pointer;
transition:all .25s ease;color:var(–muted);
white-space:nowrap;
}
.step-pill .snum{
font-family:var(–mono);font-size:10px;
width:18px;height:18px;border-radius:50%;
border:1px solid currentColor;
display:flex;align-items:center;justify-content:center;
flex-shrink:0;
}
.step-pill.active{
background:linear-gradient(135deg,rgba(0,255,136,.18),rgba(56,189,248,.10));
color:var(–green);
border:1px solid rgba(0,255,136,.35);
}
.step-pill.done{ color:var(–blue); }
.step-pill.done .snum{ border-color:var(–blue); }

/* ── Main grid ───────────────────────────────────────────────────────────── */
.main{display:grid;grid-template-columns:1fr 380px;gap:20px;align-items:start}
@media(max-width:900px){.main{grid-template-columns:1fr}}

/* ── Wizard panel ────────────────────────────────────────────────────────── */
.wizard{
border:1px solid var(–border);border-radius:var(–radius);
background:var(–panel);overflow:hidden;
}
.wizard-inner{padding:24px}

.step-content{
display:none;
animation:stepIn .3s ease;
}
.step-content.active{display:block}
@keyframes stepIn{
from{opacity:0;transform:translateY(8px)}
to{opacity:1;transform:translateY(0)}
}

.section-label{
font-family:var(–mono);font-size:10px;
color:var(–muted);letter-spacing:.12em;text-transform:uppercase;
margin-bottom:14px;display:flex;align-items:center;gap:8px;
}
.section-label::after{content:’’;flex:1;height:1px;background:var(–border)}

.step-title{font-size:20px;font-weight:800;margin-bottom:5px}
.step-desc{color:var(–muted);font-size:13px;line-height:1.6;margin-bottom:20px}

/* ── Selection cards ─────────────────────────────────────────────────────── */
.sel-grid{display:grid;gap:10px}
.sel-grid.cols2{grid-template-columns:1fr 1fr}
.sel-grid.cols4{grid-template-columns:1fr 1fr 1fr 1fr}
@media(max-width:680px){.sel-grid.cols4,.sel-grid.cols2{grid-template-columns:1fr 1fr}}

.sel-card{
border:1px solid var(–border);border-radius:12px;
background:rgba(255,255,255,.025);
padding:14px;cursor:pointer;
transition:all .2s ease;position:relative;overflow:hidden;
}
.sel-card::before{
content:’’;position:absolute;inset:0;
background:linear-gradient(135deg,rgba(0,255,136,.06),rgba(56,189,248,.04));
opacity:0;transition:opacity .2s;
}
.sel-card:hover{border-color:rgba(0,255,136,.3);transform:translateY(-1px)}
.sel-card:hover::before{opacity:1}
.sel-card.sel{
border-color:rgba(0,255,136,.55);
background:rgba(0,255,136,.06);
box-shadow:var(–glow-g);
}
.sel-card.sel::before{opacity:1}
.sel-card .check{
position:absolute;top:10px;right:10px;
width:18px;height:18px;border-radius:50%;
background:var(–green);color:#050912;
display:flex;align-items:center;justify-content:center;
font-size:10px;opacity:0;transition:opacity .2s;
}
.sel-card.sel .check{opacity:1}

.card-icon{font-size:22px;margin-bottom:8px;line-height:1}
.card-title{font-size:14px;font-weight:700;margin-bottom:4px}
.card-meta{font-size:12px;color:var(–muted);line-height:1.5}
.card-badge{
display:inline-block;margin-top:7px;
font-family:var(–mono);font-size:9px;
padding:2px 7px;border-radius:99px;
border:1px solid var(–border);color:var(–muted);
}
.card-badge.high{color:var(–red);border-color:rgba(248,113,113,.35)}
.card-badge.medium{color:var(–amber);border-color:rgba(251,191,36,.35)}
.card-badge.low{color:var(–green);border-color:rgba(0,255,136,.35)}

/* Project cards (richer) */
.proj-card .proj-claim{
font-size:11.5px;color:var(–text);line-height:1.5;
border-left:2px solid var(–green);padding-left:9px;
margin-top:10px;
}
.proj-card .proj-fail{
font-family:var(–mono);font-size:10.5px;color:var(–red);
margin-top:8px;padding:6px 9px;
background:rgba(248,113,113,.06);border-radius:7px;
border:1px solid rgba(248,113,113,.15);
}

/* ── AI pane ──────────────────────────────────────────────────────────────── */
.ai-pane{
border:1px solid rgba(129,140,248,.25);border-radius:12px;
background:rgba(129,140,248,.04);padding:18px;
margin-top:20px;
}
.ai-pane-label{
font-family:var(–mono);font-size:10px;color:var(–violet);
letter-spacing:.1em;text-transform:uppercase;
display:flex;align-items:center;gap:8px;margin-bottom:12px;
}
.ai-pane-label::before{content:‘◆’;font-size:8px}
.ai-textarea{
width:100%;min-height:80px;
background:rgba(0,0,0,.4);
border:1px solid var(–border);border-radius:9px;
color:var(–text);font-family:var(–display);font-size:13px;
padding:12px;resize:vertical;outline:none;
transition:border-color .2s;
}
.ai-textarea:focus{border-color:rgba(129,140,248,.5);box-shadow:0 0 0 3px rgba(129,140,248,.08)}
.ai-textarea::placeholder{color:var(–muted)}

/* ── Nav row ─────────────────────────────────────────────────────────────── */
.nav-row{
display:flex;align-items:center;justify-content:space-between;
margin-top:22px;padding-top:18px;
border-top:1px solid var(–border);
}
.btn{
display:inline-flex;align-items:center;gap:7px;
padding:10px 18px;border-radius:10px;
font-family:var(–display);font-size:13px;font-weight:600;
cursor:pointer;border:1px solid var(–border);
background:rgba(255,255,255,.04);color:var(–text);
transition:all .2s;text-decoration:none;
}
.btn:hover{border-color:rgba(255,255,255,.25);background:rgba(255,255,255,.07)}
.btn:disabled{opacity:.35;pointer-events:none}
.btn.primary{
border-color:rgba(0,255,136,.4);
background:linear-gradient(135deg,rgba(0,255,136,.20),rgba(56,189,248,.12));
color:var(–green);
}
.btn.primary:hover{
border-color:rgba(0,255,136,.65);
background:linear-gradient(135deg,rgba(0,255,136,.28),rgba(56,189,248,.18));
box-shadow:var(–glow-g);
}
.btn.violet{
border-color:rgba(129,140,248,.4);
background:rgba(129,140,248,.08);color:var(–violet);
}
.btn.violet:hover{background:rgba(129,140,248,.14);box-shadow:var(–glow-v)}
.btn.ghost{background:transparent;border-color:var(–border);color:var(–muted)}
.btn.ghost:hover{color:var(–text)}
.btn svg{width:14px;height:14px}
.btn.sm{padding:7px 13px;font-size:12px}

/* ── Preview dock ─────────────────────────────────────────────────────────── */
.preview-dock{
border:1px solid var(–border);border-radius:var(–radius);
background:var(–panel);
position:sticky;top:20px;overflow:hidden;
}
.dock-header{
padding:16px 20px;border-bottom:1px solid var(–border);
display:flex;align-items:center;justify-content:space-between;
}
.dock-title{font-size:13px;font-weight:700;color:var(–muted)}
.dock-body{padding:20px}

/* Score ring */
.score-ring-wrap{
display:flex;align-items:center;gap:18px;
margin-bottom:20px;
}
.score-ring-svg{flex-shrink:0;filter:drop-shadow(0 0 12px rgba(0,255,136,.25))}
.score-ring-track{fill:none;stroke:rgba(255,255,255,.06);stroke-width:7}
.score-ring-fill{
fill:none;stroke:url(#ringGrad);stroke-width:7;
stroke-linecap:round;
transform:rotate(-90deg);transform-origin:center;
transition:stroke-dashoffset .6s cubic-bezier(.4,0,.2,1);
}
.score-number{font-size:28px;font-weight:800;font-family:var(–mono)}
.score-label{font-size:11px;color:var(–muted);margin-top:2px}
.score-verdict{font-size:12px;font-weight:600;margin-top:6px;line-height:1.4}

/* Claim display */
.claim-block{
border-left:2px solid var(–green);padding:10px 12px;
background:rgba(0,255,136,.04);border-radius:0 8px 8px 0;
margin-bottom:12px;
}
.claim-block .label{
font-family:var(–mono);font-size:9px;color:var(–green);
text-transform:uppercase;letter-spacing:.1em;margin-bottom:4px;
}
.claim-block .text{font-size:12px;line-height:1.55;color:var(–text)}

.falsifier-block{
border-left:2px solid var(–red);padding:10px 12px;
background:rgba(248,113,113,.04);border-radius:0 8px 8px 0;
margin-bottom:16px;
}
.falsifier-block .label{font-family:var(–mono);font-size:9px;color:var(–red);text-transform:uppercase;letter-spacing:.1em;margin-bottom:4px}
.falsifier-block .text{font-family:var(–mono);font-size:11px;line-height:1.55;color:var(–text)}

/* Witnesses */
.witnesses-label{
font-family:var(–mono);font-size:9px;color:var(–muted);
text-transform:uppercase;letter-spacing:.1em;margin-bottom:10px;
}
.witness-item{
display:flex;align-items:flex-start;gap:10px;
padding:8px 0;border-bottom:1px solid var(–border);
animation:witnessIn .3s ease forwards;opacity:0;
}
.witness-item:last-child{border-bottom:none}
@keyframes witnessIn{from{opacity:0;transform:translateX(-6px)}to{opacity:1;transform:translateX(0)}}
.w-dot{
width:8px;height:8px;border-radius:50%;
flex-shrink:0;margin-top:3px;
}
.w-dot.hard{background:var(–red);box-shadow:0 0 6px rgba(248,113,113,.5)}
.w-dot.soft{background:var(–amber);box-shadow:0 0 6px rgba(251,191,36,.4)}
.w-id{font-family:var(–mono);font-size:10px;color:var(–muted);flex-shrink:0;width:90px;padding-top:1px}
.w-text{font-size:11px;color:var(–text);line-height:1.45}
.w-fail{font-family:var(–mono);font-size:10px;color:var(–muted);margin-top:2px;line-height:1.35}

/* ── Output tabs ──────────────────────────────────────────────────────────── */
.tabs{display:flex;gap:2px;margin-bottom:12px;padding:4px;background:var(–surface);border-radius:9px}
.tab{
flex:1;padding:7px;border-radius:7px;
font-family:var(–mono);font-size:11px;
cursor:pointer;border:none;background:none;
color:var(–muted);transition:all .2s;
}
.tab.active{background:var(–panel);color:var(–text)}

.output-box{
background:#030509;border:1px solid var(–border);border-radius:9px;
padding:14px;font-family:var(–mono);font-size:11px;
color:#a8c0e8;line-height:1.7;white-space:pre-wrap;
overflow-wrap:anywhere;max-height:320px;overflow-y:auto;
position:relative;
}
.output-box::-webkit-scrollbar{width:4px}
.output-box::-webkit-scrollbar-thumb{background:var(–dim);border-radius:99px}
.output-box .k{color:#7dd3fc}   /* keys */
.output-box .v{color:#a7f3d0}   /* values */
.output-box .c{color:#4a5a7a}   /* comments */

.copy-row{display:flex;gap:8px;margin-bottom:12px}

/* ── AI loading spinner ───────────────────────────────────────────────────── */
.ai-status{
display:flex;align-items:center;gap:10px;
font-family:var(–mono);font-size:11px;color:var(–violet);
margin-top:10px;opacity:0;transition:opacity .3s;
}
.ai-status.visible{opacity:1}
.spinner{
width:14px;height:14px;border:2px solid rgba(129,140,248,.2);
border-top-color:var(–violet);border-radius:50%;
animation:spin .7s linear infinite;
}
@keyframes spin{to{transform:rotate(360deg)}}

/* ── Terminal cursor blink ───────────────────────────────────────────────── */
.cursor{
display:inline-block;width:7px;height:13px;
background:var(–green);margin-left:2px;
animation:blink .85s step-end infinite;vertical-align:text-bottom;
}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}

/* ── Badges ───────────────────────────────────────────────────────────────── */
.badge{
display:inline-flex;align-items:center;gap:5px;
font-family:var(–mono);font-size:10px;
padding:3px 8px;border-radius:99px;
border:1px solid var(–border);color:var(–muted);
}
.badge.green{color:var(–green);border-color:rgba(0,255,136,.3);background:rgba(0,255,136,.06)}
.badge.blue{color:var(–blue);border-color:rgba(56,189,248,.3);background:rgba(56,189,248,.06)}
.badge.red{color:var(–red);border-color:rgba(248,113,113,.3);background:rgba(248,113,113,.06)}
.badge.amber{color:var(–amber);border-color:rgba(251,191,36,.3);background:rgba(251,191,36,.06)}

/* ── Divider ────────────────────────────────────────────────────────────── */
hr.fancy{border:none;border-top:1px solid var(–border);margin:18px 0}

/* ── Confirmation flash ───────────────────────────────────────────────────── */
@keyframes flashIn{0%{opacity:0;transform:scale(.9)}60%{transform:scale(1.03)}100%{opacity:1;transform:scale(1)}}
.flash{animation:flashIn .35s ease}

/* ── Tooltip ─────────────────────────────────────────────────────────────── */
[data-tip]{position:relative;cursor:help}
[data-tip]::after{
content:attr(data-tip);
position:absolute;bottom:calc(100% + 6px);left:50%;transform:translateX(-50%);
background:#1a2540;border:1px solid var(–border);border-radius:7px;
font-size:11px;padding:5px 9px;white-space:nowrap;pointer-events:none;
opacity:0;transition:opacity .15s;color:var(–text);z-index:99;
}
[data-tip]:hover::after{opacity:1}
</style>

</head>
<body>
<div class="root">

  <!-- ── Header ── -->

  <div class="header">
    <div class="header-left">
      <div class="logo">
        <div class="logo-mark">IF</div>
        <span class="logo-text">Idea Forge</span>
        <span class="logo-badge">openline.v1</span>
      </div>
      <p class="tagline">
        Turn frustration into a <em>testable</em> plan.
        Pick a topic, pick a project, get an Opportunity Pack with a pre-registered falsifier — the cheapest test that would kill it.
      </p>
    </div>
    <div class="header-stats">
      <div class="stat-pill"><div class="dot"></div> 94/94 tests passing</div>
      <div class="stat-pill" data-tip="openline.science.v1">receipt_family: v1</div>
    </div>
  </div>

  <!-- ── Step pills ── -->

  <div class="steps-track" id="stepTrack">
    <div class="step-pill active" data-step="0"><span class="snum">1</span> Topic</div>
    <div class="step-pill" data-step="1"><span class="snum">2</span> Project</div>
    <div class="step-pill" data-step="2"><span class="snum">3</span> Context</div>
    <div class="step-pill" data-step="3"><span class="snum">4</span> Generate</div>
  </div>

  <!-- ── Main grid ── -->

  <div class="main">

```
<!-- ── Wizard ── -->
<div class="wizard">
  <div class="wizard-inner">

    <!-- Step 1: Topic -->
    <div class="step-content active" data-step="0">
      <div class="section-label">Step 1 of 4</div>
      <div class="step-title">What problem are you solving?</div>
      <div class="step-desc">Pick the domain that matches your frustration. Each one has projects with pre-built falsifiers.</div>
      <div class="sel-grid cols2" id="topicsGrid"></div>
      <div class="nav-row">
        <div></div>
        <button class="btn primary" onclick="goStep(1)">
          Continue <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14m-7-7 7 7-7 7"/></svg>
        </button>
      </div>
    </div>

    <!-- Step 2: Project -->
    <div class="step-content" data-step="1">
      <div class="section-label">Step 2 of 4</div>
      <div class="step-title">Choose your project</div>
      <div class="step-desc">Each project has: what success looks like, how it can fake success, and what test would settle it. Pick the one closest to what you want to build.</div>
      <div class="sel-grid" id="projectsGrid"></div>
      <div class="nav-row">
        <button class="btn ghost" onclick="goStep(0)">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M19 12H5m7 7-7-7 7-7"/></svg>
          Back
        </button>
        <button class="btn primary" onclick="goStep(2)">
          Continue <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14m-7-7 7 7-7 7"/></svg>
        </button>
      </div>
    </div>

    <!-- Step 3: Context -->
    <div class="step-content" data-step="2">
      <div class="section-label">Step 3 of 4</div>
      <div class="step-title">Your setup & time window</div>
      <div class="step-desc">These shape the minimum viable test plan. The window sets how aggressive your falsifier gets.</div>
      <div class="section-label" style="margin-top:16px">Who's running it?</div>
      <div class="sel-grid cols2" id="setupsGrid"></div>
      <div class="section-label" style="margin-top:20px">Time window</div>
      <div class="sel-grid cols2" id="windowsGrid"></div>
      <div class="nav-row">
        <button class="btn ghost" onclick="goStep(1)">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M19 12H5m7 7-7-7 7-7"/></svg>
          Back
        </button>
        <button class="btn primary" onclick="goStep(3)">
          Continue <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14m-7-7 7 7-7 7"/></svg>
        </button>
      </div>
    </div>

    <!-- Step 4: Generate -->
    <div class="step-content" data-step="3">
      <div class="section-label">Step 4 of 4</div>
      <div class="step-title">Generate your Pack</div>
      <div class="step-desc">Hit Generate to build your Opportunity Pack — or describe your specific idea and Claude will customize the claim, falsifier, and court tests for you.</div>

      <div class="ai-pane">
        <div class="ai-pane-label">AI Customization (optional)</div>
        <textarea class="ai-textarea" id="aiIdea" placeholder="e.g. I want to build a loop governor for Claude agents that monitors repeated tool calls and halts when it detects spinning on an unsolvable subtask…"></textarea>
        <div class="ai-status" id="aiStatus">
          <div class="spinner"></div>
          <span id="aiStatusText">Generating custom pack via Claude…</span>
        </div>
      </div>

      <div class="nav-row">
        <button class="btn ghost" onclick="goStep(2)">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M19 12H5m7 7-7-7 7-7"/></svg>
          Back
        </button>
        <div style="display:flex;gap:8px">
          <button class="btn violet" id="aiGenBtn" onclick="generateWithAI()">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
            AI Customize
          </button>
          <button class="btn primary" id="genBtn" onclick="buildArtifact()">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/></svg>
            Generate Pack
          </button>
        </div>
      </div>
    </div>

  </div><!-- /wizard-inner -->
</div><!-- /wizard -->

<!-- ── Preview dock ── -->
<div class="preview-dock">
  <div class="dock-header">
    <div class="dock-title">Live Preview</div>
    <div id="docStatus" class="badge green" style="opacity:0">
      <span>●</span> ready
    </div>
  </div>
  <div class="dock-body">

    <!-- Score ring -->
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
        <div class="score-label" id="scoreLabel">testability score</div>
        <div class="score-verdict" id="scoreVerdict" style="color:var(--muted)">Pick a project to score it.</div>
      </div>
    </div>

    <hr class="fancy"/>

    <!-- Claim + falsifier -->
    <div id="claimWrap" style="opacity:.3">
      <div class="claim-block">
        <div class="label">predicted_claim</div>
        <div class="text" id="previewClaim">Choose a project on the left.</div>
      </div>
      <div class="falsifier-block">
        <div class="label">falsifier (pre-registered)</div>
        <div class="text" id="previewFalsifier">—</div>
      </div>
    </div>

    <!-- Witnesses -->
    <div id="witnessWrap" style="display:none">
      <div class="witnesses-label">Court tests · dual-witness protocol</div>
      <div id="witnessList"></div>
    </div>

    <hr class="fancy"/>

    <!-- Output tabs -->
    <div class="tabs">
      <button class="tab active" onclick="switchTab('issue',this)">Issue body</button>
      <button class="tab" onclick="switchTab('yaml',this)">YAML spec</button>
    </div>

    <div class="copy-row">
      <button class="btn sm" id="copyBtn" onclick="doCopy()">Copy</button>
      <a class="btn sm primary" id="ghLink" href="#" target="_blank" rel="noopener" style="opacity:.4;pointer-events:none">
        <svg viewBox="0 0 24 24" fill="currentColor" style="width:12px;height:12px"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.44 9.8 8.2 11.38.6.11.82-.26.82-.58v-2.04c-3.34.73-4.04-1.6-4.04-1.6-.55-1.38-1.34-1.75-1.34-1.75-1.08-.74.08-.73.08-.73 1.2.08 1.83 1.23 1.83 1.23 1.06 1.82 2.8 1.29 3.48.99.1-.77.42-1.3.76-1.6-2.67-.3-5.47-1.33-5.47-5.93 0-1.31.47-2.38 1.24-3.22-.14-.3-.54-1.52.1-3.18 0 0 1-.32 3.3 1.23a11.5 11.5 0 0 1 3-.4c1.02 0 2.04.14 3 .4 2.28-1.55 3.29-1.23 3.29-1.23.65 1.66.24 2.88.12 3.18.77.84 1.23 1.91 1.23 3.22 0 4.61-2.8 5.63-5.48 5.92.43.37.81 1.1.81 2.22v3.29c0 .32.22.7.82.58C20.56 21.8 24 17.3 24 12c0-6.63-5.37-12-12-12z"/></svg>
        Open Issue
      </a>
    </div>

    <div class="output-box" id="outputBox" style="min-height:120px">(generate to see output)</div>

  </div>
</div>
```

  </div><!-- /main -->
</div><!-- /root -->

<script>
/* ── Data ──────────────────────────────────────────────────────────────────── */
const REPO = "https://github.com/terryncew/openline-idea-forge/issues/new";

const TOPICS = [
  { key:"ai-governance", icon:"🧠", title:"AI Governance", meta:"Stop runaway behavior. Make decisions auditable and reviewable.", color:"blue" },
  { key:"climate",       icon:"🌱", title:"Climate & Carbon", meta:"No vibes. Carbon accounting, stability, durability.", color:"green" },
  { key:"cost",          icon:"⚡", title:"Cost & Productivity", meta:"Reduce waste. Shorten time-to-results. Cut parasitics.", color:"amber" },
  { key:"privacy",       icon:"🔒", title:"Privacy & Freedom", meta:"Proof without surveillance. Minimal records, max verifiability.", color:"violet" },
];

const PROJECTS = {
  "ai-governance": [
    {
      id:"AG-LOOPKILL", domain:"agents",
      title:"Loop Kill Switch for AI Agents",
      kpi:"Reduce cost-per-solved ≥30% while keeping false stops ≤2%",
      cheat_risk:"high",
      claim:"A loop governor reduces repeated-action burn by ≥30% on held-out real tasks while keeping false stops at or below 2%.",
      cheat:"It 'saves money' by prematurely stopping hard-but-solvable work.",
      falsifier:"FAIL if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
      buyer:"Teams shipping production agents where budget + reliability both matter.",
      notes:"Lock the definition of 'solved' up front. Track cost-per-solved AND false stops simultaneously.",
      limits:["Does not make the model smarter — it reduces waste and makes behavior reviewable.","If 'solved' is not pre-defined, results are not meaningful.","This is a guardrail + audit layer, not an evaluator."],
      witnesses:[
        ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
        ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded within window","Repetition exceeds bound — looping"],
        ["W3_TESTS","stability","hard","Regression suite passes on completion","Tests fail or regressions spike"],
        ["W4_COST","cost_feasibility","soft","Cost-per-solved stays within cap","Cost-per-solved worsens beyond cap"],
      ]
    },
    {
      id:"AG-PUBLICLOG", domain:"agents",
      title:"Minimal Public Receipt Log for AI Actions",
      kpi:"Prove what happened without storing private content",
      cheat_risk:"medium",
      claim:"A minimal receipt log proves what an AI did (actions + timestamps + checks) without logging user content.",
      cheat:"It produces summaries that look official but can't be audited, or it leaks sensitive content.",
      falsifier:"FAIL if auditors can't verify decisions OR if the log requires storing private content to be useful.",
      buyer:"Any org deploying AI in high-stakes workflows: support, legal, compliance.",
      notes:"Keep logs content-minimal. Require independent verification of receipts.",
      limits:["This stores decision traces, not conversations.","This does not prevent all misuse — it makes misuse harder to deny.","If it leaks content, it fails unconditionally."],
      witnesses:[
        ["W1_VERIFY","origin","hard","Independent verifier validates receipts","Receipts cannot be verified"],
        ["W2_PRIVACY","cheat_suppression","hard","No user content stored; leakage tests pass","Content leakage required or occurs"],
        ["W3_STABILITY","stability","hard","Works across multiple runs and tools","Only works in one demo setup"],
        ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"],
      ]
    },
  ],
  "climate": [
    {
      id:"CO2-HER", domain:"co2",
      title:"CO₂ Conversion Without Hydrogen Cheat",
      kpi:"FE(CO) ≥90%, HER below bound, ≥10h time-on-stream",
      cheat_risk:"high",
      claim:"A CO₂RR setup holds Faradaic Efficiency to CO ≥90% while keeping HER below bound for ≥10 hours continuous operation.",
      cheat:"It looks good briefly, or carbon accounting doesn't close.",
      falsifier:"FAIL if carbon balance doesn't close OR FE collapses before 10h OR HER dominates current.",
      buyer:"CO₂ electrolysis startups and industrial R&D teams.",
      notes:"Carbon balance is non-negotiable. Stability over time matters more than peak performance.",
      limits:["Not a full climate claim without lifecycle accounting.","Peak performance is not the win — stability is.","If carbon balance doesn't close, the result is not credible."],
      witnesses:[
        ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
        ["W2_SIDE","cheat_suppression","hard","Side reactions bounded at target current","Side reaction dominates current"],
        ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay or deactivation"],
        ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable at target scale","Fast degradation or high replacement cost"],
      ]
    },
  ],
  "cost": [
    {
      id:"BAT-SEI", domain:"batteries",
      title:"Battery Additive That Survives Real Failure Modes",
      kpi:"CE +1%, lower impedance growth, gas below threshold ≥100 cycles",
      cheat_risk:"medium",
      claim:"An additive improves Coulombic Efficiency by ≥1% and reduces impedance growth while keeping gas evolution below threshold over ≥100 cycles.",
      cheat:"It looks good early but parasitics (gas/impedance) dominate later, or it doesn't replicate across batches.",
      falsifier:"FAIL if replicate loses effect OR parasitics exceed bound OR CE gain disappears by cycle 100.",
      buyer:"Battery startups, electrolyte suppliers, OEM labs.",
      notes:"Track parasitics (gas + EIS), not just capacity. Replicate on a second batch.",
      limits:["Does not generalize across chemistries without re-test.","Short tests are unreliable — parasitics take time.","Replication on a second batch is required."],
      witnesses:[
        ["W1_ORIGIN","origin","hard","Effect replicates on separate build/batch","Effect vanishes on replicate"],
        ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS bounded","Parasitics dominate"],
        ["W3_STABILITY","stability","hard","CE and EIS within bounds ≥100 cycles","CE collapses or EIS runaway"],
        ["W4_COST","cost_feasibility","soft","Feasible and safe at scale","Prohibitive or unsafe"],
      ]
    },
  ],
  "privacy": [
    {
      id:"PRIV-RECORD", domain:"agents",
      title:"Proof Without Surveillance for High-Stakes AI",
      kpi:"Auditable outcomes with minimal private data logging",
      cheat_risk:"medium",
      claim:"A proof log supports audits and dispute resolution without recording private user content.",
      cheat:"It stores too much (privacy failure) or too little (audit failure).",
      falsifier:"FAIL if audit cannot reconstruct the decision OR if logs include private content.",
      buyer:"Civic orgs, journalists, compliance teams, public-interest tech groups.",
      notes:"Minimize data stored. Maximize verifiability. Make disputes resolvable by outside parties.",
      limits:["This is not surveillance — it's a dispute-resolving record.","Too much logging fails privacy; too little fails audit.","Must be verifiable by an independent outside party."],
      witnesses:[
        ["W1_VERIFY","origin","hard","Outside verifier validates the record","Outside verification fails"],
        ["W2_PRIVACY","cheat_suppression","hard","Content-minimal logging passes leakage tests","Content stored or leaks"],
        ["W3_UTILITY","stability","hard","Record resolves example disputes","Record cannot settle disputes"],
        ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"],
      ]
    },
  ],
};

const SETUPS = [
  { key:"solo",    icon:"👤", title:"Solo",        meta:"You, running the test alone.",             note:"Do the cheapest falsifier test first. If it survives, recruit help.",                          score:4  },
  { key:"team",    icon:"👥", title:"Small team",  meta:"2–5 people splitting builder/skeptic/recorder.", note:"Assign one person specifically to disprove the claim.",                                score:9  },
  { key:"agents",  icon:"🤖", title:"AI-assisted", meta:"Use Claude or GPT for research + drafting.", note:"Agents can gather evidence; the falsifier is still the ultimate judge.",                  score:11 },
  { key:"lab",     icon:"🔬", title:"Lab/org",     meta:"Access to proper instrumentation or infra.",   note:"Higher signal but slower cycle time. Match test to instrument precision.",               score:14 },
];

const WINDOWS = [
  { key:"1h",      icon:"⚡", title:"1 hour",   meta:"Try to disprove fast.",                 plan:["Run the smallest test that hits W1_ORIGIN + W2_cheat_suppression.","If it fails, stop. If it survives, schedule a longer run.","Log every decision."],  score:4  },
  { key:"1d",      icon:"📅", title:"One day",  meta:"Enough to learn if it's worth a week.", plan:["Run cheap test + tighten controls.","Extend window — look for decay and parasitics.","Independent rerun on a fresh environment."],                          score:9  },
  { key:"weekend", icon:"🗓",  title:"Weekend",  meta:"Cheap → mid → independent rerun.",      plan:["Cheap test: W1_ORIGIN + W2_cheat_suppression.","Mid test: longer window + stricter controls.","Independent rerun on new batch or fresh environment."],    score:14 },
];

/* ── State ─────────────────────────────────────────────────────────────────── */
let state = {
  step: 0,
  topic: TOPICS[0].key,
  project: null,
  setup: SETUPS[1].key,
  window: WINDOWS[2].key,
  activeTab: 'issue',
  issueBody: '',
  yamlBody: '',
  ghUrl: '',
  aiOverride: null,
};

/* ── Render helpers ──────────────────────────────────────────────────────────── */
function $ (id){ return document.getElementById(id); }

function makeSelCard(opts){
  const d = document.createElement('div');
  d.className = 'sel-card' + (opts.selected ? ' sel' : '');
  d.innerHTML = `
    <div class="check">✓</div>
    ${opts.icon ? `<div class="card-icon">${opts.icon}</div>` : ''}
    <div class="card-title">${opts.title}</div>
    <div class="card-meta">${opts.meta}</div>
    ${opts.badge ? `<span class="card-badge ${opts.badgeClass||''}">${opts.badge}</span>` : ''}
    ${opts.extra || ''}
  `;
  d.onclick = opts.onclick;
  return d;
}

function renderTopics(){
  const g = $('topicsGrid'); g.innerHTML='';
  TOPICS.forEach(t => {
    g.appendChild(makeSelCard({
      icon: t.icon, title: t.title, meta: t.meta,
      selected: state.topic === t.key,
      onclick(){ state.topic = t.key; state.project = null; state.aiOverride = null; renderTopics(); renderProjects(); updatePreview(); }
    }));
  });
}

function renderProjects(){
  const list = PROJECTS[state.topic] || [];
  if (!state.project && list.length) state.project = list[0];
  const g = $('projectsGrid'); g.innerHTML='';
  list.forEach(p => {
    const riskClass = p.cheat_risk === 'high' ? 'high' : p.cheat_risk === 'medium' ? 'medium' : 'low';
    const d = makeSelCard({
      title: p.title, meta: p.kpi,
      badge: `cheat_risk: ${p.cheat_risk}`, badgeClass: riskClass,
      selected: state.project && state.project.id === p.id,
      extra: `
        <div class="proj-claim">${p.claim}</div>
        <div class="proj-fail">FAIL: ${p.falsifier}</div>
      `,
      onclick(){ state.project = p; state.aiOverride = null; renderProjects(); updatePreview(); }
    });
    d.classList.add('proj-card');
    g.appendChild(d);
  });
  updatePreview();
}

function renderSetups(){
  const g = $('setupsGrid'); g.innerHTML='';
  SETUPS.forEach(s => {
    g.appendChild(makeSelCard({
      icon: s.icon, title: s.title, meta: s.meta + ' <br><small style="opacity:.7">' + s.note + '</small>',
      selected: state.setup === s.key,
      onclick(){ state.setup = s.key; renderSetups(); updatePreview(); }
    }));
  });
}

function renderWindows(){
  const g = $('windowsGrid'); g.innerHTML='';
  WINDOWS.forEach(w => {
    g.appendChild(makeSelCard({
      icon: w.icon, title: w.title, meta: w.meta,
      selected: state.window === w.key,
      onclick(){ state.window = w.key; renderWindows(); updatePreview(); }
    }));
  });
}

/* ── Step navigation ──────────────────────────────────────────────────────── */
function goStep(n){
  state.step = n;
  document.querySelectorAll('.step-content').forEach(el => {
    el.classList.toggle('active', +el.dataset.step === n);
  });
  document.querySelectorAll('.step-pill').forEach(el => {
    const s = +el.dataset.step;
    el.classList.toggle('active', s === n);
    el.classList.toggle('done', s < n);
  });
}

document.querySelectorAll('.step-pill').forEach(el => {
  el.addEventListener('click', () => {
    if (+el.dataset.step < state.step || state.project) goStep(+el.dataset.step);
  });
});

/* ── Score ─────────────────────────────────────────────────────────────────── */
function computeScore(p){
  if (!p) return 0;
  const base    = 50;
  const witness = Math.min(20, (p.witnesses?.length||0) * 5);
  const cheat   = p.cheat_risk === 'high' ? 10 : p.cheat_risk === 'medium' ? 6 : 3;
  const setup   = SETUPS.find(x=>x.key===state.setup)?.score || 0;
  const win     = WINDOWS.find(x=>x.key===state.window)?.score || 0;
  return Math.min(100, base + witness + cheat + setup + win);
}

function updatePreview(){
  const p = state.aiOverride || state.project;
  if (!p){ return; }

  // Score
  const s = computeScore(p);
  $('scoreNum').textContent = s;
  const circumference = 2 * Math.PI * 33;
  const offset = circumference - (s / 100) * circumference;
  $('ringFill').style.strokeDashoffset = offset;

  const verdict = s >= 85 ? ['var(--green)', 'High confidence — testable this week.'] :
                  s >= 70 ? ['var(--blue)', 'Testable with tight guardrails.'] :
                             ['var(--amber)', 'Needs stronger proof to be credible.'];
  $('scoreVerdict').style.color = verdict[0];
  $('scoreVerdict').textContent = verdict[1];

  // Status badge
  $('docStatus').style.opacity = '1';

  // Claim + falsifier
  $('claimWrap').style.opacity = '1';
  $('previewClaim').textContent = p.claim;
  $('previewFalsifier').textContent = p.falsifier;

  // Witnesses
  const wl = $('witnessList'); wl.innerHTML = '';
  $('witnessWrap').style.display = 'block';
  p.witnesses.forEach((w, i) => {
    const item = document.createElement('div');
    item.className = 'witness-item';
    item.style.animationDelay = `${i*60}ms`;
    item.innerHTML = `
      <div class="w-dot ${w[2]}"></div>
      <div class="w-id">${w[0]}</div>
      <div>
        <div class="w-text">PASS: ${w[3]}</div>
        <div class="w-fail">FAIL: ${w[4]}</div>
      </div>
    `;
    wl.appendChild(item);
  });
}

/* ── Build artifact ───────────────────────────────────────────────────────── */
function buildArtifact(){
  const p = state.aiOverride || state.project;
  if (!p) { alert('Please select a project first.'); return; }

  const setup = SETUPS.find(x=>x.key===state.setup);
  const win   = WINDOWS.find(x=>x.key===state.window);
  const score = computeScore(p);
  const id    = `OP-${p.domain.toUpperCase()}-${new Date().toISOString().slice(2,10).replaceAll('-','')}`;

  const witnessLines = (p.witnesses||[]).map(w =>
    `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
  ).join('\n');
  const limitLines = (p.limits||[]).map(x => `- ${x}`).join('\n');

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

COMMON FAILURE / SHORTCUT:
- ${p.cheat}

COURT TESTS (dual-witness protocol):
${witnessLines}

FALSIFIER (cheapest disproof):
- ${p.falsifier}

MINIMUM PLAN (${win.title}):
${win.plan.map((s,i) => `- Step ${i+1}: ${s}`).join('\n')}

SETUP NOTE:
- ${setup.note}

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
${(p.limits||[]).map(x => `  - "${esc(x)}"`).join('\n')}
goal_kpi: "${esc(p.kpi)}"
claim: "${esc(p.claim)}"
common_failure: "${esc(p.cheat)}"
court_tests:
${(p.witnesses||[]).map(w => `  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${esc(w[3])}"
    fail_condition: "${esc(w[4])}"`).join('\n')}
falsifier: "${esc(p.falsifier)}"
min_plan:
${win.plan.map((s,i) => `  - tier: "${i===0?'cheap':i===1?'mid':'expensive'}"
    step: "${esc(s)}"`).join('\n')}
beneficiary: "${esc(p.buyer)}"
notes: "${esc(p.notes)}"
receipt_family: "openline.science.v1"
`;

  renderOutput();

  const title = `Opportunity Pack: ${p.domain.toUpperCase()} — ${p.title}`;
  state.ghUrl = `${REPO}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(state.issueBody)}`;
  $('ghLink').href = state.ghUrl;
  $('ghLink').style.opacity = '1';
  $('ghLink').style.pointerEvents = 'auto';

  // Animate score
  updatePreview();

  // Flash output
  $('outputBox').classList.remove('flash');
  void $('outputBox').offsetWidth;
  $('outputBox').classList.add('flash');
}

function esc(s){ return String(s||'').replaceAll('"','\\"'); }

function renderOutput(){
  const txt = state.activeTab === 'issue' ? state.issueBody : state.yamlBody;
  if (!txt){ $('outputBox').textContent = '(generate to see output)'; return; }
  // Syntax highlight
  const lines = txt.split('\n').map(line => {
    // YAML key: value
    const m = line.match(/^(\s*)([\w_]+)(:)(.*)/);
    if (m) return `${m[1]}<span class="k">${m[2]}</span>${m[3]}<span class="v">${m[4]}</span>`;
    // ALL CAPS lines = headings
    if (/^[A-Z][A-Z\s\/()]+:/.test(line)) return `<span style="color:#7dd3fc;font-weight:700">${line}</span>`;
    // - items
    if (/^\s*-/.test(line)) return `<span style="color:#a7f3d0">${line}</span>`;
    return line;
  }).join('\n');
  $('outputBox').innerHTML = lines;
}

function switchTab(tab, el){
  state.activeTab = tab;
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  el.classList.add('active');
  renderOutput();
}

function doCopy(){
  const txt = state.activeTab === 'issue' ? state.issueBody : state.yamlBody;
  if (!txt) return;
  navigator.clipboard.writeText(txt).then(() => {
    const btn = $('copyBtn');
    btn.textContent = '✓ Copied';
    btn.style.color = 'var(--green)';
    setTimeout(() => { btn.textContent = 'Copy'; btn.style.color = ''; }, 2000);
  }).catch(() => alert('Copy failed. Select text manually.'));
}

/* ── AI generation ────────────────────────────────────────────────────────── */
async function generateWithAI(){
  const idea = $('aiIdea').value.trim();
  if (!idea) { $('aiIdea').focus(); return; }

  const btn = $('aiGenBtn');
  const status = $('aiStatus');
  btn.disabled = true;
  status.classList.add('visible');
  $('aiStatusText').textContent = 'Generating custom pack via Claude…';

  const prompt = `You are building an Opportunity Pack for a science/engineering idea.
The user's idea: "${idea}"

Return ONLY a valid JSON object with these exact fields (no markdown, no explanation):
{
  "id": "CUSTOM-${Date.now()}",
  "domain": "one of: agents, materials, synbio, co2, batteries",
  "title": "Short title (max 60 chars)",
  "kpi": "Key metric with specific threshold",
  "cheat_risk": "high or medium or low",
  "claim": "One-sentence falsifiable claim with specific threshold",
  "cheat": "How this could appear to work without actually working",
  "falsifier": "FAIL if: [specific measurable condition that disproves the claim]",
  "buyer": "Who benefits if this is true",
  "notes": "Key methodological note",
  "limits": ["Limit 1", "Limit 2", "Limit 3"],
  "witnesses": [
    ["W1_ORIGIN","origin","hard","Pass condition","Fail condition"],
    ["W2_CHEAT","cheat_suppression","hard","Pass condition","Fail condition"],
    ["W3_STABILITY","stability","hard","Pass condition","Fail condition"],
    ["W4_COST","cost_feasibility","soft","Pass condition","Fail condition"]
  ]
}`;

  try {
    const resp = await fetch('https://api.anthropic.com/v1/messages', {
      method:'POST',
      headers:{'Content-Type':'application/json'},
      body: JSON.stringify({
        model:'claude-sonnet-4-20250514',
        max_tokens:1000,
        messages:[{role:'user',content:prompt}]
      })
    });
    const data = await resp.json();
    const raw = data.content?.find(c=>c.type==='text')?.text || '';
    const clean = raw.replace(/```json\n?|```/g,'').trim();
    const parsed = JSON.parse(clean);

    // Validate required fields
    if (!parsed.claim || !parsed.falsifier || !parsed.witnesses) throw new Error('Missing fields');

    state.aiOverride = parsed;
    state.project = parsed;
    updatePreview();
    $('aiStatusText').textContent = '✓ Custom pack generated';
    status.style.color = 'var(--green)';
    setTimeout(() => {
      status.classList.remove('visible');
      status.style.color = '';
    }, 3000);

    // Auto-trigger build
    buildArtifact();

  } catch(e) {
    $('aiStatusText').textContent = 'Error — try again or use Generate Pack.';
    status.style.color = 'var(--red)';
    setTimeout(() => { status.classList.remove('visible'); status.style.color=''; }, 4000);
  } finally {
    btn.disabled = false;
  }
}

/* ── Init ─────────────────────────────────────────────────────────────────── */
renderTopics();
renderProjects();
renderSetups();
renderWindows();
updatePreview();

// Keyboard shortcuts
document.addEventListener('keydown', e => {
  if (e.target.tagName === 'TEXTAREA') return;
  if (e.key === 'Enter' && e.metaKey) buildArtifact();
  if (e.key === 'ArrowRight' && state.step < 3) goStep(state.step+1);
  if (e.key === 'ArrowLeft' && state.step > 0)  goStep(state.step-1);
});
</script>

</body>
</html>
