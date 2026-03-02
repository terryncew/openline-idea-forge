<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Idea Forge</title>
  <style>
    :root{
      --bg:#0b0c10; --panel:#101218; --line:rgba(255,255,255,.10);
      --text:#e9eef7; --muted:#a8b3c7; --accent:#6ea8ff;
      --good:#7CFF9B; --warn:#ffd166; --bad:#ff6b6b;
      --shadow: 0 10px 30px rgba(0,0,0,.35);
    }
    @media (prefers-color-scheme: light){
      :root{ --bg:#fbfcff; --panel:#fff; --line:rgba(15,20,40,.12);
        --text:#0b1020; --muted:#3f4b66; --accent:#1f6feb; --shadow:0 10px 30px rgba(10,20,40,.12);}
    }
    body{margin:0;background:var(--bg);color:var(--text);font-family: ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;}
    .wrap{max-width:980px;margin:0 auto;padding:18px 14px 40px;}
    .hero{border:1px solid var(--line);border-radius:18px;padding:18px;background:linear-gradient(135deg, rgba(110,168,255,.16), rgba(124,240,210,.10));box-shadow:var(--shadow);}
    h1{margin:0 0 8px;font-size:34px;letter-spacing:.2px}
    .sub{margin:0;color:var(--muted);line-height:1.4}
    .grid{display:grid;grid-template-columns:1fr;gap:12px;margin-top:14px}
    @media(min-width:860px){.grid{grid-template-columns:1fr 1fr}}
    .card{border:1px solid var(--line);border-radius:16px;background:var(--panel);padding:14px}
    .card h2{margin:0 0 10px;font-size:16px}
    label{display:block;font-size:12px;color:var(--muted);margin:10px 0 6px}
    select, input, textarea{
      width:100%;box-sizing:border-box;border-radius:12px;border:1px solid var(--line);
      background:rgba(255,255,255,.04);color:var(--text);padding:10px 10px;font-size:14px;
    }
    textarea{min-height:92px;resize:vertical}
    .row{display:flex;gap:10px;flex-wrap:wrap}
    .row > div{flex:1;min-width:180px}
    .btnrow{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
    button, a.btn{
      appearance:none;border-radius:12px;border:1px solid var(--line);
      background:rgba(255,255,255,.04);color:var(--text);
      padding:10px 12px;font-size:14px;cursor:pointer;text-decoration:none;display:inline-block;
    }
    button.primary{border-color:rgba(110,168,255,.35);background:linear-gradient(135deg, rgba(110,168,255,.30), rgba(124,240,210,.18));}
    .mono{font-family: ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono",monospace;
      font-size:12.5px;white-space:pre-wrap;overflow-wrap:anywhere;line-height:1.35;
      border:1px solid var(--line);border-radius:16px;background:#0b0f1a;color:#d8e2ff;padding:12px}
    @media (prefers-color-scheme: light){.mono{background:#0b1020;color:#e9eef7}}
    .pill{display:inline-block;padding:4px 8px;border:1px solid var(--line);border-radius:999px;font-size:12px;color:var(--muted);margin-right:6px}
    .hint{color:var(--muted);font-size:13px;line-height:1.35}
    .courtline{display:flex;gap:10px;align-items:center;margin:8px 0}
    .badge{min-width:76px;text-align:center;font-weight:800;border-radius:10px;padding:6px 10px;border:1px solid var(--line);background:rgba(255,255,255,.04)}
    .bPASS{color:var(--good);border-color:rgba(124,255,155,.45)}
    .bESC{color:var(--warn);border-color:rgba(255,209,102,.55)}
    .bFAIL{color:var(--bad);border-color:rgba(255,107,107,.55)}
    .small{font-size:12px;color:var(--muted)}
  </style>
</head>
<body>
<div class="wrap">
  <div class="hero">
    <h1>Idea Forge</h1>
    <p class="sub">Pick filters like shopping. Get a Court-ready Opportunity Pack + machine YAML + one-click GitHub Issue.</p>
    <div style="margin-top:10px">
      <span class="pill">CHEAT_PATH required</span>
      <span class="pill">Falsifier-first</span>
      <span class="pill">PASS / ESCAPE / FAIL</span>
    </div>
  </div>

  <div class="grid">
    <div class="card">
      <h2>1) Filters</h2>

      <div class="row">
        <div>
          <label>Domain</label>
          <select id="domain">
            <option value="agents">Agents</option>
            <option value="batteries">Batteries</option>
            <option value="co2">CO₂ Electrolysis</option>
            <option value="synbio">SynBio</option>
          </select>
        </div>
        <div>
          <label>Goal (KPI)</label>
          <select id="goal"></select>
        </div>
      </div>

      <div class="row">
        <div>
          <label>Cheat risk (what usually fakes wins)</label>
          <select id="cheat"></select>
        </div>
        <div>
          <label>Proof mode</label>
          <select id="proof">
            <option value="cheap">Cheap proof (fast kill)</option>
            <option value="balanced" selected>Balanced</option>
            <option value="strict">Strict (hard to pass)</option>
          </select>
        </div>
      </div>

      <label>Claim (one sentence)</label>
      <input id="claim" placeholder="Example: Reduce loop burn by 30% on SWE-style tasks without increasing false kills." />

      <label>Buyer</label>
      <input id="buyer" placeholder="Example: Any team shipping production agents (cost + incident risk)." />

      <label>Notes</label>
      <textarea id="notes" placeholder="Known risks, missing info, assumptions."></textarea>

      <div class="btnrow">
        <button class="primary" id="build">Generate Pack</button>
        <button id="copyIssue">Copy Issue Body</button>
        <button id="copyYaml">Copy YAML</button>
        <a class="btn" id="openIssue" target="_blank" rel="noopener">Open GitHub Issue</a>
      </div>

      <p class="small">Tip: “Open GitHub Issue” will prefill the issue title + body. Works with GitHub web on iPhone.</p>
    </div>

    <div class="card">
      <h2>2) The Court (v1)</h2>
      <div class="courtline"><div class="badge bPASS">PASS</div><div class="hint">All hard witnesses + origin controls satisfied.</div></div>
      <div class="courtline"><div class="badge bESC">ESCAPE</div><div class="hint">Big spike, one witness fails → higher burden of proof.</div></div>
      <div class="courtline"><div class="badge bFAIL">FAIL</div><div class="hint">Hard witness fails without compelling spike, or origin controls fail.</div></div>

      <div style="margin-top:12px">
        <h2>3) Generated Output</h2>
        <p class="hint">This is what gets submitted. It forces CHEAT_PATH + witnesses + falsifier.</p>
        <div class="mono" id="outIssue">(generate to see output)</div>
        <div style="height:10px"></div>
        <div class="mono" id="outYaml">(generate to see YAML)</div>
      </div>
    </div>
  </div>
</div>

<script>
  // Set this to your repo for the "Open GitHub Issue" button:
  const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

  const presets = {
    agents: {
      goals: ["Reduce cost-per-solved", "Reduce loop rate", "Increase pass@1 on tasks", "Reduce false stops"],
      cheats: ["Loop/idle burn", "Benchmark gaming", "Non-reproducible success", "Definition-of-done hacks"],
      witnesses: [
        ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
        ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded in window","Repetition exceeds bound (zombie loop)"],
        ["W3_REGRESSION","stability","hard","Regression/tests pass on completion","Tests fail or frequent regressions"],
        ["W4_COST","cost_feasibility","soft","Cost-per-solved within cap vs baseline","Cost-per-solved worsens beyond cap"]
      ],
      cheatPathDefault: "Agent pads steps (repeats low-entropy actions) or 'solves' by changing the definition of done."
    },
    batteries: {
      goals: ["Improve CE", "Reduce impedance growth", "Reduce gas evolution", "Improve cycle life at high V"],
      cheats: ["Short-cycle illusion", "Impurity-sensitive effect", "Gas/side reactions hidden", "Thermal instability"],
      witnesses: [
        ["W1_ORIGIN","origin","hard","Effect replicates in separate build/batch","Effect vanishes on independent replicate"],
        ["W2_PARASITICS","cheat_suppression","hard","Gas/EIS proxies bounded","Parasitics dominate (gas spike / EIS runaway)"],
        ["W3_STABILITY","stability","hard","CE+EIS drift within bounds over N cycles","CE collapses or EIS drift exceeds bound"],
        ["W4_COST","cost_feasibility","soft","Feasible additive + safety constraints","Prohibitive cost or safety violation"]
      ],
      cheatPathDefault: "Looks good for 5–10 cycles, then parasitics dominate (gas, impedance) and the win disappears."
    },
    co2: {
      goals: ["Increase FE to target", "Suppress HER", "Improve stability time-on-stream", "Lower energy per mole"],
      cheats: ["HER dominance", "Carbon balance not closed", "Short peak performance", "Contamination artifacts"],
      witnesses: [
        ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
        ["W2_HER","cheat_suppression","hard","HER bounded at target current","HER dominates current"],
        ["W3_TOS","stability","hard","Stable time-on-stream for T hours","Rapid decay / deactivation"],
        ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation / high replacement cost"]
      ],
      cheatPathDefault: "System ‘wins’ by making hydrogen or by hiding missing carbon in accounting."
    },
    synbio: {
      goals: ["Increase yield", "Increase stability at process conditions", "Reduce assay noise", "Reduce cost per gram"],
      cheats: ["Assay artifact", "Contamination", "Non-scalable expression", "Short-lived activity"],
      witnesses: [
        ["W1_CONTROLS","origin","hard","Negative + contamination controls clean","Signal present in blanks/controls"],
        ["W2_ORTHO","cheat_suppression","hard","Orthogonal assay confirms activity","Second assay contradicts"],
        ["W3_HALFLIFE","stability","hard","Half-life meets bound at process conditions","Rapid deactivation"],
        ["W4_YIELD","cost_feasibility","soft","Expression/yield feasible","Unscalable yield"]
      ],
      cheatPathDefault: "Fluorescence/assay artifacts or contamination produce a fake ‘hit’ that vanishes under controls."
    }
  };

  function el(id){ return document.getElementById(id); }

  function refreshDropdowns(){
    const d = el("domain").value;
    el("goal").innerHTML = presets[d].goals.map(x => `<option>${x}</option>`).join("");
    el("cheat").innerHTML = presets[d].cheats.map(x => `<option>${x}</option>`).join("");
  }

  function genID(domain){
    const stamp = new Date().toISOString().slice(2,10).replaceAll("-","");
    const tag = domain.toUpperCase();
    return `OP-${tag}-${stamp}`;
  }

  function build(){
    const domain = el("domain").value;
    const goal = el("goal").value;
    const cheat = el("cheat").value;
    const proof = el("proof").value;
    const claim = (el("claim").value || "").trim();
    const buyer = (el("buyer").value || "").trim();
    const notes = (el("notes").value || "").trim();

    const id = genID(domain);
    const preset = presets[domain];

    // Proof mode tweaks
    let escape = [];
    if (proof === "cheap") escape = ["Independent rerun", "Longer window (2x)", "Tighter stop-rule + rollback"];
    if (proof === "balanced") escape = ["Independent rerun", "Longer window", "Stricter measurement/control"];
    if (proof === "strict") escape = ["Independent rerun (different environment/batch)", "Long stability window", "Orthogonal measurement", "External replication if possible"];

    const cheatPath = preset.cheatPathDefault + " Selected risk: " + cheat + ".";

    const witnessesText = preset.witnesses.map(w => `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`).join("\n");

    const falsifier = `Fails if the claimed improvement does not replicate under the Origin witness OR if the cheat path dominates under the Cheat suppression witness.`;

    const issueBody =
`ID: ${id}
DOMAIN: ${domain}

CLAIM:
- ${claim || "(fill this in)"}  

CHEAT_PATH:
- ${cheatPath}

COURT_TESTS (independent witnesses):
${witnessesText}

FALSIFIER:
- ${falsifier}

ESCAPE_HATCH:
- If performance spike is huge but one witness fails, require:
  ${escape.map(x => `- ${x}`).join("\n  ")}

MIN_VALIDATION:
- Step 1 (cheap): run smallest test that hits Origin + Cheat suppression.
- Step 2 (mid): extend stability window; tighten controls.
- Step 3 (expensive): independent rerun (new batch / new environment).

BUYER:
- ${buyer || "(fill this in)"}

WHY THEY CARE:
- Goal/KPI: ${goal}

NOTES:
- ${notes || "(fill this in)"}
`;

    const yaml =
`schema_version: "idea_forge.v1"
kind: "opportunity_pack"
id: "${id}"
domain: "${domain}"
goal_kpi: "${goal}"
cheat_risk: "${cheat}"
claim: "${(claim||"").replaceAll('"','\\"')}"
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
buyer: "${(buyer||"").replaceAll('"','\\"')}"
notes: "${(notes||"").replaceAll('"','\\"')}"
`;

    el("outIssue").textContent = issueBody;
    el("outYaml").textContent = yaml;

    const title = `Opportunity Pack: ${domain.toUpperCase()} — ${goal}`;
    const url = `${REPO_NEW_ISSUE_URL}?title=${encodeURIComponent(title)}&body=${encodeURIComponent(issueBody)}`;
    el("openIssue").href = url;
  }

  async function copyText(text){
    try { await navigator.clipboard.writeText(text); }
    catch(e){ alert("Copy failed. Select text manually and copy."); }
  }

  el("domain").addEventListener("change", refreshDropdowns);
  el("build").addEventListener("click", build);
  el("copyIssue").addEventListener("click", () => copyText(el("outIssue").textContent));
  el("copyYaml").addEventListener("click", () => copyText(el("outYaml").textContent));

  refreshDropdowns();
</script>
</body>
</html>
