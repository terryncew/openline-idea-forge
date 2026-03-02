<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Idea Forge</title>
<style>
:root{
  --bg:#0b0c10; --panel:#101218; --line:rgba(255,255,255,.12);
  --text:#e9eef7; --muted:#a8b3c7; --accent:#6ea8ff; --mint:#7cf0d2;
  --good:#7CFF9B; --warn:#ffd166; --bad:#ff6b6b;
  --shadow: 0 12px 30px rgba(0,0,0,.35);
  --mono: ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono",monospace;
}
@media (prefers-color-scheme: light){
  :root{ --bg:#fbfcff; --panel:#ffffff; --line:rgba(15,20,40,.12);
    --text:#0b1020; --muted:#3f4b66; --accent:#1f6feb; --mint:#00a884; --shadow:0 10px 30px rgba(10,20,40,.12);}
}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--text);font-family: ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;}
a{color:inherit}
.wrap{max-width:1040px;margin:0 auto;padding:18px 14px 52px;}
.hero{
  border:1px solid var(--line); border-radius:18px; padding:18px;
  background: linear-gradient(135deg, rgba(110,168,255,.18), rgba(124,240,210,.10));
  box-shadow: var(--shadow);
}
h1{margin:0 0 6px;font-size:32px;letter-spacing:.2px}
.lead{margin:0;color:var(--muted);line-height:1.45;max-width:78ch}
.row{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}
.pill{display:inline-block;padding:6px 10px;border:1px solid var(--line);border-radius:999px;font-size:12px;color:var(--muted);background:rgba(255,255,255,.04)}
.grid{display:grid;grid-template-columns:1fr;gap:12px;margin-top:14px}
@media(min-width:980px){.grid{grid-template-columns:1.05fr .95fr}}
.card{border:1px solid var(--line);border-radius:16px;background:var(--panel);padding:14px}
.card h2{margin:0 0 10px;font-size:16px}
.bar{height:10px;border-radius:999px;background:rgba(255,255,255,.08);overflow:hidden;border:1px solid var(--line)}
.bar > div{height:100%;width:0%;background:linear-gradient(90deg, var(--accent), var(--mint))}
.kpi{display:flex;justify-content:space-between;gap:10px;align-items:center;margin-top:10px}
.stageTitle{font-weight:900;letter-spacing:.2px}
.small{font-size:12px;color:var(--muted);line-height:1.35}
.tip{color:var(--muted);font-size:13px;line-height:1.4;margin-top:8px}
.btnrow{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
button,a.btn{
  appearance:none;border-radius:12px;border:1px solid var(--line);
  background:rgba(255,255,255,.04);color:var(--text);
  padding:10px 12px;font-size:14px;cursor:pointer;text-decoration:none;display:inline-block;
}
button.primary{border-color:rgba(110,168,255,.40);background:linear-gradient(135deg, rgba(110,168,255,.34), rgba(124,240,210,.16));}
hr{border:none;border-top:1px solid var(--line);margin:14px 0}
.cards{display:grid;grid-template-columns:1fr;gap:10px;margin-top:10px}
@media(min-width:980px){.cards{grid-template-columns:1fr 1fr}}
.choice{
  border:1px solid var(--line); border-radius:14px; padding:12px; background:rgba(255,255,255,.03);
  cursor:pointer;
}
.choice:hover{ border-color: rgba(110,168,255,.45); }
.choice.sel{ outline: 2px solid rgba(110,168,255,.45); }
.ctitle{font-weight:900;margin:0 0 6px}
.cmeta{margin:0;color:var(--muted);font-size:13px;line-height:1.35}
.mini{
  font-family:var(--mono);font-size:12.5px;white-space:pre-wrap;overflow-wrap:anywhere;
  border:1px solid var(--line);border-radius:16px;background:#0b0f1a;color:#d8e2ff;padding:12px;
}
@media (prefers-color-scheme: light){.mini{background:#0b1020;color:#e9eef7}}
.badge{display:inline-block;padding:4px 8px;border-radius:999px;border:1px solid var(--line);font-size:12px;color:var(--muted)}
.good{color:var(--good);border-color:rgba(124,255,155,.45)}
.warn{color:var(--warn);border-color:rgba(255,209,102,.55)}
.scorebox{
  border:1px solid var(--line); border-radius:14px; padding:12px; background:rgba(255,255,255,.03);
}
.scorebig{font-weight:900;font-size:28px;letter-spacing:.2px}
.scoremeta{color:var(--muted);font-size:13px;line-height:1.35;margin-top:6px}
.subhead{color:var(--muted);font-size:13px;line-height:1.35;margin-top:6px}
</style>
</head>
<body>
<div class="wrap">

  <div class="hero">
    <h1>Idea Forge</h1>
    <p class="lead">
      A simple way to turn frustration into a testable plan.
      Pick a topic, pick a project, and you’ll get a ready-to-share Opportunity Pack (with a clear “how this could be wrong” test).
    </p>
    <div class="row">
      <span class="pill">No blank forms</span>
      <span class="pill">Clear steps</span>
      <span class="pill">Outputs an issue + a spec</span>
      <span class="pill">Built for people who want something better</span>
    </div>
  </div>

  <div class="grid">
    <div class="card">
      <div class="kpi">
        <div class="stageTitle" id="stageTitle">Build your pack</div>
        <div class="small" id="progressText">Progress: 0%</div>
      </div>
      <div class="bar"><div id="barFill"></div></div>

      <div class="subhead">
        What you’re doing: choosing a project that can be tested, then generating a pack with (1) the claim, (2) the common failure/shortcut, (3) independent checks, and (4) the cheapest test that would disprove it.
      </div>

      <hr/>

      <div class="stageTitle">1) Choose a topic</div>
      <div id="step1" class="cards"></div>

      <hr/>

      <div class="stageTitle">2) Choose a project</div>
      <div class="tip">Each project includes: what success looks like, how it can fake success, and what test would settle it.</div>
      <div id="step2" class="cards"></div>

      <hr/>

      <div class="stageTitle">3) Choose your setup</div>
      <div id="step3" class="cards"></div>

      <hr/>

      <div class="stageTitle">4) Choose your time window</div>
      <div id="step4" class="cards"></div>

      <div class="btnrow">
        <button class="primary" id="generate">Generate Opportunity Pack</button>
        <a class="btn" id="openIssueTop" target="_blank" rel="noopener">Open GitHub Issue</a>
      </div>
      <div class="small">If the Issue button is disabled, click Generate once.</div>
    </div>

    <div class="card">
      <h2>Preview</h2>
      <div class="scorebox">
        <div class="scorebig" id="score">—</div>
        <div class="scoremeta" id="scoremeta">Choose options on the left. You’ll see a rank and clear limits.</div>
      </div>

      <hr/>

      <h2>Output</h2>
      <div class="tip">These are copy-paste ready.</div>

      <div class="btnrow">
        <button id="copyIssue">Copy Issue Body</button>
        <button id="copyYaml">Copy YAML</button>
        <a class="btn primary" id="openIssue" target="_blank" rel="noopener">Open GitHub Issue</a>
      </div>

      <hr/>

      <div class="small">Issue body</div>
      <div class="mini" id="outIssue">(generate to see output)</div>

      <div style="height:10px"></div>

      <div class="small">Spec (YAML)</div>
      <div class="mini" id="outYaml">(generate to see output)</div>

      <p class="small">
        Plain-language note: “Receipts” here means a record other people can verify later. The goal is less “trust me,” more “show the record.”
      </p>
    </div>
  </div>
