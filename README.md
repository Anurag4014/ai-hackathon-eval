<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>AI Hackathon — Judge Evaluation Sheet</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap');

  :root {
    --navy:      #0D1B2A;
    --navy-mid:  #1A2F48;
    --navy-light:#243B55;
    --blue:      #1E6FD9;
    --blue-light:#3B8FFF;
    --cyan:      #00C2FF;
    --white:     #F0F6FF;
    --muted:     #8BA8C4;
    --green:     #10B981;
    --amber:     #F59E0B;
    --red:       #EF4444;
    --card:      #162236;
    --border:    rgba(255,255,255,0.08);
    --radius:    10px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--navy);
    color: var(--white);
    min-height: 100vh;
  }

  /* ── HEADER ── */
  .site-header {
    background: linear-gradient(135deg, var(--navy-mid) 0%, #0a1628 100%);
    border-bottom: 1px solid var(--border);
    padding: 28px 40px 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 100;
  }
  .header-left { display: flex; align-items: center; gap: 16px; }
  .header-icon {
    width: 48px; height: 48px;
    background: linear-gradient(135deg, var(--blue), var(--cyan));
    border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 22px;
  }
  .header-title h1 {
    font-size: 20px; font-weight: 800;
    background: linear-gradient(90deg, var(--white), var(--cyan));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    letter-spacing: -0.3px;
  }
  .header-title p { font-size: 12px; color: var(--muted); margin-top: 2px; }
  .progress-wrap { display: flex; align-items: center; gap: 12px; }
  .progress-label { font-size: 12px; color: var(--muted); }
  .progress-bar { width: 180px; height: 6px; background: var(--navy-light); border-radius: 99px; overflow: hidden; }
  .progress-fill { height: 100%; background: linear-gradient(90deg, var(--blue), var(--cyan)); border-radius: 99px; transition: width 0.4s ease; }
  .progress-pct { font-size: 12px; color: var(--cyan); font-weight: 600; font-family: 'JetBrains Mono', monospace; }

  /* ── TABS (use cases) ── */
  .tabs-bar {
    background: var(--navy-mid);
    border-bottom: 1px solid var(--border);
    padding: 0 40px;
    display: flex; align-items: flex-end; gap: 4px;
    overflow-x: auto;
  }
  .tab-btn {
    padding: 12px 22px;
    background: transparent;
    border: none; border-bottom: 3px solid transparent;
    color: var(--muted);
    font-family: 'Inter', sans-serif;
    font-size: 13px; font-weight: 500;
    cursor: pointer;
    white-space: nowrap;
    transition: all 0.2s;
  }
  .tab-btn:hover { color: var(--white); }
  .tab-btn.active { color: var(--cyan); border-bottom-color: var(--cyan); }
  .tab-btn .tab-badge {
    display: inline-block; margin-left: 6px;
    background: var(--navy-light); border-radius: 99px;
    padding: 1px 7px; font-size: 11px; color: var(--muted);
  }
  .tab-btn.active .tab-badge { background: rgba(0,194,255,0.15); color: var(--cyan); }
  .tab-btn.done .tab-badge { background: rgba(16,185,129,0.15); color: var(--green); }
  .tab-btn.done { color: var(--green); }

  /* ── MAIN ── */
  .main { padding: 32px 40px; max-width: 1400px; margin: 0 auto; }
  .panel { display: none; }
  .panel.active { display: block; }

  /* Use case title bar */
  .uc-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 24px;
  }
  .uc-title-group h2 { font-size: 22px; font-weight: 700; }
  .uc-title-group p { font-size: 13px; color: var(--muted); margin-top: 4px; }
  .uc-title-input {
    background: var(--card); border: 1px solid var(--border);
    border-radius: var(--radius); padding: 8px 14px;
    color: var(--white); font-family: 'Inter', sans-serif;
    font-size: 15px; font-weight: 600; width: 420px;
    outline: none; transition: border-color 0.2s;
  }
  .uc-title-input:focus { border-color: var(--blue-light); }

  /* Judge columns */
  .judges-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 20px;
  }
  .judge-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    overflow: hidden;
  }
  .judge-card-header {
    padding: 14px 20px;
    background: linear-gradient(90deg, var(--navy-light), var(--card));
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 12px;
  }
  .judge-avatar {
    width: 36px; height: 36px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 15px; font-weight: 700;
    flex-shrink: 0;
  }
  .judge-1 .judge-avatar { background: linear-gradient(135deg, #1E6FD9, #00C2FF); }
  .judge-2 .judge-avatar { background: linear-gradient(135deg, #7C3AED, #EC4899); }
  .judge-name-input {
    background: transparent; border: none;
    border-bottom: 1px dashed rgba(255,255,255,0.2);
    color: var(--white); font-family: 'Inter', sans-serif;
    font-size: 14px; font-weight: 600;
    outline: none; width: 180px; padding: 2px 0;
    transition: border-color 0.2s;
  }
  .judge-name-input:focus { border-bottom-color: var(--cyan); }
  .judge-completion { margin-left: auto; font-size: 11px; color: var(--muted); font-family: 'JetBrains Mono', monospace; }

  /* Criteria table */
  .criteria-table { width: 100%; border-collapse: collapse; }
  .criteria-table thead tr th {
    padding: 10px 14px;
    font-size: 11px; font-weight: 600; letter-spacing: 0.6px;
    text-transform: uppercase; color: var(--muted);
    background: rgba(255,255,255,0.03);
    border-bottom: 1px solid var(--border);
    text-align: left;
  }
  .criteria-table thead tr th.center { text-align: center; }
  .criteria-table tbody tr { border-bottom: 1px solid var(--border); transition: background 0.15s; }
  .criteria-table tbody tr:last-child { border-bottom: none; }
  .criteria-table tbody tr:hover { background: rgba(255,255,255,0.02); }
  .td-criteria { padding: 12px 14px; width: 38%; }
  .criteria-name { font-size: 13px; font-weight: 600; color: var(--white); }
  .criteria-desc { font-size: 11px; color: var(--muted); margin-top: 3px; line-height: 1.5; }
  .td-rating { text-align: center; padding: 10px 6px; width: 20%; }
  .td-feedback { padding: 10px 12px; width: 42%; }

  /* Rating pills */
  .rating-group { display: flex; gap: 6px; justify-content: center; }
  .rating-label {
    cursor: pointer;
    padding: 5px 10px;
    border-radius: 6px;
    font-size: 11px; font-weight: 600;
    border: 1.5px solid transparent;
    transition: all 0.18s;
    white-space: nowrap;
    user-select: none;
  }
  .rating-label input { display: none; }
  /* Fair */
  .rating-fair { border-color: rgba(245,158,11,0.3); color: #B97A0A; background: rgba(245,158,11,0.08); }
  .rating-fair:hover { border-color: rgba(245,158,11,0.6); color: var(--amber); }
  input[type=radio]:checked + .rating-fair,
  .rating-fair.selected { border-color: var(--amber); color: var(--amber); background: rgba(245,158,11,0.18); }
  /* Good */
  .rating-good { border-color: rgba(16,185,129,0.3); color: #0A8A62; background: rgba(16,185,129,0.08); }
  .rating-good:hover { border-color: rgba(16,185,129,0.6); color: var(--green); }
  input[type=radio]:checked + .rating-good,
  .rating-good.selected { border-color: var(--green); color: var(--green); background: rgba(16,185,129,0.18); }
  /* Can Be Improved */
  .rating-improve { border-color: rgba(239,68,68,0.3); color: #A83030; background: rgba(239,68,68,0.08); font-size: 10px; }
  .rating-improve:hover { border-color: rgba(239,68,68,0.6); color: var(--red); }
  input[type=radio]:checked + .rating-improve,
  .rating-improve.selected { border-color: var(--red); color: var(--red); background: rgba(239,68,68,0.18); }

  /* Feedback textarea */
  .feedback-input {
    width: 100%; background: rgba(255,255,255,0.04);
    border: 1px solid var(--border); border-radius: 6px;
    color: var(--white); font-family: 'Inter', sans-serif;
    font-size: 12px; padding: 7px 10px;
    resize: vertical; min-height: 44px; outline: none;
    transition: border-color 0.2s;
  }
  .feedback-input:focus { border-color: var(--blue-light); background: rgba(30,111,217,0.06); }
  .feedback-input::placeholder { color: rgba(139,168,196,0.5); }

  /* Verdict section */
  .verdict-section {
    margin-top: 16px; padding: 16px 20px;
    background: rgba(245,158,11,0.06);
    border: 1px solid rgba(245,158,11,0.2);
    border-radius: 10px;
  }
  .verdict-label { font-size: 12px; font-weight: 700; color: var(--amber); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 10px; }
  .verdict-options { display: flex; gap: 10px; flex-wrap: wrap; }
  .verdict-pill {
    cursor: pointer; padding: 7px 16px;
    border-radius: 8px; font-size: 12px; font-weight: 600;
    border: 1.5px solid transparent; transition: all 0.18s;
    user-select: none;
  }
  .verdict-pill input { display: none; }
  .v-high { border-color: rgba(16,185,129,0.3); color: #0A8A62; background: rgba(16,185,129,0.07); }
  .v-high:hover { border-color: var(--green); color: var(--green); }
  input[type=radio]:checked + .v-high { border-color: var(--green); color: var(--green); background: rgba(16,185,129,0.18); }
  .v-rec { border-color: rgba(59,143,255,0.3); color: #1A5FA8; background: rgba(59,143,255,0.07); }
  .v-rec:hover { border-color: var(--blue-light); color: var(--blue-light); }
  input[type=radio]:checked + .v-rec { border-color: var(--blue-light); color: var(--blue-light); background: rgba(59,143,255,0.18); }
  .v-needs { border-color: rgba(239,68,68,0.3); color: #A83030; background: rgba(239,68,68,0.07); }
  .v-needs:hover { border-color: var(--red); color: var(--red); }
  input[type=radio]:checked + .v-needs { border-color: var(--red); color: var(--red); background: rgba(239,68,68,0.18); }

  .overall-feedback {
    margin-top: 12px;
    width: 100%; background: rgba(255,255,255,0.04);
    border: 1px solid rgba(245,158,11,0.2); border-radius: 6px;
    color: var(--white); font-family: 'Inter', sans-serif;
    font-size: 13px; padding: 10px 12px;
    min-height: 60px; resize: vertical; outline: none;
    transition: border-color 0.2s;
  }
  .overall-feedback:focus { border-color: var(--amber); }
  .overall-feedback::placeholder { color: rgba(139,168,196,0.4); }

  /* Judge name row */
  .judge-meta-row {
    display: flex; align-items: center; gap: 20px;
    padding: 12px 20px;
    background: rgba(255,255,255,0.02);
    border-top: 1px solid var(--border);
    font-size: 12px; color: var(--muted);
  }
  .meta-field { display: flex; align-items: center; gap: 8px; }
  .meta-field span { white-space: nowrap; }

  /* ── BOTTOM BAR ── */
  .bottom-bar {
    position: fixed; bottom: 0; left: 0; right: 0;
    background: rgba(13,27,42,0.95);
    backdrop-filter: blur(12px);
    border-top: 1px solid var(--border);
    padding: 14px 40px;
    display: flex; align-items: center; justify-content: space-between;
    z-index: 100;
  }
  .nav-btns { display: flex; gap: 10px; }
  .btn {
    padding: 9px 22px; border-radius: 8px; border: none;
    font-family: 'Inter', sans-serif; font-size: 13px; font-weight: 600;
    cursor: pointer; transition: all 0.2s;
  }
  .btn-ghost { background: transparent; border: 1px solid var(--border); color: var(--muted); }
  .btn-ghost:hover { border-color: var(--muted); color: var(--white); }
  .btn-primary { background: linear-gradient(135deg, var(--blue), var(--blue-light)); color: white; }
  .btn-primary:hover { opacity: 0.88; transform: translateY(-1px); }
  .btn-success { background: linear-gradient(135deg, var(--green), #059669); color: white; }
  .btn-success:hover { opacity: 0.88; transform: translateY(-1px); }
  .btn-export { background: linear-gradient(135deg, #7C3AED, #A855F7); color: white; }
  .btn-export:hover { opacity: 0.88; transform: translateY(-1px); }
  .step-info { font-size: 12px; color: var(--muted); }
  .step-info strong { color: var(--white); }

  /* ── SUMMARY MODAL ── */
  .modal-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(0,0,0,0.7); backdrop-filter: blur(6px);
    z-index: 200; align-items: center; justify-content: center;
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 32px; width: 90%; max-width: 860px;
    max-height: 90vh; overflow-y: auto;
  }
  .modal h2 { font-size: 20px; font-weight: 700; margin-bottom: 6px; }
  .modal p { font-size: 13px; color: var(--muted); margin-bottom: 24px; }
  .summary-uc { margin-bottom: 24px; }
  .summary-uc h3 {
    font-size: 14px; font-weight: 700; color: var(--cyan);
    border-bottom: 1px solid var(--border); padding-bottom: 8px; margin-bottom: 12px;
  }
  .summary-row {
    display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 8px;
  }
  .summary-judge { background: var(--navy-mid); border-radius: 8px; padding: 12px 14px; }
  .summary-judge h4 { font-size: 12px; color: var(--muted); margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.5px; }
  .summary-criteria-row { display: flex; justify-content: space-between; align-items: center; margin-bottom: 4px; font-size: 12px; }
  .summary-criteria-name { color: var(--muted); }
  .badge { padding: 2px 8px; border-radius: 4px; font-size: 10px; font-weight: 700; }
  .badge-good { background: rgba(16,185,129,0.2); color: var(--green); }
  .badge-fair { background: rgba(245,158,11,0.2); color: var(--amber); }
  .badge-improve { background: rgba(239,68,68,0.2); color: var(--red); }
  .badge-none { background: rgba(139,168,196,0.1); color: var(--muted); }
  .verdict-badge { display: inline-block; padding: 4px 12px; border-radius: 6px; font-size: 12px; font-weight: 700; margin-top: 8px; }
  .verdict-high { background: rgba(16,185,129,0.2); color: var(--green); }
  .verdict-rec { background: rgba(59,143,255,0.2); color: var(--blue-light); }
  .verdict-needs { background: rgba(239,68,68,0.2); color: var(--red); }
  .verdict-none { background: rgba(139,168,196,0.1); color: var(--muted); }
  .modal-actions { display: flex; gap: 10px; margin-top: 24px; flex-wrap: wrap; }

  /* ── TOAST ── */
  .toast {
    position: fixed; bottom: 80px; right: 24px;
    background: var(--green); color: white;
    padding: 12px 20px; border-radius: 10px;
    font-size: 13px; font-weight: 600;
    transform: translateY(20px); opacity: 0;
    transition: all 0.3s; z-index: 300;
  }
  .toast.show { transform: translateY(0); opacity: 1; }

  /* Responsive */
  @media (max-width: 900px) {
    .judges-grid { grid-template-columns: 1fr; }
    .main { padding: 20px; }
    .tabs-bar { padding: 0 20px; }
    .site-header { padding: 16px 20px; }
    .uc-title-input { width: 100%; }
    .bottom-bar { padding: 12px 20px; flex-wrap: wrap; gap: 10px; }
  }
</style>
</head>
<body>

<!-- HEADER -->
<header class="site-header">
  <div class="header-left">
    <div class="header-icon">🤖</div>
    <div class="header-title">
      <h1>AI Hackathon — Judge Evaluation</h1>
      <p>Confidential · For judge use only</p>
    </div>
  </div>
  <div class="progress-wrap">
    <span class="progress-label">Overall completion</span>
    <div class="progress-bar"><div class="progress-fill" id="progressFill" style="width:0%"></div></div>
    <span class="progress-pct" id="progressPct">0%</span>
  </div>
</header>

<!-- TABS -->
<nav class="tabs-bar" id="tabsBar"></nav>

<!-- MAIN PANELS -->
<main class="main" id="mainPanels"></main>

<!-- BOTTOM BAR -->
<div class="bottom-bar">
  <div class="step-info" id="stepInfo"></div>
  <div class="nav-btns">
    <button class="btn btn-ghost" id="btnPrev" onclick="navigate(-1)">← Previous</button>
    <button class="btn btn-primary" id="btnNext" onclick="navigate(1)">Next →</button>
    <button class="btn btn-success" onclick="showSummary()">📋 Review & Export</button>
  </div>
</div>

<!-- SUMMARY MODAL -->
<div class="modal-overlay" id="summaryModal">
  <div class="modal">
    <h2>📋 Evaluation Summary</h2>
    <p>Review all scores before exporting. You can close this and continue editing.</p>
    <div id="summaryContent"></div>
    <div class="modal-actions">
      <button class="btn btn-export" onclick="exportCSV()">⬇ Export as CSV</button>
      <button class="btn btn-primary" onclick="printSummary()">🖨 Print Summary</button>
      <button class="btn btn-ghost" onclick="closeSummary()">Close</button>
    </div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
// ── CONFIG ──────────────────────────────────────────────────────────────
const NUM_USE_CASES = 9;
const USE_CASE_TITLES = [
  'AI-Powered Frontend Performance Autopilot',
  'Recurring Incident & Problem Mining Agent',
  'Production-Driven Test Strategy',
  'Invoice Validation & Auto-Submission Agent',
  'P1 War-Room Co-Pilot',
  'Automated PR Sign-off',
  'AI-Powered Micro-Video Generator',
  'Predictive Support & Glitch Detection',
  'KB Chatbot for Support Team',
];
const JUDGES = [
  { id: 'j1', label: 'Devvrat', initials: 'DV', class: 'judge-1' },
  { id: 'j2', label: 'Maanya', initials: 'MA', class: 'judge-2' },
];
const CRITERIA = [
  { id: 'problem',    name: 'Problem Relevance',   desc: 'Is the problem real, meaningful and clearly defined?' },
  { id: 'ai',         name: 'AI Innovation',        desc: 'Is AI used creatively and does it add genuine value?' },
  { id: 'technical',  name: 'Technical Execution',  desc: 'Quality of build, stability and working demo.' },
  { id: 'impact',     name: 'Impact & Scalability', desc: 'Real-world potential and ability to scale.' },
  { id: 'ux',         name: 'UX & Presentation',    desc: 'Clarity of demo, interface design and communication.' },
  { id: 'feasibility',name: 'Feasibility',           desc: 'Realistic to deploy? Data/infra/cost considered?' },
  { id: 'business',   name: 'Business Value',        desc: 'Clear ROI, revenue potential or cost savings.' },
];
const RATINGS = [
  { value: 'fair',    label: 'Fair',            cls: 'rating-fair' },
  { value: 'good',    label: 'Good',            cls: 'rating-good' },
  { value: 'improve', label: 'Can Be Improved', cls: 'rating-improve' },
];
const VERDICTS = [
  { value: 'highly', label: '⭐ Highly Recommended', cls: 'v-high' },
  { value: 'rec',    label: '👍 Recommended',         cls: 'v-rec' },
  { value: 'needs',  label: '🔧 Needs Work',          cls: 'v-needs' },
];

let currentUC = 0;
let state = {}; // state[ucIdx][judgeId] = { name, ratings: {criteriaId: val}, feedback: {criteriaId: text}, verdict, overallFeedback }

// ── INIT STATE ──────────────────────────────────────────────────────────
function initState() {
  for (let i = 0; i < NUM_USE_CASES; i++) {
    state[i] = {};
    JUDGES.forEach(j => {
      state[i][j.id] = { name: j.label, ratings: {}, feedback: {}, verdict: '', overallFeedback: '' };
    });
    state[i].ucTitle = USE_CASE_TITLES[i] || `Use Case ${i + 1}`;
  }
}

// ── BUILD UI ────────────────────────────────────────────────────────────
function buildUI() {
  const tabsBar = document.getElementById('tabsBar');
  const mainPanels = document.getElementById('mainPanels');
  tabsBar.innerHTML = '';
  mainPanels.innerHTML = '';

  for (let i = 0; i < NUM_USE_CASES; i++) {
    // Tab
    const tab = document.createElement('button');
    tab.className = 'tab-btn' + (i === 0 ? ' active' : '');
    tab.id = `tab-${i}`;
    const shortTitle = USE_CASE_TITLES[i] ? `UC${i+1}: ${USE_CASE_TITLES[i].split(' ').slice(0,3).join(' ')}…` : `Use Case ${i+1}`;
    tab.innerHTML = `${shortTitle} <span class="tab-badge" id="tabBadge-${i}">—</span>`;
    tab.onclick = () => switchTab(i);
    tabsBar.appendChild(tab);

    // Panel
    const panel = document.createElement('div');
    panel.className = 'panel' + (i === 0 ? ' active' : '');
    panel.id = `panel-${i}`;
    panel.innerHTML = buildPanel(i);
    mainPanels.appendChild(panel);
  }
}

function buildPanel(ucIdx) {
  const judgesHTML = JUDGES.map(j => buildJudgeCard(ucIdx, j)).join('');
  return `
    <div class="uc-header">
      <div class="uc-title-group">
        <h2>Use Case ${ucIdx + 1}</h2>
        <p>Complete all criteria for both judges</p>
      </div>
      <div class="uc-title-display" id="ucTitle-${ucIdx}"
        style="font-size:15px;font-weight:700;color:var(--cyan);padding:8px 0;">${USE_CASE_TITLES[ucIdx]}</div>
    </div>
    <div class="judges-grid">${judgesHTML}</div>
    <div style="height:80px"></div>
  `;
}

function buildJudgeCard(ucIdx, judge) {
  const criteriaRows = CRITERIA.map(c => buildCriteriaRow(ucIdx, judge, c)).join('');
  return `
    <div class="judge-card ${judge.class}" id="judgeCard-${ucIdx}-${judge.id}">
      <div class="judge-card-header">
        <div class="judge-avatar">${judge.initials}</div>
        <div>
          <input type="text" class="judge-name-input"
            id="judgeName-${ucIdx}-${judge.id}"
            placeholder="Enter judge name…"
            value="${judge.label}"
            oninput="onNameChange(${ucIdx}, '${judge.id}', this.value)" />
          <div style="font-size:11px;color:var(--muted);margin-top:2px">${judge.label}</div>
        </div>
        <span class="judge-completion" id="judgeComp-${ucIdx}-${judge.id}">0/${CRITERIA.length}</span>
      </div>

      <table class="criteria-table">
        <thead>
          <tr>
            <th>Criteria</th>
            <th class="center" colspan="3">Rating</th>
            <th>Feedback / Notes</th>
          </tr>
        </thead>
        <tbody>${criteriaRows}</tbody>
      </table>

      <div style="padding:0 16px 16px">
        <div class="verdict-section">
          <div class="verdict-label">Final Verdict</div>
          <div class="verdict-options">
            ${VERDICTS.map(v => `
              <label class="verdict-pill">
                <input type="radio" name="verdict-${ucIdx}-${judge.id}"
                  value="${v.value}"
                  onchange="onVerdictChange(${ucIdx},'${judge.id}','${v.value}')">
                <span class="${v.cls}">${v.label}</span>
              </label>
            `).join('')}
          </div>
          <textarea class="overall-feedback"
            id="overallFeedback-${ucIdx}-${judge.id}"
            placeholder="Overall summary comment for this use case…"
            oninput="onOverallFeedback(${ucIdx},'${judge.id}',this.value)"></textarea>
        </div>
      </div>

    </div>
  `;
}

function buildCriteriaRow(ucIdx, judge, criteria) {
  const ratingsHTML = RATINGS.map(r => `
    <td class="td-rating">
      <label class="rating-label">
        <input type="radio"
          name="rating-${ucIdx}-${judge.id}-${criteria.id}"
          value="${r.value}"
          onchange="onRatingChange(${ucIdx},'${judge.id}','${criteria.id}','${r.value}')">
        <span class="${r.cls}">${r.label}</span>
      </label>
    </td>
  `).join('');

  return `
    <tr>
      <td class="td-criteria">
        <div class="criteria-name">${criteria.name}</div>
        <div class="criteria-desc">${criteria.desc}</div>
      </td>
      ${ratingsHTML}
      <td class="td-feedback">
        <textarea class="feedback-input"
          id="feedback-${ucIdx}-${judge.id}-${criteria.id}"
          placeholder="Notes…"
          oninput="onFeedbackChange(${ucIdx},'${judge.id}','${criteria.id}',this.value)"></textarea>
      </td>
    </tr>
  `;
}

// ── EVENT HANDLERS ──────────────────────────────────────────────────────
function onTitleChange(ucIdx, value) {
  state[ucIdx].ucTitle = value;
  document.getElementById(`tab-${ucIdx}`).childNodes[0].textContent = value || `Use Case ${ucIdx + 1} `;
  updateProgress();
}
function onNameChange(ucIdx, judgeId, value) {
  state[ucIdx][judgeId].name = value;
}
function onRatingChange(ucIdx, judgeId, criteriaId, value) {
  state[ucIdx][judgeId].ratings[criteriaId] = value;
  updateJudgeCompletion(ucIdx, judgeId);
  updateProgress();
  updateTabBadge(ucIdx);
}
function onFeedbackChange(ucIdx, judgeId, criteriaId, value) {
  state[ucIdx][judgeId].feedback[criteriaId] = value;
}
function onVerdictChange(ucIdx, judgeId, value) {
  state[ucIdx][judgeId].verdict = value;
  updateProgress();
  updateTabBadge(ucIdx);
}
function onOverallFeedback(ucIdx, judgeId, value) {
  state[ucIdx][judgeId].overallFeedback = value;
}

// ── COMPLETION TRACKING ─────────────────────────────────────────────────
function updateJudgeCompletion(ucIdx, judgeId) {
  const filled = Object.keys(state[ucIdx][judgeId].ratings).length;
  document.getElementById(`judgeComp-${ucIdx}-${judgeId}`).textContent = `${filled}/${CRITERIA.length}`;
}

function ucCompletionScore(ucIdx) {
  let total = 0, filled = 0;
  JUDGES.forEach(j => {
    total += CRITERIA.length;
    filled += Object.keys(state[ucIdx][j.id].ratings).length;
  });
  return total === 0 ? 0 : filled / total;
}

function updateTabBadge(ucIdx) {
  const score = ucCompletionScore(ucIdx);
  const badge = document.getElementById(`tabBadge-${ucIdx}`);
  const tab = document.getElementById(`tab-${ucIdx}`);
  if (score === 1) {
    badge.textContent = '✓';
    tab.classList.add('done');
  } else if (score > 0) {
    badge.textContent = `${Math.round(score * 100)}%`;
    tab.classList.remove('done');
  } else {
    badge.textContent = '—';
    tab.classList.remove('done');
  }
}

function updateProgress() {
  let total = 0, filled = 0;
  for (let i = 0; i < NUM_USE_CASES; i++) {
    JUDGES.forEach(j => {
      total += CRITERIA.length;
      filled += Object.keys(state[i][j.id].ratings).length;
    });
  }
  const pct = total === 0 ? 0 : Math.round((filled / total) * 100);
  document.getElementById('progressFill').style.width = pct + '%';
  document.getElementById('progressPct').textContent = pct + '%';
}

// ── NAVIGATION ──────────────────────────────────────────────────────────
function switchTab(idx) {
  document.querySelectorAll('.tab-btn').forEach((t, i) => t.classList.toggle('active', i === idx));
  document.querySelectorAll('.panel').forEach((p, i) => p.classList.toggle('active', i === idx));
  currentUC = idx;
  updateStepInfo();
}
function navigate(dir) {
  const next = Math.max(0, Math.min(NUM_USE_CASES - 1, currentUC + dir));
  switchTab(next);
}
function updateStepInfo() {
  document.getElementById('stepInfo').innerHTML =
    `Use case <strong>${currentUC + 1}</strong> of <strong>${NUM_USE_CASES}</strong>`;
  document.getElementById('btnPrev').disabled = currentUC === 0;
  document.getElementById('btnNext').style.display = currentUC === NUM_USE_CASES - 1 ? 'none' : '';
}

// ── SUMMARY ─────────────────────────────────────────────────────────────
function showSummary() {
  const content = document.getElementById('summaryContent');
  content.innerHTML = Array.from({ length: NUM_USE_CASES }, (_, i) => {
    const ucTitle = state[i].ucTitle || `Use Case ${i + 1}`;
    const judgesHTML = JUDGES.map(j => {
      const jState = state[i][j.id];
      const criteriaHTML = CRITERIA.map(c => {
        const r = jState.ratings[c.id];
        const badgeCls = r === 'good' ? 'badge-good' : r === 'fair' ? 'badge-fair' : r === 'improve' ? 'badge-improve' : 'badge-none';
        const label = r === 'good' ? 'Good' : r === 'fair' ? 'Fair' : r === 'improve' ? 'Can Be Improved' : '—';
        return `<div class="summary-criteria-row"><span class="summary-criteria-name">${c.name}</span><span class="badge ${badgeCls}">${label}</span></div>`;
      }).join('');
      const vLabel = jState.verdict === 'highly' ? '⭐ Highly Recommended' : jState.verdict === 'rec' ? '👍 Recommended' : jState.verdict === 'needs' ? '🔧 Needs Work' : null;
      const vCls = jState.verdict === 'highly' ? 'verdict-high' : jState.verdict === 'rec' ? 'verdict-rec' : jState.verdict === 'needs' ? 'verdict-needs' : 'verdict-none';
      return `
        <div class="summary-judge">
          <h4>${jState.name || j.label}</h4>
          ${criteriaHTML}
          ${vLabel ? `<div class="verdict-badge ${vCls}">${vLabel}</div>` : '<div class="verdict-badge verdict-none">No verdict yet</div>'}
          ${jState.overallFeedback ? `<p style="font-size:12px;color:var(--muted);margin-top:8px">${jState.overallFeedback}</p>` : ''}
        </div>`;
    }).join('');
    return `
      <div class="summary-uc">
        <h3>${ucTitle}</h3>
        <div class="summary-row">${judgesHTML}</div>
      </div>`;
  }).join('');
  document.getElementById('summaryModal').classList.add('open');
}
function closeSummary() {
  document.getElementById('summaryModal').classList.remove('open');
}

// ── CSV EXPORT ───────────────────────────────────────────────────────────
function exportCSV() {
  const rows = [['Use Case', 'Judge', 'Judge Name', 'Criteria', 'Rating', 'Feedback', 'Verdict', 'Overall Feedback']];
  for (let i = 0; i < NUM_USE_CASES; i++) {
    const ucTitle = state[i].ucTitle || `Use Case ${i + 1}`;
    JUDGES.forEach(j => {
      const jState = state[i][j.id];
      CRITERIA.forEach(c => {
        rows.push([
          ucTitle,
          j.label,
          jState.name || '',
          c.name,
          jState.ratings[c.id] || '',
          (jState.feedback[c.id] || '').replace(/"/g, '""'),
          jState.verdict || '',
          (jState.overallFeedback || '').replace(/"/g, '""'),
        ]);
      });
    });
  }
  const csv = rows.map(r => r.map(v => `"${v}"`).join(',')).join('\n');
  const blob = new Blob([csv], { type: 'text/csv' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'AI_Hackathon_Evaluations.csv';
  a.click();
  showToast('CSV exported successfully!');
}

// ── PRINT ────────────────────────────────────────────────────────────────
function printSummary() {
  window.print();
}

// ── TOAST ────────────────────────────────────────────────────────────────
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 3000);
}

// ── BOOT ─────────────────────────────────────────────────────────────────
initState();
buildUI();
switchTab(0);

</script>
</body>
</html>
