<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Interactive AI Pipeline</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Fira+Code:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #060610;
  --surface: #0d0d1a;
  --card: #111125;
  --border: #1a1a35;
  --accent: #0ff;
  --accent2: #f0f;
  --accent3: #ff9500;
  --genai: #00ffcc;
  --trad: #ff6b35;
  --lookup: #b48eff;
  --text: #dde2ff;
  --muted: #555577;
  --glow: rgba(0,255,255,0.15);
}

* { margin:0; padding:0; box-sizing:border-box; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Fira Code', monospace;
  min-height: 100vh;
  overflow-x: hidden;
}

/* ── ANIMATED BACKGROUND GRID ── */
body::before {
  content:'';
  position:fixed;
  inset:0;
  background-image:
    linear-gradient(rgba(0,255,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,255,255,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events:none;
  z-index:0;
}

/* ── SCANNING LINE ── */
body::after {
  content:'';
  position:fixed;
  left:0; right:0;
  height:2px;
  background: linear-gradient(90deg, transparent, rgba(0,255,255,0.4), transparent);
  animation: scan 6s linear infinite;
  pointer-events:none;
  z-index:0;
}
@keyframes scan { from{top:-2px} to{top:100vh} }

.wrapper {
  position:relative;
  z-index:1;
  max-width:1200px;
  margin:0 auto;
  /*padding:40px 24px 80px;*/
}

/* ── HEADER ── */
header { text-align:center; margin-bottom:60px; }
.top-label {
  display:inline-flex; align-items:center; gap:8px;
  font-size:10px; letter-spacing:0.3em; text-transform:uppercase;
  color:var(--accent); margin-bottom:20px;
}
.top-label::before, .top-label::after {
  content:''; width:30px; height:1px; background:var(--accent);
}
h1 {
  font-family:'Syne', sans-serif;
  font-size:clamp(24px,5vw,48px);
  font-weight:800;
  color:#fff;
  line-height:1.1;
}
h1 em { color:var(--accent); font-style:normal; }
.subtitle {
  margin-top:12px;
  font-size:11px;
  color:var(--muted);
  letter-spacing:0.12em;
}
.hint {
  margin-top:16px;
  display:inline-flex; align-items:center; gap:8px;
  font-size:11px; color:var(--muted);
  border:1px solid var(--border);
  padding:6px 14px; border-radius:20px;
  animation: pulse-hint 2s ease infinite;
}
@keyframes pulse-hint {
  0%,100%{border-color:var(--border);}
  50%{border-color:rgba(0,255,255,0.3);}
}

/* ── TABS ── */
.tabs {
  display:flex; gap:4px;
  margin-bottom:32px;
  border-bottom:1px solid var(--border);
  padding-bottom:0;
}
.tab-btn {
  font-family:'Syne',sans-serif;
  font-size:12px; font-weight:600;
  letter-spacing:0.1em;
  text-transform:uppercase;
  padding:10px 20px;
  background:none;
  border:none; border-bottom:2px solid transparent;
  color:var(--muted);
  cursor:pointer;
  transition:all 0.2s;
  position:relative; bottom:-1px;
}
.tab-btn.active { color:var(--accent); border-bottom-color:var(--accent); }
.tab-btn:hover:not(.active) { color:var(--text); }

.tab-panel { display:none; }
.tab-panel.active { display:block; }

/* ── PIPELINE DIAGRAM ── */
.pipeline-wrap {
  position:relative;
  margin-bottom:40px;
}

/* Animated data packet travelling along pipeline */
.data-flow-track {
  position:absolute;
  top:50%; left:0; right:0;
  height:2px;
  transform:translateY(-50%);
  pointer-events:none;
  overflow:hidden;
  border-radius:2px;
}
.data-packet {
  position:absolute;
  width:40px; height:4px;
  background:linear-gradient(90deg, transparent, var(--accent), transparent);
  border-radius:2px;
  top:-1px;
  animation: packet 3s linear infinite;
  box-shadow:0 0 8px var(--accent);
}
@keyframes packet { from{left:-40px} to{left:100%} }

.pipeline {
  display:flex;
  align-items:center;
  gap:0;
  position:relative;
}

/* Connector line */
.connector {
  flex:1;
  height:2px;
  background:linear-gradient(90deg, var(--border), rgba(0,255,255,0.2), var(--border));
  position:relative;
  min-width:20px;
}
.connector::after {
  content:'▶';
  position:absolute;
  right:-8px; top:50%;
  transform:translateY(-50%);
  font-size:10px;
  color:var(--accent);
  opacity:0.6;
}

.pipe-node {
  width:130px;
  flex-shrink:0;
  background:var(--card);
  border:1px solid var(--border);
  border-radius:10px;
  padding:18px 14px;
  cursor:pointer;
  transition:all 0.25s ease;
  position:relative;
  text-align:center;
}
.pipe-node:hover, .pipe-node.active {
  border-color:var(--accent);
  box-shadow:0 0 24px rgba(0,255,255,0.2), inset 0 0 20px rgba(0,255,255,0.04);
  transform:translateY(-4px);
}
.pipe-node.active::before {
  content:'';
  position:absolute;
  inset:-1px; border-radius:10px;
  background:linear-gradient(135deg, rgba(0,255,255,0.1), transparent);
  pointer-events:none;
}
.pipe-node .node-icon {
  font-size:26px;
  display:block;
  margin-bottom:8px;
  filter:drop-shadow(0 0 6px rgba(0,255,255,0.3));
}
.pipe-node .node-title {
  font-family:'Syne',sans-serif;
  font-size:11px;
  font-weight:700;
  color:#fff;
  line-height:1.3;
}
.pipe-node .node-sub {
  font-size:9px;
  color:var(--muted);
  margin-top:4px;
  letter-spacing:0.05em;
}
.node-pulse {
  position:absolute;
  top:8px; right:8px;
  width:7px; height:7px;
  border-radius:50%;
  background:var(--accent);
  box-shadow:0 0 6px var(--accent);
}
.node-pulse::after {
  content:'';
  position:absolute;
  inset:-3px; border-radius:50%;
  border:1px solid var(--accent);
  animation:ripple 2s ease infinite;
}
@keyframes ripple {
  0%{transform:scale(1);opacity:1}
  100%{transform:scale(2.5);opacity:0}
}

/* ── DETAIL PANEL ── */
.detail-panel {
  background:var(--card);
  border:1px solid var(--border);
  border-radius:12px;
  padding:28px;
  margin-top:24px;
  animation:slideIn 0.3s ease;
  min-height:180px;
  position:relative;
  overflow:hidden;
}
.detail-panel::before {
  content:'';
  position:absolute;
  top:0; left:0; right:0; height:2px;
  background:linear-gradient(90deg,var(--accent),var(--accent2));
}
@keyframes slideIn {
  from{opacity:0;transform:translateY(10px)}
  to{opacity:1;transform:translateY(0)}
}
.detail-panel .dp-header {
  display:flex; align-items:center; gap:16px;
  margin-bottom:20px;
}
.dp-icon { font-size:36px; }
.dp-title {
  font-family:'Syne',sans-serif;
  font-size:20px; font-weight:800;
  color:#fff;
}
.dp-subtitle { font-size:11px; color:var(--accent); margin-top:2px; letter-spacing:0.1em; }
.dp-body { font-size:12px; color:var(--text); line-height:1.8; }
.dp-tags { display:flex; flex-wrap:wrap; gap:8px; margin-top:16px; }
.dp-tag {
  font-size:10px;
  padding:4px 12px;
  border-radius:4px;
  letter-spacing:0.08em;
}
.dp-tag.green { background:rgba(0,255,204,0.12); color:var(--genai); border:1px solid rgba(0,255,204,0.25); }
.dp-tag.purple { background:rgba(180,142,255,0.12); color:var(--lookup); border:1px solid rgba(180,142,255,0.25); }
.dp-tag.orange { background:rgba(255,107,53,0.12); color:var(--trad); border:1px solid rgba(255,107,53,0.25); }
.dp-tag.cyan { background:rgba(0,255,255,0.1); color:var(--accent); border:1px solid rgba(0,255,255,0.2); }

.dp-default {
  text-align:center;
  padding:30px;
  color:var(--muted);
}
.dp-default .arrow { font-size:24px; margin-bottom:10px; opacity:0.4; }

/* ── ARCHITECTURE ── */
.arch-grid {
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
  gap:16px;
}
.arch-card {
  background:var(--card);
  border:1px solid var(--border);
  border-radius:10px;
  padding:20px;
  cursor:pointer;
  transition:all 0.25s;
  position:relative;
  overflow:hidden;
}
.arch-card:hover {
  transform:translateY(-3px);
  border-color:rgba(0,255,255,0.4);
  box-shadow:0 8px 32px rgba(0,0,0,0.4);
}
.arch-card::after {
  content:'';
  position:absolute;
  top:0; left:0; right:0; height:2px;
}
.arch-card:nth-child(1)::after{background:var(--accent);}
.arch-card:nth-child(2)::after{background:var(--accent2);}
.arch-card:nth-child(3)::after{background:var(--accent3);}
.arch-card:nth-child(4)::after{background:var(--genai);}
.arch-card:nth-child(5)::after{background:var(--lookup);}

.arch-num {
  font-family:'Syne',sans-serif;
  font-size:48px; font-weight:800;
  opacity:0.05; position:absolute;
  top:4px; right:10px; color:#fff;
  line-height:1;
}
.arch-icon { font-size:28px; margin-bottom:10px; }
.arch-title {
  font-family:'Syne',sans-serif;
  font-size:13px; font-weight:700;
  color:#fff; margin-bottom:8px;
}
.arch-desc { font-size:11px; color:var(--muted); line-height:1.7; }

/* ── PROMPT TABLE ── */
.prompt-section {}
.prompt-intro {
  font-size:12px; color:var(--muted);
  margin-bottom:24px; line-height:1.8;
}

.prompt-cards { display:flex; flex-direction:column; gap:12px; }
.prompt-card {
  background:var(--card);
  border:1px solid var(--border);
  border-radius:8px;
  padding:18px 20px;
  display:grid;
  grid-template-columns:32px 1fr auto auto auto;
  align-items:center;
  gap:16px;
  cursor:pointer;
  transition:all 0.2s;
}
.prompt-card:hover {
  border-color:rgba(0,255,255,0.3);
  background:#13132a;
}
.prompt-card.expanded { border-color:var(--accent); }

.pnum {
  font-family:'Syne',sans-serif;
  font-size:16px; font-weight:800;
  color:var(--muted);
}
.ptext { font-size:12px; color:#fff; }
.ptext em { font-style:normal; color:var(--muted); font-size:11px; display:block; margin-top:3px; }

.chip {
  font-size:9px; font-weight:600;
  padding:4px 10px; border-radius:3px;
  letter-spacing:0.1em; text-transform:uppercase;
  white-space:nowrap;
}
.chip-genai { background:rgba(0,255,204,0.12); color:var(--genai); border:1px solid rgba(0,255,204,0.3); }
.chip-trad { background:rgba(255,107,53,0.12); color:var(--trad); border:1px solid rgba(255,107,53,0.3); }
.chip-lookup { background:rgba(180,142,255,0.12); color:var(--lookup); border:1px solid rgba(180,142,255,0.3); }

.ptask {
  font-size:10px; color:var(--muted);
  white-space:nowrap;
}

.pexpand {
  font-size:16px; color:var(--muted);
  transition:transform 0.2s;
}
.prompt-card.expanded .pexpand { transform:rotate(180deg); color:var(--accent); }

.prompt-detail {
  display:none;
  grid-column:1/-1;
  padding-top:14px;
  border-top:1px solid var(--border);
  margin-top:6px;
  font-size:11px;
  color:var(--text);
  line-height:1.8;
}
.prompt-card.expanded .prompt-detail { display:block; }

.pd-grid { display:grid; grid-template-columns:1fr 1fr 1fr; gap:16px; }
.pd-box {
  background:rgba(255,255,255,0.02);
  border:1px solid var(--border);
  border-radius:6px;
  padding:12px;
}
.pd-label { font-size:9px; color:var(--accent); letter-spacing:0.15em; text-transform:uppercase; margin-bottom:6px; }
.pd-value { font-size:11px; color:#fff; line-height:1.6; }

/* ── LEGEND ── */
.legend {
  display:flex; gap:20px; flex-wrap:wrap;
  margin-top:24px;
  padding:14px 18px;
  background:var(--card);
  border:1px solid var(--border);
  border-radius:8px;
}
.legend-item { display:flex; align-items:center; gap:8px; font-size:11px; color:var(--muted); }
.ldot { width:8px; height:8px; border-radius:2px; }

/* ── FLOW ANIMATION ── */
.flow-demo {
  background:var(--card);
  border:1px solid var(--border);
  border-radius:10px;
  padding:20px;
  margin-top:28px;
}
.flow-title {
  font-family:'Syne',sans-serif;
  font-size:11px; font-weight:700;
  color:var(--accent); letter-spacing:0.15em;
  text-transform:uppercase;
  margin-bottom:16px;
}
.flow-steps {
  display:flex;
  flex-direction:column;
  gap:8px;
}
.flow-step {
  display:flex; align-items:center; gap:14px;
  font-size:11px;
  opacity:0.3;
  transition:opacity 0.5s, transform 0.5s;
  transform:translateX(-8px);
}
.flow-step.active { opacity:1; transform:translateX(0); }
.flow-step.done { opacity:0.5; }
.fs-dot {
  width:8px; height:8px; border-radius:50%;
  background:var(--accent); flex-shrink:0;
  box-shadow:0 0 6px var(--accent);
}
.flow-step.done .fs-dot { background:var(--muted); box-shadow:none; }
.fs-bar {
  flex:1; height:1px;
  background:linear-gradient(90deg, var(--accent), transparent);
  opacity:0.4;
}

/* ── RESPONSIVE ── */
@media(max-width:700px){
  .pipeline { flex-direction:column; align-items:stretch; }
  .connector { width:2px; height:24px; align-self:center; flex:none;
    background:linear-gradient(var(--border),rgba(0,255,255,0.2),var(--border)); }
  .connector::after { content:'▼'; right:unset; top:unset; bottom:-10px; left:50%; transform:translateX(-50%); }
  .pipe-node { width:100%; text-align:left; display:flex; align-items:center; gap:14px; }
  .pipe-node .node-icon { font-size:22px; margin:0; }
  .prompt-card { grid-template-columns:28px 1fr; }
  .chip,.ptask,.pexpand { display:none; }
  .prompt-card.expanded .chip,
  .prompt-card.expanded .ptask,
  .prompt-card.expanded .pexpand { display:inline-flex; }
  .pd-grid { grid-template-columns:1fr; }
  .data-flow-track { display:none; }
}
</style>
</head>
<body>
<div class="wrapper">

  <!-- HEADER -->
  <header>
    <!--div class="top-label">AI Systems Reference</div-->
    <h1>End-to-End <em>AI Pipeline</em></h1>
    <p class="subtitle">click any component to explore · interactive diagram</p>
    <p class="hint">👆 Click nodes to see detailed explanations</p>
  </header>

  <!-- TABS -->
  <div class="tabs">
    <button class="tab-btn active" onclick="switchTab('pipeline')">① Pipeline Flow</button>
    <button class="tab-btn" onclick="switchTab('architecture')">② Architecture</button>
    <button class="tab-btn" onclick="switchTab('prompts')">③ Prompt Classifier</button>
  </div>

  <!-- ═══════════════════════════════════════════════ -->
  <!-- TAB 1: PIPELINE -->
  <!-- ═══════════════════════════════════════════════ -->
  <div class="tab-panel active" id="tab-pipeline">

    <div class="pipeline-wrap">
      <!-- Animated data line -->
      <div class="data-flow-track">
        <div class="data-packet"></div>
        <div class="data-packet" style="animation-delay:1s"></div>
        <div class="data-packet" style="animation-delay:2s"></div>
      </div>

      <div class="pipeline">

        <div class="pipe-node" id="node-input" onclick="showDetail('input')">
          <div class="node-pulse"></div>
          <span class="node-icon">⌨️</span>
          <div class="node-title">User Input</div>
          <div class="node-sub">Prompt</div>
        </div>

        <div class="connector"></div>

        <div class="pipe-node" id="node-ui" onclick="showDetail('ui')">
          <span class="node-icon">🌐</span>
          <div class="node-title">Web Interface</div>
          <div class="node-sub">UI Layer</div>
        </div>

        <div class="connector"></div>

        <div class="pipe-node" id="node-app" onclick="showDetail('app')">
          <span class="node-icon">⚙️</span>
          <div class="node-title">Application Layer</div>
          <div class="node-sub">Logic & Routing</div>
        </div>

        <div class="connector"></div>

        <div class="pipe-node" id="node-llm" onclick="showDetail('llm')">
          <span class="node-icon">🧠</span>
          <div class="node-title">LLM / Model</div>
          <div class="node-sub">Transformer</div>
        </div>

        <div class="connector"></div>

        <div class="pipe-node" id="node-cloud" onclick="showDetail('cloud')">
          <span class="node-icon">☁️</span>
          <div class="node-title">Cloud Models</div>
          <div class="node-sub">DALL-E etc.</div>
        </div>

        <div class="connector"></div>

        <div class="pipe-node" id="node-output" onclick="showDetail('output')">
          <span class="node-icon">📤</span>
          <div class="node-title">Output</div>
          <div class="node-sub">Response</div>
        </div>

      </div>
    </div>

    <!-- Detail Panel -->
    <div class="detail-panel" id="detail-panel">
      <div class="dp-default">
        <div class="arrow">↑</div>
        <div>Click any node above to see details</div>
      </div>
    </div>

    <!-- Live Flow Demo -->
    <div class="flow-demo">
      <div class="flow-title">▶ Live Flow Simulation</div>
      <div class="flow-steps" id="flow-steps">
        <div class="flow-step" id="fs0">
          <div class="fs-dot"></div>
          <div style="flex:1">User types: <span style="color:var(--accent)">"Generate an image of a sunset"</span></div>
        </div>
        <div class="flow-step" id="fs1">
          <div class="fs-dot"></div>
          <div style="flex:1">Web interface captures input, sends HTTP request to application layer</div>
          <div class="fs-bar"></div>
        </div>
        <div class="flow-step" id="fs2">
          <div class="fs-dot"></div>
          <div style="flex:1">App layer detects image-generation task → routes to DALL-E API</div>
          <div class="fs-bar"></div>
        </div>
        <div class="flow-step" id="fs3">
          <div class="fs-dot"></div>
          <div style="flex:1">LLM parses and enriches the prompt using transformer attention</div>
          <div class="fs-bar"></div>
        </div>
        <div class="flow-step" id="fs4">
          <div class="fs-dot"></div>
          <div style="flex:1">DALL-E model generates image in cloud → returns URL</div>
          <div class="fs-bar"></div>
        </div>
        <div class="flow-step" id="fs5">
          <div class="fs-dot"></div>
          <div style="flex:1">✅ Image displayed to user in browser — <span style="color:var(--genai)">GenAI: Image Generation</span></div>
        </div>
      </div>
      <button onclick="runFlow()" id="flow-btn" style="
        margin-top:16px; font-family:'Fira Code',monospace; font-size:11px;
        background:rgba(0,255,255,0.1); color:var(--accent);
        border:1px solid rgba(0,255,255,0.3); border-radius:6px;
        padding:8px 18px; cursor:pointer; transition:all 0.2s;
        letter-spacing:0.1em;
      " onmouseover="this.style.background='rgba(0,255,255,0.2)'"
         onmouseout="this.style.background='rgba(0,255,255,0.1)'">▶ Run Simulation</button>
    </div>

  </div>

  <!-- ═══════════════════════════════════════════════ -->
  <!-- TAB 2: ARCHITECTURE -->
  <!-- ═══════════════════════════════════════════════ -->
  <div class="tab-panel" id="tab-architecture">
    <div class="arch-grid">

      <div class="arch-card" onclick="toggleArch(this)">
        <div class="arch-num">01</div>
        <div class="arch-icon">🏗️</div>
        <div class="arch-title">Transformer Architecture</div>
        <div class="arch-desc">The foundational neural network design behind modern LLMs. Processes all input tokens <em>in parallel</em> using attention mechanisms — not sequentially like older RNNs. This parallelism makes training on massive data practical.</div>
      </div>

      <div class="arch-card" onclick="toggleArch(this)">
        <div class="arch-num">02</div>
        <div class="arch-icon">👁️</div>
        <div class="arch-title">Self-Attention</div>
        <div class="arch-desc">Allows each token to "look at" every other token in the sequence, computing relevance scores. This is what lets the model understand that "it" in "The cat sat because it was tired" refers to "the cat" — even across long distances.</div>
      </div>

      <div class="arch-card" onclick="toggleArch(this)">
        <div class="arch-num">03</div>
        <div class="arch-icon">🧠</div>
        <div class="arch-title">Large Language Model</div>
        <div class="arch-desc">Trained on billions of text tokens, LLMs (Claude, GPT-4, Gemini) can generate coherent text, answer questions, summarize, translate, and reason. They predict the next most likely token given all prior context.</div>
      </div>

      <div class="arch-card" onclick="toggleArch(this)">
        <div class="arch-num">04</div>
        <div class="arch-icon">🎨</div>
        <div class="arch-title">Image Models (DALL-E)</div>
        <div class="arch-desc">Diffusion models learn to remove noise from images iteratively. Given a text prompt, they reverse the noise process to generate brand-new images that match the description — a completely different paradigm from LLMs.</div>
      </div>

      <div class="arch-card" onclick="toggleArch(this)">
        <div class="arch-num">05</div>
        <div class="arch-icon">📊</div>
        <div class="arch-title">Traditional ML Models</div>
        <div class="arch-desc">Classical algorithms (SVM, Naive Bayes, Random Forests, BERT fine-tuned classifiers) for structured tasks. They're trained on labeled examples to classify, detect spam, score sentiment, or predict churn — no generation involved.</div>
      </div>

    </div>
  </div>

  <!-- ═══════════════════════════════════════════════ -->
  <!-- TAB 3: PROMPTS -->
  <!-- ═══════════════════════════════════════════════ -->
  <div class="tab-panel" id="tab-prompts">
    <p class="prompt-intro">
      Click any prompt to expand its full classification breakdown — including AI type, task category, which model handles it, and how data flows through the pipeline.
    </p>

    <div class="prompt-cards">

      <div class="prompt-card" onclick="togglePrompt(this)">
        <div class="pnum">01</div>
        <div class="ptext">"Generate an image of a sunset over mountains"
          <em>GenAI → Image Generation</em>
        </div>
        <span class="chip chip-genai">GenAI</span>
        <span class="ptask">🎨 Image Gen</span>
        <span class="pexpand">▼</span>
        <div class="prompt-detail">
          <div class="pd-grid">
            <div class="pd-box">
              <div class="pd-label">AI Type</div>
              <div class="pd-value" style="color:var(--genai)">Generative AI</div>
              <div class="pd-value" style="margin-top:4px">Creates brand-new content that didn't exist before — a generated image unique to this prompt.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Model Used</div>
              <div class="pd-value">DALL-E 3 / Midjourney / Stable Diffusion</div>
              <div class="pd-value" style="margin-top:4px;color:var(--muted)">Diffusion-based image generation model.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Pipeline Path</div>
              <div class="pd-value">Input → UI → App detects image task → Routes to image model API → Generated image → Output</div>
            </div>
          </div>
        </div>
      </div>

      <div class="prompt-card" onclick="togglePrompt(this)">
        <div class="pnum">02</div>
        <div class="ptext">"Classify this email as spam or not spam"
          <em>Traditional AI → Classification</em>
        </div>
        <span class="chip chip-trad">Traditional AI</span>
        <span class="ptask">🏷️ Classification</span>
        <span class="pexpand">▼</span>
        <div class="prompt-detail">
          <div class="pd-grid">
            <div class="pd-box">
              <div class="pd-label">AI Type</div>
              <div class="pd-value" style="color:var(--trad)">Traditional AI</div>
              <div class="pd-value" style="margin-top:4px">Trained classifier predicts a discrete label from a fixed set (spam / not spam) — no generation.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Model Used</div>
              <div class="pd-value">Naive Bayes, SVM, or fine-tuned BERT classifier</div>
              <div class="pd-value" style="margin-top:4px;color:var(--muted)">Assigns probability scores to each class.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Pipeline Path</div>
              <div class="pd-value">Input → UI → App → ML Classifier model → Binary label output → Display result</div>
            </div>
          </div>
        </div>
      </div>

      <div class="prompt-card" onclick="togglePrompt(this)">
        <div class="pnum">03</div>
        <div class="ptext">"Summarize this 10-page research paper"
          <em>GenAI → Summarization</em>
        </div>
        <span class="chip chip-genai">GenAI</span>
        <span class="ptask">📝 Summarization</span>
        <span class="pexpand">▼</span>
        <div class="prompt-detail">
          <div class="pd-grid">
            <div class="pd-box">
              <div class="pd-label">AI Type</div>
              <div class="pd-value" style="color:var(--genai)">Generative AI</div>
              <div class="pd-value" style="margin-top:4px">The model generates a new condensed text, not just copying — it reasons about importance and restructures.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Model Used</div>
              <div class="pd-value">Claude, GPT-4, Gemini (long-context LLM)</div>
              <div class="pd-value" style="margin-top:4px;color:var(--muted)">Needs large context window to process full document.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Pipeline Path</div>
              <div class="pd-value">Document uploaded → App chunks text → LLM processes via transformer → Generated summary → Output</div>
            </div>
          </div>
        </div>
      </div>

      <div class="prompt-card" onclick="togglePrompt(this)">
        <div class="pnum">04</div>
        <div class="ptext">"What is the capital of France?"
          <em>Factual Q&A → Knowledge Lookup</em>
        </div>
        <span class="chip chip-lookup">Factual Q&A</span>
        <span class="ptask">🔍 Lookup</span>
        <span class="pexpand">▼</span>
        <div class="prompt-detail">
          <div class="pd-grid">
            <div class="pd-box">
              <div class="pd-label">AI Type</div>
              <div class="pd-value" style="color:var(--lookup)">Factual Q&A</div>
              <div class="pd-value" style="margin-top:4px">Retrieves a stored fact from training data. Not generation (answer is fixed), not classification (no label set).</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Model Used</div>
              <div class="pd-value">LLM (knowledge stored in weights) or Search + RAG</div>
              <div class="pd-value" style="margin-top:4px;color:var(--muted)">Simple facts often answered without search.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Pipeline Path</div>
              <div class="pd-value">Question → LLM recalls from parametric memory → Outputs factual answer directly</div>
            </div>
          </div>
        </div>
      </div>

      <div class="prompt-card" onclick="togglePrompt(this)">
        <div class="pnum">05</div>
        <div class="ptext">"Is this product review positive or negative?"
          <em>Traditional AI → Sentiment Analysis</em>
        </div>
        <span class="chip chip-trad">Traditional AI</span>
        <span class="ptask">💬 Sentiment</span>
        <span class="pexpand">▼</span>
        <div class="prompt-detail">
          <div class="pd-grid">
            <div class="pd-box">
              <div class="pd-label">AI Type</div>
              <div class="pd-value" style="color:var(--trad)">Traditional AI</div>
              <div class="pd-value" style="margin-top:4px">A form of classification — maps input text to a sentiment label. Dedicated models outperform general LLMs for this task.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Model Used</div>
              <div class="pd-value">VADER, BERT-sentiment, RoBERTa-sentiment</div>
              <div class="pd-value" style="margin-top:4px;color:var(--muted)">Fine-tuned on sentiment-labeled datasets.</div>
            </div>
            <div class="pd-box">
              <div class="pd-label">Pipeline Path</div>
              <div class="pd-value">Review text → Tokenized → Sentiment classifier → Positive/Negative/Neutral score → Output label</div>
            </div>
          </div>
        </div>
      </div>

    </div>

    <div class="legend">
      <div class="legend-item"><div class="ldot" style="background:var(--genai)"></div> GenAI — generates new content (text, images, audio)</div>
      <div class="legend-item"><div class="ldot" style="background:var(--trad)"></div> Traditional AI — classifies / predicts from fixed labels</div>
      <div class="legend-item"><div class="ldot" style="background:var(--lookup)"></div> Factual Q&A — retrieves known information from memory</div>
    </div>
  </div>

</div>

<script>
// ── NODE DETAIL DATA ──
const details = {
  input: {
    icon:'⌨️',
    title:'User Input',
    sub:'ENTRY POINT',
    body:'The user types a natural language prompt into the chat interface. This can be a question, a command, a creative request, or any text. The raw input is sent as a string to the web interface layer. Nothing is processed here yet — it is purely capturing what the user wants.',
    tags:[{t:'Text Prompt',c:'cyan'},{t:'Voice Input',c:'cyan'},{t:'Image Upload',c:'cyan'},{t:'Entry Point',c:'purple'}]
  },
  ui: {
    icon:'🌐',
    title:'Web Interface',
    sub:'UI LAYER',
    body:'The browser-based or mobile chat UI (like Claude.ai) captures the prompt and sends it via an HTTP POST request to the application backend. It handles rendering the response back to the user once received — streaming tokens in real time if supported.',
    tags:[{t:'HTTP Request',c:'cyan'},{t:'Token Streaming',c:'cyan'},{t:'React / HTML',c:'purple'},{t:'API Gateway',c:'purple'}]
  },
  app: {
    icon:'⚙️',
    title:'Application Layer',
    sub:'LOGIC & ROUTING',
    body:'The backend application receives the prompt and makes routing decisions. It decides which model to call (LLM for text, DALL-E for images, classifier for labels), handles authentication, applies system prompts, manages conversation history, and formats the final response.',
    tags:[{t:'Prompt Engineering',c:'orange'},{t:'Model Routing',c:'orange'},{t:'Auth / Rate Limits',c:'purple'},{t:'Context Management',c:'cyan'}]
  },
  llm: {
    icon:'🧠',
    title:'LLM / Model',
    sub:'TRANSFORMER + SELF-ATTENTION',
    body:'The Large Language Model is the core AI engine. Built on the Transformer architecture, it tokenizes the input, applies self-attention across all tokens simultaneously, and predicts the next most likely token — repeating this until the full response is generated. Self-attention lets it understand context across the entire input.',
    tags:[{t:'Transformer',c:'cyan'},{t:'Self-Attention',c:'cyan'},{t:'Token Prediction',c:'purple'},{t:'Claude / GPT-4',c:'green'}]
  },
  cloud: {
    icon:'☁️',
    title:'Cloud / External Models',
    sub:'SPECIALIZED APIs',
    body:'For tasks beyond the LLM\'s core capability — like generating images, converting text to speech, or running computer vision — the application calls specialized external APIs. DALL-E handles image generation, Whisper handles speech-to-text, and other domain-specific models handle their respective modalities.',
    tags:[{t:'DALL-E (Images)',c:'orange'},{t:'Whisper (Speech)',c:'orange'},{t:'Vision APIs',c:'orange'},{t:'External APIs',c:'purple'}]
  },
  output: {
    icon:'📤',
    title:'Output',
    sub:'FINAL RESPONSE',
    body:'The final response is returned to the user. This could be: generated text (streamed word by word), an image URL (rendered in the browser), a classification label with confidence score, a structured JSON response, or a combination. The web interface renders it appropriately based on content type.',
    tags:[{t:'Text Response',c:'green'},{t:'Generated Image',c:'green'},{t:'JSON / Structured',c:'green'},{t:'Streamed Tokens',c:'cyan'}]
  }
};

function showDetail(key) {
  // Deactivate all nodes
  document.querySelectorAll('.pipe-node').forEach(n => n.classList.remove('active'));
  // Activate clicked
  document.getElementById('node-' + key).classList.add('active');

  const d = details[key];
  const panel = document.getElementById('detail-panel');

  const tagHTML = d.tags.map(t => `<span class="dp-tag ${t.c}">${t.t}</span>`).join('');

  panel.innerHTML = `
    <div class="dp-header">
      <div class="dp-icon">${d.icon}</div>
      <div>
        <div class="dp-title">${d.title}</div>
        <div class="dp-subtitle">${d.sub}</div>
      </div>
    </div>
    <div class="dp-body">${d.body}</div>
    <div class="dp-tags">${tagHTML}</div>
  `;
}

// ── FLOW SIMULATION ──
let flowRunning = false;
function runFlow() {
  if (flowRunning) return;
  flowRunning = true;
  const btn = document.getElementById('flow-btn');
  btn.textContent = '⏳ Running...';
  btn.disabled = true;

  const steps = document.querySelectorAll('.flow-step');
  steps.forEach(s => { s.classList.remove('active','done'); });

  let i = 0;
  function next() {
    if (i > 0) steps[i-1].classList.replace('active','done');
    if (i < steps.length) {
      steps[i].classList.add('active');
      i++;
      setTimeout(next, 900);
    } else {
      btn.textContent = '▶ Run Again';
      btn.disabled = false;
      flowRunning = false;
    }
  }
  next();
}

// ── TABS ──
function switchTab(name) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
  event.target.classList.add('active');
}

// ── PROMPT TOGGLE ──
function togglePrompt(card) {
  const wasOpen = card.classList.contains('expanded');
  document.querySelectorAll('.prompt-card').forEach(c => c.classList.remove('expanded'));
  if (!wasOpen) card.classList.add('expanded');
}

// ── ARCH CARD HOVER ──
function toggleArch(card) {
  card.style.boxShadow = card.style.boxShadow ? '' : '0 0 30px rgba(0,255,255,0.15)';
}

// Auto-run simulation on load after delay
setTimeout(() => runFlow(), 1200);
</script>
</body>
</html>
