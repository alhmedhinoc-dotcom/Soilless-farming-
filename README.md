# Soilless-farming-<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
<meta name="apple-mobile-web-app-title" content="GrowSmart" />
<meta name="theme-color" content="#0d2818" />
<meta name="description" content="Learn soilless farming — hydroponics, aeroponics, aquaponics and more." />
<title>GrowSmart — Soilless Farming</title>

<!-- PWA Manifest inline -->

<script>
const manifest = {
  name: "GrowSmart — Soilless Farming",
  short_name: "GrowSmart",
  description: "Learn soilless farming techniques",
  start_url: "/",
  display: "standalone",
  background_color: "#0d2818",
  theme_color: "#0d2818",
  orientation: "portrait",
  icons: [
    { src: "data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 192 192'><rect width='192' height='192' rx='40' fill='%230d2818'/><text y='130' x='96' text-anchor='middle' font-size='110'>🌿</text></svg>", sizes: "192x192", type: "image/svg+xml" },
    { src: "data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'><rect width='512' height='512' rx='100' fill='%230d2818'/><text y='360' x='256' text-anchor='middle' font-size='300'>🌿</text></svg>", sizes: "512x512", type: "image/svg+xml" }
  ]
};
const blob = new Blob([JSON.stringify(manifest)], {type:'application/json'});
const manifestURL = URL.createObjectURL(blob);
const link = document.createElement('link');
link.rel = 'manifest'; link.href = manifestURL;
document.head.appendChild(link);
</script>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Outfit:wght@300;400;500;600;700&display=swap" rel="stylesheet" />

<style>
:root {
  --green-deep: #0d2818;
  --green-mid: #1a4a2e;
  --green-bright: #2d7a4f;
  --green-light: #4caf78;
  --green-glow: #6fcf97;
  --lime: #a8e063;
  --text: #f0ece4;
  --muted: #7a9e88;
  --surface: rgba(255,255,255,0.05);
  --surface2: rgba(255,255,255,0.08);
  --border: rgba(255,255,255,0.09);
  --nav-h: 68px;
  --safe-bottom: env(safe-area-inset-bottom, 0px);
  --safe-top: env(safe-area-inset-top, 0px);
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

html, body {
  height: 100%;
  overscroll-behavior: none;
}

body {
  font-family: 'Outfit', sans-serif;
  background: var(--green-deep);
  color: var(--text);
  overflow: hidden;
}

/* ── SPLASH SCREEN ─────────────────────────────────────── */
#splash {
  position: fixed;
  inset: 0;
  background: var(--green-deep);
  z-index: 9999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
  transition: opacity 0.6s ease, transform 0.6s ease;
}

#splash.hide {
  opacity: 0;
  transform: scale(1.05);
  pointer-events: none;
}

.splash-icon {
  font-size: 80px;
  animation: splashBounce 1s cubic-bezier(0.34,1.56,0.64,1) both;
}
@keyframes splashBounce {
  from { transform: scale(0.3) rotate(-20deg); opacity: 0; }
  to   { transform: scale(1) rotate(0deg); opacity: 1; }
}

.splash-title {
  font-family: 'Playfair Display', serif;
  font-size: 2.4rem;
  font-weight: 900;
  color: var(--lime);
  letter-spacing: -0.03em;
  animation: fadeUp 0.6s 0.3s ease both;
}

.splash-sub {
  color: var(--muted);
  font-size: 0.88rem;
  animation: fadeUp 0.6s 0.5s ease both;
}

.splash-bar {
  width: 160px;
  height: 3px;
  background: var(--border);
  border-radius: 100px;
  overflow: hidden;
  margin-top: 12px;
  animation: fadeUp 0.6s 0.6s ease both;
}
.splash-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--green-bright), var(--lime));
  border-radius: 100px;
  animation: splashLoad 1.6s 0.5s ease forwards;
}
@keyframes splashLoad {
  from { width: 0; }
  to   { width: 100%; }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* ── APP SHELL ─────────────────────────────────────────── */
#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  height: 100dvh;
}

/* ── TOP BAR ───────────────────────────────────────────── */
.topbar {
  padding: calc(var(--safe-top) + 14px) 20px 14px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(13,40,24,0.95);
  backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
  z-index: 50;
}

.topbar-logo {
  font-family: 'Playfair Display', serif;
  font-size: 1.25rem;
  font-weight: 900;
  color: var(--lime);
  display: flex;
  align-items: center;
  gap: 8px;
}

.topbar-logo .icon-box {
  width: 32px; height: 32px;
  background: linear-gradient(135deg, var(--green-bright), var(--lime));
  border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  font-size: 16px;
}

.status-dot {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 0.72rem;
  font-weight: 600;
  color: var(--green-glow);
  background: rgba(111,207,151,0.1);
  border: 1px solid rgba(111,207,151,0.2);
  padding: 5px 11px;
  border-radius: 100px;
}
.dot-pulse {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--lime);
  animation: pulse 1.8s ease infinite;
}
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(0.7); }
}

/* ── PAGE CONTAINER ────────────────────────────────────── */
#pages {
  flex: 1;
  overflow: hidden;
  position: relative;
}

.page {
  position: absolute;
  inset: 0;
  overflow-y: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
  padding: 20px 18px calc(var(--nav-h) + var(--safe-bottom) + 20px);
  opacity: 0;
  transform: translateX(30px);
  pointer-events: none;
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.page.active {
  opacity: 1;
  transform: translateX(0);
  pointer-events: all;
}

.page.exit-left {
  opacity: 0;
  transform: translateX(-30px);
}

/* ── BOTTOM NAV ────────────────────────────────────────── */
.bottom-nav {
  position: fixed;
  bottom: 0; left: 0; right: 0;
  height: calc(var(--nav-h) + var(--safe-bottom));
  padding-bottom: var(--safe-bottom);
  background: rgba(13,40,24,0.97);
  backdrop-filter: blur(20px);
  border-top: 1px solid var(--border);
  display: flex;
  align-items: flex-start;
  justify-content: space-around;
  padding-top: 8px;
  z-index: 50;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3px;
  cursor: pointer;
  padding: 6px 12px;
  border-radius: 12px;
  transition: all 0.2s;
  border: none;
  background: transparent;
  flex: 1;
}

.nav-icon {
  font-size: 22px;
  transition: transform 0.2s cubic-bezier(0.34,1.56,0.64,1);
}
.nav-label {
  font-size: 0.65rem;
  font-weight: 600;
  color: var(--muted);
  letter-spacing: 0.02em;
  transition: color 0.2s;
}

.nav-item.active .nav-icon { transform: scale(1.2); }
.nav-item.active .nav-label { color: var(--lime); }
.nav-item:active .nav-icon { transform: scale(0.9); }

/* ── SECTION HEADERS ───────────────────────────────────── */
.page-header {
  margin-bottom: 22px;
}
.chip {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 0.68rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--lime);
  margin-bottom: 8px;
}
.chip::before { content:''; width:18px; height:1px; background:var(--lime); }