</div>

<script>
const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

const game = {
  topics: [
    { key:"ai-governance", title:"AI you can trust", meta:"Stop runaway behavior. Make decisions auditable." },
    { key:"climate", title:"Climate that holds up", meta:"No vibes. Accounting, stability, durability." },
    { key:"cost", title:"Cost of living & productivity", meta:"Reduce waste. Shorten time-to-results." },
    { key:"privacy", title:"Privacy & freedom", meta:"Proof without surveillance. Minimal records." }
  ],
  projectsByTopic: {
    "ai-governance": [
      {
        id:"AG-LOOPKILL",
        domain:"agents",
        title:"Stop AI from wasting money in loops",
        kpi:"Reduce cost-per-solved without false stops",
        cheat_risk:"high",
        claim:"A loop governor reduces repeated-action burn by ≥30% on real tasks while keeping false stops ≤2%.",
        cheat:"It appears to ‘save money’ by prematurely stopping hard-but-solvable work.",
        falsifier:"Fails if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
        buyer:"Teams shipping production agents (budget + reliability).",
        notes:"Lock the definition of solved. Use held-out tasks. Track cost-per-solved + false stops.",
        limits:[
          "This does not make the model smarter. It reduces waste and makes behavior reviewable.",
          "If “solved” is not defined up front, the results won’t be meaningful.",
          "This is a guardrail + audit layer, not a replacement for evaluation."
        ],
        witnesses:[
          ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
          ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded in window","Repetition exceeds bound (looping)"],
          ["W3_TESTS","stability","hard","Regression/tests pass on completion","Tests fail or regressions spike"],
          ["W4_COST","cost_feasibility","soft","Cost-per-solved stays within cap","Cost-per-solved worsens beyond cap"]
        ]
      },
      {
        id:"AG-PUBLICLOG",
        domain:"agents",
        title:"A minimal public record for AI actions (without logging content)",
        kpi:"Prove what happened without storing private content",
        cheat_risk:"medium",
        claim:"A minimal receipt log proves what an AI did (actions + timestamps + checks) without logging user content.",
        cheat:"It produces summaries that look official but cannot be audited, or it leaks sensitive content.",
        falsifier:"Fails if auditors can’t verify decisions OR if the log requires storing private content to be useful.",
        buyer:"Any org deploying AI in high-stakes workflows (support, legal, compliance).",
        notes:"Keep logs content-minimal. Require independent verification of receipts.",
        limits:[
          "This does not store conversations. It stores decision traces.",
          "This does not prevent all misuse; it makes misuse harder to deny.",
          "If it leaks content, it fails."
        ],
        witnesses:[
          ["W1_VERIFY","origin","hard","Independent verifier validates receipts","Receipts can’t be verified"],
          ["W2_PRIVACY","cheat_suppression","hard","No user content stored; leakage tests pass","Content leakage required or occurs"],
          ["W3_STABILITY","stability","hard","Works across multiple runs/tools","Only works in one demo setup"],
          ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"]
        ]
      }
    ],
    "climate": [
      {
        id:"CO2-HER",
        domain:"co2",
        title:"CO₂ conversion that doesn’t “cheat” into hydrogen",
        kpi:"High FE to target + bounded side reactions + time-on-stream",
        cheat_risk:"high",
        claim:"A CO₂RR setup holds FE(CO) ≥90% while keeping HER below bound for ≥10 hours time-on-stream.",
        cheat:"It looks good briefly, or the accounting doesn’t close (missing carbon).",
        falsifier:"Fails if carbon balance doesn’t close OR FE collapses before 10 hours OR HER dominates current.",
        buyer:"CO₂ electrolysis startups + industrial R&D.",
        notes:"Carbon balance is non-negotiable. Stability matters more than peak performance.",
        limits:[
          "This is not a full climate claim without lifecycle accounting.",
          "Peak performance is not the win; stability is the win.",
          "If carbon balance doesn’t close, the result is not credible."
        ],
        witnesses:[
          ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
          ["W2_SIDE","cheat_suppression","hard","Side reaction bounded at target current","Side reaction dominates current"],
          ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay/deactivation"],
          ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation/high replacement cost"]
        ]
      }
    ],
    "cost": [
      {
        id:"BAT-SEI",
        domain:"batteries",
        title:"Battery additive that survives real-world failure modes",
        kpi:"Better efficiency + lower impedance growth over time",
        cheat_risk:"medium",
        claim:"An additive improves CE by ≥1% and reduces impedance growth while keeping gas evolution below threshold over ≥100 cycles.",
        cheat:"It looks good early but parasitics (gas/impedance) dominate later, or it doesn’t replicate across batches.",
        falsifier:"Fails if replicate loses effect OR parasitics exceed bound OR CE gain disappears by cycle 100.",
        buyer:"Battery startups + electrolyte suppliers + OEM labs.",
        notes:"Track parasitics (gas/EIS), not just capacity. Replicate on a second batch.",
        limits:[
          "Does not generalize across chemistries without re-test.",
          "Short tests are unreliable; parasitics take time.",
          "Replication is required."
        ],
        witnesses:[
          ["W1_ORIGIN","origin","hard","Effect replicates on separate build/batch","Effect vanishes on replicate"],
          ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS bounded","Parasitics dominate"],
          ["W3_STABILITY","stability","hard","CE+EIS within bounds ≥100 cycles","CE collapses/EIS runaway"],
          ["W4_COST","cost_feasibility","soft","Feasible + safe","Prohibitive or unsafe"]
        ]
      }
    ],
    "privacy": [
      {
        id:"PRIV-RECORD",
        domain:"agents",
        title:"Proof without surveillance (for high-stakes AI)",
        kpi:"Auditable outcomes with minimal logging",
        cheat_risk:"medium",
        claim:"A proof log supports audits and disputes without recording private user content.",
        cheat:"It stores too much, or stores too little to be useful.",
        falsifier:"Fails if audit cannot reconstruct the decision OR if logs include private content.",
        buyer:"Civic orgs, journalists, compliance teams, public-interest tech groups.",
        notes:"Minimize data. Maximize verifiability. Make disputes resolvable.",
        limits:[
          "This is not surveillance. It’s a dispute-resolving record.",
          "Too much logging fails privacy; too little logging fails audit.",
          "Must be verifiable by an outside party."
        ],
        witnesses:[
          ["W1_VERIFY","origin","hard","Outside verifier validates the record","Outside verification fails"],
          ["W2_PRIVACY","cheat_suppression","hard","Content-minimal logging passes leakage tests","Content is stored or leaks"],
          ["W3_UTILITY","stability","hard","Record resolves disputes in examples","Record cannot settle disputes"],
          ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"]
        ]
      }
    ]
  },
  setups: [
    { key:"solo", title:"Solo", meta:"You want a plan you can run yourself.", score:+4,
      note:"Do the cheapest falsifier test first. If it survives, recruit help." },
    { key:"friends", title:"Friends (2–5)", meta:"Split roles: builder, skeptic, recorder.", score:+9,
      note:"Assign one person to try to disprove the claim. They are the reviewer." },
    { key:"agents", title:"Agents", meta:"Use Claude/ChatGPT for drafting and research.", score:+11,
      note:"Agents can gather evidence and draft plans; the falsifier stays the boss." }
  ],
  windows: [
    { key:"1h", title:"1 hour", meta:"Try to disprove fast.", score:+4,
      plan:["Run the smallest test that hits Origin + Cheat suppression.","If it fails, stop. If it survives, schedule a longer run."]},
    { key:"1d", title:"One day", meta:"Enough to learn if it’s worth a week.", score:+9,
      plan:["Run cheap test + tighten controls.","Extend window. Look for decay / parasitics.","If it survives, do an independent rerun."]},
    { key:"weekend", title:"Weekend", meta:"Cheap+mid+independent rerun.", score:+14,
      plan:["Cheap test (origin + cheat suppression).","Mid test (longer window + stricter controls).","Independent rerun (new batch/environment)."]}
  ]
};

