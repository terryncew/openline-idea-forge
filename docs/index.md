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
.wrap{max-width:980px;margin:0 auto;padding:18px 14px 48px;}
.hero{
  border:1px solid var(--line); border-radius:18px; padding:18px;
  background: linear-gradient(135deg, rgba(110,168,255,.18), rgba(124,240,210,.10));
  box-shadow: var(--shadow);
}
h1{margin:0 0 6px;font-size:34px;letter-spacing:.2px}
.lead{margin:0;color:var(--muted);line-height:1.45}
.row{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}
.pill{display:inline-block;padding:6px 10px;border:1px solid var(--line);border-radius:999px;font-size:12px;color:var(--muted);background:rgba(255,255,255,.04)}
.grid{display:grid;grid-template-columns:1fr;gap:12px;margin-top:14px}
@media(min-width:920px){.grid{grid-template-columns:1.1fr .9fr}}
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
.hidden{display:none}
.cards{display:grid;grid-template-columns:1fr;gap:10px;margin-top:10px}
@media(min-width:920px){.cards{grid-template-columns:1fr 1fr}}
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
</style>
</head>
<body>
<div class="wrap">

  <div class="hero">
    <h1>Idea Forge</h1>
    <p class="lead">Choose-your-own-adventure for real, testable problems. No blank boxes. Pick options → get a finished Opportunity Pack + one-click GitHub Issue.</p>
    <div class="row">
      <span class="pill">No typing required</span>
      <span class="pill">Prefilled cheat path + falsifier</span>
      <span class="pill">Ends with a real artifact</span>
      <span class="pill">Not spooky</span>
    </div>
  </div>

  <div class="grid">
    <div class="card">
      <div class="kpi">
        <div class="stageTitle" id="stageTitle">Step 1/4 · Pick an Interest</div>
        <div class="small" id="xp">Progress: 0%</div>
      </div>
      <div class="bar"><div id="barFill"></div></div>

      <!-- Step 1: Interest -->
      <div id="step1" class="cards"></div>

      <!-- Step 2: Mission -->
      <div id="step2wrap" class="hidden">
        <hr/>
        <div class="stageTitle">Step 2/4 · Pick a Mission</div>
        <div class="tip">These are solvable today. Tap one.</div>
        <div id="step2" class="cards"></div>
      </div>

      <!-- Step 3: Proof Style -->
      <div id="step3wrap" class="hidden">
        <hr/>
        <div class="stageTitle">Step 3/4 · Pick Your Proof Style</div>
        <div class="tip"><span class="badge warn">Shortcut warning:</span> stricter proof = slower, but fewer fake wins.</div>
        <div id="step3" class="cards"></div>
      </div>

      <!-- Step 4: Time/Budget -->
      <div id="step4wrap" class="hidden">
        <hr/>
        <div class="stageTitle">Step 4/4 · Pick Your Weekend</div>
        <div class="tip">This sets the minimum validation plan. Tap one.</div>
        <div id="step4" class="cards"></div>

        <div class="btnrow">
          <button class="primary" id="generate">Generate Artifact →</button>
          <a class="btn" id="openIssueTop" target="_blank" rel="noopener">Open GitHub Issue</a>
        </div>
        <p class="small">If the Issue button is disabled, hit Generate once.</p>
      </div>
    </div>

    <div class="card">
      <h2>Your Finished Artifact</h2>
      <p class="tip">When you hit Generate, you get a Court-ready Opportunity Pack + YAML. Screenshot this panel to share.</p>

      <div class="btnrow">
        <button id="copyIssue">Copy Issue Body</button>
        <button id="copyYaml">Copy YAML</button>
        <a class="btn primary" id="openIssue" target="_blank" rel="noopener">Open GitHub Issue</a>
      </div>

      <hr/>

      <div class="small">Issue body</div>
      <div class="mini" id="outIssue">(pick options on the left → generate)</div>

      <div style="height:10px"></div>

      <div class="small">YAML</div>
      <div class="mini" id="outYaml">(pick options on the left → generate)</div>

      <p class="small">Viral move: “I picked a mission, got a falsifier, and shipped a real test plan in 60 seconds.”</p>
    </div>
  </div>
</div>

<script>
const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

