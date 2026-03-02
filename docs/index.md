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
</style>
</head>
<body>
<div class="wrap">

  <div class="hero">
    <h1>Idea Forge</h1>
    <p class="lead">A mini-game that turns “cool idea” into a Court-ready Opportunity Pack. You’ll finish with a real artifact you can submit.</p>
    <div class="row">
      <span class="pill">Level 1: Claim</span>
      <span class="pill">Level 2: Cheat Path (Boss)</span>
      <span class="pill">Level 3: Court</span>
      <span class="pill">Level 4: Falsifier</span>
      <span class="pill">Reward: GitHub Issue + YAML</span>
    </div>
  </div>

  <div class="grid">
    <div class="card">
      <div class="kpi">
        <div class="stageTitle" id="stageTitle">Level 1/4 · The Claim</div>
        <div class="xp" id="xp">XP: 0</div>
      </div>
      <div class="bar" aria-label="progress"><div id="barFill"></div></div>

      <!-- Stage 1 -->
      <div id="stage1">
        <p class="tip"><b>Rule:</b> One sentence. Measurable. If it can’t be measured, it’s poetry (poetry is great, different lane).</p>

        <label>Domain</label>
        <select id="domain">
          <option value="agents">Agents</option>
          <option value="batteries">Batteries</option>
          <option value="co2">CO₂ Electrolysis</option>
          <option value="synbio">SynBio</option>
        </select>

        <label>Goal (KPI)</label>
        <select id="goal"></select>

        <label>Write your claim (one sentence)</label>
        <input id="claim" placeholder="Example: Cut loop burn by 30% on SWE-style tasks without increasing false kills." />

        <div class="btnrow">
          <button class="primary" id="next1">Next →</button>
        </div>
        <p class="small">Pro tip: keep it boring. Boring claims are easier to prove.</p>
      </div>

      <!-- Stage 2 -->
      <div id="stage2" class="hidden">
        <p class="tip"><span class="badge warn">Boss fight</span> The system will try to “win” without doing the real task. Name the easiest lie first.</p>

        <label>Cheat risk (what usually fakes wins here)</label>
        <select id="cheat"></select>

        <label>CHEAT_PATH (write the easiest way your claim could look true while being fake)</label>
        <textarea id="cheatPath" placeholder="Example: It ‘solves’ by repeating low-entropy actions, or by redefining ‘done’ so failures look like success."></textarea>

        <div class="btnrow">
          <button id="back2">← Back</button>
          <button class="primary" id="next2">Next →</button>
        </div>
        <p class="small">If you can’t name the cheat path, you don’t own the claim yet.</p>
      </div>

      <!-- Stage 3 -->
      <div id="stage3" class="hidden">
        <p class="tip">Now we build the Court: 3–4 independent witnesses. Different angles. Different failure modes.</p>

        <label>Proof mode</label>
        <select id="proof">
          <option value="cheap">Cheap proof (fast kill)</option>
          <option value="balanced" selected>Balanced</option>
          <option value="strict">Strict (hard to pass)</option>
        </select>

        <label>Buyer (who pays if true?)</label>
        <input id="buyer" placeholder="Example: Teams shipping production agents (cost + incident risk)." />

        <label>Notes (risks / assumptions)</label>
        <textarea id="notes" placeholder="Example: depends on task mix; needs held-out evaluation; watch false stops."></textarea>

        <div class="btnrow">
          <button id="back3">← Back</button>
          <button class="primary" id="next3">Next →</button>
        </div>
      </div>

      <!-- Stage 4 -->
      <div id="stage4" class="hidden">
        <p class="tip"><b>Final move:</b> write the falsifier. The cheapest observation that kills the claim. This is what makes it real.</p>

        <label>FALSIFIER (cheapest kill switch)</label>
        <textarea id="falsifier" placeholder="Example: If held-out pass rate does not improve AND loop rate does not fall under the cheat suppression witness, the claim fails."></textarea>

        <div class="btnrow">
          <button id="back4">← Back</button>
          <button class="primary" id="finish">Finish → Generate Artifact</button>
        </div>
        <p class="small">If you can’t write the falsifier, you’re not done. That’s fine—most people aren’t.</p>
      </div>

      <!-- Finish -->
      <div id="stage5" class="hidden">
        <p class="tip"><span class="badge good">Reward</span> You now have a Court-ready Opportunity Pack. This is the part where most “ideas” die. Yours didn’t.</p>

        <div class="btnrow">
          <button id="copyIssue">Copy Issue Body</button>
          <button id="copyYaml">Copy YAML</button>
          <a class="btn primary" id="openIssue" target="_blank" rel="noopener">Open GitHub Issue</a>
        </div>

        <hr/>

        <div class="small">Issue body</div>
        <div class="mini" id="outIssue"></div>

        <div style="height:10px"></div>
        <div class="small">YAML pack</div>
        <div class="mini" id="outYaml"></div>

        <p class="small">Share tip: screenshot this “Reward” screen. That’s your viral proof-of-work.</p>
      </div>
    </div>

    <div class="card">
      <h2>How the game teaches you</h2>
      <p class="tip"><b>Level 1 (Claim):</b> forces measurability.</p>
      <p class="tip"><b>Level 2 (Cheat Path):</b> forces humility. Most “breakthroughs” are just metric hacks.</p>
      <p class="tip"><b>Level 3 (Court):</b> forces independent witnesses instead of one leaderboard.</p>
      <p class="tip"><b>Level 4 (Falsifier):</b> turns belief into a bet with a clear loss condition.</p>
      <hr/>
      <p class="small">Not spooky version of the whole idea: we’re building a fair scoreboard that can’t be quietly rewritten.</p>
    </div>
  </div>
