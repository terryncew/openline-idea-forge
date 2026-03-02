<script>
const REPO_NEW_ISSUE_URL = "https://github.com/terryncew/openline-idea-forge/issues/new";

const game = {
  themes: [
    {
      key:"public-truth",
      title:"Truth people can check",
      meta:"Less “trust us.” More “show the record.”",
      missions:[
        {
          id:"AG-LOOPKILL",
          domain:"agents",
          title:"Stop AI from wasting money in loops",
          kpi:"Reduce cost-per-solved without false stops",
          cheat_risk:"high",
          claim:"A loop governor reduces repeated-action burn by ≥30% on real tasks while keeping false stops ≤2%.",
          cheat:"It ‘wins’ by killing hard-but-solvable tasks (quietly lowering the denominator).",
          falsifier:"Fails if held-out solved rate drops OR false stops exceed 2% while loop burn does not fall by ≥30%.",
          buyer:"Teams shipping production agents (budget + reliability).",
          notes:"Lock the definition of solved. Use held-out tasks. Track cost-per-solved + false stops.",
          limits:[
            "Does not make the model smarter. It makes waste visible and stoppable.",
            "Needs a fixed ‘solved’ rubric or people will game the scoreboard.",
            "Works best as a guardrail + audit layer, not a magic judge."
          ],
          witnesses:[
            ["W1_REPLAY","origin","hard","Deterministic replay reproduces outcome","Outcome not reproducible under replay"],
            ["W2_LOOP","cheat_suppression","hard","Repeated signatures bounded in window","Repetition exceeds bound (zombie loop)"],
            ["W3_TESTS","stability","hard","Regression/tests pass on completion","Tests fail or regressions spike"],
            ["W4_COST","cost_feasibility","soft","Cost-per-solved stays within cap","Cost-per-solved worsens beyond cap"]
          ]
        },
        {
          id:"CHIP-YIELD",
          domain:"microchips",
          title:"Improve yield without hiding scrap",
          kpi:"Yield up with audited defect taxonomy",
          cheat_risk:"high",
          claim:"A recommender improves yield by ≥X% while keeping defect accounting consistent (no relabeling).",
          cheat:"It ‘wins’ by reclassifying defects or shifting scrap categories.",
          falsifier:"Fails if the gain disappears under a fixed taxonomy + blind audit.",
          buyer:"Foundry ops / packaging / test teams.",
          notes:"Lock defect taxonomy. Require blind audit. Track yield + rework + scrap.",
          limits:[
            "Does not claim physics wins if accounting changes.",
            "One-lot spikes don’t count. Must hold across lots.",
            "Blind audit is the point; without it, it’s PR."
          ],
          witnesses:[
            ["W1_AUDIT","origin","hard","Blind audit confirms taxonomy unchanged","Taxonomy drift/relabeling detected"],
            ["W2_STABILITY","stability","hard","Gain holds over multiple lots","One-lot spike only"],
            ["W3_COST","cost_feasibility","soft","Cost per good die improves","Cost balloons with no net gain"]
          ]
        }
      ]
    },
    {
      key:"climate",
      title:"Climate that actually pencils out",
      meta:"No vibes. Carbon balance. Time-on-stream. Durability.",
      missions:[
        {
          id:"CO2-HER",
          domain:"co2",
          title:"CO₂ conversion that doesn’t cheat into hydrogen",
          kpi:"High FE to CO + bounded HER + 10h stability",
          cheat_risk:"high",
          claim:"A CO₂RR setup holds FE(CO) ≥90% while keeping HER below bound for ≥10 hours time-on-stream.",
          cheat:"It ‘wins’ via bad accounting (carbon balance doesn’t close) or a short peak that collapses.",
          falsifier:"Fails if carbon balance doesn’t close OR FE collapses before 10h OR HER dominates current.",
          buyer:"CO₂ electrolysis startups + industrial R&D.",
          notes:"Carbon balance is non-negotiable. Stability matters more than peak.",
          limits:[
            "Does not claim net-negative carbon without lifecycle accounting.",
            "Peak FE is not the win; stability is the win.",
            "If carbon balance doesn’t close, it’s not real."
          ],
          witnesses:[
            ["W1_CARBON","origin","hard","Carbon balance closes","Carbon balance does not close"],
            ["W2_HER","cheat_suppression","hard","HER bounded at target current","HER dominates current"],
            ["W3_TOS","stability","hard","Stable time-on-stream ≥10h","Rapid decay/deactivation"],
            ["W4_DURABILITY","cost_feasibility","soft","Durability acceptable","Fast degradation/high replacement cost"]
          ]
        }
      ]
    },
    {
      key:"privacy",
      title:"Privacy & freedom (without ‘trust us’)",
      meta:"Anti-surveillance people usually hate new systems. This one asks for proofs, not monitoring.",
      missions:[
        {
          id:"AG-PUBLICLOG",
          domain:"agents",
          title:"A public record for AI actions (without leaking content)",
          kpi:"Prove what happened without exposing private data",
          cheat_risk:"medium",
          claim:"A minimal receipt log proves what an AI did (actions + timestamps + checks) without logging user content.",
          cheat:"It ‘wins’ by logging pretty summaries that can’t be audited, or by leaking sensitive details.",
          falsifier:"Fails if auditors can’t verify decisions OR if the log requires storing private content to be useful.",
          buyer:"Any org deploying AI where trust is broken (support, legal, compliance).",
          notes:"This is ‘less watching, more proof.’ The log should be content-minimal.",
          limits:[
            "Does not store your conversations. It stores decision traces.",
            "Does not prevent all misuse; it makes misuse harder to deny.",
            "If it leaks content, it fails."
          ],
          witnesses:[
            ["W1_AUDIT","origin","hard","Independent verifier can validate receipts","Receipts can’t be verified"],
            ["W2_PRIVACY","cheat_suppression","hard","No user content stored; leakage tests pass","Content leakage required or occurs"],
            ["W3_STABILITY","stability","hard","Works across multiple runs/tools","Only works in one demo setup"],
            ["W4_COST","cost_feasibility","soft","Overhead acceptable","Overhead makes it unusable"]
          ]
        }
      ]
    },
    {
      key:"cost-of-living",
      title:"Cost of living / jobs / dignity",
      meta:"Make tech help regular people: stop waste, shorten time-to-results.",
      missions:[
        {
          id:"BAT-SEI",
          domain:"batteries",
          title:"Battery additive that survives parasitics",
          kpi:"CE + impedance stability over 100 cycles",
          cheat_risk:"medium",
          claim:"An additive improves CE by ≥1% and reduces impedance growth while keeping gas evolution below threshold over ≥100 cycles.",
          cheat:"Looks great early; parasitics explode later; effect doesn’t replicate.",
          falsifier:"Fails if replicate loses effect OR parasitics exceed bound OR CE gain disappears by cycle 100.",
          buyer:"Battery startups + suppliers + OEM labs.",
          notes:"Track gas/EIS, not just capacity. Replicate on a second batch.",
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
      ]
    }
  ],
  crews:[
    { key:"solo", title:"Solo", meta:"You just want a plan you can run." , score:+4,
      add:"Do the cheap falsifier test first. If it survives, recruit help." },
    { key:"friends", title:"Friends (2–5 people)", meta:"Split roles: builder, skeptic, recorder." , score:+9,
      add:"Assign one person to try to kill it. Make them ‘the Court.’" },
    { key:"agents", title:"Agents (Claude/ChatGPT)", meta:"Use agents like interns with a leash." , score:+11,
      add:"Agents can draft plans and gather evidence. The falsifier stays the boss." }
  ],
  weekends:[
    { key:"1h", title:"1 hour", meta:"Try to kill it fast." , score:+4,
      plan:["Run the smallest test that hits Origin + Cheat suppression.","If it fails, stop. If it survives, queue a longer run."]},
    { key:"1d", title:"One day", meta:"Cheap+mid. Enough to learn." , score:+9,
      plan:["Run cheap test + tighten controls.","Extend window. Look for decay / parasitics.","If it survives, do independent rerun."]},
    { key:"weekend", title:"Weekend", meta:"Cheap+mid+independent rerun." , score:+14,
      plan:["Cheap test (origin + cheat suppression).","Mid test (longer window + stricter controls).","Independent rerun (new batch/environment)."]}
  ]
};

const el = id => document.getElementById(id);
let sel = { theme:null, mission:null, crew:null, weekend:null };

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

function scoreNow(){
  if (!sel.mission) return null;
  const base = 50;
  const witnessScore = Math.min(20, (sel.mission.witnesses?.length || 0) * 5);
  const cheatRisk = sel.mission.cheat_risk === "high" ? 10 : sel.mission.cheat_risk === "medium" ? 6 : 3;
  const crewScore = sel.crew ? sel.crew.score : 0;
  const weekendScore = sel.weekend ? sel.weekend.score : 0;
  return Math.max(0, Math.min(100, base + witnessScore + cheatRisk + crewScore + weekendScore));
}

function updateScorePanel(){
  const s = scoreNow();
  if (!sel.mission){
    el("score").textContent = "—";
    el("scoremeta").textContent = "Pick options on the left. You’ll see a rank + the limits.";
    return;
  }
  const label = s >= 85 ? "High chance of being testable this week" : s >= 70 ? "Testable with guardrails" : "Too squishy unless you tighten proof";
  const limits = (sel.mission.limits || []).map(x => `• ${x}`).join(" ");
  el("score").textContent = `${s}/100`;
  el("scoremeta").innerHTML = `<b>${label}.</b><br/>Limited to: ${limits}`;
}

function renderStep1(){
  const box = el("step1"); box.innerHTML = "";
  game.themes.forEach((t, idx) => {
    const d = card(t.title, t.meta);
    d.onclick = () => {
      sel.theme = t; sel.mission=null; sel.crew=null; sel.weekend=null;
      document.querySelectorAll("#step1 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      
      // FIX: Hide downstream steps and update progress BEFORE rendering Step 2
      el("step3wrap").classList.add("hidden");
      el("step4wrap").classList.add("hidden");
      setProgress(25);

      el("step2wrap").classList.remove("hidden");
      renderStep2();
      updateScorePanel();
    };
    box.appendChild(d);
    if (idx===0 && !sel.theme){ d.click(); }
  });
}

function renderStep2(){
  const box = el("step2"); box.innerHTML = "";
  (sel.theme.missions || []).forEach((m, idx) => {
    const d = card(m.title, `<b>KPI:</b> ${m.kpi}<br/><b>Cheat risk:</b> ${m.cheat_risk}`);
    d.onclick = () => {
      sel.mission = m; sel.crew=null; sel.weekend=null;
      document.querySelectorAll("#step2 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      
      // FIX: Hide downstream steps and update progress BEFORE rendering Step 3
      el("step4wrap").classList.add("hidden");
      setProgress(50);

      el("step3wrap").classList.remove("hidden");
      renderStep3();
      updateScorePanel();
    };
    box.appendChild(d);
    if (idx===0 && !sel.mission){ d.click(); }
  });
}

function renderStep3(){
  const box = el("step3"); box.innerHTML = "";
  game.crews.forEach((c, idx) => {
    const d = card(c.title, `${c.meta}<br/><span class="small">${c.add}</span>`);
    d.onclick = () => {
      sel.crew = c; sel.weekend=null;
      document.querySelectorAll("#step3 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      
      setProgress(75);

      el("step4wrap").classList.remove("hidden");
      renderStep4();
      updateScorePanel();
    };
    box.appendChild(d);
    if (idx===1 && !sel.crew){ d.click(); } // default friends
  });
}

function renderStep4(){
  const box = el("step4"); box.innerHTML = "";
  game.weekends.forEach((w, idx) => {
    const d = card(w.title, `${w.meta}<br/><span class="small">Adds +${w.score} score</span>`);
    d.onclick = () => {
      sel.weekend = w;
      document.querySelectorAll("#step4 .choice").forEach(x => x.classList.remove("sel"));
      d.classList.add("sel");
      setProgress(90);
      updateScorePanel();
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
  if (!sel.mission || !sel.crew || !sel.weekend) return;
  const m = sel.mission;
  const crew = sel.crew;
  const weekend = sel.weekend;
  const score = scoreNow();

  const id = genID(m.domain);
  const witnessesText = (m.witnesses || []).map(w =>
    `- ${w[0]} (${w[1]}, ${w[2]}): PASS if ${w[3]}. FAIL if ${w[4]}.`
  ).join("\n");

  const limitsText = (m.limits || []).map(x => `- ${x}`).join("\n");

  const issueBody =
`ID: ${id}
DOMAIN: ${m.domain}

RANKING:
- testability_score: ${score}/100
- crew: ${crew.key}
- weekend: ${weekend.key}

LIMITS:
${limitsText}

CLAIM:
- ${m.claim}

CHEAT_PATH:
- ${m.cheat}

COURT_TESTS (independent witnesses):
${witnessesText}

FALSIFIER:
- ${m.falsifier}

MIN_VALIDATION (${weekend.title}):
- Step 1 (cheap): ${weekend.plan[0]}
- Step 2 (mid): ${weekend.plan[1] || "Tighten controls + extend window."}
- Step 3 (expensive): ${weekend.plan[2] || "Independent rerun (new batch/environment)."}

CREW NOTE:
- ${crew.add}

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
theme: "${sel.theme.key}"
domain: "${m.domain}"
title: "${m.title.replaceAll('"','\\"')}"
ranking:
  testability_score: ${score}
  crew: "${crew.key}"
  weekend: "${weekend.key}"
limits:
${(m.limits||[]).map(x => `  - "${x.replaceAll('"','\\"')}"`).join("\n")}
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
min_validation:
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
  el("stageTitle").textContent = "Complete · Pack Ready";
  updateScorePanel();
}

async function copyText(text){
  try { await navigator.clipboard.writeText(text); }
  catch(e){ alert("Copy failed. Select text manually and copy."); }
}

el("generate").addEventListener("click", buildArtifact);
el("copyIssue").addEventListener("click", () => copyText(el("outIssue").textContent));
el("copyYaml").addEventListener("click", () => copyText(el("outYaml").textContent));

// FIX: Set progress to 0 before starting the click cascade, so it doesn't instantly overwrite your 90% progress bar.
setProgress(0);
renderStep1();
</script>