const data = {
  interests: [
    { key:"agents", name:"Agents", meta:"Build stuff with Claude/ChatGPT. Stop loop-burn. Ship faster." },
    { key:"climate", name:"Climate", meta:"CO₂, power, efficiency. Real measurements. No vibes." },
    { key:"energy", name:"Energy", meta:"Batteries + storage. Parasitics matter. Replication matters." },
    { key:"microchips", name:"Microchips", meta:"Yield, scrap, auditability. No accounting hacks." },
    { key:"health", name:"Health", meta:"Synbio/enzyme hits that survive controls + orthogonal assays." }
  ],
  missions: {
    agents: [
      {
        id:"AG-LOOPKILL",
        title:"Kill zombie loops without killing winners",
        domain:"agents",
        kpi:"Reduce cost-per-solved without false stops",
        claim:"A loop governor reduces repeated-action burn by ≥30% on SWE-style tasks while keeping false stops ≤2%.",
        cheat:"It ‘wins’ by getting stricter in a way that just kills hard-but-solvable tasks (quietly lowering denominator).",
        falsifier:"Fails if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
        buyer:"Teams shipping production agents (budget + reliability).",
        notes:"Lock the definition of solved. Use a held-out task mix. Track cost-per-solved + false stops.",
        witnesses:[
          ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
          ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded in window","Repetition exceeds bound (zombie loop)"],
          ["W3_TESTS","stability","hard","Regression/tests pass on completion","Tests fail or regressions spike"],
          ["W4_COST","cost_feasibility","soft","Cost-per-solved within cap vs baseline","Cost-per-solved worsens beyond cap"]
        ]
      },
      {
        id:"AG-AUTODOCKET",
        title:"A ‘Court’ eval that predicts incidents better than one leaderboard",
        domain:"agents",
        kpi:"Predict production failures better than single benchmark score",
        claim:"A 3-witness eval (replay + cost + stability) predicts incident rate better than a single benchmark score on a held-out workload slice.",
        cheat:"It ‘wins’ by picking witnesses that correlate on one dataset but don’t generalize.",
        falsifier:"Fails if the advantage disappears on a different repo mix / toolset / time window.",
        buyer:"Agent platforms + internal eval teams.",
        notes:"Two task mixes, one held out. Report correlation + confidence intervals.",
        witnesses:[
          ["W1_INDEP","origin","hard","Holds on held-out workload slice","Breaks on held-out slice"],
          ["W2_REPLAY","replay","hard","Deterministic rerun matches outcome","Not reproducible"],
          ["W3_COST","cost_feasibility","soft","Cost stays bounded vs baseline","Cost explodes for marginal gain"]
        ]
      }
    ],
    climate: [
      {
        id:"CO2-HER",
        title:"Stop CO₂ systems from cheating into hydrogen",
        domain:"co2",
        kpi:"High FE to CO + bounded HER + 10h stability",
        claim:"A CO₂RR setup holds FE(CO) ≥90% at target current while keeping HER below bound for ≥10 hours time-on-stream.",
        cheat:"It ‘wins’ via bad accounting (carbon balance doesn’t close) or a short peak that collapses after minutes.",
        falsifier:"Fails if carbon balance doesn’t close OR FE collapses before 10 hours OR HER dominates current.",
        buyer:"CO₂ electrolysis startups + industrial R&D.",
        notes:"Carbon balance is non-negotiable. Time-on-stream matters more than peak FE.",
        witnesses:[
          ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
          ["W2_HER","cheat_suppression","hard","HER bounded at target current","HER dominates current"],
          ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay/deactivation"],
          ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation/high replacement cost"]
        ]
      }
    ],
    energy: [
      {
        id:"BAT-SEI",
        title:"SEI win that survives parasitics (not a 10-cycle mirage)",
        domain:"batteries",
        kpi:"CE + impedance stability over 100 cycles",
        claim:"An additive improves CE by ≥1% and reduces impedance growth while keeping gas evolution below threshold over ≥100 cycles.",
        cheat:"Looks great early; parasitics (gas/impedance) explode later; or effect won’t replicate across batches.",
        falsifier:"Fails if replicate loses the effect OR parasitic proxy rises beyond bound OR CE gain disappears by cycle 100.",
        buyer:"Battery startups + electrolyte suppliers + OEM labs.",
        notes:"Track gas/EIS, not just capacity. Replicate on a second batch.",
        witnesses:[
          ["W1_ORIGIN","origin","hard","Effect replicates on separate build/batch","Effect vanishes on replicate"],
          ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS bounded","Parasitics dominate"],
          ["W3_STABILITY","stability","hard","CE+EIS within bounds ≥100 cycles","CE collapses/EIS runaway"],
          ["W4_COST","cost_feasibility","soft","Feasible + safe","Prohibitive or unsafe"]
        ]
      }
    ],
    microchips: [
      {
        id:"CHIP-YIELD",
        title:"Improve yield without hiding scrap",
        domain:"chips",
        kpi:"Yield up with audited defect taxonomy",
        claim:"A process-change recommender improves yield by ≥X% while keeping defect accounting consistent (no reclassification).",
        cheat:"It ‘wins’ by relabeling defects or shifting scrap categories (accounting hack).",
        falsifier:"Fails if yield gain disappears under a fixed taxonomy + blind audit.",
        buyer:"Foundry ops / packaging / test teams.",
        notes:"Lock defect taxonomy. Require blind audit. Track yield + rework + scrap.",
        witnesses:[
          ["W1_AUDIT","origin","hard","Blind audit confirms taxonomy unchanged","Taxonomy drift / relabeling detected"],
          ["W2_STABILITY","stability","hard","Gain holds over multiple lots","One-lot spike only"],
          ["W3_COST","cost_feasibility","soft","Cost per good die improves","Cost balloons with no net gain"]
        ]
      }
    ],
    health: [
      {
        id:"BIO-CONTROLS",
        title:"Enzyme hit that survives controls + orthogonal assay",
        domain:"synbio",
        kpi:"Real activity (not artifact) + stability",
        claim:"A candidate shows activity improvement ≥Y% and survives contamination controls + an orthogonal assay confirmation.",
        cheat:"Fluorescence/assay artifact or contamination produces a fake hit.",
        falsifier:"Fails if signal appears in blanks/controls OR orthogonal assay contradicts the first assay.",
        buyer:"Industrial biotech + assay-heavy R&D teams.",
        notes:"Two assays or it didn’t happen. Controls are the product.",
        witnesses:[
          ["W1_CONTROLS","origin","hard","Controls clean","Signal in blanks/controls"],
          ["W2_ORTHO","cheat_suppression","hard","Orthogonal assay confirms","Second assay contradicts"],
          ["W3_HALFLIFE","stability","hard","Half-life meets bound","Rapid deactivation"],
          ["W4_YIELD","cost_feasibility","soft","Yield feasible","Unscalable yield"]
        ]
      }
    ]
  },
  proofStyles: [
    { key:"fast", title:"Fast & scrappy", meta:"Kill bad ideas fast. Accept some false negatives.", escape:["Independent rerun","2x window","Tighter stop-rule"] },
    { key:"balanced", title:"Balanced", meta:"Good default. Hard to fake, not too slow.", escape:["Independent rerun","Longer window","Stricter controls"] },
    { key:"strict", title:"Strict court", meta:"Hard to pass. Best for public claims.", escape:["Independent rerun (different setup)","Long stability window","Orthogonal measurement","External replication if possible"] }
  ],
  weekends: [
    { key:"1h", title:"1 hour", meta:"Just enough to falsify the cheat path.", plan:[
      "Run the smallest test that hits Origin + Cheat suppression.",
      "If it fails, stop. If it survives, queue a longer run."
    ]},
    { key:"1d", title:"One day", meta:"Cheap+mid. Enough to learn if it’s worth a week.", plan:[
      "Run cheap test + tighten controls.",
      "Extend window. Look for decay / parasitics.",
      "If it survives, do independent rerun."
    ]},
    { key:"weekend", title:"Weekend", meta:"Cheap+mid+one independent rerun.", plan:[
      "Cheap test (origin + cheat suppression).",
      "Mid test (longer window + stricter controls).",
      "Independent rerun (new batch/environment)."
    ]}
  ]
};