const el = id => document.getElementById(id);
let sel = { topic: game.topics[0].key, project: null, setup: game.setups[1].key, window: game.windows[2].key };

function setProgress(p){
  el("barFill").style.width = `${p}%`;
  el("progressText").textContent = `Progress: ${p}%`;
}

function card(title, meta){
  const d = document.createElement("div");
  d.className = "choice";
  d.innerHTML = `<p class="ctitle">${title}</p><p class="cmeta">${meta}</p>`;
  return d;
}

function computeScore(project){
  if (!project) return null;
  const base = 50;
  const witnessScore = Math.min(20, (project.witnesses?.length || 0) * 5);
  const cheatRisk = project.cheat_risk === "high" ? 10 : project.cheat_risk === "medium" ? 6 : 3;
  const setupScore = game.setups.find(x=>x.key===sel.setup)?.score || 0;
  const windowScore = game.windows.find(x=>x.key===sel.window)?.score || 0;
  return Math.max(0, Math.min(100, base + witnessScore + cheatRisk + setupScore + windowScore));
}

function updatePreview(){
  const p = sel.project;
  if (!p){
    el("score").textContent = "—";
    el("scoremeta").textContent = "Choose a project to see the preview.";
    return;
  }
  const s = computeScore(p);
  const label = s >= 85 ? "High chance of being testable this week" : s >= 70 ? "Testable with guardrails" : "Needs tighter proof to be credible";
  const limits = (p.limits || []).map(x => `• ${x}`).join(" ");
  el("score").textContent = `${s}/100`;
  el("scoremeta").innerHTML = `<b>${label}.</b><br/>Limits: ${limits}`;
}

