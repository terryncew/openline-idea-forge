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
label{display:block;font-size:12px;color:var(--muted);margin:10px 0 6px}
select,input,textarea{
  width:100%;border-radius:12px;border:1px solid var(--line);
  background:rgba(255,255,255,.04);color:var(--text);
  padding:10px;font-size:14px;
}
textarea{min-height:96px;resize:vertical}
button,a.btn{
  appearance:none;border-radius:12px;border:1px solid var(--line);
  background:rgba(255,255,255,.04);color:var(--text);
  padding:10px 12px;font-size:14px;cursor:pointer;text-decoration:none;display:inline-block;
}
button.primary{border-color:rgba(110,168,255,.40);background:linear-gradient(135deg, rgba(110,168,255,.34), rgba(124,240,210,.16));}
.btnrow{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
.small{font-size:12px;color:var(--muted);line-height:1.35}
.bar{height:10px;border-radius:999px;background:rgba(255,255,255,.08);overflow:hidden;border:1px solid var(--line)}
.bar > div{height:100%;width:0%;background:linear-gradient(90deg, var(--accent), var(--mint))}
.kpi{display:flex;justify-content:space-between;gap:10px;align-items:center;margin-top:10px}
.xp{font-size:12px;color:var(--muted)}
.stageTitle{font-weight:900;letter-spacing:.2px}
.tip{color:var(--muted);font-size:13px;line-height:1.4;margin-top:8px}
.mini{
  font-family:var(--mono);font-size:12.5px;white-space:pre-wrap;overflow-wrap:anywhere;
  border:1px solid var(--line);border-radius:16px;background:#0b0f1a;color:#d8e2ff;padding:12px;
}
@media (prefers-color-scheme: light){.mini{background:#0b1020;color:#e9eef7}}
.badge{display:inline-block;padding:4px 8px;border-radius:999px;border:1px solid var(--line);font-size:12px;color:var(--muted)}
.good{color:var(--good);border-color:rgba(124,255,155,.45)}
.warn{color:var(--warn);border-color:rgba(255,209,102,.55)}
.bad{color:var(--bad);border-color:rgba(255,107,107,.55)}
hr{border:none;border-top:1px solid var(--line);margin:14px 0}
.hidden{display:none}
.cards{display:grid;grid-template-columns:1fr;gap:10px;margin-top:10px}
@media(min-width:920px){.cards{grid-template-columns:1fr 1fr}}
.mission{
  border:1px solid var(--line); border-radius:14px; padding:12px; background:rgba(255,255,255,.03);
  cursor:pointer;
}
.mission:hover{ border-color: rgba(110,168,255,.45); }
.mtitle{font-weight:900;margin:0 0 6px}
.mmeta{margin:0;color:var(--muted);font-size:13px;line-height:1.35}
.sel{ outline: 2px solid rgba(110,168,255,.45); }
</style>
</head>
<body>
<div class="wrap">

  <div class="hero">
    <h1>Idea Forge</h1>
    <p class="lead">Pick an interest. Choose a solvable mission. Get a real Opportunity Pack + one-click GitHub Issue. No typing required.</p>
    <div class="row">
      <span class="pill">Guided</span>
      <span class="pill">Not spooky</span>
      <span class="pill">Ends with a real artifact</span>
      <span class="pill">Shareable</span>
    </div>
  </div>

  <div class="grid">
    <div class="card">
      <div class="kpi">
        <div class="stageTitle" id="stageTitle">Step 1/2 · Pick a Mission</div>
        <div class="xp" id="xp">XP: 0</div>
      </div>
      <div class="bar"><div id="barFill"></div></div>

      <label>Interest</label>
      <select id="interest"></select>

      <div class="tip"><b>Choose a mission.</b> These are designed to be solvable with today’s tools (and to fail loudly if they’re fake).</div>
      <div class="cards" id="missions"></div>

      <div class="btnrow">
        <button class="primary" id="generate">Generate Artifact →</button>
        <button id="toggleEdit">Optional: Edit Mode</button>
      </div>

      <div id="editBox" class="hidden">
        <hr/>
        <div class="tip"><b>Edit Mode</b> (optional). If you’re lazy, ignore this. The defaults are good.</div>

        <label>Domain</label>
        <select id="domain">
          <option value="agents">Agents</option>
          <option value="batteries">Batteries</option>
          <option value="co2">CO₂ Electrolysis</option>
          <option value="synbio">SynBio</option>
          <option value="chips">Microchips</option>
        </select>

        <label>Goal (KPI)</label>
        <input id="goal"/>

        <label>Claim</label>
        <textarea id="claim"></textarea>

        <label>Cheat path</label>
        <textarea id="cheatPath"></textarea>

        <label>Falsifier</label>
        <textarea id="falsifier"></textarea>

        <label>Buyer</label>
        <input id="buyer"/>

        <label>Notes</label>
        <textarea id="notes"></textarea>
      </div>
    </div>

    <div class="card">
      <h2>Artifact (what you leave with)</h2>
      <p class="tip">This is the “holy shit, this is real” moment: a Court-ready issue body + YAML pack.</p>

      <div class="btnrow">
        <button id="copyIssue">Copy Issue Body</button>
        <button id="copyYaml">Copy YAML</button>
        <a class="btn primary" id="openIssue" target="_blank" rel="noopener">Open GitHub Issue</a>
      </div>

      <hr/>

      <div class="small">Issue body</div>
      <div class="mini" id="outIssue">(pick a mission → generate)</div>

      <div style="height:10px"></div>

      <div class="small">YAML</div>
      <div class="mini" id="outYaml">(pick a mission → generate)</div>

      <p class="small">Viral move: screenshot this artifact panel and post it as “I just generated a testable idea pack in 60 seconds.”</p>
    </div>
  </div>
</div>

<script>
const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

const catalog = [
  // AGENTS
  {
    interest:"Agents",
    id:"AG-LOOPKILL",
    domain:"agents",
    title:"Kill Zombie Loops without killing winners",
    kpi:"Reduce cost-per-solved without false-stops",
    claim:"A loop governor reduces repeated-action burn by ≥30% on SWE-style tasks while keeping false stops ≤2%.",
    cheat:"It ‘wins’ by getting stricter in a way that just kills hard-but-solvable tasks (quietly lowering denominator).",
    falsifier:"Fails if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
    buyer:"Any team shipping production agents (cost + incident risk).",
    notes:"Use held-out tasks. Lock solved rubric. Track cost-per-solved, loop rate, and false stops.",
    witnesses:[
      ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
      ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded in window","Repetition exceeds bound (zombie loop)"],
      ["W3_TESTS","stability","hard","Regression/tests pass on completion","Tests fail or regressions spike"],
      ["W4_COST","cost_feasibility","soft","Cost-per-solved improves or stays within cap","Cost-per-solved worsens beyond cap"]
    ]
  },
  {
    interest:"Agents",
    id:"AG-EVALCOURT",
    domain:"agents",
    title:"Court-style eval that predicts incidents better than one leaderboard",
    kpi:"Increase correlation with real failures",
    claim:"A 3-witness eval (replay + cost + stability) predicts production incident rate better than a single benchmark score.",
    cheat:"It ‘wins’ by picking witnesses that correlate on one dataset but don’t generalize.",
    falsifier:"Fails if correlation advantage disappears on a new workload slice (different repos/tools).",
    buyer:"Labs and platforms shipping agent products; internal eval teams.",
    notes:"Run on two different task mixes. Hold out one mix completely.",
    witnesses:[
      ["W1_INDEP","origin","hard","Holds on held-out workload slice","Breaks on held-out slice"],
      ["W2_REPLAY","replay","hard","Deterministic rerun matches outcome","Not reproducible"],
      ["W3_COST","cost_feasibility","soft","Cost-per-solved improves or stable","Cost balloons with no reliability gain"]
    ]
  },

  // CLIMATE / CO2
  {
    interest:"Climate",
    id:"CO2-HER",
    domain:"co2",
    title:"Stop the CO₂ system from cheating into hydrogen",
    kpi:"High FE to CO with bounded HER + stability",
    claim:"A CO₂RR setup holds FE(CO) ≥90% at target current while keeping HER below the bound for ≥10 hours time-on-stream.",
    cheat:"It ‘wins’ via bad accounting (carbon balance doesn’t close) or a short peak that collapses after minutes.",
    falsifier:"Fails if carbon balance doesn’t close OR FE collapses before 10 hours OR HER dominates current.",
    buyer:"CO₂ electrolysis startups and industrial R&D.",
    notes:"Carbon balance is non-negotiable. Time-on-stream matters more than peak FE.",
    witnesses:[
      ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
      ["W2_HER","cheat_suppression","hard","HER bounded at target current","HER dominates current"],
      ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay/deactivation"],
      ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation/high replacement cost"]
    ]
  },

  // BATTERIES
  {
    interest:"Energy",
    id:"BAT-SEI",
    domain:"batteries",
    title:"SEI win that survives parasitics (not a 10-cycle mirage)",
    kpi:"CE + impedance stability",
    claim:"An additive improves CE by ≥1% and reduces impedance growth while keeping gas evolution below threshold over ≥100 cycles.",
    cheat:"It looks great early but parasitics (gas/impedance) explode later; or it’s impurity-sensitive and won’t replicate.",
    falsifier:"Fails if independent replicate loses the effect OR parasitic proxy rises beyond bound OR CE gain disappears by cycle 100.",
    buyer:"Battery startups, electrolyte suppliers, OEM labs.",
    notes:"Track gas/EIS, not just capacity. Replicate on a second batch.",
    witnesses:[
      ["W1_ORIGIN","origin","hard","Effect replicates on separate build/batch","Effect vanishes on replicate"],
      ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS bounded","Parasitics dominate"],
      ["W3_STABILITY","stability","hard","CE+EIS within bounds ≥100 cycles","CE collapses/EIS runaway"],
      ["W4_COST","cost_feasibility","soft","Feasible + safe","Prohibitive or unsafe"]
    ]
  },

  // MICROCHIPS (not chemistry, still court)
  {
    interest:"Microchips",
    id:"CHIP-YIELD",
    domain:"chips",
    title:"AI that improves yield without hiding the scrap",
    kpi:"Yield up, scrap accounting honest",
    claim:"A process-change recommender improves yield by ≥X% while keeping defect accounting consistent (no hidden reclassification).",
    cheat:"It ‘wins’ by relabeling defects or shifting scrap categories (accounting hack).",
    falsifier:"Fails if yield gain disappears when defects are audited with a fixed taxonomy and blind review.",
    buyer:"Foundry ops / advanced packaging / test teams.",
    notes:"Lock defect taxonomy. Require blind audit. Track yield + rework + scrap.",
    witnesses:[
      ["W1_AUDIT","origin","hard","Blind audit confirms defect taxonomy unchanged","Taxonomy drift / relabeling detected"],
      ["W2_STABILITY","stability","hard","Gain holds over multiple lots","One-lot spike only"],
      ["W3_COST","cost_feasibility","soft","Cost per good die improves","Cost balloons with no net gain"]
    ]
  },

  // SYNBIO
  {
    interest:"Health",
    id:"BIO-CONTROLS",
    domain:"synbio",
    title:"Enzyme hit that survives controls + orthogonal assay",
    kpi:"Real activity, not assay artifact",
    claim:"A candidate shows activity improvement ≥Y% and survives contamination controls + an orthogonal assay confirmation.",
    cheat:"Fluorescence/assay artifact or contamination produces a fake hit.",
    falsifier:"Fails if signal appears in blanks/controls OR the orthogonal assay contradicts the first assay.",
    buyer:"Industrial biotech, assay-heavy R&D teams.",
    notes:"Two assays or it didn’t happen. Controls are the product.",
    witnesses:[
      ["W1_CONTROLS","origin","hard","Controls clean","Signal in blanks/controls"],
      ["W2_ORTHO","cheat_suppression","hard","Orthogonal assay confirms","Second assay contradicts"],
      ["W3_HALFLIFE","stability","hard","Half-life meets bound","Rapid deactivation"],
      ["W4_YIELD","cost_feasibility","soft","Yield feasible","Unscalable yield"]
    ]
  }
];

const interests = [...new Set(catalog.map(x => x.interest))];

const el = id => document.getElementById(id);
let selected = null;

function setXP(v){ el("xp").textContent = `XP: ${v}`; el("barFill").style.width = `${v}%`; }

function renderInterests(){
  el("interest").innerHTML = interests.map(x => `<option>${x}</option>`).join("");
}

function renderMissions(){
  const pick = el("interest").value;
  const items = catalog.filter(x => x.interest === pick);
  const box = el("missions");
  box.innerHTML = "";
  items.forEach((m, idx) => {
    const div = document.createElement("div");
    div.className = "mission";
    div.innerHTML = `<p class="mtitle">${m.title}</p>
      <p class="mmeta"><b>Solvable today:</b> yes · <b>KPI:</b> ${m.kpi}</p>`;
    div.onclick = () => selectMission(m, div);
    box.appendChild(div);
    if (idx === 0 && !selected) selectMission(m, div);
  });
}

function selectMission(m, div){
  selected = m;
  document.querySelectorAll(".mission").forEach(x => x.classList.remove("sel"));
  div.classList.add("sel");
  setXP(50);
  // prefill edit mode fields
  el("domain").value = m.domain === "chips" ? "chips" : m.domain;
  el("goal").value = m.kpi;
  el("claim").value = m.claim;
  el("cheatPath").value = m.cheat;
  el("falsifier").value = m.falsifier;
  el("buyer").value = m.buyer;
  el("notes").value = m.notes;
}

function genID(domain){
  const stamp = new Date().toISOString().slice(2,10).replaceAll("-","");
  return `OP-${domain.toUpperCase()}-${stamp}`;
}

function buildArtifact(fromEdit=false){
  const m = selected;
  if (!m) return;

  const domain = fromEdit ? (el("domain").value || m.domain) : m.domain;
  const kpi = fromEdit ? (el("goal").value || m.kpi) : m.kpi;
  const claim = fromEdit ? (el("claim").value || m.claim) : m.claim;
  const cheat = fromEdit ? (el("cheatPath").value || m.cheat) : m.cheat;
  const falsifier = fromEdit ? (el("falsifier").value || m.falsifier) : m.falsifier;
  const buyer = fromEdit ? (el("buyer").value || m.buyer) : m.buyer;
  const notes = fromEdit ? (el("notes").value || m.notes) : m.notes;

  const id = genID(domain);

  const witnessesText = (m.witnesses || []).map(w =>
    `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
  ).join("\n");

  const issueBody =
`ID: ${id}
DOMAIN: ${domain}

CLAIM:
- ${claim}

CHEAT_PATH:
- ${cheat}

COURT_TESTS (independent witnesses):
${witnessesText}

FALSIFIER:
- ${falsifier}

ESCAPE_HATCH:
- If performance spike is huge but one witness fails, require:
  - Independent rerun (fresh environment/batch)
  - Longer window (2x)
  - Stricter measurement/control

MIN_VALIDATION:
- Step 1 (cheap): smallest test that hits Origin + Cheat suppression.
- Step 2 (mid): extend window; tighten controls.
- Step 3 (expensive): independent rerun (new batch / new environment).

BUYER:
- ${buyer}

WHY THEY CARE:
- KPI: ${kpi}

NOTES:
- ${notes}
`;

  const yaml =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
domain: "${domain}"
goal_kpi: "${kpi}"
claim: "${String(claim).replaceAll('"','\\"')}"
cheat_path: "${String(cheat).replaceAll('"','\\"')}"
court_tests:
${(m.witnesses||[]).map(w => `  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${String(w[3]).replaceAll('"','\\"')}"
    fail_condition: "${String(w[4]).replaceAll('"','\\"')}"`).join("\n")}
falsifier: "${String(falsifier).replaceAll('"','\\"')}"
escape_hatch:
  trigger: "major_spike_and_one_witness_failed"
  required_escalations:
    - "independent rerun"
    - "longer window"
    - "stricter controls"
buyer: "${String(buyer).replaceAll('"','\\"')}"
notes: "${String(notes).replaceAll('"','\\"')}"
`;

  el("outIssue").textContent = issueBody;
  el("outYaml").textContent = yaml;

  const title = `Opportunity Pack: ${domain.toUpperCase()} — ${m.title}`;
  el("openIssue").href = `${REPO_NEW_ISSUE_URL}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(issueBody)}`;
  setXP(100);
  el("stageTitle").textContent = "Step 2/2 · Artifact Ready";
}

async function copyText(text){
  try { await navigator.clipboard.writeText(text); }
  catch(e){ alert("Copy failed. Select text manually and copy."); }
}

el("toggleEdit").addEventListener("click", () => el("editBox").classList.toggle("hidden"));
el("interest").addEventListener("change", () => { selected=null; setXP(0); renderMissions(); });
el("generate").addEventListener("click", () => buildArtifact(!el("editBox").classList.contains("hidden")));
el("copyIssue").addEventListener("click", () => copyText(el("outIssue").textContent));
el("copyYaml").addEventListener("click", () => copyText(el("outYaml").textContent));

renderInterests();
renderMissions();
setXP(0);
</script>
</body>
</html>