.page-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.6rem, 6vw, 2.2rem);
  font-weight: 900;
  line-height: 1.15;
  letter-spacing: -0.02em;
}
.page-title em { font-style: italic; color: var(--lime); }

.page-sub {
  color: var(--muted);
  font-size: 0.85rem;
  line-height: 1.7;
  margin-top: 8px;
}

/* ── HOME PAGE ─────────────────────────────────────────── */
.hero-card {
  background: linear-gradient(135deg, var(--green-mid) 0%, #0d2818 100%);
  border: 1px solid rgba(168,224,99,0.2);
  border-radius: 20px;
  padding: 28px 24px;
  margin-bottom: 20px;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.hero-card::before {
  content: '🌿';
  position: absolute;
  font-size: 120px;
  top: -20px; right: -20px;
  opacity: 0.07;
  pointer-events: none;
}

.hero-big {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.8rem, 7vw, 2.6rem);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 10px;
}
.hero-big em { font-style: italic; color: var(--lime); }

.hero-desc {
  color: var(--muted);
  font-size: 0.85rem;
  line-height: 1.7;
  margin-bottom: 18px;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: 'Outfit', sans-serif;
  font-weight: 700;
  font-size: 0.85rem;
  padding: 12px 24px;
  border-radius: 100px;
  border: none;
  cursor: pointer;
  transition: all 0.2s;
  text-decoration: none;
}
.btn-lime { background: var(--lime); color: #0d2818; }
.btn-lime:active { transform: scale(0.96); background: #bfee7a; }
.btn-ghost { background: var(--surface); border: 1px solid var(--border); color: var(--muted); }
.btn-ghost:active { transform: scale(0.96); }

.quick-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-bottom: 22px;
}
.stat-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px 10px;
  text-align: center;
}
.stat-num {
  font-family: 'Playfair Display', serif;
  font-size: 1.6rem;
  font-weight: 900;
  color: var(--lime);
  line-height: 1;
}
.stat-lbl { font-size: 0.68rem; color: var(--muted); margin-top: 4px; line-height: 1.3; }

.home-section-title {
  font-family: 'Playfair Display', serif;
  font-weight: 700;
  font-size: 1.1rem;
  margin-bottom: 14px;
}

.lesson-list { display: flex; flex-direction: column; gap: 10px; }
.lesson-card {
  display: flex;
  align-items: center;
  gap: 14px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px;
  cursor: pointer;
  transition: all 0.2s;
  border: none;
  width: 100%;
  text-align: left;
  color: var(--text);
  font-family: 'Outfit', sans-serif;
}
.lesson-card:active { transform: scale(0.98); background: var(--surface2); }
.lesson-icon-box {
  width: 44px; height: 44px;
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  font-size: 22px;
  flex-shrink: 0;
  background: var(--surface2);
}
.lesson-text h4 { font-weight: 600; font-size: 0.9rem; margin-bottom: 2px; }
.lesson-text p { font-size: 0.75rem; color: var(--muted); }
.lesson-arrow { margin-left: auto; color: var(--muted); font-size: 0.9rem; flex-shrink: 0; }

/* ── LEARN PAGE ────────────────────────────────────────── */
.method-tabs {
  display: flex;
  gap: 8px;
  overflow-x: auto;
  padding-bottom: 4px;
  scrollbar-width: none;
  margin-bottom: 20px;
}
.method-tabs::-webkit-scrollbar { display: none; }

.mtab {
  flex-shrink: 0;
  padding: 8px 18px;
  border-radius: 100px;
  font-size: 0.8rem;
  font-weight: 600;
  cursor: pointer;
  border: 1px solid var(--border);
  color: var(--muted);
  background: transparent;
  transition: all 0.2s;
  font-family: 'Outfit', sans-serif;
  white-space: nowrap;
}
.mtab.active { background: var(--lime); color: #0d2818; border-color: var(--lime); }
.mtab:active { transform: scale(0.95); }

.method-content { display: none; }
.method-content.active { display: block; }

.method-header {
  background: linear-gradient(135deg, var(--green-mid), var(--green-deep));
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 22px;
  margin-bottom: 16px;
}
.method-header h3 {
  font-family: 'Playfair Display', serif;
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 8px;
}
.method-header p { color: var(--muted); font-size: 0.84rem; line-height: 1.7; }

.diagram-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 18px;
  margin-bottom: 16px;
  text-align: center;
}
.diagram-card h4 {
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 14px;
}
.diagram-card svg { width: 100%; max-width: 300px; height: auto; }

.facts-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 18px 20px;
}
.facts-card h4 { font-size: 0.78rem; font-weight: 700; margin-bottom: 14px; color: var(--lime); letter-spacing: 0.04em; text-transform: uppercase; }
.fact-row {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  padding: 10px 0;
  border-bottom: 1px solid var(--border);
  font-size: 0.83rem;
  color: var(--muted);
}
.fact-row:last-child { border: none; }
.fact-row .dot { color: var(--lime); flex-shrink: 0; margin-top: 1px; }

/* ── NUTRIENTS PAGE ────────────────────────────────────── */
.nutrient-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 18px;
  margin-bottom: 12px;
  transition: all 0.2s;
}
.nutrient-card:active { transform: scale(0.98); }

.nutrient-top {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-bottom: 10px;
}
.nutrient-symbol {
  width: 44px; height: 44px;
  border-radius: 12px;
  background: linear-gradient(135deg, var(--green-mid), var(--green-bright));
  border: 1px solid rgba(168,224,99,0.2);
  display: flex; align-items: center; justify-content: center;
  font-family: 'Playfair Display', serif;
  font-weight: 900;
  font-size: 1.1rem;
  color: var(--lime);
  flex-shrink: 0;
}
.nutrient-name { font-weight: 600; font-size: 0.95rem; }
.nutrient-type { font-size: 0.7rem; color: var(--muted); margin-top: 2px; }

.nutrient-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}
.nutrient-info-box {
  background: rgba(255,255,255,0.03);
  border-radius: 10px;
  padding: 10px 12px;
}
.nutrient-info-label { font-size: 0.65rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.06em; color: var(--muted); margin-bottom: 3px; }
.nutrient-info-val { font-size: 0.8rem; color: var(--text); line-height: 1.4; }

/* ── QUIZ PAGE ─────────────────────────────────────────── */
.quiz-wrap {
  max-width: 480px;
  margin: 0 auto;
}

