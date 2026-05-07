[index.html](https://github.com/user-attachments/files/27470096/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CodeMind AI — Debug Smarter</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050A0E;
    --surface: #0C1419;
    --surface2: #111D25;
    --border: #1E3040;
    --accent: #00FFB2;
    --accent2: #FF4D6D;
    --accent3: #4DFFEF;
    --text: #E8F4F0;
    --muted: #5A7A8A;
    --mono: 'Space Mono', monospace;
    --sans: 'Syne', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    overflow-x: hidden;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.4;
  }

  /* ── GRID BACKGROUND ── */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,255,178,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,178,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  /* ── NAV ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1.2rem 4rem;
    background: rgba(5,10,14,0.85);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--border);
  }

  .logo {
    font-family: var(--mono);
    font-size: 1.1rem;
    color: var(--accent);
    letter-spacing: -0.02em;
  }

  .logo span { color: var(--accent2); }

  nav ul {
    display: flex;
    gap: 2.5rem;
    list-style: none;
  }

  nav ul a {
    text-decoration: none;
    color: var(--muted);
    font-size: 0.85rem;
    font-weight: 600;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  nav ul a:hover { color: var(--accent); }

  .nav-cta {
    background: var(--accent);
    color: var(--bg) !important;
    padding: 0.5rem 1.2rem;
    border-radius: 2px;
    font-family: var(--mono) !important;
    font-size: 0.75rem !important;
    letter-spacing: 0.05em !important;
  }

  .nav-cta:hover { background: var(--accent3); color: var(--bg) !important; }

  /* ── HERO ── */
  .hero {
    position: relative;
    z-index: 1;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 8rem 2rem 4rem;
    overflow: hidden;
  }

  .hero-glow {
    position: absolute;
    width: 700px;
    height: 700px;
    background: radial-gradient(circle, rgba(0,255,178,0.08) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    pointer-events: none;
    animation: pulse 4s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { transform: translate(-50%,-50%) scale(1); opacity: 0.8; }
    50% { transform: translate(-50%,-50%) scale(1.1); opacity: 1; }
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    font-family: var(--mono);
    font-size: 0.7rem;
    color: var(--accent);
    border: 1px solid rgba(0,255,178,0.3);
    padding: 0.35rem 0.8rem;
    border-radius: 100px;
    margin-bottom: 2rem;
    letter-spacing: 0.1em;
    animation: fadeUp 0.6s ease both;
  }

  .badge::before {
    content: '';
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent);
    animation: blink 1.5s step-end infinite;
  }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  h1 {
    font-size: clamp(3rem, 7vw, 6.5rem);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.04em;
    margin-bottom: 1.5rem;
    animation: fadeUp 0.7s 0.1s ease both;
  }

  h1 .line2 {
    display: block;
    color: transparent;
    -webkit-text-stroke: 1px rgba(0,255,178,0.5);
  }

  h1 .accent-word {
    color: var(--accent);
    position: relative;
  }

  .hero-sub {
    max-width: 540px;
    font-size: 1.05rem;
    color: var(--muted);
    line-height: 1.7;
    margin-bottom: 3rem;
    animation: fadeUp 0.7s 0.2s ease both;
  }

  .hero-actions {
    display: flex;
    gap: 1rem;
    align-items: center;
    animation: fadeUp 0.7s 0.3s ease both;
  }

  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    padding: 0.9rem 2.2rem;
    border-radius: 2px;
    font-family: var(--mono);
    font-size: 0.85rem;
    font-weight: 700;
    text-decoration: none;
    letter-spacing: 0.05em;
    transition: all 0.2s;
    border: none;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }

  .btn-primary::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.15), transparent);
    opacity: 0;
    transition: opacity 0.2s;
  }

  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 0 30px rgba(0,255,178,0.4); }
  .btn-primary:hover::after { opacity: 1; }

  .btn-ghost {
    color: var(--muted);
    padding: 0.9rem 2rem;
    font-family: var(--mono);
    font-size: 0.85rem;
    text-decoration: none;
    border: 1px solid var(--border);
    border-radius: 2px;
    transition: all 0.2s;
  }

  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ── CODE TERMINAL DEMO ── */
  .terminal-wrap {
    position: relative;
    z-index: 1;
    max-width: 820px;
    margin: 4rem auto;
    animation: fadeUp 0.8s 0.4s ease both;
  }

  .terminal {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 40px 80px rgba(0,0,0,0.5), 0 0 0 1px rgba(0,255,178,0.05);
  }

  .terminal-bar {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.8rem 1.2rem;
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
  }

  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot.red { background: #FF5F57; }
  .dot.yellow { background: #FFBC2E; }
  .dot.green { background: #28C941; }

  .terminal-title {
    flex: 1;
    text-align: center;
    font-family: var(--mono);
    font-size: 0.72rem;
    color: var(--muted);
  }

  .terminal-body {
    padding: 1.5rem;
    font-family: var(--mono);
    font-size: 0.82rem;
    line-height: 1.8;
  }

  .t-error { color: var(--accent2); }
  .t-comment { color: var(--muted); }
  .t-keyword { color: #C792EA; }
  .t-string { color: #C3E88D; }
  .t-fn { color: #82AAFF; }
  .t-num { color: #F78C6C; }
  .t-ai { color: var(--accent); }
  .t-fix { color: var(--accent3); }
  .t-divider { border: none; border-top: 1px solid var(--border); margin: 1rem 0; }
  .cursor { display: inline-block; width: 8px; height: 14px; background: var(--accent); animation: blink 1s step-end infinite; vertical-align: middle; }

  /* ── SECTION SHARED ── */
  section {
    position: relative;
    z-index: 1;
    padding: 6rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-label {
    font-family: var(--mono);
    font-size: 0.7rem;
    color: var(--accent);
    letter-spacing: 0.18em;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 3.2rem);
    font-weight: 800;
    letter-spacing: -0.03em;
    line-height: 1.1;
    margin-bottom: 1.2rem;
  }

  .section-sub {
    color: var(--muted);
    font-size: 1rem;
    line-height: 1.7;
    max-width: 520px;
  }

  /* ── SERVICES ── */
  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
    margin-top: 3.5rem;
  }

  .service-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 2rem;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
    cursor: default;
  }

  .service-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: var(--card-accent, var(--accent));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s;
  }

  .service-card:hover {
    transform: translateY(-6px);
    border-color: rgba(0,255,178,0.2);
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);
  }

  .service-card:hover::before { transform: scaleX(1); }

  .service-icon {
    width: 44px; height: 44px;
    display: flex; align-items: center; justify-content: center;
    background: rgba(0,255,178,0.08);
    border-radius: 4px;
    margin-bottom: 1.5rem;
    font-size: 1.4rem;
  }

  .service-card h3 {
    font-size: 1.1rem;
    font-weight: 700;
    margin-bottom: 0.7rem;
    letter-spacing: -0.02em;
  }

  .service-card p {
    font-size: 0.88rem;
    color: var(--muted);
    line-height: 1.65;
  }

  .service-card .tag {
    display: inline-block;
    margin-top: 1.2rem;
    font-family: var(--mono);
    font-size: 0.65rem;
    color: var(--card-accent, var(--accent));
    border: 1px solid currentColor;
    padding: 0.2rem 0.6rem;
    border-radius: 2px;
    opacity: 0.7;
  }

  /* ── HOW IT WORKS ── */
  .steps {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 0;
    margin-top: 3.5rem;
    position: relative;
  }

  .steps::before {
    content: '';
    position: absolute;
    top: 2rem;
    left: 12.5%; right: 12.5%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border) 20%, var(--border) 80%, transparent);
  }

  .step {
    padding: 0 1.5rem;
    text-align: center;
  }

  .step-num {
    width: 4rem; height: 4rem;
    border-radius: 50%;
    background: var(--surface);
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    margin: 0 auto 1.5rem;
    font-family: var(--mono);
    font-size: 1rem;
    font-weight: 700;
    color: var(--accent);
    position: relative;
    z-index: 1;
  }

  .step h4 { font-size: 0.95rem; font-weight: 700; margin-bottom: 0.6rem; }
  .step p { font-size: 0.82rem; color: var(--muted); line-height: 1.6; }

  /* ── LANGUAGES ── */
  .lang-scroll {
    overflow: hidden;
    margin: 3rem -4rem 0;
    padding: 0;
    position: relative;
  }

  .lang-scroll::before,
  .lang-scroll::after {
    content: '';
    position: absolute;
    top: 0; bottom: 0;
    width: 100px;
    z-index: 1;
  }

  .lang-scroll::before { left: 0; background: linear-gradient(90deg, var(--bg), transparent); }
  .lang-scroll::after { right: 0; background: linear-gradient(-90deg, var(--bg), transparent); }

  .lang-track {
    display: flex;
    gap: 1.5rem;
    animation: scroll 22s linear infinite;
    width: max-content;
  }

  @keyframes scroll {
    from { transform: translateX(0); }
    to   { transform: translateX(-50%); }
  }

  .lang-item {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    padding: 0.6rem 1.2rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 2px;
    font-family: var(--mono);
    font-size: 0.78rem;
    color: var(--muted);
    white-space: nowrap;
    transition: color 0.2s, border-color 0.2s;
  }

  /* ── STATS ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(4,1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    margin-top: 5rem;
  }

  .stat {
    background: var(--surface);
    padding: 2rem;
    text-align: center;
  }

  .stat-num {
    font-size: 2.8rem;
    font-weight: 800;
    letter-spacing: -0.04em;
    color: var(--accent);
    display: block;
    line-height: 1;
    margin-bottom: 0.4rem;
  }

  .stat-label {
    font-size: 0.78rem;
    color: var(--muted);
    font-family: var(--mono);
  }

  /* ── TESTIMONIALS ── */
  .testimonials {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 1.5rem;
    margin-top: 3.5rem;
  }

  .testi {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 1.8rem;
    transition: border-color 0.3s;
  }

  .testi:hover { border-color: rgba(0,255,178,0.2); }

  .testi-quote {
    font-size: 0.9rem;
    color: var(--text);
    line-height: 1.7;
    margin-bottom: 1.5rem;
    opacity: 0.85;
  }

  .testi-author {
    display: flex;
    align-items: center;
    gap: 0.8rem;
  }

  .avatar {
    width: 38px; height: 38px;
    border-radius: 50%;
    background: var(--surface2);
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-size: 1rem;
  }

  .author-name { font-size: 0.85rem; font-weight: 700; display: block; }
  .author-role { font-size: 0.72rem; color: var(--muted); font-family: var(--mono); }

  .stars { color: #FFD700; font-size: 0.75rem; margin-bottom: 1rem; letter-spacing: 0.1em; }

  /* ── PRICING ── */
  .pricing-grid {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 1.5rem;
    margin-top: 3.5rem;
    align-items: start;
  }

  .price-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 2rem;
    transition: transform 0.3s;
  }

  .price-card.featured {
    border-color: var(--accent);
    background: linear-gradient(135deg, rgba(0,255,178,0.05), var(--surface));
    transform: scale(1.04);
    box-shadow: 0 0 40px rgba(0,255,178,0.1);
  }

  .price-card:hover:not(.featured) { transform: translateY(-4px); }

  .plan-name {
    font-family: var(--mono);
    font-size: 0.75rem;
    color: var(--muted);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .price-amt {
    font-size: 2.6rem;
    font-weight: 800;
    letter-spacing: -0.04em;
    line-height: 1;
    margin-bottom: 0.3rem;
  }

  .price-amt sup { font-size: 1rem; font-weight: 400; }
  .price-amt span { font-size: 0.9rem; font-weight: 400; color: var(--muted); }
  .price-desc { font-size: 0.82rem; color: var(--muted); margin-bottom: 1.8rem; }

  .price-features {
    list-style: none;
    margin-bottom: 2rem;
    display: flex;
    flex-direction: column;
    gap: 0.7rem;
  }

  .price-features li {
    font-size: 0.84rem;
    display: flex;
    align-items: flex-start;
    gap: 0.6rem;
    color: var(--text);
    opacity: 0.85;
  }

  .price-features li::before {
    content: '✓';
    color: var(--accent);
    font-family: var(--mono);
    flex-shrink: 0;
  }

  /* ── CTA BANNER ── */
  .cta-banner {
    position: relative;
    z-index: 1;
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 5rem 4rem;
    text-align: center;
    overflow: hidden;
  }

  .cta-banner::before {
    content: '';
    position: absolute;
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,255,178,0.06) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%,-50%);
    pointer-events: none;
  }

  .cta-banner h2 {
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800;
    letter-spacing: -0.03em;
    margin-bottom: 1rem;
  }

  .cta-banner p { color: var(--muted); margin-bottom: 2.5rem; font-size: 1rem; }

  /* ── FOOTER ── */
  footer {
    position: relative;
    z-index: 1;
    padding: 3rem 4rem;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  footer p {
    font-family: var(--mono);
    font-size: 0.72rem;
    color: var(--muted);
  }

  footer nav ul {
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  footer nav ul a {
    color: var(--muted);
    text-decoration: none;
    font-family: var(--mono);
    font-size: 0.72rem;
    letter-spacing: 0.05em;
    transition: color 0.2s;
  }

  footer nav ul a:hover { color: var(--accent); }

  /* ── DEMO CHAT WIDGET ── */
  .demo-section {
    position: relative;
    z-index: 1;
    padding: 6rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .chat-demo {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    max-width: 720px;
    margin: 3rem auto 0;
    overflow: hidden;
    box-shadow: 0 30px 60px rgba(0,0,0,0.4);
  }

  .chat-header {
    background: var(--surface2);
    border-bottom: 1px solid var(--border);
    padding: 1rem 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.8rem;
  }

  .chat-header .ai-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    background: var(--accent);
    animation: blink 1.5s step-end infinite;
  }

  .chat-header-title {
    font-family: var(--mono);
    font-size: 0.8rem;
    color: var(--text);
  }

  .chat-messages {
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    min-height: 260px;
    max-height: 320px;
    overflow-y: auto;
    font-size: 0.85rem;
    line-height: 1.6;
  }

  .msg {
    display: flex;
    gap: 0.8rem;
    align-items: flex-start;
  }

  .msg-avatar {
    width: 30px; height: 30px;
    border-radius: 4px;
    background: var(--surface2);
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    font-size: 0.85rem;
    flex-shrink: 0;
  }

  .msg-avatar.ai { background: rgba(0,255,178,0.1); border-color: rgba(0,255,178,0.3); }

  .msg-bubble {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 0.7rem 1rem;
    flex: 1;
    color: var(--text);
    opacity: 0.9;
  }

  .msg-bubble.ai { border-color: rgba(0,255,178,0.15); background: rgba(0,255,178,0.04); }
  .msg-bubble code {
    font-family: var(--mono);
    font-size: 0.78rem;
    background: rgba(0,0,0,0.3);
    padding: 0.1rem 0.3rem;
    border-radius: 2px;
    color: var(--accent3);
  }

  .chat-input {
    display: flex;
    padding: 1rem 1.5rem;
    border-top: 1px solid var(--border);
    gap: 0.8rem;
  }

  .chat-input input {
    flex: 1;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 0.6rem 1rem;
    color: var(--text);
    font-family: var(--mono);
    font-size: 0.8rem;
    outline: none;
    transition: border-color 0.2s;
  }

  .chat-input input:focus { border-color: var(--accent); }
  .chat-input input::placeholder { color: var(--muted); }

  .chat-input button {
    background: var(--accent);
    color: var(--bg);
    border: none;
    border-radius: 3px;
    padding: 0.6rem 1.2rem;
    font-family: var(--mono);
    font-size: 0.78rem;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.2s;
  }

  .chat-input button:hover {
    box-shadow: 0 0 20px rgba(0,255,178,0.4);
    transform: translateY(-1px);
  }

  /* ── SCROLLBAR ── */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }

  @media (max-width: 900px) {
    nav { padding: 1rem 1.5rem; }
    nav ul { display: none; }
    section, .demo-section { padding: 4rem 1.5rem; }
    .services-grid, .testimonials, .pricing-grid { grid-template-columns: 1fr; }
    .steps { grid-template-columns: repeat(2,1fr); }
    .steps::before { display: none; }
    .stats-row { grid-template-columns: repeat(2,1fr); }
    .price-card.featured { transform: none; }
    footer { flex-direction: column; text-align: center; }
    .cta-banner { padding: 4rem 1.5rem; }
    h1 { font-size: 2.8rem; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="logo">Code<span>Mind</span>.ai</div>
  <ul>
    <li><a href="#services">Services</a></li>
    <li><a href="#how">How it Works</a></li>
    <li><a href="#demo">Demo</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#pricing" class="nav-cta">Get Started →</a></li>
  </ul>
</nav>

<!-- HERO -->
<div class="hero">
  <div class="hero-glow"></div>
  <div class="badge">AI-Powered Code Intelligence · v2.0</div>
  <h1>
    Debug Faster.<br>
    <span class="line2">Ship <span class="accent-word">Smarter.</span></span>
  </h1>
  <p class="hero-sub">
    CodeMind is your AI pair programmer — paste any error, describe any bug,
    and get instant, precise fixes with clear explanations. Built for developers who value their time.
  </p>
  <div class="hero-actions">
    <a href="#demo" class="btn-primary">Try it Free →</a>
    <a href="#services" class="btn-ghost">See Services</a>
  </div>
</div>

<!-- TERMINAL -->
<div class="terminal-wrap" style="padding:0 2rem;">
  <div class="terminal">
    <div class="terminal-bar">
      <div class="dot red"></div>
      <div class="dot yellow"></div>
      <div class="dot green"></div>
      <div class="terminal-title">codemind — debug session</div>
    </div>
    <div class="terminal-body">
      <div><span class="t-comment">// Your error → CodeMind's fix</span></div>
      <div>&nbsp;</div>
      <div><span class="t-error">TypeError: Cannot read properties of undefined (reading 'map')</span></div>
      <div><span class="t-comment">&nbsp;&nbsp;at UserList (/app/components/UserList.jsx:14:22)</span></div>
      <div>&nbsp;</div>
      <hr class="t-divider">
      <div><span class="t-ai">⚡ CodeMind AI Analysis:</span></div>
      <div>&nbsp;</div>
      <div><span class="t-comment">// ✗ Before — users may be undefined on first render</span></div>
      <div><span class="t-keyword">const</span> UserList = ({ users }) => (</div>
      <div>&nbsp;&nbsp;<span class="t-fn">users</span>.map(u => &lt;div key={u.id}&gt;{u.name}&lt;/div&gt;)</div>
      <div>);</div>
      <div>&nbsp;</div>
      <div><span class="t-comment">// ✓ Fix — add optional chaining + fallback</span></div>
      <div><span class="t-keyword">const</span> UserList = ({ users <span class="t-ai">= []</span> }) => (</div>
      <div>&nbsp;&nbsp;<span class="t-fn">users</span><span class="t-fix">?.</span>map(u => &lt;div key={u.id}&gt;{u.name}&lt;/div&gt;) <span class="t-fix">?? null</span></div>
      <div>);</div>
      <div>&nbsp;</div>
      <div><span class="t-ai">✓ Fixed in 0.4s — root cause: prop not initialized before async fetch completes</span> <span class="cursor"></span></div>
    </div>
  </div>
</div>

<!-- SERVICES -->
<section id="services">
  <div class="section-label">// services</div>
  <div class="section-title">Everything a developer needs</div>
  <div class="section-sub">From cryptic stack traces to complex architectural decisions — CodeMind has you covered across the entire development lifecycle.</div>
  <div class="services-grid">
    <div class="service-card" style="--card-accent:#00FFB2">
      <div class="service-icon">🐛</div>
      <h3>Error Diagnosis</h3>
      <p>Paste any stack trace, runtime error, or exception. Get a root-cause analysis with step-by-step fixes in seconds, not hours.</p>
      <span class="tag">INSTANT FIX</span>
    </div>
    <div class="service-card" style="--card-accent:#4DFFEF">
      <div class="service-icon">🔍</div>
      <h3>Code Review AI</h3>
      <p>Submit your pull requests for AI-powered review. Catch bugs, security holes, performance issues, and anti-patterns before they ship.</p>
      <span class="tag">AUTOMATED</span>
    </div>
    <div class="service-card" style="--card-accent:#FF4D6D">
      <div class="service-icon">⚡</div>
      <h3>Performance Optimizer</h3>
      <p>Identify slow queries, memory leaks, and bottlenecks. Get concrete optimization suggestions with benchmarks and before/after comparisons.</p>
      <span class="tag">PROFILER</span>
    </div>
    <div class="service-card" style="--card-accent:#C792EA">
      <div class="service-icon">🔄</div>
      <h3>Code Refactoring</h3>
      <p>Transform messy, legacy code into clean, maintainable architecture. Supports modern patterns for React, Python, Go, Rust, and more.</p>
      <span class="tag">MODERNIZE</span>
    </div>
    <div class="service-card" style="--card-accent:#82AAFF">
      <div class="service-icon">📚</div>
      <h3>Docs Generator</h3>
      <p>Auto-generate clear, accurate documentation for any function, class, or API endpoint. JSDoc, docstrings, OpenAPI — all formats supported.</p>
      <span class="tag">AUTODOC</span>
    </div>
    <div class="service-card" style="--card-accent:#F78C6C">
      <div class="service-icon">🛡️</div>
      <h3>Security Scanner</h3>
      <p>Detect SQL injection, XSS, CSRF, and dependency vulnerabilities. Get remediation code, not just warnings — so you can patch immediately.</p>
      <span class="tag">CVE AWARE</span>
    </div>
  </div>
</section>

<!-- LANGUAGE SCROLL -->
<section style="padding: 2rem 4rem">
  <div class="section-label" style="text-align:center;margin-bottom:2rem;">// supported languages & frameworks</div>
  <div class="lang-scroll">
    <div class="lang-track">
      <!-- duplicate for infinite loop -->
      <div class="lang-item">🐍 Python</div>
      <div class="lang-item">⚛️ React</div>
      <div class="lang-item">🟨 JavaScript</div>
      <div class="lang-item">🔷 TypeScript</div>
      <div class="lang-item">☕ Java</div>
      <div class="lang-item">🦀 Rust</div>
      <div class="lang-item">🐹 Go</div>
      <div class="lang-item">💜 C++</div>
      <div class="lang-item">🔴 Ruby</div>
      <div class="lang-item">🐘 PHP</div>
      <div class="lang-item">🍃 Node.js</div>
      <div class="lang-item">🐦 Swift</div>
      <div class="lang-item">🤖 Kotlin</div>
      <div class="lang-item">🎯 Dart</div>
      <div class="lang-item">🐍 Python</div>
      <div class="lang-item">⚛️ React</div>
      <div class="lang-item">🟨 JavaScript</div>
      <div class="lang-item">🔷 TypeScript</div>
      <div class="lang-item">☕ Java</div>
      <div class="lang-item">🦀 Rust</div>
      <div class="lang-item">🐹 Go</div>
      <div class="lang-item">💜 C++</div>
      <div class="lang-item">🔴 Ruby</div>
      <div class="lang-item">🐘 PHP</div>
      <div class="lang-item">🍃 Node.js</div>
      <div class="lang-item">🐦 Swift</div>
      <div class="lang-item">🤖 Kotlin</div>
      <div class="lang-item">🎯 Dart</div>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section id="how">
  <div class="section-label">// how it works</div>
  <div class="section-title">From error to fix in 4 steps</div>
  <div class="steps">
    <div class="step">
      <div class="step-num">01</div>
      <h4>Paste Your Code</h4>
      <p>Drop in your error message, code snippet, or describe your problem in plain English.</p>
    </div>
    <div class="step">
      <div class="step-num">02</div>
      <h4>AI Analyzes</h4>
      <p>CodeMind scans for root causes, related patterns, and known issues across millions of cases.</p>
    </div>
    <div class="step">
      <div class="step-num">03</div>
      <h4>Get the Fix</h4>
      <p>Receive corrected code with a clear explanation of what went wrong and why.</p>
    </div>
    <div class="step">
      <div class="step-num">04</div>
      <h4>Ship Confidently</h4>
      <p>Apply the fix, run the tests, and deploy. CodeMind learns your codebase over time.</p>
    </div>
  </div>

  <!-- STATS -->
  <div class="stats-row">
    <div class="stat"><span class="stat-num">98%</span><span class="stat-label">Fix Accuracy Rate</span></div>
    <div class="stat"><span class="stat-num">0.4s</span><span class="stat-label">Average Response Time</span></div>
    <div class="stat"><span class="stat-num">50K+</span><span class="stat-label">Active Developers</span></div>
    <div class="stat"><span class="stat-num">2M+</span><span class="stat-label">Bugs Fixed This Month</span></div>
  </div>
</section>

<!-- LIVE DEMO -->
<div class="demo-section" id="demo">
  <div class="section-label">// live demo</div>
  <div class="section-title">Try it right now</div>
  <div class="section-sub">No signup needed. Paste an error or describe your bug and see CodeMind in action.</div>

  <div class="chat-demo">
    <div class="chat-header">
      <div class="ai-dot"></div>
      <div class="chat-header-title">CodeMind AI — Ready</div>
    </div>
    <div class="chat-messages" id="chatMessages">
      <div class="msg">
        <div class="msg-avatar ai">🤖</div>
        <div class="msg-bubble ai">Hey! Paste your error message or code snippet below and I'll diagnose it instantly. I support all major languages and frameworks.</div>
      </div>
    </div>
    <div class="chat-input">
      <input type="text" id="chatInput" placeholder="Paste your error or describe your bug..." />
      <button onclick="sendMessage()">Send →</button>
    </div>
  </div>
</div>

<!-- TESTIMONIALS -->
<section>
  <div class="section-label">// testimonials</div>
  <div class="section-title">Loved by developers worldwide</div>
  <div class="testimonials">
    <div class="testi">
      <div class="stars">★★★★★</div>
      <div class="testi-quote">"CodeMind found a race condition in our Node.js service that we'd been chasing for three weeks. It explained the issue clearly and gave us the exact fix. Incredible."</div>
      <div class="testi-author">
        <div class="avatar">👨‍💻</div>
        <div>
          <span class="author-name">Marcus Chen</span>
          <span class="author-role">Senior Backend Engineer @ Stripe</span>
        </div>
      </div>
    </div>
    <div class="testi">
      <div class="stars">★★★★★</div>
      <div class="testi-quote">"I use CodeMind every day. It's like having a senior dev sitting next to me. The explanations actually teach me why something went wrong, not just how to patch it."</div>
      <div class="testi-author">
        <div class="avatar">👩‍💻</div>
        <div>
          <span class="author-name">Priya Nair</span>
          <span class="author-role">Fullstack Developer @ Vercel</span>
        </div>
      </div>
    </div>
    <div class="testi">
      <div class="stars">★★★★★</div>
      <div class="testi-quote">"We integrated CodeMind into our CI pipeline for automated code review. It catches real security issues and performance problems that our team was missing. Worth every penny."</div>
      <div class="testi-author">
        <div class="avatar">🧑‍💻</div>
        <div>
          <span class="author-name">Alex Rivera</span>
          <span class="author-role">CTO @ DevFlow Labs</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section id="pricing">
  <div class="section-label">// pricing</div>
  <div class="section-title">Simple, honest pricing</div>
  <div class="section-sub">No hidden fees. Cancel anytime. Start free.</div>
  <div class="pricing-grid">
    <div class="price-card">
      <div class="plan-name">// Starter</div>
      <div class="price-amt"><sup>$</sup>0 <span>/ mo</span></div>
      <div class="price-desc">For developers getting started</div>
      <ul class="price-features">
        <li>50 AI queries / month</li>
        <li>Error diagnosis & fixes</li>
        <li>5 languages supported</li>
        <li>Community support</li>
      </ul>
      <a href="#" class="btn-ghost" style="display:block;text-align:center;padding:0.75rem;">Get Started Free</a>
    </div>
    <div class="price-card featured">
      <div class="plan-name" style="color:var(--accent);">// Pro ⭐</div>
      <div class="price-amt"><sup>$</sup>19 <span>/ mo</span></div>
      <div class="price-desc">For professional developers</div>
      <ul class="price-features">
        <li>Unlimited AI queries</li>
        <li>All 6 services included</li>
        <li>All languages & frameworks</li>
        <li>Priority response (&lt;0.4s)</li>
        <li>VS Code & JetBrains plugin</li>
        <li>Chat history & saved fixes</li>
      </ul>
      <a href="#" class="btn-primary" style="display:block;text-align:center;">Start Pro Trial →</a>
    </div>
    <div class="price-card">
      <div class="plan-name">// Team</div>
      <div class="price-amt"><sup>$</sup>49 <span>/ mo</span></div>
      <div class="price-desc">Per seat, for engineering teams</div>
      <ul class="price-features">
        <li>Everything in Pro</li>
        <li>Shared team context</li>
        <li>CI/CD pipeline integration</li>
        <li>Codebase-aware analysis</li>
        <li>Admin dashboard & analytics</li>
        <li>Dedicated Slack support</li>
      </ul>
      <a href="#" class="btn-ghost" style="display:block;text-align:center;padding:0.75rem;">Contact Sales</a>
    </div>
  </div>
</section>

<!-- CTA -->
<div class="cta-banner">
  <div class="badge" style="margin:0 auto 1.5rem;">Join 50,000+ developers</div>
  <h2>Stop wrestling with bugs.<br>Start building.</h2>
  <p>Your first 50 fixes are completely free. No credit card required.</p>
  <a href="#demo" class="btn-primary">Try CodeMind Free →</a>
</div>

<!-- FOOTER -->
<footer>
  <div class="logo">Code<span>Mind</span>.ai</div>
  <nav>
    <ul>
      <li><a href="#">Privacy</a></li>
      <li><a href="#">Terms</a></li>
      <li><a href="#">Blog</a></li>
      <li><a href="#">Docs</a></li>
      <li><a href="#">Status</a></li>
    </ul>
  </nav>
  <p>© 2026 CodeMind AI. Built for developers, by developers.</p>
</footer>

<script>
const responses = [
  (msg) => `**Root Cause Identified:** The error in your code is likely due to an uninitialized variable or async timing issue.\n\n**Fix:** Add proper null checks and ensure your async operations complete before accessing the data.\n\n\`\`\`\nif (!data || !data.length) return null;\n\`\`\`\n\nThis pattern prevents undefined access errors in 90% of similar cases.`,
  (msg) => `**Diagnosis Complete:** I've analyzed your problem. This looks like a classic closure/scope issue in a loop.\n\n**Fix:** Replace \`var\` with \`let\` or use \`.forEach()\` instead of a \`for\` loop to create proper block scope for each iteration.\n\nThe fix is minimal but the impact is significant — this is one of JavaScript's most common gotchas.`,
  (msg) => `**Security Issue Detected:** Your query appears vulnerable to SQL injection. Never concatenate user input directly into queries.\n\n**Fix:** Use parameterized queries:\n\`db.query("SELECT * FROM users WHERE id = ?", [userId])\`\n\nThis completely eliminates the injection vector and is a drop-in replacement.`,
  (msg) => `**Performance Bottleneck Found:** The nested loop creates O(n²) complexity. For large datasets this will be very slow.\n\n**Fix:** Convert the inner array to a \`Set\` or \`Map\` for O(1) lookups:\n\`const lookup = new Map(items.map(i => [i.id, i]));\`\n\nThis reduces your time complexity to O(n) — up to 1000x faster on large datasets.`,
];

let msgCount = 0;

async function sendMessage() {
  const input = document.getElementById('chatInput');
  const messages = document.getElementById('chatMessages');
  const text = input.value.trim();
  if (!text) return;

  // User message
  messages.innerHTML += `
    <div class="msg">
      <div class="msg-avatar">👤</div>
      <div class="msg-bubble">${escapeHtml(text)}</div>
    </div>
  `;
  input.value = '';
  messages.scrollTop = messages.scrollHeight;

  // Typing indicator
  const typingId = 'typing-' + Date.now();
  messages.innerHTML += `
    <div class="msg" id="${typingId}">
      <div class="msg-avatar ai">🤖</div>
      <div class="msg-bubble ai" style="color:var(--muted);font-family:var(--mono);font-size:0.78rem;">Analyzing<span class="cursor"></span></div>
    </div>
  `;
  messages.scrollTop = messages.scrollHeight;

  // Simulate AI response
  await sleep(900 + Math.random() * 600);
  document.getElementById(typingId)?.remove();

  const response = responses[msgCount % responses.length](text);
  msgCount++;

  messages.innerHTML += `
    <div class="msg">
      <div class="msg-avatar ai">🤖</div>
      <div class="msg-bubble ai">${formatResponse(response)}</div>
    </div>
  `;
  messages.scrollTop = messages.scrollHeight;
}

function formatResponse(text) {
  return text
    .replace(/\*\*(.*?)\*\*/g, '<strong style="color:var(--accent)">$1</strong>')
    .replace(/`([^`]+)`/g, '<code>$1</code>')
    .replace(/\n/g, '<br>');
}

function escapeHtml(t) {
  return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }

document.getElementById('chatInput').addEventListener('keydown', e => {
  if (e.key === 'Enter') sendMessage();
});

// Animate sections on scroll
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.style.animation = 'fadeUp 0.6s ease both';
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.service-card, .step, .testi, .price-card, .stat').forEach(el => {
  el.style.opacity = '0';
  observer.observe(el);
});
</script>
</body>
</html>