function renderTopics(){
  const box = el("step1"); box.innerHTML = "";
  game.topics.forEach(t => {
    const d = card(t.title, t.meta);
    if (t.key === sel.topic) d.classList.add("sel");
    d.onclick = () => {
      sel.topic = t.key;
      sel.project = null;
      renderTopics();
      renderProjects();
      updatePreview();
      setProgress(25);
      disableIssueLinks();
    };
    box.appendChild(d);
  });
}

function renderProjects(){
  const box = el("step2"); box.innerHTML = "";
  const list = game.projectsByTopic[sel.topic] || [];
  if (!sel.project && list.length) sel.project = list[0];
  list.forEach(p => {
    const d = card(p.title, `<b>KPI:</b> ${p.kpi}<br/><b>Common failure:</b> ${p.cheat}`);
    if (sel.project && p.id === sel.project.id) d.classList.add("sel");
    d.onclick = () => {
      sel.project = p;
      renderProjects();
      updatePreview();
      setProgress(50);
      disableIssueLinks();
    };
    box.appendChild(d);
  });
}

function renderSetups(){
  const box = el("step3"); box.innerHTML = "";
  game.setups.forEach(s => {
    const d = card(s.title, `${s.meta}<br/><span class="small">${s.note}</span>`);
    if (s.key === sel.setup) d.classList.add("sel");
    d.onclick = () => {
      sel.setup = s.key;
      renderSetups();
      updatePreview();
      setProgress(75);
      disableIssueLinks();
    };
    box.appendChild(d);
  });
}