.quiz-progress-bar-wrap {
  height: 4px;
  background: var(--border);
  border-radius: 100px;
  overflow: hidden;
  margin-bottom: 24px;
}
.quiz-bar-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--green-bright), var(--lime));
  border-radius: 100px;
  transition: width 0.4s ease;
}

.q-counter { font-size: 0.72rem; color: var(--muted); font-weight: 600; margin-bottom: 10px; }

.q-text {
  font-family: 'Playfair Display', serif;
  font-size: 1.15rem;
  font-weight: 700;
  line-height: 1.4;
  margin-bottom: 22px;
}

.q-opts { display: flex; flex-direction: column; gap: 10px; }
.q-opt {
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: 13px;
  padding: 14px 16px;
  color: var(--muted);
  font-family: 'Outfit', sans-serif;
  font-size: 0.88rem;
  cursor: pointer;
  text-align: left;
  transition: all 0.15s;
  width: 100%;
  line-height: 1.4;
}
.q-opt:active { transform: scale(0.98); }
.q-opt.correct { border-color: var(--green-light); background: rgba(76,175,120,0.1); color: var(--green-glow); }
.q-opt.wrong { border-color: #e05252; background: rgba(224,82,82,0.08); color: #e05252; }

.q-feedback {
  margin-top: 14px;
  padding: 13px 16px;
  border-radius: 12px;
  font-size: 0.82rem;
  line-height: 1.5;
  display: none;
}
.q-feedback.show { display: block; }
.q-feedback.ok { background: rgba(76,175,120,0.1); color: var(--green-glow); border: 1px solid rgba(76,175,120,0.2); }
.q-feedback.err { background: rgba(224,82,82,0.08); color: #e05252; border: 1px solid rgba(224,82,82,0.2); }

.q-next-wrap { margin-top: 18px; text-align: right; }

.score-screen { text-align: center; padding: 20px 0; display: none; }
.score-screen.show { display: block; }
.score-big {
  font-family: 'Playfair Display', serif;
  font-size: 5rem;
  font-weight: 900;
  color: var(--lime);
  line-height: 1;
  margin-bottom: 6px;
}
.score-sub { color: var(--muted); font-size: 0.88rem; margin-bottom: 24px; }

/* ── GLOSSARY PAGE ─────────────────────────────────────── */
.gloss-search {
  position: relative;
  margin-bottom: 18px;
}
.gloss-search input {
  width: 100%;
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: 13px;
  color: var(--text);
  font-family: 'Outfit', sans-serif;
  font-size: 0.88rem;
  padding: 13px 16px 13px 42px;
  outline: none;
  transition: border-color 0.2s;
}
.gloss-search input:focus { border-color: var(--lime); }
.gloss-search input::placeholder { color: var(--muted); }
.gloss-search-icon {
  position: absolute;
  left: 14px; top: 50%;
  transform: translateY(-50%);
  font-size: 16px;
  pointer-events: none;
}

.gloss-item {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px 18px;
  margin-bottom: 10px;
  transition: all 0.2s;
}
.gloss-term { font-weight: 700; font-size: 0.9rem; color: var(--lime); margin-bottom: 5px; }
.gloss-def { font-size: 0.82rem; color: var(--muted); line-height: 1.6; }

/* ── CYCLE SECTION ─────────────────────────────────────── */
.cycle-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  margin-top: 16px;
}
.cycle-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 18px 14px;
  text-align: center;
  position: relative;
}
.cycle-num {
  position: absolute;
  top: -9px; left: 50%;
  transform: translateX(-50%);
  background: var(--lime);
  color: #0d2818;
  width: 20px; height: 20px;
  border-radius: 50%;
  font-size: 0.65rem;
  font-weight: 800;
  display: flex; align-items: center; justify-content: center;
}
.cycle-emoji { font-size: 1.8rem; margin-bottom: 8px; }
.cycle-name { font-weight: 600; font-size: 0.82rem; margin-bottom: 4px; }
.cycle-desc { font-size: 0.72rem; color: var(--muted); line-height: 1.4; }

/* ── OFFLINE BANNER ────────────────────────────────────── */
#offlineBanner {
  display: none;
  position: fixed;
  top: 60px; left: 16px; right: 16px;
  background: #2c1a10;
  border: 1px solid #8b4513;
  border-radius: 12px;
  padding: 10px 16px;
  font-size: 0.8rem;
  color: #f4a261;
  z-index: 200;
  text-align: center;
}

/* scrollbar hidden for all pages */
.page::-webkit-scrollbar { display: none; }
.page { scrollbar-width: none; }
</style>

</head>
<body>

<!-- OFFLINE BANNER -->

<div id="offlineBanner">📡 You're offline — all content still available!</div>

<!-- SPLASH SCREEN -->

<div id="splash">
  <div class="splash-icon">🌿</div>
  <div class="splash-title">GrowSmart</div>
  <div class="splash-sub">Soilless Farming Guide</div>
  <div class="splash-bar"><div class="splash-fill"></div></div>
</div>

<!-- APP -->

<div id="app">

  <!-- TOP BAR -->

  <div class="topbar">
    <div class="topbar-logo">
      <div class="icon-box">🌿</div>
      GrowSmart
    </div>
    <div class="status-dot">
      <div class="dot-pulse"></div>
      Live
    </div>
  </div>

  <!-- PAGES -->

  <div id="pages">