const el = id => document.getElementById(id);
let sel = { interest:null, mission:null, proof:null, weekend:null };

function setProgress(p){ el("barFill").style.width = `${p}%`; el("xp").textContent = `Progress: ${p}%`; }

function card(title, meta){
  const d = document.createElement("div");
  d.className = "choice";
  d.innerHTML = `<p class="ctitle">${title}</p><p class="cmeta">${meta}</p>`;
  return d;
}

function renderStep1(){
  const box = el("step1"); box.innerHTML = "";
  data.interests.forEach((i, idx) => {
    const d = card(i.name, i.meta);
    d.onclick = () => {
      sel.interest = i.key; sel.mission=null; sel.proof=null; sel.weekend=null;
      document.querySelectorAll("#step1 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      el("step2wrap").classList.remove("hidden");
      renderStep2();
      el("step3wrap").classList.add("hidden");
      el("step4wrap").classList.add("hidden");
      setProgress(25);
    };
    box.appendChild(d);
    if (idx===0 && !sel.interest){ d.click(); }
  });
}

function renderStep2(){
  const box = el("step2"); box.innerHTML = "";
  (data.missions[sel.interest] || []).forEach((m, idx) => {
    const d = card(m.title, `<b>KPI:</b> ${m.kpi}<br/><b>Solvable today:</b> yes`);
    d.onclick = () => {
      sel.mission = m; sel.proof=null; sel.weekend=null;
      document.querySelectorAll("#step2 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      el("step3wrap").classList.remove("hidden");
      renderStep3();
      el("step4wrap").classList.add("hidden");
      setProgress(50);
    };
    box.appendChild(d);
    if (idx===0 && !sel.mission){ d.click(); }
  });
}

function renderStep3(){
  const box = el("step3"); box.innerHTML = "";
  data.proofStyles.forEach((p, idx) => {
    const d = card(p.title, p.meta);
    d.onclick = () => {
      sel.proof = p; sel.weekend=null;
      document.querySelectorAll("#step3 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      el("step4wrap").classList.remove("hidden");
      renderStep4();
      setProgress(75);
    };
    box.appendChild(d);
    if (idx===1 && !sel.proof){ d.click(); } // default balanced
  });
}

function renderStep4(){
  const box = el("step4"); box.innerHTML = "";
  data.weekends.forEach((w, idx) => {
    const d = card(w.title, `${w.meta}<br/><span class="small">Plan: ${w.plan[0]}</span>`);
    d.onclick = () => {
      sel.weekend = w;
      document.querySelectorAll("#step4 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      setProgress(90);
    };
    box.appendChild(d);
    if (idx===2 && !sel.weekend){ d.click(); } // default weekend
  });
  el("openIssueTop").style.pointerEvents = "none";
  el("openIssueTop").style.opacity = "0.55";
}

function genID(domain){
  const stamp = new Date().toISOString().slice(2,10).replaceAll("-","");
  return `OP-${domain.toUpperCase()}-${stamp}`;
}

function buildArtifact(){
  if (!sel.mission || !sel.proof || !sel.weekend) return;

  const m = sel.mission;
  const proof = sel.proof;
  const weekend = sel.weekend;

  const id = genID(m.domain);
  const witnessesText = (m.witnesses || []).map(w =>
    `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
  ).join("\n");

  const issueBody =
`ID: ${id}
DOMAIN: ${m.domain}

CLAIM:
- ${m.claim}

CHEAT_PATH:
- ${m.cheat}

COURT_TESTS (independent witnesses):
${witnessesText}

FALSIFIER:
- ${m.falsifier}

ESCAPE_HATCH:
- If performance spike is huge but one witness fails, require:
  ${proof.escape.map(x => `- ${x}`).join("\n  ")}

MIN_VALIDATION (${weekend.title}):
- Step 1 (cheap): ${weekend.plan[0]}
- Step 2 (mid): ${weekend.plan[1] || "Tighten controls + extend window."}
- Step 3 (expensive): ${weekend.plan[2] || "Independent rerun (new batch/environment)."}

BUYER:
- ${m.buyer}

WHY THEY CARE:
- KPI: ${m.kpi}

NOTES:
- ${m.notes}
`;

  const yaml =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
interest: "${sel.interest}"
domain: "${m.domain}"
title: "${m.title.replaceAll('"','\\"')}"
goal_kpi: "${m.kpi.replaceAll('"','\\"')}"
claim: "${m.claim.replaceAll('"','\\"')}"
cheat_path: "${m.cheat.replaceAll('"','\\"')}"
court_tests:
${(m.witnesses||[]).map(w => `  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${String(w[3]).replaceAll('"','\\"')}"
    fail_condition: "${String(w[4]).replaceAll('"','\\"')}"`).join("\n")}
falsifier: "${m.falsifier.replaceAll('"','\\"')}"
escape_hatch:
  style: "${proof.key}"
  required_escalations:
${proof.escape.map(x => `    - "${x.replaceAll('"','\\"')}"`).join("\n")}
min_validation:
  weekend: "${weekend.key}"
  steps:
${weekend.plan.map((s, i) => `    - tier: "${i===0?"cheap":i===1?"mid":"expensive"}"
      step: "${s.replaceAll('"','\\"')}"`).join("\n")}
buyer: "${m.buyer.replaceAll('"','\\"')}"
notes: "${m.notes.replaceAll('"','\\"')}"
`;

  el("outIssue").textContent = issueBody;
  el("outYaml").textContent = yaml;

  const title = `Opportunity Pack: ${m.domain.toUpperCase()} — ${m.title}`;
  const url = `${REPO_NEW_ISSUE_URL}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(issueBody)}`;

  el("openIssue").href = url;
  el("openIssueTop").href = url;
  el("openIssueTop").style.pointerEvents = "auto";
  el("openIssueTop").style.opacity = "1";

  setProgress(100);
  el("stageTitle").textContent = "Complete · Artifact Ready";
}

async function copyText(text){
  try { await navigator.clipboard.writeText(text); }
  catch(e){ alert("Copy failed. Select text manually and copy."); }
}

el("generate").addEventListener("click", buildArtifact);
el("copyIssue").addEventListener("click", () => copyText(el("outIssue").textContent));
el("copyYaml").addEventListener("click", () => copyText(el("outYaml").textContent));

renderStep1();
setProgress(0);
</script>
</body>
</html>
