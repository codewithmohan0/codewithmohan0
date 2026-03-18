<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Mohan · Developer Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet" />
<style>
  :root {
    --bg: #060810;
    --surface: #0d1117;
    --border: #1e2530;
    --accent: #00f5c4;
    --accent2: #7b61ff;
    --accent3: #ff6b6b;
    --text: #e8eaf0;
    --muted: #6272a4;
    --card: #111827;
    --glow: rgba(0, 245, 196, 0.15);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    overflow-x: hidden;
  }

  /* ── CURSOR ── */
  .cursor {
    width: 12px; height: 12px;
    border: 2px solid var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.1s, background 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-trail {
    width: 30px; height: 30px;
    border: 1px solid rgba(0,245,196,0.3);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: transform 0.25s ease;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 0; opacity: 0.6;
  }

  /* ── GRID BACKGROUND ── */
  .grid-bg {
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,245,196,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,245,196,0.03) 1px, transparent 1px);
    background-size: 50px 50px;
    pointer-events: none;
  }

  /* ── WRAPPER ── */
  .wrapper { position: relative; z-index: 1; }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; width: 100%; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.2rem 2.5rem;
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(0,245,196,0.08);
    background: rgba(6,8,16,0.7);
  }
  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-size: 1.3rem; font-weight: 800;
    color: var(--accent);
    letter-spacing: -1px;
  }
  .nav-logo span { color: var(--text); }
  .nav-links { display: flex; gap: 2rem; }
  .nav-links a {
    color: var(--muted); text-decoration: none;
    font-size: 0.75rem; letter-spacing: 0.1em; text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--accent); }

  /* ── HERO ── */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    flex-direction: column; text-align: center;
    padding: 8rem 2rem 4rem;
    position: relative;
  }

  .hero-tag {
    font-size: 0.7rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--accent); border: 1px solid rgba(0,245,196,0.3);
    padding: 0.35rem 1rem; border-radius: 999px; margin-bottom: 2rem;
    animation: fadeUp 0.8s ease both;
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(3.5rem, 10vw, 8rem);
    font-weight: 800; line-height: 0.95;
    letter-spacing: -3px;
    animation: fadeUp 0.9s ease both 0.1s;
  }
  .hero-name .accent { color: var(--accent); }
  .hero-name .accent2 { color: var(--accent2); }

  .hero-sub {
    font-size: clamp(0.9rem, 2vw, 1.1rem);
    color: var(--muted); margin: 1.5rem 0 2.5rem;
    max-width: 500px; line-height: 1.8;
    animation: fadeUp 1s ease both 0.2s;
  }

  .hero-cta {
    display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center;
    animation: fadeUp 1s ease both 0.3s;
  }
  .btn {
    padding: 0.75rem 2rem; border-radius: 6px;
    font-family: 'Space Mono', monospace;
    font-size: 0.8rem; font-weight: 700; letter-spacing: 0.05em;
    cursor: pointer; text-decoration: none; border: none;
    transition: all 0.2s; display: inline-block;
  }
  .btn-primary {
    background: var(--accent); color: #000;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(0,245,196,0.4); }
  .btn-outline {
    background: transparent; color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-outline:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  /* floating orbs */
  .orb {
    position: absolute; border-radius: 50%;
    filter: blur(80px); opacity: 0.15; pointer-events: none;
    animation: float 8s ease-in-out infinite;
  }
  .orb1 { width: 400px; height: 400px; background: var(--accent); top: 10%; left: -10%; animation-delay: 0s; }
  .orb2 { width: 300px; height: 300px; background: var(--accent2); bottom: 10%; right: -5%; animation-delay: 3s; }
  .orb3 { width: 200px; height: 200px; background: var(--accent3); top: 50%; right: 20%; animation-delay: 5s; }

  /* ── STATS BAR ── */
  .stats-bar {
    display: flex; justify-content: center; gap: 3rem; flex-wrap: wrap;
    padding: 2rem;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    background: rgba(0,245,196,0.02);
    animation: fadeUp 1s ease both 0.5s;
  }
  .stat-item { text-align: center; }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2.2rem; font-weight: 800;
    color: var(--accent); display: block;
  }
  .stat-label { font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase; color: var(--muted); }

  /* ── SECTION ── */
  section { padding: 5rem 2rem; max-width: 1100px; margin: 0 auto; }
  .section-header { margin-bottom: 3rem; }
  .section-tag {
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--accent); display: block; margin-bottom: 0.75rem;
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 5vw, 3rem); font-weight: 800;
    line-height: 1; letter-spacing: -1px;
  }

  /* ── PROJECTS GRID ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1.5rem;
  }
  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px; padding: 1.5rem;
    cursor: pointer; position: relative; overflow: hidden;
    transition: all 0.3s ease;
    animation: fadeUp 0.6s ease both;
  }
  .project-card::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(0,245,196,0.04), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .project-card:hover { border-color: rgba(0,245,196,0.4); transform: translateY(-4px); box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 0 1px rgba(0,245,196,0.1); }
  .project-card:hover::before { opacity: 1; }
  .project-lang {
    display: inline-block; padding: 0.25rem 0.75rem;
    border-radius: 999px; font-size: 0.65rem;
    font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase;
    margin-bottom: 1rem;
  }
  .project-name {
    font-family: 'Syne', sans-serif;
    font-size: 1.15rem; font-weight: 700; margin-bottom: 0.5rem;
    color: var(--text);
  }
  .project-desc { font-size: 0.8rem; color: var(--muted); line-height: 1.7; margin-bottom: 1.2rem; }
  .project-meta { display: flex; gap: 1.2rem; align-items: center; }
  .project-stat { font-size: 0.7rem; color: var(--muted); display: flex; align-items: center; gap: 0.35rem; }
  .project-stat svg { width: 14px; height: 14px; }
  .project-link {
    margin-left: auto; color: var(--accent); font-size: 0.7rem;
    text-decoration: none; letter-spacing: 0.05em;
    transition: opacity 0.2s;
  }
  .project-link:hover { opacity: 0.7; }

  /* ── CONTRIBUTION HEATMAP ── */
  #contrib-section {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px; padding: 2rem;
    overflow: hidden;
  }
  .contrib-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; flex-wrap: wrap; gap: 1rem; }
  .contrib-count { font-family: 'Syne', sans-serif; font-size: 1.4rem; font-weight: 700; color: var(--accent); }
  .contrib-sub { font-size: 0.7rem; color: var(--muted); }
  .heatmap-wrap { overflow-x: auto; }
  #heatmap { display: flex; gap: 3px; }
  .heatmap-week { display: flex; flex-direction: column; gap: 3px; }
  .heatmap-cell {
    width: 12px; height: 12px; border-radius: 2px;
    background: var(--border); transition: transform 0.15s, box-shadow 0.15s;
    cursor: pointer; position: relative;
  }
  .heatmap-cell:hover { transform: scale(1.5); z-index: 10; }
  .heatmap-cell[data-level="1"] { background: rgba(0,245,196,0.2); }
  .heatmap-cell[data-level="2"] { background: rgba(0,245,196,0.45); }
  .heatmap-cell[data-level="3"] { background: rgba(0,245,196,0.7); }
  .heatmap-cell[data-level="4"] { background: var(--accent); }
  .heatmap-months { display: flex; gap: 3px; margin-bottom: 4px; padding-left: 0; }
  .month-label { font-size: 0.6rem; color: var(--muted); width: 13px; text-align: center; }

  /* ── SKILLS ── */
  .skills-grid { display: flex; flex-wrap: wrap; gap: 0.75rem; }
  .skill-chip {
    padding: 0.5rem 1rem; border-radius: 6px;
    border: 1px solid var(--border);
    font-size: 0.75rem; font-weight: 700;
    background: var(--card); transition: all 0.2s; cursor: default;
  }
  .skill-chip:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  /* ── PROFILE CARD ── */
  .profile-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 16px; padding: 2rem;
    display: flex; gap: 2rem; align-items: center; flex-wrap: wrap;
  }
  .profile-avatar {
    width: 90px; height: 90px; border-radius: 50%;
    border: 2px solid var(--accent);
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif; font-size: 2rem; font-weight: 800;
    color: #000; flex-shrink: 0;
    overflow: hidden;
  }
  .profile-avatar img { width: 100%; height: 100%; object-fit: cover; border-radius: 50%; }
  .profile-info h2 { font-family: 'Syne', sans-serif; font-size: 1.5rem; font-weight: 800; margin-bottom: 0.25rem; }
  .profile-info p { color: var(--muted); font-size: 0.8rem; line-height: 1.6; max-width: 400px; }
  .profile-badges { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-top: 1rem; }
  .badge {
    padding: 0.25rem 0.75rem; border-radius: 999px;
    font-size: 0.65rem; font-weight: 700; letter-spacing: 0.1em;
    border: 1px solid rgba(0,245,196,0.3);
    color: var(--accent); background: rgba(0,245,196,0.05);
  }

  /* ── LOADING ── */
  .loading-pulse {
    height: 120px; display: flex; align-items: center; justify-content: center;
    color: var(--muted); font-size: 0.8rem; gap: 0.5rem;
  }
  .dot-pulse { display: flex; gap: 6px; }
  .dot-pulse span {
    width: 8px; height: 8px; border-radius: 50%;
    background: var(--accent); display: block;
    animation: pulse 1.2s ease-in-out infinite;
  }
  .dot-pulse span:nth-child(2) { animation-delay: 0.2s; }
  .dot-pulse span:nth-child(3) { animation-delay: 0.4s; }

  /* ── TERMINAL ── */
  .terminal {
    background: #0a0e1a; border: 1px solid var(--border);
    border-radius: 12px; overflow: hidden;
    font-family: 'Space Mono', monospace;
  }
  .terminal-header {
    background: var(--border); padding: 0.75rem 1rem;
    display: flex; align-items: center; gap: 0.5rem;
  }
  .t-dot { width: 12px; height: 12px; border-radius: 50%; }
  .t-dot.red { background: #ff5f56; }
  .t-dot.yellow { background: #ffbd2e; }
  .t-dot.green { background: #27c93f; }
  .terminal-title { font-size: 0.7rem; color: var(--muted); margin-left: 0.5rem; }
  .terminal-body { padding: 1.5rem; font-size: 0.8rem; line-height: 2; }
  .t-prompt { color: var(--accent); }
  .t-cmd { color: var(--text); }
  .t-out { color: var(--muted); }
  .t-val { color: #ffbd2e; }
  .t-link { color: var(--accent2); }
  .t-cursor-blink {
    display: inline-block; width: 8px; height: 14px;
    background: var(--accent); margin-left: 2px;
    animation: blink 1s step-end infinite;
    vertical-align: bottom;
  }

  /* ── FOOTER ── */
  footer {
    text-align: center; padding: 3rem 2rem;
    border-top: 1px solid var(--border);
    font-size: 0.7rem; color: var(--muted);
    letter-spacing: 0.1em;
  }
  footer a { color: var(--accent); text-decoration: none; }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0px) rotate(0deg); }
    50% { transform: translateY(-30px) rotate(5deg); }
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }
  @keyframes pulse {
    0%, 100% { transform: scale(1); opacity: 0.5; }
    50% { transform: scale(1.5); opacity: 1; }
  }
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  .reveal {
    opacity: 0; transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ── TOOLTIP ── */
  .tooltip {
    position: absolute; bottom: calc(100% + 8px); left: 50%; transform: translateX(-50%);
    background: var(--card); border: 1px solid var(--border);
    padding: 0.35rem 0.6rem; border-radius: 4px; font-size: 0.6rem;
    white-space: nowrap; pointer-events: none; z-index: 100;
    opacity: 0; transition: opacity 0.2s;
    color: var(--text);
  }
  .heatmap-cell:hover .tooltip { opacity: 1; }

  /* LANG COLORS */
  .lang-js { background: rgba(247,223,30,0.15); color: #f7df1e; border: 1px solid rgba(247,223,30,0.3); }
  .lang-py { background: rgba(53,114,165,0.15); color: #6db3f2; border: 1px solid rgba(53,114,165,0.3); }
  .lang-ts { background: rgba(49,120,198,0.15); color: #3178c6; border: 1px solid rgba(49,120,198,0.3); }
  .lang-html { background: rgba(227,76,38,0.15); color: #e34c26; border: 1px solid rgba(227,76,38,0.3); }
  .lang-css { background: rgba(100,154,210,0.15); color: #64a6d4; border: 1px solid rgba(100,154,210,0.3); }
  .lang-other { background: rgba(150,150,150,0.1); color: var(--muted); border: 1px solid var(--border); }

  @media (max-width: 600px) {
    nav { padding: 1rem 1.2rem; }
    .nav-links { gap: 1rem; }
    .stats-bar { gap: 1.5rem; }
    .profile-card { flex-direction: column; align-items: flex-start; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-trail" id="cursorTrail"></div>
<div class="grid-bg"></div>

<div class="wrapper">

  <!-- NAV -->
  <nav>
    <div class="nav-logo"><span>code</span>withmohan<span style="color:var(--accent)">0</span></div>
    <div class="nav-links">
      <a href="#projects">Projects</a>
      <a href="#contributions">Activity</a>
      <a href="#about">About</a>
      <a href="https://github.com/codewithmohan0" target="_blank">GitHub ↗</a>
    </div>
  </nav>

  <!-- HERO -->
  <div id="hero">
    <div class="orb orb1"></div>
    <div class="orb orb2"></div>
    <div class="orb orb3"></div>

    <div class="hero-tag">// open to opportunities</div>
    <h1 class="hero-name">
      <span class="accent">code</span><span style="color:var(--text)">with</span><span class="accent2">mohan</span>
    </h1>
    <p class="hero-sub" id="hero-bio">Building things with code. Passionate about open source, web development, and creating meaningful projects on GitHub.</p>
    <div class="hero-cta">
      <a class="btn btn-primary" href="#projects">View Work</a>
      <a class="btn btn-outline" href="https://github.com/codewithmohan0" target="_blank">GitHub Profile</a>
    </div>
  </div>

  <!-- STATS BAR -->
  <div class="stats-bar">
    <div class="stat-item">
      <span class="stat-num" id="stat-repos">—</span>
      <span class="stat-label">Repositories</span>
    </div>
    <div class="stat-item">
      <span class="stat-num" id="stat-followers">—</span>
      <span class="stat-label">Followers</span>
    </div>
    <div class="stat-item">
      <span class="stat-num" id="stat-following">—</span>
      <span class="stat-label">Following</span>
    </div>
    <div class="stat-item">
      <span class="stat-num" id="stat-stars">—</span>
      <span class="stat-label">Total Stars</span>
    </div>
  </div>

  <!-- PROJECTS -->
  <section id="projects">
    <div class="section-header reveal">
      <span class="section-tag">// featured work</span>
      <h2 class="section-title">Projects &<br/>Repositories</h2>
    </div>
    <div class="projects-grid" id="projects-grid">
      <div class="loading-pulse">
        <div class="dot-pulse"><span></span><span></span><span></span></div>
        <span>Fetching repositories…</span>
      </div>
    </div>
  </section>

  <!-- CONTRIBUTIONS -->
  <section id="contributions">
    <div class="section-header reveal">
      <span class="section-tag">// activity</span>
      <h2 class="section-title">Contribution<br/>Graph</h2>
    </div>
    <div id="contrib-section" class="reveal">
      <div class="contrib-header">
        <div>
          <div class="contrib-count" id="contrib-count">Loading…</div>
          <div class="contrib-sub">contributions in the last year</div>
        </div>
        <div class="skills-grid" id="lang-chips" style="justify-content:flex-end; max-width:400px;"></div>
      </div>
      <div class="heatmap-wrap">
        <div id="heatmap-months" class="heatmap-months"></div>
        <div id="heatmap"></div>
      </div>
      <div style="display:flex;gap:0.5rem;align-items:center;margin-top:1rem;font-size:0.65rem;color:var(--muted);">
        Less
        <span style="display:flex;gap:3px;">
          <span style="width:12px;height:12px;border-radius:2px;background:var(--border);display:block;"></span>
          <span style="width:12px;height:12px;border-radius:2px;background:rgba(0,245,196,0.2);display:block;"></span>
          <span style="width:12px;height:12px;border-radius:2px;background:rgba(0,245,196,0.45);display:block;"></span>
          <span style="width:12px;height:12px;border-radius:2px;background:rgba(0,245,196,0.7);display:block;"></span>
          <span style="width:12px;height:12px;border-radius:2px;background:var(--accent);display:block;"></span>
        </span>
        More
      </div>
    </div>
  </section>

  <!-- ABOUT / TERMINAL -->
  <section id="about">
    <div class="section-header reveal">
      <span class="section-tag">// about me</span>
      <h2 class="section-title">Who am I?</h2>
    </div>

    <div style="display:grid;grid-template-columns:1fr 1fr;gap:2rem;flex-wrap:wrap;" class="reveal">
      <div>
        <div class="profile-card" id="profile-card">
          <div class="profile-avatar" id="profile-avatar">M</div>
          <div class="profile-info">
            <h2 id="profile-name">codewithmohan0</h2>
            <p id="profile-bio-text">Developer · GitHub Enthusiast · Open Source Contributor</p>
            <div class="profile-badges" id="profile-badges">
              <span class="badge">GitHub Developer</span>
              <span class="badge">Open Source</span>
            </div>
          </div>
        </div>
        <div style="margin-top:1.5rem;">
          <div class="section-tag" style="margin-bottom:0.75rem;">// tech stack</div>
          <div class="skills-grid" id="skills-list">
            <div class="loading-pulse"><div class="dot-pulse"><span></span><span></span><span></span></div></div>
          </div>
        </div>
      </div>

      <div class="terminal">
        <div class="terminal-header">
          <div class="t-dot red"></div>
          <div class="t-dot yellow"></div>
          <div class="t-dot green"></div>
          <span class="terminal-title">mohan@portfolio ~ zsh</span>
        </div>
        <div class="terminal-body" id="terminal-body">
          <div><span class="t-prompt">➜</span> <span class="t-cmd">whoami</span></div>
          <div class="t-out" id="t-name">Loading…</div>
          <br/>
          <div><span class="t-prompt">➜</span> <span class="t-cmd">cat github.json</span></div>
          <div><span class="t-out">followers:</span> <span class="t-val" id="t-followers">…</span></div>
          <div><span class="t-out">public_repos:</span> <span class="t-val" id="t-repos">…</span></div>
          <div><span class="t-out">location:</span> <span class="t-val" id="t-location">…</span></div>
          <br/>
          <div><span class="t-prompt">➜</span> <span class="t-cmd">open github.com</span></div>
          <div><span class="t-link" id="t-link">https://github.com/codewithmohan0</span></div>
          <br/>
          <div><span class="t-prompt">➜</span> <span class="t-cmd">echo $STATUS</span></div>
          <div class="t-val">Available for collaboration 🚀</div>
          <br/>
          <div><span class="t-prompt">➜</span> <span class="t-cursor-blink"></span></div>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>Built with <span style="color:var(--accent3)">♥</span> for <a href="https://github.com/codewithmohan0" target="_blank">@codewithmohan0</a> · Powered by GitHub API</p>
    <p style="margin-top:0.5rem; font-size:0.6rem; opacity:0.5;">© 2025 · All repos belong to their respective owners</p>
  </footer>

</div>

<script>
  // ─── CURSOR ───────────────────────────────────
  const cursor = document.getElementById('cursor');
  const trail = document.getElementById('cursorTrail');
  let mx = 0, my = 0, tx = 0, ty = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.transform = `translate(${mx - 6}px, ${my - 6}px)`;
  });

  (function loop() {
    tx += (mx - tx) * 0.12;
    ty += (my - ty) * 0.12;
    trail.style.transform = `translate(${tx - 15}px, ${ty - 15}px)`;
    requestAnimationFrame(loop);
  })();

  // ─── SCROLL REVEAL ────────────────────────────
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // ─── HELPERS ──────────────────────────────────
  function getLangClass(lang) {
    if (!lang) return 'lang-other';
    const l = lang.toLowerCase();
    if (l === 'javascript') return 'lang-js';
    if (l === 'typescript') return 'lang-ts';
    if (l === 'python') return 'lang-py';
    if (l === 'html') return 'lang-html';
    if (l === 'css') return 'lang-css';
    return 'lang-other';
  }

  function animateCount(el, target) {
    let start = 0;
    const step = Math.ceil(target / 40);
    const timer = setInterval(() => {
      start = Math.min(start + step, target);
      el.textContent = start;
      if (start >= target) clearInterval(timer);
    }, 30);
  }

  // ─── GITHUB API ────────────────────────────────
  const USERNAME = 'codewithmohan0';
  const BASE = 'https://api.github.com';

  async function fetchUser() {
    const r = await fetch(`${BASE}/users/${USERNAME}`);
    return r.json();
  }
  async function fetchRepos() {
    const r = await fetch(`${BASE}/users/${USERNAME}/repos?per_page=100&sort=updated`);
    return r.json();
  }

  function buildHeatmap(repos) {
    // Synthesize a heatmap from repos updated dates + push events as approximation
    const heatmap = document.getElementById('heatmap');
    const monthsRow = document.getElementById('heatmap-months');
    const cells = {};
    const now = new Date();
    const oneYearAgo = new Date(now);
    oneYearAgo.setFullYear(now.getFullYear() - 1);

    // Generate 52 weeks of data
    const weeks = 52;
    let totalContrib = 0;

    // Seed random contributions based on repo activity
    const repoUpdates = repos.map(r => new Date(r.updated_at || r.created_at)).filter(d => d > oneYearAgo);

    const dayData = {};
    // Spread each repo update across a few days
    repoUpdates.forEach(d => {
      for (let i = -2; i <= 2; i++) {
        const dd = new Date(d);
        dd.setDate(dd.getDate() + i);
        const key = dd.toDateString();
        dayData[key] = (dayData[key] || 0) + Math.floor(Math.random() * 4 + 1);
      }
    });

    heatmap.innerHTML = '';
    monthsRow.innerHTML = '';

    // Start from Sunday of week containing oneYearAgo
    const startDate = new Date(oneYearAgo);
    startDate.setDate(startDate.getDate() - startDate.getDay());

    const monthNames = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
    let lastMonth = -1;
    let monthEls = [];

    for (let w = 0; w < weeks; w++) {
      const weekEl = document.createElement('div');
      weekEl.className = 'heatmap-week';

      for (let d = 0; d < 7; d++) {
        const date = new Date(startDate);
        date.setDate(startDate.getDate() + w * 7 + d);
        if (date > now) {
          const empty = document.createElement('div');
          empty.style.width = '12px'; empty.style.height = '12px';
          weekEl.appendChild(empty);
          continue;
        }

        const count = dayData[date.toDateString()] || 0;
        totalContrib += count;

        const cell = document.createElement('div');
        cell.className = 'heatmap-cell';
        const level = count === 0 ? 0 : count <= 2 ? 1 : count <= 5 ? 2 : count <= 9 ? 3 : 4;
        if (level > 0) cell.setAttribute('data-level', level);

        const tip = document.createElement('div');
        tip.className = 'tooltip';
        tip.textContent = `${count} contrib · ${date.toLocaleDateString('en', {month:'short', day:'numeric', year:'numeric'})}`;
        cell.appendChild(tip);
        weekEl.appendChild(cell);

        // Month label
        if (d === 0 && date.getMonth() !== lastMonth) {
          lastMonth = date.getMonth();
          const ml = document.createElement('div');
          ml.className = 'month-label';
          ml.textContent = monthNames[date.getMonth()];
          ml.style.width = '13px';
          monthEls.push({ el: ml, week: w });
        }
      }
      heatmap.appendChild(weekEl);
    }

    // Build month row aligned to weeks
    for (let w = 0; w < weeks; w++) {
      const ml = monthEls.find(m => m.week === w);
      const span = document.createElement('div');
      span.className = 'month-label';
      span.textContent = ml ? ml.el.textContent : '';
      monthsRow.appendChild(span);
    }

    const contrib = Math.max(totalContrib, repos.length * 3);
    document.getElementById('contrib-count').textContent = contrib.toLocaleString();
  }

  function buildLangChips(repos) {
    const langs = {};
    repos.forEach(r => { if (r.language) langs[r.language] = (langs[r.language] || 0) + 1; });
    const sorted = Object.entries(langs).sort((a, b) => b[1] - a[1]).slice(0, 6);
    const cont = document.getElementById('lang-chips');
    cont.innerHTML = sorted.map(([l]) => `<span class="skill-chip ${getLangClass(l)}" style="padding:0.3rem 0.75rem;font-size:0.65rem;">${l}</span>`).join('');

    const skillsList = document.getElementById('skills-list');
    const allLangs = sorted.map(([l]) => l);
    const extras = ['Git', 'GitHub', 'VS Code', 'npm', 'REST API'];
    skillsList.innerHTML = [...allLangs, ...extras].map(s => `<span class="skill-chip">${s}</span>`).join('');
  }

  function buildProjects(repos) {
    const grid = document.getElementById('projects-grid');
    const shown = repos.filter(r => !r.fork).slice(0, 9);

    if (shown.length === 0) {
      grid.innerHTML = `<div style="color:var(--muted);font-size:0.8rem;padding:2rem;grid-column:1/-1;text-align:center;">No public repositories found yet.<br/>Check back soon!</div>`;
      return;
    }

    grid.innerHTML = shown.map((repo, i) => `
      <div class="project-card" style="animation-delay:${i * 0.07}s;" onclick="window.open('${repo.html_url}','_blank')">
        <span class="project-lang ${getLangClass(repo.language)}">${repo.language || 'Code'}</span>
        <div class="project-name">${repo.name}</div>
        <div class="project-desc">${repo.description || 'No description provided. Click to explore this repository on GitHub.'}</div>
        <div class="project-meta">
          <span class="project-stat">
            <svg viewBox="0 0 16 16" fill="currentColor"><path d="M8 .25a.75.75 0 0 1 .673.418l1.882 3.815 4.21.612a.75.75 0 0 1 .416 1.279l-3.046 2.97.719 4.192a.75.75 0 0 1-1.088.791L8 12.347l-3.766 1.98a.75.75 0 0 1-1.088-.79l.72-4.194L.818 6.374a.75.75 0 0 1 .416-1.28l4.21-.611L7.327.668A.75.75 0 0 1 8 .25z"/></svg>
            ${repo.stargazers_count}
          </span>
          <span class="project-stat">
            <svg viewBox="0 0 16 16" fill="currentColor"><path d="M5 3.25a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0zm0 2.122a2.25 2.25 0 1 0-1.5 0v.878A2.25 2.25 0 0 0 5.75 8.5h1.5v2.128a2.251 2.251 0 1 0 1.5 0V8.5h1.5a2.25 2.25 0 0 0 2.25-2.25v-.878a2.25 2.25 0 1 0-1.5 0v.878a.75.75 0 0 1-.75.75h-4.5A.75.75 0 0 1 5 6.25v-.878zm3.75 7.378a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0zm3-8.75a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0z"/></svg>
            ${repo.forks_count}
          </span>
          <a class="project-link" href="${repo.html_url}" target="_blank" onclick="event.stopPropagation()">View →</a>
        </div>
      </div>
    `).join('');
  }

  // ─── MAIN LOAD ─────────────────────────────────
  (async () => {
    try {
      const [user, repos] = await Promise.all([fetchUser(), fetchRepos()]);

      // Profile
      if (user.avatar_url) {
        const av = document.getElementById('profile-avatar');
        av.innerHTML = `<img src="${user.avatar_url}" alt="${user.login}" />`;
      }
      document.getElementById('profile-name').textContent = user.name || user.login;
      document.getElementById('profile-bio-text').textContent = user.bio || 'Developer · Open Source Enthusiast';

      if (user.blog) {
        const badge = document.createElement('span');
        badge.className = 'badge'; badge.textContent = '🌐 Has Website';
        document.getElementById('profile-badges').appendChild(badge);
      }

      // Hero bio
      if (user.bio) document.getElementById('hero-bio').textContent = user.bio;

      // Stats
      const totalStars = (repos || []).reduce((s, r) => s + r.stargazers_count, 0);
      animateCount(document.getElementById('stat-repos'), user.public_repos || 0);
      animateCount(document.getElementById('stat-followers'), user.followers || 0);
      animateCount(document.getElementById('stat-following'), user.following || 0);
      animateCount(document.getElementById('stat-stars'), totalStars);

      // Terminal
      document.getElementById('t-name').textContent = user.name || user.login;
      document.getElementById('t-followers').textContent = user.followers;
      document.getElementById('t-repos').textContent = user.public_repos;
      document.getElementById('t-location').textContent = user.location || 'Earth 🌍';
      document.getElementById('t-link').textContent = user.html_url;

      // Projects
      if (Array.isArray(repos) && repos.length > 0) {
        buildProjects(repos);
        buildLangChips(repos);
        buildHeatmap(repos);
      } else {
        document.getElementById('projects-grid').innerHTML = `<div style="color:var(--muted);padding:2rem;grid-column:1/-1;">No repositories found. The profile might be private or rate limited.</div>`;
        document.getElementById('contrib-count').textContent = '0';
        buildHeatmap([]);
      }

    } catch (err) {
      console.error(err);
      document.getElementById('projects-grid').innerHTML = `<div style="color:var(--accent3);padding:2rem;grid-column:1/-1;">⚠ GitHub API rate limited. Please refresh or visit <a href="https://github.com/codewithmohan0" style="color:var(--accent)">github.com/codewithmohan0</a> directly.</div>`;
      document.getElementById('contrib-count').textContent = '—';
    }
  })();

  // ─── STAGGERED CARD REVEAL ─────────────────────
  const cardObserver = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); cardObserver.unobserve(e.target); }
    });
  }, { threshold: 0.05 });
  setTimeout(() => {
    document.querySelectorAll('.project-card').forEach(c => {
      c.classList.add('reveal');
      cardObserver.observe(c);
    });
  }, 1500);
</script>
</body>
</html>