```
<!-- ── HOME ── -->
<div class="page active" id="page-home">
  <div class="hero-card">
    <div class="hero-big">Farming Without <em>Soil</em></div>
    <div class="hero-desc">Discover modern techniques that grow more food using less water, no pesticides, and zero soil.</div>
    <button class="btn btn-lime" onclick="goTo('learn')">Start Learning →</button>
  </div>

  <div class="quick-stats">
    <div class="stat-card">
      <div class="stat-num">90%</div>
      <div class="stat-lbl">Less water used</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">50%</div>
      <div class="stat-lbl">Faster growth</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">10×</div>
      <div class="stat-lbl">More yield</div>
    </div>
  </div>

  <div class="home-section-title">Lessons</div>
  <div class="lesson-list">
    <button class="lesson-card" onclick="goTo('learn')">
      <div class="lesson-icon-box">💧</div>
      <div class="lesson-text">
        <h4>Farming Methods</h4>
        <p>Hydroponics, Aeroponics, Aquaponics & NFT</p>
      </div>
      <span class="lesson-arrow">›</span>
    </button>
    <button class="lesson-card" onclick="goTo('nutrients')">
      <div class="lesson-icon-box">🧪</div>
      <div class="lesson-text">
        <h4>Plant Nutrients</h4>
        <p>What plants need and why it matters</p>
      </div>
      <span class="lesson-arrow">›</span>
    </button>
    <button class="lesson-card" onclick="goTo('quiz')">
      <div class="lesson-icon-box">🧠</div>
      <div class="lesson-text">
        <h4>Knowledge Quiz</h4>
        <p>Test what you've learned — 5 questions</p>
      </div>
      <span class="lesson-arrow">›</span>
    </button>
    <button class="lesson-card" onclick="goTo('glossary')">
      <div class="lesson-icon-box">📖</div>
      <div class="lesson-text">
        <h4>Glossary</h4>
        <p>Key terms explained simply</p>
      </div>
      <span class="lesson-arrow">›</span>
    </button>
  </div>

  <div style="margin-top:24px">
    <div class="home-section-title">Growth Cycle</div>
    <div class="cycle-grid">
      <div class="cycle-card"><div class="cycle-num">1</div><div class="cycle-emoji">🌱</div><div class="cycle-name">Germination</div><div class="cycle-desc">Seeds sprout in sterile media like rockwool</div></div>
      <div class="cycle-card"><div class="cycle-num">2</div><div class="cycle-emoji">💧</div><div class="cycle-name">Nutrients</div><div class="cycle-desc">Roots absorb minerals directly from solution</div></div>
      <div class="cycle-card"><div class="cycle-num">3</div><div class="cycle-emoji">☀️</div><div class="cycle-name">Photosynthesis</div><div class="cycle-desc">LED or natural light drives plant growth</div></div>
      <div class="cycle-card"><div class="cycle-num">4</div><div class="cycle-emoji">🥬</div><div class="cycle-name">Harvest</div><div class="cycle-desc">Crops harvested 30–50% faster than soil</div></div>
    </div>
  </div>
</div>

<!-- ── LEARN ── -->
<div class="page" id="page-learn">
  <div class="page-header">
    <div class="chip">Methods</div>
    <h1 class="page-title">Farming <em>Techniques</em></h1>
    <p class="page-sub">Tap each method to explore how it works.</p>
  </div>

  <div class="method-tabs">
    <button class="mtab active" onclick="switchMethod('hydro', this)">💧 Hydroponics</button>
    <button class="mtab" onclick="switchMethod('aero', this)">💨 Aeroponics</button>
    <button class="mtab" onclick="switchMethod('aqua', this)">🐟 Aquaponics</button>
    <button class="mtab" onclick="switchMethod('nft', this)">〰️ NFT</button>
  </div>

  <!-- HYDRO -->
  <div class="method-content active" id="mc-hydro">
    <div class="method-header">
      <h3>💧 Hydroponics</h3>
      <p>Plants grow with roots in or near a water-based nutrient solution. The most widely used soilless system worldwide, with multiple sub-types.</p>
    </div>
    <div class="diagram-card">
      <h4>System Diagram</h4>
      <svg viewBox="0 0 300 240" xmlns="http://www.w3.org/2000/svg">
        <ellipse cx="150" cy="20" rx="55" ry="11" fill="#ffee58" opacity="0.85"/>
        <text x="150" y="25" text-anchor="middle" font-size="10" fill="#4a3f00" font-family="Outfit,sans-serif" font-weight="600">💡 LED Light</text>
        <line x1="112" y1="31" x2="95" y2="50" stroke="#ffee58" stroke-width="1.2" opacity="0.5"/>
        <line x1="150" y1="31" x2="150" y2="50" stroke="#ffee58" stroke-width="1.2" opacity="0.5"/>
        <line x1="188" y1="31" x2="205" y2="50" stroke="#ffee58" stroke-width="1.2" opacity="0.5"/>
        <rect x="55" y="50" width="190" height="14" rx="4" fill="#2d7a4f"/>
        <line x1="95" y1="50" x2="95" y2="32" stroke="#4caf78" stroke-width="2.2"/>
        <ellipse cx="86" cy="29" rx="12" ry="8" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="103" cy="25" rx="12" ry="8" fill="#6fcf97" opacity="0.9"/>
        <line x1="150" y1="50" x2="150" y2="29" stroke="#4caf78" stroke-width="2.2"/>
        <ellipse cx="141" cy="25" rx="12" ry="8" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="158" cy="21" rx="12" ry="8" fill="#6fcf97" opacity="0.9"/>
        <line x1="205" y1="50" x2="205" y2="32" stroke="#4caf78" stroke-width="2.2"/>
        <ellipse cx="196" cy="29" rx="12" ry="8" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="213" cy="25" rx="12" ry="8" fill="#6fcf97" opacity="0.9"/>
        <line x1="95" y1="64" x2="91" y2="88" stroke="#a8e063" stroke-width="1.1" opacity="0.7"/>
        <line x1="95" y1="64" x2="99" y2="90" stroke="#a8e063" stroke-width="1.1" opacity="0.7"/>
        <line x1="150" y1="64" x2="146" y2="88" stroke="#a8e063" stroke-width="1.1" opacity="0.7"/>
        <line x1="150" y1="64" x2="154" y2="91" stroke="#a8e063" stroke-width="1.1" opacity="0.7"/>
        <line x1="205" y1="64" x2="201" y2="88" stroke="#a8e063" stroke-width="1.1" opacity="0.7"/>
        <line x1="205" y1="64" x2="209" y2="90" stroke="#a8e063" stroke-width="1.1" opacity="0.7"/>
        <rect x="38" y="96" width="224" height="64" rx="8" fill="rgba(30,100,160,0.25)" stroke="#4a9fda" stroke-width="1.4"/>
        <text x="150" y="122" text-anchor="middle" font-size="10" fill="#7ec8f7" font-family="Outfit,sans-serif" font-weight="500">Nutrient Solution</text>
        <text x="150" y="137" text-anchor="middle" font-size="9" fill="#4a9fda" font-family="Outfit,sans-serif">(Water + Minerals)</text>
        <path d="M50 112 Q74 104 98 112 Q122 120 146 112 Q170 104 194 112 Q218 120 252 112" stroke="#4a9fda" stroke-width="1" fill="none" opacity="0.5"/>
        <rect x="120" y="168" width="60" height="26" rx="6" fill="#1a4a2e" stroke="#2d7a4f" stroke-width="1.3"/>
        <text x="150" y="184" text-anchor="middle" font-size="9" fill="#6fcf97" font-family="Outfit,sans-serif" font-weight="600">⚙ Pump</text>
        <line x1="120" y1="181" x2="50" y2="181" stroke="#2d7a4f" stroke-width="2"/>
        <line x1="50" y1="96" x2="50" y2="181" stroke="#2d7a4f" stroke-width="2"/>
        <line x1="180" y1="181" x2="250" y2="181" stroke="#2d7a4f" stroke-width="2"/>
        <line x1="250" y1="96" x2="250" y2="181" stroke="#2d7a4f" stroke-width="2"/>
        <text x="150" y="218" text-anchor="middle" font-size="9" fill="#8aab96" font-family="Outfit,sans-serif">Recirculating water • pH monitored</text>
      </svg>
    </div>
    <div class="facts-card">
      <h4>Key Facts</h4>
      <div class="fact-row"><span class="dot">✦</span> Uses 90% less water than soil farming</div>
      <div class="fact-row"><span class="dot">✦</span> Plants grow 30–50% faster</div>
      <div class="fact-row"><span class="dot">✦</span> Best for: leafy greens, herbs, tomatoes</div>
      <div class="fact-row"><span class="dot">✦</span> Ideal pH range: 5.5 – 6.5</div>
      <div class="fact-row"><span class="dot">✦</span> Great for beginners and commercial farms</div>
    </div>
  </div>

  <!-- AERO -->
  <div class="method-content" id="mc-aero">
    <div class="method-header">
      <h3>💨 Aeroponics</h3>
      <p>The most advanced soilless method. Roots hang in open air and are periodically misted with a fine nutrient spray, maximizing oxygen exposure.</p>
    </div>
    <div class="diagram-card">
      <h4>System Diagram</h4>
      <svg viewBox="0 0 300 240" xmlns="http://www.w3.org/2000/svg">
        <rect x="45" y="48" width="210" height="13" rx="4" fill="#2d7a4f"/>
        <line x1="90" y1="48" x2="90" y2="28" stroke="#4caf78" stroke-width="2.2"/>
        <ellipse cx="80" cy="24" rx="13" ry="8" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="99" cy="20" rx="12" ry="7" fill="#6fcf97" opacity="0.9"/>
        <line x1="150" y1="48" x2="150" y2="25" stroke="#4caf78" stroke-width="2.2"/>
        <ellipse cx="140" cy="21" rx="13" ry="8" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="161" cy="17" rx="12" ry="7" fill="#6fcf97" opacity="0.9"/>
        <line x1="210" y1="48" x2="210" y2="28" stroke="#4caf78" stroke-width="2.2"/>
        <ellipse cx="200" cy="24" rx="13" ry="8" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="219" cy="20" rx="12" ry="7" fill="#6fcf97" opacity="0.9"/>
        <rect x="38" y="61" width="224" height="100" rx="8" fill="rgba(20,60,40,0.6)" stroke="#2d7a4f" stroke-width="1.4"/>
        <text x="150" y="80" text-anchor="middle" font-size="10" fill="#6fcf97" font-family="Outfit,sans-serif" font-weight="600">AIR + MIST CHAMBER</text>
        <line x1="90" y1="61" x2="87" y2="108" stroke="#a8e063" stroke-width="1.1"/>
        <line x1="90" y1="61" x2="93" y2="112" stroke="#a8e063" stroke-width="1.1"/>
        <line x1="150" y1="61" x2="147" y2="110" stroke="#a8e063" stroke-width="1.1"/>
        <line x1="150" y1="61" x2="153" y2="114" stroke="#a8e063" stroke-width="1.1"/>
        <line x1="210" y1="61" x2="207" y2="108" stroke="#a8e063" stroke-width="1.1"/>
        <line x1="210" y1="61" x2="213" y2="112" stroke="#a8e063" stroke-width="1.1"/>
        <circle cx="90" cy="135" r="4" fill="#4a9fda"/>
        <circle cx="150" cy="135" r="4" fill="#4a9fda"/>
        <circle cx="210" cy="135" r="4" fill="#4a9fda"/>
        <path d="M90 131 Q80 122 74 116" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M90 131 Q90 120 90 110" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M90 131 Q100 122 106 116" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M150 131 Q140 122 134 116" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M150 131 Q150 120 150 108" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M150 131 Q160 122 166 116" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M210 131 Q200 122 194 116" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M210 131 Q210 120 210 108" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <path d="M210 131 Q220 122 226 116" stroke="#7ec8f7" stroke-width="1" fill="none" opacity="0.7"/>
        <text x="150" y="153" text-anchor="middle" font-size="9" fill="#4a9fda" font-family="Outfit,sans-serif">💦 Mist Nozzles</text>
        <rect x="100" y="175" width="100" height="32" rx="6" fill="rgba(30,100,160,0.2)" stroke="#4a9fda" stroke-width="1.2"/>
        <text x="150" y="191" text-anchor="middle" font-size="9" fill="#7ec8f7" font-family="Outfit,sans-serif" font-weight="500">Nutrient Reservoir</text>
        <text x="150" y="202" text-anchor="middle" font-size="8" fill="#4a9fda" font-family="Outfit,sans-serif">+ High-Pressure Pump</text>
        <line x1="150" y1="161" x2="150" y2="175" stroke="#2d7a4f" stroke-width="1.4"/>
        <text x="150" y="225" text-anchor="middle" font-size="9" fill="#8aab96" font-family="Outfit,sans-serif">Roots misted every 3–5 minutes</text>
      </svg>
    </div>
    <div class="facts-card">
      <h4>Key Facts</h4>
      <div class="fact-row"><span class="dot">✦</span> Uses up to 95% less water than soil</div>
      <div class="fact-row"><span class="dot">✦</span> Fastest plant growth of all methods</div>
      <div class="fact-row"><span class="dot">✦</span> Best for: potatoes, root vegetables, lettuce</div>
      <div class="fact-row"><span class="dot">✦</span> Higher setup cost — precision required</div>
      <div class="fact-row"><span class="dot">✦</span> Used by NASA for space farming research</div>
    </div>
  </div>

  <!-- AQUA -->
  <div class="method-content" id="mc-aqua">
    <div class="method-header">
      <h3>🐟 Aquaponics</h3>
      <p>A symbiotic system combining fish farming with hydroponics. Fish waste feeds plants; plants filter water for fish — a perfect closed-loop ecosystem.</p>
    </div>
    <div class="diagram-card">
      <h4>System Diagram</h4>
      <svg viewBox="0 0 300 240" xmlns="http://www.w3.org/2000/svg">
        <rect x="35" y="25" width="230" height="38" rx="6" fill="#1a4a2e" stroke="#2d7a4f" stroke-width="1.4"/>
        <text x="150" y="42" text-anchor="middle" font-size="10" fill="#6fcf97" font-family="Outfit,sans-serif" font-weight="600">🌿 Plant Grow Beds</text>
        <text x="150" y="56" text-anchor="middle" font-size="8" fill="#4caf78" font-family="Outfit,sans-serif">Roots filter water naturally</text>
        <line x1="75" y1="63" x2="75" y2="96" stroke="#4a9fda" stroke-width="1.8" stroke-dasharray="4,3"/>
        <line x1="225" y1="63" x2="225" y2="96" stroke="#4a9fda" stroke-width="1.8" stroke-dasharray="4,3"/>
        <rect x="35" y="96" width="230" height="78" rx="8" fill="rgba(30,80,150,0.25)" stroke="#4a9fda" stroke-width="1.4"/>
        <path d="M50 120 Q72 112 94 120 Q116 128 138 120 Q160 112 182 120 Q204 128 250 120" stroke="#4a9fda" stroke-width="1.1" fill="none" opacity="0.6"/>
        <text x="95" y="148" font-size="18" text-anchor="middle">🐟</text>
        <text x="150" y="158" font-size="16" text-anchor="middle">🐠</text>
        <text x="205" y="146" font-size="18" text-anchor="middle">🐡</text>
        <text x="150" y="184" text-anchor="middle" font-size="9" fill="#7ec8f7" font-family="Outfit,sans-serif" font-weight="500">Fish Tank</text>
        <line x1="150" y1="174" x2="150" y2="200" stroke="#a8e063" stroke-width="1.8"/>
        <rect x="110" y="200" width="80" height="26" rx="6" fill="#1a4a2e" stroke="#2d7a4f" stroke-width="1.2"/>
        <text x="150" y="213" text-anchor="middle" font-size="9" fill="#6fcf97" font-family="Outfit,sans-serif" font-weight="500">⚙ Pump</text>
        <text x="150" y="224" text-anchor="middle" font-size="8" fill="#4caf78" font-family="Outfit,sans-serif">Sends nutrients up</text>
        <path d="M110 213 Q45 213 45 174" stroke="#a8e063" stroke-width="1.4" fill="none" stroke-dasharray="4,3"/>
        <path d="M190 213 Q255 213 255 174" stroke="#a8e063" stroke-width="1.4" fill="none" stroke-dasharray="4,3"/>
        <line x1="45" y1="96" x2="45" y2="63" stroke="#a8e063" stroke-width="1.4" stroke-dasharray="4,3"/>
        <line x1="255" y1="96" x2="255" y2="63" stroke="#a8e063" stroke-width="1.4" stroke-dasharray="4,3"/>
      </svg>
    </div>
    <div class="facts-card">
      <h4>Key Facts</h4>
      <div class="fact-row"><span class="dot">✦</span> Produces both fish and vegetables</div>
      <div class="fact-row"><span class="dot">✦</span> Naturally organic — no synthetic fertilizers</div>
      <div class="fact-row"><span class="dot">✦</span> Best fish: tilapia, catfish, trout, koi</div>
      <div class="fact-row"><span class="dot">✦</span> Best plants: lettuce, kale, basil, watercress</div>
      <div class="fact-row"><span class="dot">✦</span> Uses 10× less water than conventional farming</div>
    </div>
  </div>

  <!-- NFT -->
  <div class="method-content" id="mc-nft">
    <div class="method-header">
      <h3>〰️ NFT System</h3>
      <p>Nutrient Film Technique — a thin film of nutrient solution flows continuously over roots in sloped channels, optimizing both nutrient absorption and oxygen uptake.</p>
    </div>
    <div class="diagram-card">
      <h4>System Diagram</h4>
      <svg viewBox="0 0 300 240" xmlns="http://www.w3.org/2000/svg">
        <line x1="25" y1="75" x2="275" y2="93" stroke="#2d7a4f" stroke-width="9" stroke-linecap="round"/>
        <line x1="25" y1="120" x2="275" y2="138" stroke="#2d7a4f" stroke-width="9" stroke-linecap="round"/>
        <line x1="25" y1="165" x2="275" y2="183" stroke="#2d7a4f" stroke-width="9" stroke-linecap="round"/>
        <line x1="25" y1="78" x2="275" y2="96" stroke="#4a9fda" stroke-width="2" opacity="0.7"/>
        <line x1="25" y1="123" x2="275" y2="141" stroke="#4a9fda" stroke-width="2" opacity="0.7"/>
        <line x1="25" y1="168" x2="275" y2="186" stroke="#4a9fda" stroke-width="2" opacity="0.7"/>
        <line x1="80" y1="75" x2="80" y2="52" stroke="#4caf78" stroke-width="2"/>
        <ellipse cx="73" cy="48" rx="11" ry="7" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="87" cy="44" rx="11" ry="7" fill="#6fcf97" opacity="0.9"/>
        <line x1="150" y1="80" x2="150" y2="55" stroke="#4caf78" stroke-width="2"/>
        <ellipse cx="143" cy="51" rx="11" ry="7" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="157" cy="47" rx="11" ry="7" fill="#6fcf97" opacity="0.9"/>
        <line x1="220" y1="85" x2="220" y2="60" stroke="#4caf78" stroke-width="2"/>
        <ellipse cx="213" cy="56" rx="11" ry="7" fill="#4caf78" opacity="0.9"/>
        <ellipse cx="227" cy="52" rx="11" ry="7" fill="#6fcf97" opacity="0.9"/>
        <text x="282" y="97" font-size="11" fill="#4a9fda">→</text>
        <text x="282" y="141" font-size="11" fill="#4a9fda">→</text>
        <text x="282" y="186" font-size="11" fill="#4a9fda">→</text>
        <rect x="70" y="200" width="160" height="30" rx="6" fill="rgba(30,100,160,0.25)" stroke="#4a9fda" stroke-width="1.2"/>
        <text x="150" y="214" text-anchor="middle" font-size="9" fill="#7ec8f7" font-family="Outfit,sans-serif" font-weight="500">💧 Nutrient Reservoir</text>
        <text x="150" y="225" text-anchor="middle" font-size="8" fill="#4a9fda" font-family="Outfit,sans-serif">Collects & recirculates</text>
        <line x1="65" y1="200" x2="65" y2="75" stroke="#1a4a2e" stroke-width="2.5"/>
        <text x="50" y="140" font-size="8" fill="#a8e063" font-family="Outfit,sans-serif" transform="rotate(-90 50 140)">Pump ↑</text>
      </svg>
    </div>
    <div class="facts-card">
      <h4>Key Facts</h4>
      <div class="fact-row"><span class="dot">✦</span> Very water efficient — thin continuous film</div>
      <div class="fact-row"><span class="dot">✦</span> Simple low-cost channels (PVC pipes)</div>
      <div class="fact-row"><span class="dot">✦</span> Best for: lettuce, spinach, herbs, strawberries</div>
      <div class="fact-row"><span class="dot">✦</span> Not ideal for heavy fruiting plants</div>
      <div class="fact-row"><span class="dot">✦</span> Most popular commercial hydroponics system</div>
    </div>
  </div>
</div>

<!-- ── NUTRIENTS ── -->
<div class="page" id="page-nutrients">
  <div class="page-header">
    <div class="chip">Plant Science</div>
    <h1 class="page-title">Essential <em>Nutrients</em></h1>
    <p class="page-sub">In soilless farming you control every nutrient. Here's what plants need and why.</p>
  </div>

  <div id="nutrientList"></div>
</div>

<!-- ── QUIZ ── -->
<div class="page" id="page-quiz">
  <div class="page-header">
    <div class="chip">Test Yourself</div>
    <h1 class="page-title">Knowledge <em>Quiz</em></h1>
    <p class="page-sub">5 questions — how well do you know soilless farming?</p>
  </div>

  <div class="quiz-wrap">
    <div class="quiz-progress-bar-wrap">
      <div class="quiz-bar-fill" id="qBar" style="width:0%"></div>
    </div>
    <div id="quizBody">
      <div class="q-counter" id="qCounter"></div>
      <div class="q-text" id="qText"></div>
      <div class="q-opts" id="qOpts"></div>
      <div class="q-feedback" id="qFeedback"></div>
      <div class="q-next-wrap">
        <button class="btn btn-lime" id="qNext" onclick="nextQ()" style="display:none">Next →</button>
      </div>
    </div>
    <div class="score-screen" id="scoreScreen">
      <div style="font-size:3rem;margin-bottom:8px;">🏆</div>
      <div class="score-big" id="scoreBig"></div>
      <div class="score-sub" id="scoreSub"></div>
      <button class="btn btn-lime" onclick="restartQuiz()">Try Again 🔄</button>
    </div>
  </div>
</div>

<!-- ── GLOSSARY ── -->
<div class="page" id="page-glossary">
  <div class="page-header">
    <div class="chip">Reference</div>
    <h1 class="page-title">Glossary</h1>
    <p class="page-sub">Search key terms used in soilless farming.</p>
  </div>

  <div class="gloss-search">
    <span class="gloss-search-icon">🔍</span>
    <input type="text" placeholder="Search terms..." oninput="filterGloss(this.value)" />
  </div>

  <div id="glossList"></div>
</div>
```

  </div><!-- /pages -->

  <!-- BOTTOM NAV -->

  <nav class="bottom-nav">
    <button class="nav-item active" onclick="goTo('home')" id="nav-home">
      <div class="nav-icon">🏠</div>
      <div class="nav-label">Home</div>
    </button>
    <button class="nav-item" onclick="goTo('learn')" id="nav-learn">
      <div class="nav-icon">💧</div>
      <div class="nav-label">Learn</div>
    </button>
    <button class="nav-item" onclick="goTo('nutrients')" id="nav-nutrients">
      <div class="nav-icon">🧪</div>
      <div class="nav-label">Nutrients</div>
    </button>
    <button class="nav-item" onclick="goTo('quiz')" id="nav-quiz">
      <div class="nav-icon">🧠</div>
      <div class="nav-label">Quiz</div>
    </button>
    <button class="nav-item" onclick="goTo('glossary')" id="nav-glossary">
      <div class="nav-icon">📖</div>
      <div class="nav-label">Glossary</div>
    </button>
  </nav>