</div>

<script>
  // Change this if you rename the repo:
  const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

  const presets = {
    agents: {
      goals: ["Reduce cost-per-solved", "Reduce loop rate", "Increase pass@1", "Reduce false stops"],
      cheats: ["Loop/idle burn", "Definition-of-done hacks", "Benchmark gaming", "Non-reproducible success"],
      witnesses: [
        ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
        ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded in window","Repetition exceeds bound (zombie loop)"],
        ["W3_TESTS","stability","hard","Regression/tests pass on completion","Tests fail or regressions spike"],
        ["W4_COST","cost_feasibility","soft","Cost-per-solved within cap vs baseline","Cost-per-solved worsens beyond cap"]
      ],
      cheatDefault: "Agent ‘wins’ by padding steps (repeating low-entropy actions) or by redefining what counts as done."
    },
    batteries: {
      goals: ["Improve CE", "Reduce impedance growth", "Reduce gas evolution", "Improve cycle life at high V"],
      cheats: ["Short-cycle illusion", "Impurity-sensitive effect", "Hidden parasitics", "Thermal instability"],
      witnesses: [
        ["W1_ORIGIN","origin","hard","Effect replicates in separate build/batch","Effect vanishes on independent replicate"],
        ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS proxies bounded","Parasitics dominate (gas spike / EIS runaway)"],
        ["W3_STABILITY","stability","hard","CE+EIS drift within bounds over N cycles","CE collapses or EIS drift exceeds bound"],
        ["W4_COST","cost_feasibility","soft","Feasible additive + safety constraints","Prohibitive cost or safety violation"]
      ],
      cheatDefault: "Looks good for 5–10 cycles, then parasitics dominate and the win disappears."
    },
    co2: {
      goals: ["Increase FE to target", "Suppress HER", "Improve time-on-stream", "Lower energy per mole"],
      cheats: ["HER dominance", "Carbon balance not closed", "Short peak performance", "Contamination artifacts"],
      witnesses: [
        ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
        ["W2_HER","cheat_suppression","hard","HER bounded at target current","HER dominates current"],
        ["W3_TOS","stability","hard","Stable time-on-stream for T hours","Rapid decay / deactivation"],
        ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation / high replacement cost"]
      ],
      cheatDefault: "System ‘wins’ by making hydrogen or by hiding missing carbon in accounting."
    },
    synbio: {
      goals: ["Increase yield", "Increase stability", "Reduce assay noise", "Reduce cost per gram"],
      cheats: ["Assay artifact", "Contamination", "Non-scalable expression", "Short-lived activity"],
      witnesses: [
        ["W1_CONTROLS","origin","hard","Negative + contamination controls clean","Signal present in blanks/controls"],
        ["W2_ORTHO","cheat_suppression","hard","Orthogonal assay confirms activity","Second assay contradicts"],
        ["W3_HALFLIFE","stability","hard","Half-life meets bound at process conditions","Rapid deactivation"],
        ["W4_YIELD","cost_feasibility","soft","Expression/yield feasible","Unscalable yield"]
      ],
      cheatDefault: "Assay artifacts or contamination produce a fake ‘hit’ that vanishes under controls."
    }
  };

  const el = id => document.getElementById(id);
  let xp = 0;

  function setXP(v){ xp = v; el("xp").textContent = `XP: ${xp}`; }
  function setBar(p){ el("barFill").style.width = `${p}%`; }

  function show(stage){
    ["stage1","stage2","stage3","stage4","stage5"].forEach(id => el(id).classList.add("hidden"));
    el(stage).classList.remove("hidden");
  }

  function refresh(){
    const d = el("domain").value;
    el("goal").innerHTML = presets[d].goals.map(x => `<option>${x}</option>`).join("");
    el("cheat").innerHTML = presets[d].cheats.map(x => `<option>${x}</option>`).join("");
    if (!el("cheatPath").value) el("cheatPath").value = presets[d].cheatDefault;
  }

  function genID(domain){
    const stamp = new Date().toISOString().slice(2,10).replaceAll("-","");
    return `OP-${domain.toUpperCase()}-${stamp}`;
  }

  function buildArtifact(){
    const domain = el("domain").value;
    const goal = el("goal").value;
    const cheat = el("cheat").value;
    const claim = (el("claim").value || "").trim();
    const cheatPath = (el("cheatPath").value || "").trim();
    const proof = el("proof").value;
    const buyer = (el("buyer").value || "").trim();
    const notes = (el("notes").value || "").trim();
    const falsifier = (el("falsifier").value || "").trim();

    const id = genID(domain);
    const preset = presets[domain];

    let escape = [];
    if (proof === "cheap") escape = ["Independent rerun", "Longer window (2x)", "Tighter stop-rule + rollback"];
    if (proof === "balanced") escape = ["Independent rerun", "Longer window", "Stricter measurement/control"];
    if (proof === "strict") escape = ["Independent rerun (different environment/batch)", "Long stability window", "Orthogonal measurement", "External replication if possible"];

    const witnessesText = preset.witnesses
      .map(w => `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`)
      .join("\n");

    const issueBody =
`ID: ${id}
DOMAIN: ${domain}

CLAIM:
- ${claim}

CHEAT_PATH:
- ${cheatPath} (risk: ${cheat})

COURT_TESTS (independent witnesses):
${witnessesText}

FALSIFIER:
- ${falsifier}

ESCAPE_HATCH:
- If performance spike is huge but one witness fails, require:
  ${escape.map(x => `- ${x}`).join("\n  ")}

MIN_VALIDATION:
- Step 1 (cheap): smallest test that hits Origin + Cheat suppression.
- Step 2 (mid): extend window; tighten controls.
- Step 3 (expensive): independent rerun (new batch / new environment).

BUYER:
- ${buyer}

WHY THEY CARE:
- Goal/KPI: ${goal}

NOTES:
- ${notes}
`;

    const yaml =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
domain: "${domain}"
goal_kpi: "${goal}"
cheat_risk: "${cheat}"
claim: "${claim.replaceAll('"','\\"')}"
cheat_path: "${cheatPath.replaceAll('"','\\"')}"
court_tests:
${preset.witnesses.map(w => `  - id: "${w[0]}"
    role: "${w[1]}"
    hardness: "${w[2]}"
    pass_condition: "${w[3].replaceAll('"','\\"')}"
    fail_condition: "${w[4].replaceAll('"','\\"')}"`).join("\n")}
falsifier: "${falsifier.replaceAll('"','\\"')}"
escape_hatch:
  trigger: "major_spike_and_one_witness_failed"
  required_escalations:
${escape.map(x => `    - "${x.replaceAll('"','\\"')}"`).join("\n")}
buyer: "${buyer.replaceAll('"','\\"')}"
notes: "${notes.replaceAll('"','\\"')}"
`;

    el("outIssue").textContent = issueBody;
    el("outYaml").textContent = yaml;

    const title = `Opportunity Pack: ${domain.toUpperCase()} — ${goal}`;
    el("openIssue").href = `${REPO_NEW_ISSUE_URL}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(issueBody)}`;
  }

  async function copyText(text){
    try { await navigator.clipboard.writeText(text); }
    catch(e){ alert("Copy failed. Select text manually and copy."); }
  }

  // stage nav
  el("domain").addEventListener("change", refresh);

  el("next1").addEventListener("click", () => {
    if (!(el("claim").value || "").trim()) return alert("Write the one-sentence claim first.");
    setXP(25); setBar(25); el("stageTitle").textContent = "Level 2/4 · Boss Fight: Cheat Path";
    show("stage2");
  });

  el("back2").addEventListener("click", () => { setXP(0); setBar(0); el("stageTitle").textContent="Level 1/4 · The Claim"; show("stage1"); });

  el("next2").addEventListener("click", () => {
    if (!(el("cheatPath").value || "").trim()) return alert("Name the cheat path. That’s the whole point.");
    setXP(50); setBar(50); el("stageTitle").textContent = "Level 3/4 · Build the Court";
    show("stage3");
  });

  el("back3").addEventListener("click", () => { setXP(25); setBar(25); el("stageTitle").textContent="Level 2/4 · Boss Fight: Cheat Path"; show("stage2"); });

  el("next3").addEventListener("click", () => {
    if (!(el("buyer").value || "").trim()) return alert("Add the buyer. One sentence.");
    setXP(75); setBar(75); el("stageTitle").textContent = "Level 4/4 · The Falsifier";
    show("stage4");
  });

  el("back4").addEventListener("click", () => { setXP(50); setBar(50); el("stageTitle").textContent="Level 3/4 · Build the Court"; show("stage3"); });

  el("finish").addEventListener("click", () => {
    if (!(el("falsifier").value || "").trim()) return alert("Write the falsifier (cheapest kill switch).");
    setXP(100); setBar(100); el("stageTitle").textContent = "Complete · Reward";
    buildArtifact();
    show("stage5");
  });

  el("copyIssue").addEventListener("click", () => copyText(el("outIssue").textContent));
  el("copyYaml").addEventListener("click", () => copyText(el("outYaml").textContent));

  refresh();
</script>
</body>
</html>