function renderWindows(){
  const box = el("step4"); box.innerHTML = "";
  game.windows.forEach(w => {
    const d = card(w.title, `${w.meta}<br/><span class="small">Plan: ${w.plan[0]}</span>`);
    if (w.key === sel.window) d.classList.add("sel");
    d.onclick = () => {
      sel.window = w.key;
      renderWindows();
      updatePreview();
      setProgress(90);
      disableIssueLinks();
    };
    box.appendChild(d);
  });
}

function genID(domain){
  const stamp = new Date().toISOString().slice(2,10).replaceAll("-","");
  return `OP-${domain.toUpperCase()}-${stamp}`;
}

function disableIssueLinks(){
  el("openIssueTop").style.pointerEvents = "none";
  el("openIssueTop").style.opacity = "0.55";
  el("openIssue").style.pointerEvents = "none";
  el("openIssue").style.opacity = "0.55";
}

function enableIssueLinks(url){
  el("openIssueTop").href = url;
  el("openIssue").href = url;
  el("openIssueTop").style.pointerEvents = "auto";
  el("openIssueTop").style.opacity = "1";
  el("openIssue").style.pointerEvents = "auto";
  el("openIssue").style.opacity = "1";
}

function buildArtifact(){
  const p = sel.project;
  if (!p) return;

  const setup = game.setups.find(x=>x.key===sel.setup);
  const window = game.windows.find(x=>x.key===sel.window);
  const score = computeScore(p);

  const id = genID(p.domain);
  const witnessesText = (p.witnesses || []).map(w =>
    `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
  ).join("\n");

  const limitsText = (p.limits || []).map(x => `- ${x}`).join("\n");

  const issueBody =
`ID: ${id}
TOPIC: ${sel.topic}
DOMAIN: ${p.domain}

RANKING:
- testability_score: ${score}/100
- setup: ${setup.key}
- time_window: ${window.key}

LIMITS:
${limitsText}

CLAIM:
- ${p.claim}

COMMON FAILURE / SHORTCUT:
- ${p.cheat}

COURT TESTS (independent checks):
${witnessesText}

FALSIFIER (cheapest disproof):
- ${p.falsifier}

MINIMUM PLAN (${window.title}):
- Step 1: ${window.plan[0]}
- Step 2: ${window.plan[1] || "Tighten controls + extend time window."}
- Step 3: ${window.plan[2] || "Independent rerun (new batch/environment)."}

SETUP NOTE:
- ${setup.note}

WHO BENEFITS IF TRUE:
- ${p.buyer}

WHY IT MATTERS:
- KPI: ${p.kpi}

NOTES:
- ${p.notes}
`;

  const yaml =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
topic: "${sel.topic}"
domain: "${p.domain}"
title: "${p.title.replaceAll('"','\\"')}"
ranking:
  testability_score: ${score}
  setup: "${setup.key}"
  time_window: "${window.key}"
limits:
${(p.limits||[]).map(x => `  - "${x.replaceAll('"','\\"')}"`).join("\n")}
goal_kpi: "${p.kpi.replaceAll('"','\\"')}"
claim: "${p.claim.replaceAll('"','\\"')}"
common_failure: "${p.cheat.replaceAll('"','\\"')}"
court_tests:
${(p.witnesses||[]).map(w => `  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${String(w[3]).replaceAll('"','\\"')}"
    fail_condition: "${String(w[4]).replaceAll('"','\\"')}"`).join("\n")}
falsifier: "${p.falsifier.replaceAll('"','\\"')}"
min_plan:
  steps:
${(window.plan||[]).map((s, i) => `    - tier: "${i===0?"cheap":i===1?"mid":"expensive"}"
      step: "${s.replaceAll('"','\\"')}"`).join("\n")}
beneficiary: "${p.buyer.replaceAll('"','\\"')}"
notes: "${p.notes.replaceAll('"','\\"')}"
`;

  el("outIssue").textContent = issueBody;
  el("outYaml").textContent = yaml;

  const title = `Opportunity Pack: ${p.domain.toUpperCase()} — ${p.title}`;
  const url = `${REPO_NEW_ISSUE_URL}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(issueBody)}`;
  enableIssueLinks(url);

  setProgress(100);
}

async function copyText(text){
  try { await navigator.clipboard.writeText(text); }
  catch(e){ alert("Copy failed. Select text manually and copy."); }
}

el("generate").addEventListener("click", buildArtifact);
el("copyIssue").addEventListener("click", () => copyText(el("outIssue").textContent));
el("copyYaml").addEventListener("click", () => copyText(el("outYaml").textContent));

disableIssueLinks();
setProgress(0);
renderTopics();
renderProjects();
renderSetups();
renderWindows();
updatePreview();
</script>
</body>
</html>