</div><!-- /app -->

<script>
// ── SPLASH ──────────────────────────────────────────────────────
setTimeout(() => {
  document.getElementById('splash').classList.add('hide');
  setTimeout(() => { document.getElementById('splash').remove(); }, 700);
}, 2200);

// ── NAVIGATION ──────────────────────────────────────────────────
let currentPage = 'home';

function goTo(id) {
  if (id === currentPage) return;
  const old = document.getElementById('page-' + currentPage);
  const next = document.getElementById('page-' + id);
  old.classList.add('exit-left');
  setTimeout(() => { old.classList.remove('active', 'exit-left'); }, 300);
  next.classList.add('active');
  // scroll top
  next.scrollTop = 0;
  // nav highlight
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  document.getElementById('nav-' + id).classList.add('active');
  currentPage = id;
}

// ── METHOD TABS ──────────────────────────────────────────────────
function switchMethod(id, btn) {
  document.querySelectorAll('.mtab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.method-content').forEach(m => m.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('mc-' + id).classList.add('active');
}

// ── NUTRIENTS DATA ───────────────────────────────────────────────
const nutrients = [
  { sym:'N', name:'Nitrogen', type:'Macronutrient', role:'Leaf and stem growth, chlorophyll production', deficiency:'Yellowing older leaves, stunted growth' },
  { sym:'P', name:'Phosphorus', type:'Macronutrient', role:'Root development, flowering, energy transfer', deficiency:'Purple/red leaves, poor root growth' },
  { sym:'K', name:'Potassium', type:'Macronutrient', role:'Water regulation, disease resistance, fruit quality', deficiency:'Brown leaf edges, weak stems' },
  { sym:'Ca', name:'Calcium', type:'Secondary', role:'Cell wall strength, root development', deficiency:'Tip burn in lettuce, blossom end rot' },
  { sym:'Mg', name:'Magnesium', type:'Secondary', role:'Central atom of chlorophyll, enzyme activator', deficiency:'Yellowing between leaf veins' },
  { sym:'Fe', name:'Iron', type:'Micronutrient', role:'Chlorophyll synthesis, enzyme reactions', deficiency:'Yellowing new leaves while veins stay green' },
  { sym:'S', name:'Sulfur', type:'Secondary', role:'Protein synthesis, vitamin production', deficiency:'Yellowing young leaves, poor flavor' },
  { sym:'Zn', name:'Zinc', type:'Micronutrient', role:'Enzyme function, growth hormones', deficiency:'Small leaves, shortened internodes' },
  { sym:'Mn', name:'Manganese', type:'Micronutrient', role:'Photosynthesis, enzyme activation', deficiency:'Interveinal chlorosis on young leaves' },
];

function renderNutrients() {
  const list = document.getElementById('nutrientList');
  list.innerHTML = nutrients.map(n => `
    <div class="nutrient-card">
      <div class="nutrient-top">
        <div class="nutrient-symbol">${n.sym}</div>
        <div>
          <div class="nutrient-name">${n.name}</div>
          <div class="nutrient-type">${n.type}</div>
        </div>
      </div>
      <div class="nutrient-row">
        <div class="nutrient-info-box">
          <div class="nutrient-info-label">Role</div>
          <div class="nutrient-info-val">${n.role}</div>
        </div>
        <div class="nutrient-info-box">
          <div class="nutrient-info-label">Deficiency</div>
          <div class="nutrient-info-val">${n.deficiency}</div>
        </div>
      </div>
    </div>
  `).join('');
}
renderNutrients();

// ── QUIZ ─────────────────────────────────────────────────────────
const questions = [
  { q:'Which method uses fish waste as plant fertilizer?', opts:['Aeroponics','Aquaponics','NFT','Deep Water Culture'], ans:1, explain:'Aquaponics combines fish farming with hydroponics — fish waste provides nutrients while plants clean the water.' },
  { q:'What is the ideal pH range for most hydroponic crops?', opts:['3.0–4.0','7.5–9.0','5.5–6.5','4.0–5.0'], ans:2, explain:'Most hydroponic plants thrive at pH 5.5–6.5. Outside this range, nutrient absorption is blocked.' },
  { q:'In which method are plant roots misted with nutrient solution?', opts:['Hydroponics','NFT','Aquaponics','Aeroponics'], ans:3, explain:'Aeroponics suspends roots in air and periodically mists them — maximizing nutrient delivery and oxygen.' },
  { q:'How much less water does soilless farming use vs traditional farming?', opts:['10% less','50% less','90% less','Same amount'], ans:2, explain:'Soilless systems can use up to 90% less water because water is recirculated, not lost to soil.' },
  { q:'What does EC stand for in soilless farming?', opts:['Element Content','Electrical Conductivity','Essential Carbon','Evaporation Control'], ans:1, explain:'EC (Electrical Conductivity) measures dissolved nutrient concentration in the water solution.' },
];

let qIdx=0, qScore=0, qAnswered=false;

function loadQ() {
  const q = questions[qIdx];
  document.getElementById('qCounter').textContent = `Question ${qIdx+1} of ${questions.length}`;
  document.getElementById('qBar').style.width = `${(qIdx/questions.length)*100}%`;
  document.getElementById('qText').textContent = q.q;
  document.getElementById('qOpts').innerHTML = q.opts.map((o,i) =>
    `<button class="q-opt" onclick="answerQ(${i})">${o}</button>`
  ).join('');
  document.getElementById('qFeedback').className = 'q-feedback';
  document.getElementById('qNext').style.display = 'none';
  qAnswered = false;
}

function answerQ(i) {
  if (qAnswered) return;
  qAnswered = true;
  const q = questions[qIdx];
  const btns = document.querySelectorAll('.q-opt');
  btns[i].classList.add(i===q.ans?'correct':'wrong');
  btns[q.ans].classList.add('correct');
  btns.forEach(b => b.disabled = true);
  const fb = document.getElementById('qFeedback');
  if (i===q.ans) { qScore++; fb.textContent='✅ Correct! '+q.explain; fb.className='q-feedback ok show'; }
  else { fb.textContent='❌ '+q.explain; fb.className='q-feedback err show'; }
  document.getElementById('qNext').style.display='inline-flex';
}

function nextQ() {
  qIdx++;
  if (qIdx >= questions.length) {
    document.getElementById('quizBody').style.display='none';
    document.getElementById('qBar').style.width='100%';
    const ss = document.getElementById('scoreScreen');
    ss.classList.add('show');
    document.getElementById('scoreBig').textContent=`${qScore}/${questions.length}`;
    const labels=['Keep studying! 📚','Good effort! 🌱','Not bad! 🌿','Great job! 🥬','Expert! 🌟','Perfect! 🏆'];
    document.getElementById('scoreSub').textContent=labels[qScore]||'';
  } else { loadQ(); }
}

function restartQuiz() {
  qIdx=0; qScore=0;
  document.getElementById('quizBody').style.display='block';
  document.getElementById('scoreScreen').classList.remove('show');
  loadQ();
}

loadQ();

// ── GLOSSARY ─────────────────────────────────────────────────────
const glossTerms = [
  { term:'Hydroponics', def:'Growing plants in nutrient-enriched water without soil. The most common soilless method used worldwide.' },
  { term:'Aeroponics', def:'A system where plant roots hang in air and are misted with nutrient solution at timed intervals.' },
  { term:'Aquaponics', def:'A combined fish and plant farming system where fish waste feeds plants and plants filter the water for fish.' },
  { term:'NFT', def:'Nutrient Film Technique — a thin stream of nutrient solution flows over roots in sloped channels.' },
  { term:'pH', def:'A measure of acidity/alkalinity. Most hydroponic crops grow best at pH 5.5–6.5.' },
  { term:'EC', def:'Electrical Conductivity — measures nutrient concentration in solution. Higher EC = more nutrients dissolved.' },
  { term:'Growing Medium', def:'Material (rockwool, perlite, clay pebbles, coco coir) that anchors roots instead of soil.' },
  { term:'DWC', def:'Deep Water Culture — roots are submerged directly in an oxygenated nutrient solution tank.' },
  { term:'Macronutrients', def:'Primary plant nutrients needed in large quantities: Nitrogen (N), Phosphorus (P), Potassium (K).' },
  { term:'Micronutrients', def:'Trace elements needed in tiny amounts: iron, zinc, manganese, copper, molybdenum, boron.' },
  { term:'Rockwool', def:'A fibrous growing medium made from spun volcanic rock, widely used to germinate seeds and anchor plants.' },
  { term:'Perlite', def:'Lightweight volcanic glass used as a growing medium — excellent drainage and aeration.' },
  { term:'Chlorophyll', def:'The green pigment in plants that absorbs light for photosynthesis — requires magnesium and nitrogen.' },
  { term:'Recirculating System', def:'A setup where nutrient solution is reused — collected, filtered, and pumped back to plants repeatedly.' },
];

function renderGloss(filter='') {
  const list = document.getElementById('glossList');
  const fl = filter.toLowerCase();
  const filtered = glossTerms.filter(g => g.term.toLowerCase().includes(fl) || g.def.toLowerCase().includes(fl));
  list.innerHTML = filtered.length
    ? filtered.map(g => `<div class="gloss-item"><div class="gloss-term">${g.term}</div><div class="gloss-def">${g.def}</div></div>`).join('')
    : `<div style="text-align:center;padding:40px;color:var(--muted);font-size:0.85rem;">No terms found for "<strong>${filter}</strong>"</div>`;
}
function filterGloss(v) { renderGloss(v); }
renderGloss();

// ── OFFLINE DETECTION ─────────────────────────────────────────────
window.addEventListener('offline', () => { document.getElementById('offlineBanner').style.display='block'; });
window.addEventListener('online',  () => { document.getElementById('offlineBanner').style.display='none'; });

// ── SERVICE WORKER (offline caching) ─────────────────────────────
if ('serviceWorker' in navigator) {
  const swCode = `
    const CACHE='growsmart-v1';
    self.addEventListener('install', e => {
      e.waitUntil(caches.open(CACHE).then(c => c.addAll(['/'])));
      self.skipWaiting();
    });
    self.addEventListener('fetch', e => {
      e.respondWith(caches.match(e.request).then(r => r || fetch(e.request)));
    });
  `;
  const blob = new Blob([swCode], {type:'application/javascript'});
  const swUrl = URL.createObjectURL(blob);
  navigator.serviceWorker.register(swUrl).catch(()=>{});
}

// ── INSTALL PROMPT ────────────────────────────────────────────────
let deferredPrompt;
window.addEventListener('beforeinstallprompt', e => {
  e.preventDefault();
  deferredPrompt = e;
});
</script>

</body>
</html>
