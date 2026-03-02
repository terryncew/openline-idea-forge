<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Idea Forge · OpenLine</title>
<meta name="description" content="Turn a vague idea into a testable plan. Pick a mission. Get a falsifier. Ship an Opportunity Pack."/>
<style>
:root{
  --bg:#070a12; --panel:#0d1324; --panel2:#0b1020;
  --text:#e9eefb; --muted:#9aa6c0; --line:rgba(255,255,255,.12);
  --accent:#64a7ff; --mint:#41f0c2;
  --good:#62ff9a; --warn:#ffd166; --bad:#ff6b6b;
  --mono:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono",monospace;
  --shadow:0 14px 40px rgba(0,0,0,.35);
}
*{box-sizing:border-box}
body{margin:0;background:radial-gradient(1200px 800px at 20% 0%, rgba(100,167,255,.12), transparent 60%),
radial-gradient(1000px 700px at 90% 80%, rgba(65,240,194,.10), transparent 60%), var(--bg);
color:var(--text);font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial}
.wrap{max-width:980px;margin:0 auto;padding:18px 14px 64px}
header{display:flex;gap:14px;align-items:flex-start;justify-content:space-between;flex-wrap:wrap;margin-bottom:14px}
.brand{display:flex;gap:12px;align-items:center}
.logo{width:40px;height:40px;border-radius:12px;background:linear-gradient(135deg,var(--accent),var(--mint));
display:flex;align-items:center;justify-content:center;font-weight:900;color:#07101f}
h1{margin:0;font-size:22px;letter-spacing:.2px}
.sub{margin:2px 0 0;color:var(--muted);line-height:1.35;font-size:13px;max-width:620px}
.pills{display:flex;gap:8px;flex-wrap:wrap;margin-top:8px}
.pill{border:1px solid var(--line);border-radius:999px;padding:6px 10px;font-size:12px;color:var(--muted);background:rgba(255,255,255,.03)}
.grid{display:grid;grid-template-columns:1.1fr .9fr;gap:12px;margin-top:12px}
@media(max-width:920px){.grid{grid-template-columns:1fr}}
.card{border:1px solid var(--line);border-radius:16px;background:rgba(255,255,255,.03);box-shadow:var(--shadow)}
.card .in{padding:14px}
.card h2{margin:0 0 10px;font-size:14px;color:var(--muted);letter-spacing:.3px;text-transform:uppercase}
.row{display:flex;gap:10px;flex-wrap:wrap}
.choice{flex:1;min-width:180px;border:1px solid var(--line);border-radius:14px;padding:12px;background:rgba(255,255,255,.02);
cursor:pointer;transition:transform .12s ease,border-color .12s ease}
.choice:hover{transform:translateY(-1px);border-color:rgba(100,167,255,.35)}
.choice.sel{border-color:rgba(65,240,194,.45);background:linear-gradient(135deg, rgba(100,167,255,.10), rgba(65,240,194,.06))}
.ct{font-weight:800;font-size:14px;margin:0 0 4px}
.cm{margin:0;color:var(--muted);font-size:12.5px;line-height:1.35}
.badges{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
.badge{display:inline-flex;align-items:center;gap:6px;font-size:12px;border:1px solid var(--line);border-radius:999px;padding:5px 10px;color:var(--muted)}
.dot{width:8px;height:8px;border-radius:50%}
.dot.good{background:var(--good)} .dot.warn{background:var(--warn)} .dot.bad{background:var(--bad)}
.kpi{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-top:10px}
.score{font-family:var(--mono);font-weight:800;font-size:20px}
.verdict{color:var(--muted);font-size:12.5px;line-height:1.35}
.bar{height:10px;border-radius:999px;background:rgba(255,255,255,.07);border:1px solid var(--line);overflow:hidden;margin-top:10px}
.bar>div{height:100%;width:0%;background:linear-gradient(90deg,var(--accent),var(--mint))}
.mini{font-family:var(--mono);font-size:12.5px;white-space:pre-wrap;overflow-wrap:anywhere;
border:1px solid var(--line);border-radius:14px;background:var(--panel2);color:#dbe6ff;padding:12px}
.btns{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
button,a.btn{appearance:none;border-radius:12px;border:1px solid var(--line);background:rgba(255,255,255,.04);
color:var(--text);padding:10px 12px;font-size:14px;cursor:pointer;text-decoration:none}
.primary{border-color:rgba(100,167,255,.40);background:linear-gradient(135deg, rgba(100,167,255,.30), rgba(65,240,194,.14))}
.small{color:var(--muted);font-size:12px;line-height:1.35;margin-top:10px}
hr{border:none;border-top:1px solid var(--line);margin:12px 0}
footer{margin-top:16px;color:var(--muted);font-size:12px;line-height:1.4}
kbd{font-family:var(--mono);border:1px solid var(--line);border-bottom-color:rgba(255,255,255,.2);padding:2px 6px;border-radius:7px;background:rgba(255,255,255,.03)}
</style>
</head>
<body>
<div class="wrap">

<header>
  <div class="brand">
    <div class="logo">IF</div>
    <div>
      <h1>Idea Forge</h1>
      <p class="sub">A tiny game that turns “I have a weird thought” into a testable plan. Pick a mission. You’ll get a falsifier (the cheapest way to kill it) + a pack you can submit as a GitHub Issue.</p>
      <div class="pills">
        <span class="pill">No account</span>
        <span class="pill">No API keys</span>
        <span class="pill">Produces real artifacts</span>
      </div>
    </div>
  </div>
  <div class="pills">
    <span class="pill">Default: Agents</span>
    <span class="pill">Receipt family: openline.science.v1</span>
  </div>
</header>

<div class="grid">

  <div class="card">
    <div class="in">
      <h2>1) Pick your lane</h2>
      <div class="row" id="lanes"></div>

      <hr/>

      <h2>2) Pick a mission</h2>
      <div class="row" id="missions"></div>

      <div class="small">No blanks. These are prefilled “real-world solvable” missions. You’re choosing which slope you want to climb.</div>
    </div>
  </div>

  <div class="card">
    <div class="in">
      <h2>3) Your pack (live)</h2>

      <div class="badges">
        <span class="badge"><span class="dot good"></span> Falsifier included</span>
        <span class="badge"><span class="dot warn"></span> Cheat path named</span>
        <span class="badge"><span class="dot bad"></span> Hard witnesses</span>
      </div>

      <div class="kpi">
        <div>
          <div class="score" id="score">—</div>
          <div class="verdict" id="verdict">Pick a mission to score it.</div>
        </div>
        <div style="text-align:right">
          <div style="font-family:var(--mono);font-size:12px;color:var(--muted)">testability</div>
          <div style="font-family:var(--mono);font-size:12px;color:var(--muted)" id="risk">cheat_risk: —</div>
        </div>
      </div>

      <div class="bar" aria-label="score bar"><div id="bar"></div></div>

      <div style="height:10px"></div>
      <div class="mini" id="out">(generate to see output)</div>

      <div class="btns">
        <button class="primary" id="gen">Generate Pack</button>
        <button id="copy">Copy</button>
        <a class="btn" id="openIssue" target="_blank" rel="noopener">Open GitHub Issue</a>
      </div>

      <div class="small">Share move: screenshot the score + falsifier. “You can’t spin a falsifier.”</div>

      <footer>
        Want to plug in your own agent later? This stays free: the spec, the packs, the game. Anything that runs labs / paid verification becomes the paid layer.
      </footer>
    </div>
  </div>

</div>
</div>

<script>
const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

const DATA = {
  lanes: [
    { key:"agents", title:"AI Agents", meta:"Stop loops. Reduce cost. Make behavior auditable." },
    { key:"privacy", title:"Privacy & Freedom", meta:"Proof without surveillance. Disputes become checkable." },
    { key:"climate", title:"Climate & Carbon", meta:"No vibes. Mass balance + durability + time-on-stream." }
  ],
  missions: {
    agents: [
      {
        id:"AG-LOOPKILL",
        title:"Loop Kill Switch",
        kpi:"Cut loop burn ≥30% with false-stops ≤2%",
        cheat_risk:"high",
        claim:"A loop governor reduces repeated-action burn by ≥30% on held-out real tasks while keeping false stops ≤2%.",
        cheat:"It 'saves money' by killing hard-but-solvable tasks (quietly lowering the denominator).",
        falsifier:"FAIL if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
        buyer:"Teams deploying production agents (budget + incident risk).",
        notes:"Lock the definition of 'solved' before the run. Track cost-per-solved + false stops.",
        limits:["Does not make the model smarter. It stops waste.","If 'solved' isn't pre-defined, results don't count.","This is a guardrail + audit layer, not a judge."],
        witnesses:[
          ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
          ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded within window","Repetition exceeds bound (zombie loop)"],
          ["W3_TESTS","stability","hard","Regression suite passes on completion","Tests fail or regressions spike"],
          ["W4_COST","cost_feasibility","soft","Cost-per-solved stays within cap","Cost-per-solved worsens beyond cap"],
        ]
      },
      {
        id:"AG-PUBLICLOG",
        title:"Minimal Receipt Log",
        kpi:"Prove what happened without storing content",
        cheat_risk:"medium",
        claim:"A minimal receipt log proves what an AI did (actions + timestamps + checks) without logging user content.",
        cheat:"It produces 'official' summaries that can't be audited, or it leaks sensitive content.",
        falsifier:"FAIL if auditors can't verify decisions OR if the log requires storing private content to be useful.",
        buyer:"Compliance / support / legal teams deploying AI in high-stakes workflows.",
        notes:"Content-minimal receipts. Independent verification. That’s the whole point.",
        limits:["Stores decision traces, not conversations.","Doesn't stop misuse; it makes misuse harder to deny.","If it leaks content, it fails."],
        witnesses:[
          ["W1_VERIFY","origin","hard","Independent verifier validates receipts","Receipts can't be verified"],
          ["W2_PRIVACY","cheat_suppression","hard","No user content stored; leakage tests pass","Content stored or leaks"],
          ["W3_STABILITY","stability","hard","Works across multiple runs/tools","Only works in one demo setup"],
          ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"],
        ]
      }
    ],
    privacy: [
      {
        id:"PRIV-DISPUTE",
        title:"Dispute-Ready Audit Trail",
        kpi:"Outside parties can verify outcomes",
        cheat_risk:"medium",
        claim:"A proof log settles a real dispute (what happened, when, and why) without recording private user content.",
        cheat:"It stores too much (privacy failure) or too little (audit failure).",
        falsifier:"FAIL if the record can't reconstruct the decision OR if the record includes private content.",
        buyer:"Public-interest orgs + newsrooms + compliance teams.",
        notes:"Aim for 'less watching, more proof.'",
        limits:["Not a chain. Not surveillance.","If outside verification fails, it fails.","If it leaks, it fails."],
        witnesses:[
          ["W1_VERIFY","origin","hard","Outside verifier validates record","Outside verification fails"],
          ["W2_PRIVACY","cheat_suppression","hard","Content-minimal logging passes leakage tests","Content stored or leaks"],
          ["W3_UTILITY","stability","hard","Record resolves example disputes","Record can't settle disputes"],
          ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"],
        ]
      }
    ],
    climate: [
      {
        id:"CO2-HER",
        title:"CO₂ Conversion (No Hydrogen Cheat)",
        kpi:"FE(CO) ≥90% + carbon balance + 10h stability",
        cheat_risk:"high",
        claim:"A CO₂RR setup holds FE to CO ≥90% while keeping side reactions bounded for ≥10 hours continuous operation.",
        cheat:"It looks good briefly, or carbon accounting doesn't close.",
        falsifier:"FAIL if carbon balance doesn't close OR FE collapses before 10h OR side reactions dominate current.",
        buyer:"CO₂ electrolysis startups + industrial R&D.",
        notes:"Mass balance + time-on-stream beat peak charts.",
        limits:["Not a climate claim without lifecycle accounting.","Peak isn't the win; durability is.","If mass balance fails, it's not real."],
        witnesses:[
          ["W1_BALANCE","origin","hard","Mass balance closes","Mass balance does not close"],
          ["W2_SIDE","cheat_suppression","hard","Side reactions bounded at target current","Side reactions dominate current"],
          ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay / deactivation"],
          ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation / high replacement cost"],
        ]
      }
    ]
  }
};

let state = { lane:"agents", mission:null };

const el = (id)=>document.getElementById(id);

function renderLanes(){
  const root = el("lanes"); root.innerHTML="";
  DATA.lanes.forEach(l=>{
    const d = document.createElement("div");
    d.className = "choice" + (state.lane===l.key ? " sel":"");
    d.innerHTML = `<p class="ct">${l.title}</p><p class="cm">${l.meta}</p>`;
    d.onclick = ()=>{ state.lane=l.key; state.mission=null; renderLanes(); renderMissions(); renderPreview(); };
    root.appendChild(d);
  });
}

function renderMissions(){
  const root = el("missions"); root.innerHTML="";
  const list = DATA.missions[state.lane] || [];
  if (!state.mission && list.length) state.mission = list[0];
  list.forEach(m=>{
    const d = document.createElement("div");
    d.className = "choice" + (state.mission && state.mission.id===m.id ? " sel":"");
    d.innerHTML = `<p class="ct">${m.title}</p><p class="cm">${m.kpi}</p>`;
    d.onclick = ()=>{ state.mission=m; renderMissions(); renderPreview(); };
    root.appendChild(d);
  });
}

function computeScore(m){
  if(!m) return 0;
  const base = 55;
  const witness = Math.min(20, (m.witnesses?.length||0)*5);
  const cheat = m.cheat_risk==="high" ? 12 : m.cheat_risk==="medium" ? 7 : 3;
  // simple default: a weekend test is doable if it has a falsifier + 3+ witnesses
  return Math.max(0, Math.min(100, base + witness + cheat));
}

function verdictText(s){
  if (s>=88) return "High chance this is testable right now (and hard to bullshit).";
  if (s>=75) return "Testable with guardrails. Expect one nasty surprise.";
  return "Too squishy. Tighten witnesses or pick a different mission.";
}

function renderPreview(){
  const m = state.mission;
  const s = computeScore(m);
  el("score").textContent = m ? `${s}/100` : "—";
  el("verdict").textContent = m ? verdictText(s) : "Pick a mission to score it.";
  el("risk").textContent = m ? `cheat_risk: ${m.cheat_risk}` : "cheat_risk: —";
  el("bar").style.width = m ? `${s}%` : "0%";
  el("out").textContent = "(generate to see output)";
  el("openIssue").href = REPO_NEW_ISSUE_URL;
}

function genID(domain){
  const stamp = new Date().toISOString().slice(2,10).replaceAll("-","");
  return `OP-${domain.toUpperCase()}-${stamp}`;
}

function buildPack(){
  const m = state.mission;
  if(!m) return;

  const id = genID(m.domain || state.lane);
  const score = computeScore(m);

  const witnessLines = (m.witnesses||[]).map(w =>
    `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
  ).join("\n");

  const limitLines = (m.limits||[]).map(x=>`- ${x}`).join("\n");

  const issueBody =
`ID: ${id}
LANE: ${state.lane}
DOMAIN: ${m.domain}

RANKING:
- testability_score: ${score}/100
- cheat_risk: ${m.cheat_risk}

LIMITS:
${limitLines}

CLAIM:
- ${m.claim}

CHEAT_PATH (how it fakes):
- ${m.cheat}

COURT_TESTS (independent witnesses):
${witnessLines}

FALSIFIER (cheapest disproof):
- ${m.falsifier}

BUYER:
- ${m.buyer}

NOTES:
- ${m.notes}
`;

  const yaml =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
lane: "${state.lane}"
domain: "${m.domain}"
title: "${esc(m.title)}"
ranking:
  testability_score: ${score}
  cheat_risk: "${m.cheat_risk}"
limits:
${(m.limits||[]).map(x=>`  - "${esc(x)}"`).join("\n")}
goal_kpi: "${esc(m.kpi)}"
claim: "${esc(m.claim)}"
cheat_path: "${esc(m.cheat)}"
court_tests:
${(m.witnesses||[]).map(w=>`  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${esc(w[3])}"
    fail_condition: "${esc(w[4])}"`).join("\n")}
falsifier: "${esc(m.falsifier)}"
beneficiary: "${esc(m.buyer)}"
notes: "${esc(m.notes)}"
receipt_family: "openline.science.v1"
`;

  // show both in one blob for shareability
  const blob =
`# Issue Body (paste into a GitHub Issue)
${issueBody}

--- 
# YAML Pack (machine-readable)
${yaml}
`;

  el("out").textContent = blob;

  const title = `Opportunity Pack: ${m.domain.toUpperCase()} — ${m.title}`;
  el("openIssue").href = `${REPO_NEW_ISSUE_URL}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(issueBody)}`;
}

function esc(s){ return String(s||"").replaceAll('"','\\"'); }

async function copyText(){
  const txt = el("out").textContent;
  if(!txt || txt.startsWith("(generate")) return;
  try{ await navigator.clipboard.writeText(txt); }
  catch(e){ alert("Copy failed. Select text manually and copy."); }
}

el("gen").addEventListener("click", buildPack);
el("copy").addEventListener("click", copyText);

renderLanes();
renderMissions();
renderPreview();
</script>
</body>
</html>
