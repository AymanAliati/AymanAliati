<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ayman Aliati | Cybersecurity</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&family=JetBrains+Mono:wght@300;400;600&display=swap');

  :root {
    --cyan: #00f5ff;
    --green: #00ff41;
    --red: #ff003c;
    --gold: #ffd700;
    --bg: #020408;
    --panel: #060d14;
    --border: #0a2a3a;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--cyan);
    font-family: 'Share Tech Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed;
    width: 20px; height: 20px;
    border: 2px solid var(--cyan);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.1s;
    mix-blend-mode: difference;
  }
  .cursor-dot {
    position: fixed;
    width: 4px; height: 4px;
    background: var(--cyan);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
  }

  /* Matrix canvas */
  #matrix {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.13;
  }

  /* Scanlines overlay */
  .scanlines {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 1;
    pointer-events: none;
    background: repeating-linear-gradient(
      to bottom,
      transparent,
      transparent 2px,
      rgba(0,245,255,0.015) 2px,
      rgba(0,245,255,0.015) 4px
    );
  }

  /* Main wrapper */
  .wrapper {
    position: relative;
    z-index: 2;
    max-width: 960px;
    margin: 0 auto;
    padding: 20px;
  }

  /* ===== HERO ===== */
  .hero {
    text-align: center;
    padding: 60px 20px 40px;
    position: relative;
  }

  .hero::before {
    content: '';
    position: absolute;
    top: 0; left: 50%;
    transform: translateX(-50%);
    width: 600px; height: 2px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    animation: scanH 3s ease-in-out infinite;
  }

  @keyframes scanH {
    0%,100% { opacity: 0.3; } 50% { opacity: 1; }
  }

  .skull-art {
    font-size: 48px;
    animation: pulse 2s ease-in-out infinite;
    filter: drop-shadow(0 0 10px var(--cyan));
  }

  @keyframes pulse {
    0%,100% { transform: scale(1); filter: drop-shadow(0 0 10px var(--cyan)); }
    50% { transform: scale(1.05); filter: drop-shadow(0 0 25px var(--cyan)); }
  }

  .glitch {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(28px, 6vw, 56px);
    font-weight: 900;
    color: var(--cyan);
    text-transform: uppercase;
    letter-spacing: 6px;
    position: relative;
    display: inline-block;
    animation: glitch 4s infinite;
  }

  @keyframes glitch {
    0%,90%,100% { text-shadow: none; }
    92% { text-shadow: -3px 0 var(--red), 3px 0 var(--green); }
    94% { text-shadow: 3px 0 var(--red), -3px 0 var(--green); }
    96% { text-shadow: -3px 0 var(--red), 3px 0 var(--green); }
    98% { text-shadow: none; }
  }

  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
  }
  .glitch::before {
    color: var(--red);
    animation: glitch-before 4s infinite;
    clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
  }
  .glitch::after {
    color: var(--green);
    animation: glitch-after 4s infinite;
    clip-path: polygon(0 55%, 100% 55%, 100% 100%, 0 100%);
  }
  @keyframes glitch-before {
    0%,90%,100% { transform: none; opacity: 0; }
    92% { transform: translateX(-3px); opacity: 1; }
    96% { transform: translateX(3px); opacity: 0; }
  }
  @keyframes glitch-after {
    0%,90%,100% { transform: none; opacity: 0; }
    93% { transform: translateX(3px); opacity: 1; }
    97% { transform: translateX(-3px); opacity: 0; }
  }

  .subtitle-line {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 16px;
    margin: 14px 0;
  }

  .tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--green);
    border: 1px solid var(--green);
    padding: 4px 12px;
    border-radius: 2px;
    animation: tagPulse 2s ease-in-out infinite;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  .tag:nth-child(2) { animation-delay: 0.3s; color: var(--cyan); border-color: var(--cyan); }
  .tag:nth-child(3) { animation-delay: 0.6s; color: var(--gold); border-color: var(--gold); }

  @keyframes tagPulse {
    0%,100% { box-shadow: 0 0 4px currentColor; }
    50% { box-shadow: 0 0 12px currentColor; }
  }

  /* Typing text */
  .typing-wrapper {
    font-family: 'JetBrains Mono', monospace;
    font-size: 15px;
    color: var(--green);
    margin: 10px 0;
    min-height: 22px;
  }
  .typing-cursor { animation: blink 0.8s step-end infinite; }
  @keyframes blink { 50% { opacity: 0; } }

  /* ===== TERMINAL BLOCK ===== */
  .terminal {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    margin: 30px 0;
    box-shadow: 0 0 30px rgba(0,245,255,0.08);
    transition: box-shadow 0.3s;
  }
  .terminal:hover {
    box-shadow: 0 0 50px rgba(0,245,255,0.15);
  }

  .terminal-bar {
    background: #0d1b27;
    padding: 10px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid var(--border);
  }

  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.red { background: #ff5f56; }
  .dot.yellow { background: #ffbd2e; }
  .dot.green { background: #27c93f; }

  .terminal-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: #4a6a7a;
    flex: 1;
    text-align: center;
  }

  .terminal-body {
    padding: 20px;
    font-size: 13px;
    line-height: 1.8;
  }

  .prompt { color: var(--green); }
  .cmd { color: var(--cyan); }
  .out { color: #7ecfdf; }
  .comment { color: #3a6a7a; }
  .val-green { color: var(--green); }
  .val-gold { color: var(--gold); }
  .val-red { color: var(--red); }

  /* ===== SKILL BARS ===== */
  .section-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 14px;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--cyan);
    text-align: center;
    margin: 40px 0 20px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-title::before, .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan));
  }
  .section-title::after { background: linear-gradient(90deg, var(--cyan), transparent); }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 16px;
    margin: 20px 0;
  }

  .skill-group {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 16px;
  }

  .skill-group-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--gold);
    margin-bottom: 14px;
    text-transform: uppercase;
  }

  .skill-row {
    margin: 10px 0;
  }

  .skill-label {
    display: flex;
    justify-content: space-between;
    font-size: 12px;
    color: #7ecfdf;
    margin-bottom: 5px;
  }

  .skill-bar-bg {
    height: 5px;
    background: #0a1a25;
    border-radius: 2px;
    overflow: hidden;
  }

  .skill-bar {
    height: 100%;
    border-radius: 2px;
    width: 0;
    transition: width 1.5s cubic-bezier(0.4,0,0.2,1);
  }

  .bar-cyan { background: linear-gradient(90deg, #003a5c, var(--cyan)); }
  .bar-green { background: linear-gradient(90deg, #003a10, var(--green)); }
  .bar-gold { background: linear-gradient(90deg, #3a2800, var(--gold)); }
  .bar-red { background: linear-gradient(90deg, #3a0010, var(--red)); }

  /* ===== PROJECTS HEX GRID ===== */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 16px;
    margin: 20px 0;
  }

  .project-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 20px;
    position: relative;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.3s;
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 2px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    transition: left 0.5s;
  }

  .project-card:hover::before { left: 100%; }
  .project-card:hover {
    border-color: var(--cyan);
    box-shadow: 0 0 20px rgba(0,245,255,0.1);
    transform: translateY(-3px);
  }

  .project-icon {
    font-size: 28px;
    margin-bottom: 10px;
  }

  .project-name {
    font-family: 'Orbitron', sans-serif;
    font-size: 12px;
    color: var(--cyan);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .project-desc {
    font-size: 12px;
    color: #4a8a9a;
    line-height: 1.7;
    margin-bottom: 12px;
  }

  .tech-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
  }

  .tech-tag {
    font-size: 10px;
    padding: 2px 8px;
    border: 1px solid #0a3a4a;
    border-radius: 2px;
    color: #3a8a9a;
    letter-spacing: 1px;
  }

  /* ===== BADGES ===== */
  .badges-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    margin: 20px 0;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 6px 14px;
    font-size: 12px;
    color: #5abaca;
    text-decoration: none;
    transition: all 0.25s;
    letter-spacing: 1px;
  }
  .badge:hover {
    border-color: var(--cyan);
    color: var(--cyan);
    box-shadow: 0 0 12px rgba(0,245,255,0.2);
    transform: translateY(-2px);
  }

  /* ===== PORTFOLIO SECRET BUTTON ===== */
  .portfolio-section {
    text-align: center;
    margin: 50px 0 30px;
    position: relative;
  }

  .hack-btn {
    display: inline-block;
    padding: 0;
    background: none;
    border: none;
    cursor: pointer;
    position: relative;
  }

  .hack-btn-inner {
    display: inline-flex;
    align-items: center;
    gap: 12px;
    font-family: 'Orbitron', sans-serif;
    font-size: 13px;
    letter-spacing: 3px;
    color: var(--green);
    border: 2px solid var(--green);
    padding: 14px 32px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
    text-transform: uppercase;
  }

  .hack-btn-inner::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,255,65,0.15), transparent);
    animation: sweep 2.5s linear infinite;
  }

  @keyframes sweep {
    0% { left: -100%; }
    100% { left: 100%; }
  }

  .hack-btn:hover .hack-btn-inner {
    color: var(--bg);
    background: var(--green);
    box-shadow: 0 0 30px var(--green);
  }

  .hack-btn .corner {
    position: absolute;
    width: 10px; height: 10px;
    border-color: var(--green);
    border-style: solid;
  }
  .hack-btn .corner.tl { top: -2px; left: -2px; border-width: 2px 0 0 2px; }
  .hack-btn .corner.tr { top: -2px; right: -2px; border-width: 2px 2px 0 0; }
  .hack-btn .corner.bl { bottom: -2px; left: -2px; border-width: 0 0 2px 2px; }
  .hack-btn .corner.br { bottom: -2px; right: -2px; border-width: 0 2px 2px 0; }

  .access-hint {
    font-size: 11px;
    color: #2a5a4a;
    margin-top: 10px;
    letter-spacing: 2px;
  }

  /* Modal */
  .modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.92);
    z-index: 1000;
    display: none;
    align-items: center;
    justify-content: center;
  }

  .modal-overlay.active { display: flex; }

  .modal-box {
    background: var(--panel);
    border: 1px solid var(--cyan);
    border-radius: 4px;
    padding: 36px 40px;
    max-width: 480px;
    width: 90%;
    text-align: center;
    box-shadow: 0 0 60px rgba(0,245,255,0.2);
    animation: modalIn 0.4s cubic-bezier(0.4,0,0.2,1);
  }

  @keyframes modalIn {
    from { transform: scale(0.8) translateY(20px); opacity: 0; }
    to { transform: scale(1) translateY(0); opacity: 1; }
  }

  .modal-icon { font-size: 48px; margin-bottom: 16px; }

  .modal-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 16px;
    letter-spacing: 4px;
    color: var(--cyan);
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .modal-sub {
    font-size: 12px;
    color: #3a7a8a;
    margin-bottom: 24px;
    letter-spacing: 1px;
  }

  .decrypt-progress {
    height: 3px;
    background: #0a1a25;
    border-radius: 2px;
    margin-bottom: 20px;
    overflow: hidden;
  }

  .decrypt-bar {
    height: 100%;
    width: 0;
    background: var(--cyan);
    transition: width 1.5s ease;
  }

  .modal-url {
    display: inline-block;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    color: var(--green);
    background: #020c0a;
    border: 1px solid #003a20;
    padding: 10px 20px;
    border-radius: 3px;
    margin-bottom: 20px;
    letter-spacing: 1px;
    opacity: 0;
    transition: opacity 0.5s 1.5s;
  }

  .modal-url.visible { opacity: 1; }

  .modal-btns {
    display: flex;
    gap: 12px;
    justify-content: center;
  }

  .modal-btn {
    font-family: 'Orbitron', sans-serif;
    font-size: 11px;
    letter-spacing: 2px;
    padding: 10px 20px;
    border: 1px solid;
    background: none;
    cursor: pointer;
    text-transform: uppercase;
    transition: all 0.2s;
    text-decoration: none;
    display: inline-block;
  }

  .modal-btn.primary {
    color: var(--green);
    border-color: var(--green);
  }
  .modal-btn.primary:hover {
    background: var(--green);
    color: var(--bg);
  }
  .modal-btn.secondary {
    color: #4a6a7a;
    border-color: #1a3a4a;
  }
  .modal-btn.secondary:hover {
    border-color: #3a6a7a;
    color: #7ecfdf;
  }

  /* ===== STATS ROW ===== */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 12px;
    margin: 20px 0;
  }

  .stat-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 16px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .stat-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 100%; height: 2px;
    background: var(--cyan);
    transform: scaleX(0);
    transition: transform 0.4s;
    transform-origin: left;
  }

  .stat-card:hover::after { transform: scaleX(1); }

  .stat-number {
    font-family: 'Orbitron', sans-serif;
    font-size: 28px;
    color: var(--cyan);
    font-weight: 900;
    line-height: 1;
  }

  .stat-label {
    font-size: 10px;
    color: #3a6a7a;
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-top: 6px;
  }

  /* ===== FOOTER ===== */
  .footer {
    text-align: center;
    padding: 40px 20px;
    border-top: 1px solid var(--border);
    margin-top: 60px;
  }

  .footer-text {
    font-size: 11px;
    color: #2a4a5a;
    letter-spacing: 2px;
  }

  .blink-cursor {
    display: inline-block;
    width: 8px; height: 14px;
    background: var(--cyan);
    animation: blink 1s step-end infinite;
    vertical-align: middle;
    margin-left: 4px;
  }

  /* ===== BINARY RAIN DOTS ===== */
  .hex-row {
    display: flex;
    justify-content: center;
    gap: 6px;
    flex-wrap: wrap;
    margin: 16px 0;
    opacity: 0.4;
  }
  .hex-dot {
    font-size: 10px;
    color: var(--green);
    animation: hexFade 3s ease-in-out infinite;
  }
  .hex-dot:nth-child(2n) { animation-delay: 0.4s; color: var(--cyan); }
  .hex-dot:nth-child(3n) { animation-delay: 0.8s; }
  .hex-dot:nth-child(5n) { animation-delay: 1.2s; }
  @keyframes hexFade {
    0%,100% { opacity: 0.2; } 50% { opacity: 0.8; }
  }

  /* Animations for reveal */
  .reveal {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-dot" id="cursor-dot"></div>

<canvas id="matrix"></canvas>
<div class="scanlines"></div>

<div class="wrapper">

  <!-- HERO -->
  <div class="hero reveal" id="hero">
    <div class="skull-art">☠</div>
    <br>
    <div class="glitch" data-text="AYMAN ALIATI">AYMAN ALIATI</div>
    <div style="margin-top:16px;" class="subtitle-line">
      <span class="tag">⚔ Cybersecurity</span>
      <span class="tag">◈ Networks</span>
      <span class="tag">⬡ Web Dev</span>
    </div>
    <div class="typing-wrapper">
      <span id="typing-text"></span><span class="typing-cursor">_</span>
    </div>

    <!-- Social badges -->
    <div class="badges-row" style="margin-top:20px;">
      <a href="https://linkedin.com/in/ayman-aliati" target="_blank" class="badge">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="#0077B5"><path d="M20.45 20.45h-3.56v-5.57c0-1.33-.03-3.04-1.85-3.04-1.85 0-2.13 1.45-2.13 2.94v5.67H9.35V9h3.41v1.56h.05c.48-.9 1.64-1.85 3.37-1.85 3.6 0 4.27 2.37 4.27 5.45v6.29zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9H7.12v11.45zM22.22 0H1.77A1.75 1.75 0 0 0 0 1.72v20.56C0 23.22.8 24 1.77 24h20.45C23.2 24 24 23.22 24 22.28V1.72A1.75 1.75 0 0 0 22.22 0z"/></svg>
        LinkedIn
      </a>
      <a href="https://github.com/AymanAliati" target="_blank" class="badge">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.44 9.8 8.2 11.38.6.1.82-.26.82-.58v-2.03c-3.34.72-4.04-1.61-4.04-1.61-.54-1.38-1.33-1.74-1.33-1.74-1.09-.74.08-.73.08-.73 1.2.08 1.84 1.24 1.84 1.24 1.07 1.83 2.8 1.3 3.49 1 .1-.78.42-1.31.76-1.61-2.67-.3-5.47-1.33-5.47-5.93 0-1.31.47-2.38 1.24-3.22-.12-.3-.54-1.52.12-3.17 0 0 1.01-.32 3.3 1.23a11.5 11.5 0 0 1 3-.4c1.02 0 2.04.14 3 .4 2.28-1.55 3.3-1.23 3.3-1.23.66 1.65.24 2.87.12 3.17.77.84 1.24 1.91 1.24 3.22 0 4.61-2.81 5.63-5.48 5.92.43.37.82 1.1.82 2.22v3.29c0 .32.22.69.83.57C20.57 21.8 24 17.3 24 12 24 5.37 18.63 0 12 0z"/></svg>
        GitHub
      </a>
      <a href="mailto:aliatiaymane@gmail.com" class="badge">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M20 4H4C2.9 4 2 4.9 2 6v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
        Email
      </a>
    </div>
  </div>

  <!-- HEX BINARY DECORATION -->
  <div class="hex-row">
    <span class="hex-dot">01</span><span class="hex-dot">4F</span><span class="hex-dot">A3</span><span class="hex-dot">FF</span><span class="hex-dot">2C</span><span class="hex-dot">B7</span><span class="hex-dot">E1</span><span class="hex-dot">90</span><span class="hex-dot">5D</span><span class="hex-dot">3A</span><span class="hex-dot">C4</span><span class="hex-dot">88</span><span class="hex-dot">12</span><span class="hex-dot">6E</span><span class="hex-dot">D9</span><span class="hex-dot">07</span><span class="hex-dot">FB</span><span class="hex-dot">44</span>
  </div>

  <!-- TERMINAL WHOAMI -->
  <div class="terminal reveal">
    <div class="terminal-bar">
      <div class="dot red"></div>
      <div class="dot yellow"></div>
      <div class="dot green"></div>
      <div class="terminal-title">root@kali:~$ — bash</div>
    </div>
    <div class="terminal-body">
      <div><span class="prompt">┌──(root㉿kali)-[~]</span></div>
      <div><span class="prompt">└─$ </span><span class="cmd">cat /etc/profile.d/ayman.sh</span></div>
      <br>
      <div><span class="comment"># ===== IDENTITY =====</span></div>
      <div><span class="out">NAME</span>=<span class="val-green">"Ayman Aliati"</span></div>
      <div><span class="out">ROLE</span>=<span class="val-green">"DUT Génie Informatique — Cybersécurité & Réseaux"</span></div>
      <div><span class="out">LOCATION</span>=<span class="val-green">"Marrakech-Safi, Maroc 🇲🇦"</span></div>
      <div><span class="out">STATUS</span>=<span class="val-gold">"Searching for 2-month internship"</span></div>
      <br>
      <div><span class="comment"># ===== CERTIFICATIONS =====</span></div>
      <div><span class="out">CERTS</span>=(<span class="val-green">"CCNA1"</span> <span class="val-green">"CCNA2"</span> <span class="val-green">"Java-POO"</span> <span class="val-green">"Web Dev"</span>)</div>
      <br>
      <div><span class="comment"># ===== WEAPONS OF CHOICE =====</span></div>
      <div><span class="out">OFFENSIVE</span>=(<span class="val-red">"Nmap"</span> <span class="val-red">"Hydra"</span> <span class="val-red">"sqlmap"</span> <span class="val-red">"Burp Suite"</span> <span class="val-red">"Metasploit"</span>)</div>
      <div><span class="out">DEFENSIVE</span>=(<span class="val-green">"Wazuh"</span> <span class="val-green">"Firewalld"</span> <span class="val-green">"iptables"</span> <span class="val-green">"Wireshark"</span>)</div>
      <div><span class="out">OS</span>=<span class="val-red">"Kali Linux // Fedora // Ubuntu"</span></div>
      <br>
      <div><span class="prompt">└─$ </span><span class="cmd">echo $STATUS</span></div>
      <div><span class="val-gold">Searching for 2-month internship</span></div>
      <div><span class="prompt">└─$ </span><span class="typing-cursor" style="font-size:13px;">_</span></div>
    </div>
  </div>

  <!-- STATS -->
  <div class="section-title reveal">[ SYSTEM STATS ]</div>
  <div class="stats-row reveal">
    <div class="stat-card">
      <div class="stat-number" data-target="8">0</div>
      <div class="stat-label">Projects</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-target="2">0</div>
      <div class="stat-label">Years XP</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-target="4">0</div>
      <div class="stat-label">Certifications</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-target="10">0</div>
      <div class="stat-label">Tools Mastered</div>
    </div>
    <div class="stat-card">
      <div class="stat-number" data-target="3">0</div>
      <div class="stat-label">Languages</div>
    </div>
  </div>

  <!-- SKILLS -->
  <div class="section-title reveal">[ SKILL MATRIX ]</div>
  <div class="skills-grid reveal" id="skills-container">

    <div class="skill-group">
      <div class="skill-group-title">⚔ Cybersecurity</div>
      <div class="skill-row">
        <div class="skill-label"><span>Pentesting / OWASP</span><span>88%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-red" data-width="88"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Wazuh / SIEM</span><span>82%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-red" data-width="82"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Firewall / iptables</span><span>85%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-red" data-width="85"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Nmap / Hydra</span><span>90%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-red" data-width="90"></div></div>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">◈ Networks</div>
      <div class="skill-row">
        <div class="skill-label"><span>Cisco IOS / CCNA</span><span>85%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-cyan" data-width="85"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>LAN/DMZ / VLANs</span><span>82%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-cyan" data-width="82"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>TCP/IP / DNS / DHCP</span><span>88%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-cyan" data-width="88"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>GNS3 / VMware</span><span>78%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-cyan" data-width="78"></div></div>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">⬡ Development</div>
      <div class="skill-row">
        <div class="skill-label"><span>Python / Flask</span><span>85%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-green" data-width="85"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>React.js / JS</span><span>80%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-green" data-width="80"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>PHP / MySQL</span><span>78%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-green" data-width="78"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>C / Java (OOP)</span><span>75%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-green" data-width="75"></div></div>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">⬡ Sysadmin / AI</div>
      <div class="skill-row">
        <div class="skill-label"><span>Linux Admin</span><span>88%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-gold" data-width="88"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Bash Scripting</span><span>80%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-gold" data-width="80"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>Ollama / AI Integration</span><span>72%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-gold" data-width="72"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-label"><span>n8n Automation</span><span>70%</span></div>
        <div class="skill-bar-bg"><div class="skill-bar bar-gold" data-width="70"></div></div>
      </div>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="section-title reveal">[ OPERATIONS LOG ]</div>
  <div class="projects-grid reveal">

    <div class="project-card">
      <div class="project-icon">🔥</div>
      <div class="project-name">Firewall IDS — AI</div>
      <div class="project-desc">Système de détection d'intrusions avec Wazuh, IA Ollama pour l'analyse de logs et alertes Telegram en temps réel.</div>
      <div class="tech-tags">
        <span class="tech-tag">Firewalld</span>
        <span class="tech-tag">Wazuh</span>
        <span class="tech-tag">Ollama</span>
        <span class="tech-tag">Kali</span>
        <span class="tech-tag">Nmap</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">🌐</div>
      <div class="project-name">SecureXplorer</div>
      <div class="project-desc">Plateforme web de scan de vulnérabilités avec intégration Nmap & sqlmap via API. Auth JWT + protection CSRF.</div>
      <div class="tech-tags">
        <span class="tech-tag">Python</span>
        <span class="tech-tag">Flask</span>
        <span class="tech-tag">PHP</span>
        <span class="tech-tag">MySQL</span>
        <span class="tech-tag">sqlmap</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">🏗</div>
      <div class="project-name">Network LAN/DMZ</div>
      <div class="project-desc">Architecture réseau sécurisée et segmentée avec serveur Web en DMZ, routage multi-interfaces et tests inter-zones.</div>
      <div class="tech-tags">
        <span class="tech-tag">Fedora</span>
        <span class="tech-tag">Bind</span>
        <span class="tech-tag">Apache</span>
        <span class="tech-tag">VMware</span>
        <span class="tech-tag">NAT</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">🤖</div>
      <div class="project-name">NOTEAI Platform</div>
      <div class="project-desc">Plateforme e-learning avec moteur de recommandation IA, gestion sécurisée des utilisateurs et dashboard admin.</div>
      <div class="tech-tags">
        <span class="tech-tag">PHP</span>
        <span class="tech-tag">MySQL</span>
        <span class="tech-tag">JavaScript</span>
        <span class="tech-tag">AI</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">⚡</div>
      <div class="project-name">Email Bot Pro</div>
      <div class="project-desc">Script Python d'envoi d'emails en masse avec SMTP sécurisé, personnalisation, pièces jointes et système de logs.</div>
      <div class="tech-tags">
        <span class="tech-tag">Python</span>
        <span class="tech-tag">SMTP</span>
        <span class="tech-tag">Automation</span>
        <span class="tech-tag">HTML</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-icon">✈</div>
      <div class="project-name">Sahara Traveling</div>
      <div class="project-desc">Site de réservation de voyages responsive avec système de recherche, filtrage et interface d'administration complète.</div>
      <div class="tech-tags">
        <span class="tech-tag">HTML</span>
        <span class="tech-tag">CSS</span>
        <span class="tech-tag">JavaScript</span>
      </div>
    </div>

  </div>

  <!-- PORTFOLIO SECRET -->
  <div class="portfolio-section reveal">
    <div class="section-title" style="margin-bottom:30px;">[ ACCESS PORTFOLIO ]</div>

    <button class="hack-btn" onclick="openPortfolioModal()">
      <span class="corner tl"></span>
      <span class="corner tr"></span>
      <span class="corner bl"></span>
      <span class="corner br"></span>
      <div class="hack-btn-inner">
        <span>☠</span>
        <span>INITIATE ACCESS</span>
        <span>→</span>
      </div>
    </button>
    <div class="access-hint">[ CLICK TO DECRYPT PORTFOLIO LINK ]</div>
  </div>

  <!-- FOOTER -->
  <div class="footer reveal">
    <div class="hex-row" style="opacity:0.25;">
      <span class="hex-dot">48</span><span class="hex-dot">41</span><span class="hex-dot">43</span><span class="hex-dot">4B</span><span class="hex-dot">20</span><span class="hex-dot">54</span><span class="hex-dot">48</span><span class="hex-dot">45</span><span class="hex-dot">20</span><span class="hex-dot">50</span><span class="hex-dot">4C</span><span class="hex-dot">41</span><span class="hex-dot">4E</span><span class="hex-dot">45</span><span class="hex-dot">54</span>
    </div>
    <div class="footer-text" style="margin-top:16px;">
      © 2026 AYMAN ALIATI — ALL SYSTEMS OPERATIONAL<span class="blink-cursor"></span>
    </div>
    <div class="footer-text" style="margin-top:8px; font-size:10px;">
      aliatiaymane@gmail.com · +212 612 634 799 · Marrakech, Maroc
    </div>
  </div>

</div>

<!-- MODAL -->
<div class="modal-overlay" id="portfolioModal">
  <div class="modal-box">
    <div class="modal-icon">🔓</div>
    <div class="modal-title">Access Granted</div>
    <div class="modal-sub">DECRYPTING SECURE LINK...</div>
    <div class="decrypt-progress">
      <div class="decrypt-bar" id="decryptBar"></div>
    </div>
    <div class="modal-url" id="modalUrl">https://ayman-aliati-portfolio.vercel.app</div>
    <div class="modal-btns">
      <a href="https://ayman-aliati-portfolio.vercel.app" target="_blank" class="modal-btn primary" id="visitBtn" style="display:none;">↗ VISIT PORTFOLIO</a>
      <button class="modal-btn secondary" onclick="closePortfolioModal()">CLOSE</button>
    </div>
  </div>
</div>

<script>
  // Matrix rain
  const canvas = document.getElementById('matrix');
  const ctx = canvas.getContext('2d');

  function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);

  const chars = '01アイウエオカキクケコサシスセソタチツテトナニヌネノABCDEF0123456789☠⚡◈⬡⚔#$%&';
  const fontSize = 13;
  let columns = Math.floor(canvas.width / fontSize);
  let drops = Array(columns).fill(1);

  function drawMatrix() {
    ctx.fillStyle = 'rgba(2,4,8,0.05)';
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.font = fontSize + 'px Share Tech Mono';

    for (let i = 0; i < drops.length; i++) {
      const char = chars[Math.floor(Math.random() * chars.length)];
      const isHead = drops[i] * fontSize < canvas.height * 0.3;
      ctx.fillStyle = isHead ? '#00ff41' : `rgba(0,${Math.floor(Math.random()*80+100)},${Math.floor(Math.random()*80+150)},${Math.random()*0.8+0.2})`;
      ctx.fillText(char, i * fontSize, drops[i] * fontSize);

      if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
      drops[i]++;
    }
  }

  setInterval(drawMatrix, 45);

  // Custom cursor
  const cursor = document.getElementById('cursor');
  const cursorDot = document.getElementById('cursor-dot');
  let mouseX = 0, mouseY = 0;

  document.addEventListener('mousemove', e => {
    mouseX = e.clientX; mouseY = e.clientY;
    cursor.style.left = mouseX - 10 + 'px';
    cursor.style.top = mouseY - 10 + 'px';
    cursorDot.style.left = mouseX - 2 + 'px';
    cursorDot.style.top = mouseY - 2 + 'px';
  });

  document.addEventListener('mousedown', () => cursor.style.transform = 'scale(0.7)');
  document.addEventListener('mouseup', () => cursor.style.transform = 'scale(1)');

  // Typing animation
  const phrases = [
    'Hacking the System...',
    'Building Secure Networks...',
    'Training AI Models...',
    'Securing the Future...',
    'Vice-President @ Cyber Atlas',
    'CCNA Certified Engineer',
    'Penetration Tester',
    'Searching for 2-month internship...'
  ];
  let phraseIndex = 0, charIndex = 0, deleting = false;
  const typingEl = document.getElementById('typing-text');

  function type() {
    const current = phrases[phraseIndex];
    if (!deleting) {
      typingEl.textContent = current.slice(0, ++charIndex);
      if (charIndex === current.length) { deleting = true; setTimeout(type, 2000); return; }
    } else {
      typingEl.textContent = current.slice(0, --charIndex);
      if (charIndex === 0) { deleting = false; phraseIndex = (phraseIndex + 1) % phrases.length; }
    }
    setTimeout(type, deleting ? 40 : 80);
  }
  type();

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 80);
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(r => observer.observe(r));
  document.getElementById('hero').classList.add('visible');

  // Animate stats
  function animateStats() {
    document.querySelectorAll('[data-target]').forEach(el => {
      const target = parseInt(el.dataset.target);
      let count = 0;
      const step = Math.ceil(target / 30);
      const interval = setInterval(() => {
        count = Math.min(count + step, target);
        el.textContent = count;
        if (count >= target) clearInterval(interval);
      }, 50);
    });
  }

  const statsObserver = new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) { animateStats(); statsObserver.disconnect(); }
  }, { threshold: 0.5 });
  statsObserver.observe(document.querySelector('.stats-row'));

  // Animate skill bars
  const skillsObserver = new IntersectionObserver(entries => {
    if (entries[0].isIntersecting) {
      document.querySelectorAll('.skill-bar').forEach(bar => {
        bar.style.width = bar.dataset.width + '%';
      });
      skillsObserver.disconnect();
    }
  }, { threshold: 0.3 });
  skillsObserver.observe(document.getElementById('skills-container'));

  // Portfolio modal
  function openPortfolioModal() {
    const modal = document.getElementById('portfolioModal');
    modal.classList.add('active');
    setTimeout(() => {
      document.getElementById('decryptBar').style.width = '100%';
    }, 100);
    setTimeout(() => {
      const url = document.getElementById('modalUrl');
      url.classList.add('visible');
      document.getElementById('visitBtn').style.display = 'inline-block';
    }, 1800);
  }

  function closePortfolioModal() {
    const modal = document.getElementById('portfolioModal');
    modal.classList.remove('active');
    setTimeout(() => {
      document.getElementById('decryptBar').style.width = '0';
      document.getElementById('decryptBar').style.transition = 'none';
      document.getElementById('modalUrl').classList.remove('visible');
      document.getElementById('visitBtn').style.display = 'none';
      setTimeout(() => {
        document.getElementById('decryptBar').style.transition = 'width 1.5s ease';
      }, 50);
    }, 300);
  }

  document.getElementById('portfolioModal').addEventListener('click', function(e) {
    if (e.target === this) closePortfolioModal();
  });
</script>
</body>
</html>
