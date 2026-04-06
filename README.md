<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="RareFinds — Discover extraordinary deals daily. Shop electronics, beauty, fashion, home goods and more at unbeatable prices.">
<meta name="theme-color" content="#FF4500">
<title>RareFinds — Discover the Extraordinary</title>

<!-- Preconnect for performance -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;1,9..40,400&display=swap" rel="stylesheet">

<style>
/* ─────────────────────────────────────────────
   DESIGN TOKENS
───────────────────────────────────────────── */
:root {
  --fire: #FF4500;
  --fire-lt: #FF6B35;
  --fire-dk: #CC3700;
  --fire-glow: rgba(255, 69, 0, 0.28);
  --volt: #E8FF00;
  --volt-dk: #B8CC00;
  --purple: #9B30FF;
  --pink: #FF2D78;

  --ink: #08080F;
  --ink2: #0F0F1A;
  --ink3: #1A1A28;
  --surface: #1E1E30;
  --surface2: #252538;
  --surface3: #2E2E45;
  --glass: rgba(255, 255, 255, 0.04);
  --glass2: rgba(255, 255, 255, 0.08);
  --border: rgba(255, 255, 255, 0.07);
  --border2: rgba(255, 255, 255, 0.14);

  --text: #F0F0FF;
  --text2: rgba(240, 240, 255, 0.62);
  --text3: rgba(240, 240, 255, 0.36);

  --success: #00E676;
  --danger: #FF1744;
  --warn: #FFC107;

  --rad-xs: 6px;
  --rad-sm: 10px;
  --rad: 14px;
  --rad-lg: 20px;
  --rad-xl: 28px;
  --nav-h: 64px;
  --cat-h: 44px;

  --ease: cubic-bezier(0.4, 0, 0.2, 1);
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --t: all 0.25s var(--ease);
}

/* ─────────────────────────────────────────────
   RESET & BASE
───────────────────────────────────────────── */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; font-size: 16px; }
body {
  font-family: 'DM Sans', system-ui, -apple-system, sans-serif;
  background: var(--ink);
  color: var(--text);
  overflow-x: hidden;
  cursor: none;
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
}
a { text-decoration: none; color: inherit; }
button { font-family: inherit; cursor: none; border: none; outline: none; background: none; }
input, select { font-family: inherit; outline: none; border: none; }
img { display: block; max-width: 100%; }
ul { list-style: none; }

/* Scrollbar */
::-webkit-scrollbar { width: 3px; height: 3px; }
::-webkit-scrollbar-track { background: var(--ink); }
::-webkit-scrollbar-thumb { background: var(--fire); border-radius: 2px; }

/* ─────────────────────────────────────────────
   CUSTOM CURSOR
───────────────────────────────────────────── */
#cur, #cur-r {
  position: fixed;
  border-radius: 50%;
  pointer-events: none;
  z-index: 99999;
  transform: translate(-50%, -50%);
  will-change: left, top;
}
#cur {
  width: 10px; height: 10px;
  background: var(--fire);
  transition: width 0.18s, height 0.18s, background 0.18s;
}
#cur-r {
  width: 34px; height: 34px;
  border: 1.5px solid rgba(255, 69, 0, 0.42);
  transition: width 0.22s ease-out, height 0.22s ease-out;
}
body.hov #cur { width: 18px; height: 18px; background: var(--volt); }
body.hov #cur-r { width: 48px; height: 48px; border-color: rgba(232, 255, 0, 0.38); }

/* ─────────────────────────────────────────────
   TOAST NOTIFICATION
───────────────────────────────────────────── */
#toast {
  position: fixed;
  bottom: 28px; right: 28px;
  z-index: 9999;
  background: var(--surface2);
  border: 1px solid rgba(255, 69, 0, 0.38);
  border-radius: var(--rad);
  padding: 14px 20px;
  display: flex;
  align-items: center;
  gap: 12px;
  box-shadow: 0 14px 50px rgba(0,0,0,0.55), 0 0 30px var(--fire-glow);
  transform: translateX(130%);
  transition: transform 0.4s var(--spring);
  min-width: 250px;
  max-width: 340px;
}
#toast.show { transform: translateX(0); }
#toast-icon { font-size: 1.25rem; flex-shrink: 0; }
#toast-msg { font-size: 0.875rem; font-weight: 500; line-height: 1.4; }

/* ─────────────────────────────────────────────
   QUICK VIEW MODAL
───────────────────────────────────────────── */
#modal-bg {
  position: fixed; inset: 0;
  z-index: 8000;
  background: rgba(0, 0, 0, 0.88);
  backdrop-filter: blur(18px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s;
}
#modal-bg.open { opacity: 1; pointer-events: auto; }
#modal-box {
  width: 100%;
  max-width: 920px;
  max-height: 92vh;
  overflow-y: auto;
  background: var(--ink2);
  border: 1px solid var(--border2);
  border-radius: var(--rad-xl);
  position: relative;
  transform: translateY(24px) scale(0.96);
  transition: transform 0.35s var(--spring);
}
#modal-bg.open #modal-box { transform: translateY(0) scale(1); }
#modal-inner { display: grid; grid-template-columns: 1fr 1fr; min-height: 400px; }
.modal-close-btn {
  position: absolute; top: 16px; right: 16px; z-index: 10;
  width: 34px; height: 34px; border-radius: 50%;
  background: var(--glass2);
  border: 1px solid var(--border2);
  display: flex; align-items: center; justify-content: center;
  font-size: 0.95rem; color: var(--text);
  cursor: none; transition: var(--t);
}
.modal-close-btn:hover { background: rgba(255,23,68,0.2); border-color: rgba(255,23,68,0.5); }

/* ─────────────────────────────────────────────
   PAGE SYSTEM
───────────────────────────────────────────── */
.page { display: none; min-height: 100vh; animation: pageFade 0.3s ease; }
.page.active { display: block; }
@keyframes pageFade { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

/* ─────────────────────────────────────────────
   NAVIGATION
───────────────────────────────────────────── */
nav {
  position: fixed; top: 0; left: 0; right: 0;
  height: var(--nav-h);
  z-index: 7000;
  background: rgba(8, 8, 15, 0.9);
  backdrop-filter: blur(24px);
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  padding: 0 24px;
  gap: 16px;
}
.nav-logo {
  font-family: 'Syne', sans-serif;
  font-size: 1.5rem;
  font-weight: 800;
  letter-spacing: -0.5px;
  background: linear-gradient(90deg, var(--fire), var(--volt));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  white-space: nowrap;
  cursor: none;
  flex-shrink: 0;
}
.nav-search {
  flex: 1;
  max-width: 520px;
  display: flex;
  align-items: center;
  gap: 10px;
  background: var(--glass2);
  border: 1px solid var(--border2);
  border-radius: 100px;
  padding: 9px 18px;
  transition: var(--t);
}
.nav-search:focus-within {
  border-color: rgba(255, 69, 0, 0.55);
  box-shadow: 0 0 0 3px var(--fire-glow);
}
.nav-search input {
  flex: 1; background: none;
  color: var(--text);
  font-size: 0.875rem;
}
.nav-search input::placeholder { color: var(--text3); }
.nav-search-icon { color: var(--text3); font-size: 1rem; flex-shrink: 0; }
.nav-actions { margin-left: auto; display: flex; align-items: center; gap: 10px; }
.nav-btn {
  width: 40px; height: 40px; border-radius: 50%;
  background: var(--glass);
  border: 1px solid var(--border);
  display: flex; align-items: center; justify-content: center;
  font-size: 1rem;
  position: relative;
  transition: var(--t);
  cursor: none;
  flex-shrink: 0;
}
.nav-btn:hover { background: var(--glass2); border-color: var(--border2); transform: scale(1.05); }
.nav-badge {
  position: absolute; top: -4px; right: -4px;
  width: 18px; height: 18px;
  border-radius: 50%;
  background: var(--fire);
  font-size: 9px; font-weight: 800;
  display: flex; align-items: center; justify-content: center;
  border: 2px solid var(--ink);
  color: #fff;
}

/* ─────────────────────────────────────────────
   CATEGORY BAR
───────────────────────────────────────────── */
.cat-bar {
  position: fixed;
  top: var(--nav-h);
  left: 0; right: 0;
  z-index: 6900;
  height: var(--cat-h);
  background: rgba(12, 12, 20, 0.94);
  backdrop-filter: blur(18px);
  border-bottom: 1px solid var(--border);
  overflow-x: auto;
  white-space: nowrap;
  display: flex;
  align-items: center;
  padding: 0 24px;
  gap: 4px;
  scrollbar-width: none;
}
.cat-bar::-webkit-scrollbar { display: none; }
.cat-pill {
  padding: 7px 16px;
  font-size: 0.78rem;
  font-weight: 600;
  color: var(--text2);
  border-radius: 100px;
  transition: var(--t);
  cursor: none;
  flex-shrink: 0;
  white-space: nowrap;
}
.cat-pill:hover, .cat-pill.active {
  background: var(--fire);
  color: #fff;
}

/* ─────────────────────────────────────────────
   HERO SECTION
───────────────────────────────────────────── */
.hero {
  padding-top: calc(var(--nav-h) + var(--cat-h) + 28px);
  padding-bottom: 64px;
  padding-left: 24px;
  padding-right: 24px;
  position: relative;
  overflow: hidden;
  min-height: 560px;
  display: flex;
  align-items: center;
}
.hero-bg {
  position: absolute; inset: 0;
  background:
    radial-gradient(ellipse 70% 70% at 80% 50%, rgba(255,69,0,0.18), transparent 65%),
    radial-gradient(ellipse 50% 60% at 20% 80%, rgba(232,255,0,0.07), transparent 55%),
    radial-gradient(ellipse 40% 50% at 50% 0%, rgba(155,48,255,0.1), transparent 60%),
    var(--ink);
}
.hero-mesh {
  position: absolute; inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.022) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.022) 1px, transparent 1px);
  background-size: 48px 48px;
  opacity: 0.7;
}
.hero-content {
  position: relative;
  z-index: 2;
  max-width: 640px;
}
.hero-tag {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(255,69,0,0.12);
  border: 1px solid rgba(255,69,0,0.32);
  border-radius: 100px;
  padding: 6px 14px;
  font-size: 0.77rem;
  font-weight: 700;
  color: var(--fire-lt);
  letter-spacing: 0.4px;
  margin-bottom: 22px;
}
.live-dot {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: var(--fire);
  animation: pulse 1.6s infinite;
  flex-shrink: 0;
}
@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(255,69,0,0.65); }
  70% { box-shadow: 0 0 0 8px rgba(255,69,0,0); }
}
.hero h1 {
  font-family: 'Syne', sans-serif;
  font-size: clamp(2.6rem, 6vw, 5rem);
  font-weight: 800;
  line-height: 0.95;
  letter-spacing: -2.5px;
  margin-bottom: 20px;
}
.hero h1 em {
  font-style: normal;
  background: linear-gradient(120deg, var(--fire) 0%, var(--volt) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.hero p {
  font-size: 1.05rem;
  color: var(--text2);
  margin-bottom: 34px;
  line-height: 1.72;
  max-width: 480px;
}
.hero-btns { display: flex; gap: 14px; flex-wrap: wrap; }
.btn-fire {
  padding: 14px 32px;
  border-radius: 100px;
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff;
  font-weight: 700;
  font-size: 0.92rem;
  transition: var(--t);
  box-shadow: 0 8px 28px var(--fire-glow);
  letter-spacing: 0.2px;
  cursor: none;
}
.btn-fire:hover {
  transform: translateY(-2px);
  box-shadow: 0 14px 38px rgba(255,69,0,0.48);
}
.btn-outline {
  padding: 14px 30px;
  border-radius: 100px;
  background: var(--glass);
  border: 1px solid var(--border2);
  color: var(--text);
  font-weight: 600;
  font-size: 0.92rem;
  transition: var(--t);
  cursor: none;
}
.btn-outline:hover {
  background: var(--glass2);
  border-color: rgba(255,255,255,0.26);
  transform: translateY(-2px);
}
.hero-stats {
  display: flex;
  gap: 38px;
  margin-top: 44px;
  padding-top: 32px;
  border-top: 1px solid var(--border);
}
.stat-num {
  font-family: 'Syne', sans-serif;
  font-size: 1.75rem;
  font-weight: 800;
  line-height: 1;
}
.stat-num span { color: var(--fire); }
.stat-label { font-size: 0.75rem; color: var(--text3); margin-top: 4px; font-weight: 500; }

/* Hero floating cards */
.hero-right {
  position: absolute; right: 0; top: 0; bottom: 0;
  width: 46%;
  display: flex; align-items: center; justify-content: center;
}
.hfg { position: relative; width: 400px; height: 400px; }
.hf {
  position: absolute;
  background: var(--surface);
  border: 1px solid var(--border2);
  border-radius: var(--rad-lg);
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(0,0,0,0.5);
  cursor: none;
  transition: var(--t);
}
.hf:nth-child(1) { width: 178px; top: 20px; left: 78px; animation: hfloat 5s ease-in-out infinite 0s; }
.hf:nth-child(2) { width: 158px; top: 58px; left: 252px; animation: hfloat 5s ease-in-out infinite 1.3s; }
.hf:nth-child(3) { width: 168px; top: 225px; left: 38px; animation: hfloat 5s ease-in-out infinite 2.6s; }
.hf:nth-child(4) { width: 152px; top: 245px; left: 238px; animation: hfloat 5s ease-in-out infinite 3.9s; }
@keyframes hfloat { 0%, 100% { translate: 0 0; } 50% { translate: 0 -14px; } }
.hf:hover { transform: scale(1.05); border-color: rgba(255,69,0,0.5); }
.hf img { width: 100%; height: 128px; object-fit: cover; }
.hf-info { padding: 10px 12px; }
.hf-name { font-size: 0.7rem; font-weight: 600; margin-bottom: 5px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.hf-price { font-size: 0.82rem; font-weight: 800; color: var(--fire); }
.hf-old { font-size: 0.68rem; color: var(--text3); text-decoration: line-through; margin-left: 5px; }

/* ─────────────────────────────────────────────
   PROMO STRIP
───────────────────────────────────────────── */
.promo-strip {
  background: linear-gradient(90deg, rgba(255,69,0,0.1), rgba(232,255,0,0.05), rgba(255,69,0,0.1));
  border-top: 1px solid rgba(255,69,0,0.16);
  border-bottom: 1px solid rgba(255,69,0,0.16);
  padding: 12px 24px;
  display: flex;
  gap: 40px;
  overflow-x: auto;
  white-space: nowrap;
  scrollbar-width: none;
}
.promo-strip::-webkit-scrollbar { display: none; }
.promo-item { display: flex; align-items: center; gap: 9px; font-size: 0.82rem; font-weight: 600; color: var(--text2); flex-shrink: 0; }
.promo-item .pi { font-size: 1.05rem; }
.promo-item strong { color: var(--text); }

/* ─────────────────────────────────────────────
   SECTIONS
───────────────────────────────────────────── */
.section { padding: 60px 24px; }
.section-head {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  margin-bottom: 32px;
  gap: 16px;
}
.eyebrow {
  font-size: 0.73rem;
  font-weight: 700;
  letter-spacing: 1.2px;
  color: var(--fire);
  text-transform: uppercase;
  margin-bottom: 6px;
  display: flex;
  align-items: center;
  gap: 8px;
}
.eyebrow::before { content: ''; width: 20px; height: 2px; background: var(--fire); border-radius: 2px; }
.sec-title {
  font-family: 'Syne', sans-serif;
  font-size: 1.75rem;
  font-weight: 800;
  letter-spacing: -0.5px;
}
.sec-sub { font-size: 0.875rem; color: var(--text2); margin-top: 5px; }
.see-all {
  font-size: 0.82rem;
  font-weight: 700;
  color: var(--fire);
  border-bottom: 1px solid rgba(255,69,0,0.32);
  padding-bottom: 2px;
  transition: var(--t);
  cursor: none;
  white-space: nowrap;
}
.see-all:hover { border-color: var(--fire); }

/* Countdown */
.countdown-row { display: flex; align-items: center; gap: 10px; margin-bottom: 28px; }
.cd-label {
  font-size: 0.78rem; font-weight: 700;
  color: var(--fire);
  background: rgba(255,69,0,0.12);
  border: 1px solid rgba(255,69,0,0.26);
  border-radius: 100px;
  padding: 5px 14px;
}
.cd-block {
  background: var(--fire); color: #fff;
  border-radius: 7px; padding: 5px 10px;
  font-family: 'Syne', sans-serif;
  font-size: 1.05rem; font-weight: 800;
  min-width: 38px; text-align: center;
}
.cd-sep { color: var(--fire); font-weight: 800; font-size: 1.1rem; }

/* ─────────────────────────────────────────────
   PRODUCT CARDS
───────────────────────────────────────────── */
.prod-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 18px;
}
.prod-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--rad-lg);
  overflow: hidden;
  transition: var(--t);
  cursor: none;
  position: relative;
}
.prod-card:hover {
  transform: translateY(-7px);
  border-color: rgba(255,69,0,0.38);
  box-shadow: 0 20px 50px rgba(0,0,0,0.48), 0 0 26px var(--fire-glow);
}
.pc-img {
  position: relative;
  height: 212px;
  background: var(--ink3);
  overflow: hidden;
}
.pc-img img {
  width: 100%; height: 100%;
  object-fit: cover;
  transition: transform 0.5s var(--ease);
}
.prod-card:hover .pc-img img { transform: scale(1.09); }
.pc-img-alt {
  position: absolute; inset: 0;
  opacity: 0;
  transition: opacity 0.4s;
}
.pc-img-alt img { width: 100%; height: 100%; object-fit: cover; }
.prod-card:hover .pc-img-alt { opacity: 1; }

/* Badges */
.badge-dis {
  position: absolute; top: 10px; left: 10px; z-index: 2;
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff; font-size: 0.65rem; font-weight: 800;
  border-radius: var(--rad-xs); padding: 3px 8px;
}
.badge-hot {
  position: absolute; top: 10px; left: 10px; z-index: 2;
  background: linear-gradient(135deg, var(--purple), var(--fire));
  color: #fff; font-size: 0.65rem; font-weight: 800;
  border-radius: var(--rad-xs); padding: 3px 8px;
}
.badge-new {
  position: absolute; top: 10px; left: 10px; z-index: 2;
  background: linear-gradient(135deg, #00C853, #00E676);
  color: #08080F; font-size: 0.65rem; font-weight: 800;
  border-radius: var(--rad-xs); padding: 3px 8px;
}

/* Wishlist btn */
.pc-wish {
  position: absolute; top: 10px; right: 10px; z-index: 3;
  width: 32px; height: 32px; border-radius: 50%;
  background: rgba(8,8,15,0.68);
  backdrop-filter: blur(8px);
  border: 1px solid var(--border2);
  display: flex; align-items: center; justify-content: center;
  font-size: 0.9rem;
  opacity: 0;
  transition: var(--t);
  cursor: none;
}
.prod-card:hover .pc-wish, .pc-wish.on { opacity: 1; }
.pc-wish.on { background: rgba(255,23,68,0.22); border-color: rgba(255,23,68,0.55); }
.pc-wish:hover { transform: scale(1.1); }

/* Quick view */
.pc-qv {
  position: absolute; bottom: -38px; left: 0; right: 0;
  background: rgba(255,69,0,0.93);
  backdrop-filter: blur(8px);
  text-align: center;
  padding: 9px;
  font-size: 0.76rem; font-weight: 800;
  letter-spacing: 0.7px;
  transition: bottom 0.28s var(--ease);
  z-index: 2;
}
.prod-card:hover .pc-qv { bottom: 0; }

/* Card body */
.pc-body { padding: 13px 14px; }
.pc-cat-label { font-size: 0.65rem; font-weight: 700; color: var(--text3); letter-spacing: 0.6px; text-transform: uppercase; margin-bottom: 5px; }
.pc-name { font-size: 0.83rem; font-weight: 500; margin-bottom: 8px; line-height: 1.42; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
.pc-stars { display: flex; align-items: center; gap: 5px; margin-bottom: 9px; }
.stars { color: var(--warn); font-size: 0.72rem; letter-spacing: 0.5px; }
.review-count { font-size: 0.72rem; color: var(--text3); }
.pc-price { display: flex; align-items: baseline; gap: 7px; flex-wrap: wrap; }
.price-now { font-family: 'Syne', sans-serif; font-size: 1.08rem; font-weight: 800; color: var(--fire); }
.price-old { font-size: 0.78rem; color: var(--text3); text-decoration: line-through; }
.pc-atc {
  width: 100%; margin-top: 10px; padding: 9px;
  border-radius: 100px;
  background: linear-gradient(135deg, rgba(255,69,0,0.14), rgba(255,107,53,0.09));
  border: 1px solid rgba(255,69,0,0.32);
  color: var(--fire);
  font-weight: 700; font-size: 0.8rem;
  transition: var(--t); cursor: none;
}
.pc-atc:hover {
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff; border-color: transparent;
  box-shadow: 0 6px 20px var(--fire-glow);
}
.pc-atc.done {
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff; border-color: transparent;
}

/* ─────────────────────────────────────────────
   CATEGORY HOME GRID
───────────────────────────────────────────── */
.cat-grid-home {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
  gap: 14px;
}
.cat-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--rad);
  padding: 22px 14px;
  text-align: center;
  cursor: none;
  transition: var(--t);
  position: relative;
  overflow: hidden;
}
.cat-card::after {
  content: '';
  position: absolute; inset: 0;
  background: linear-gradient(135deg, var(--cc1, var(--fire)), var(--cc2, var(--fire-lt)));
  opacity: 0;
  transition: opacity 0.3s;
}
.cat-card:hover {
  transform: translateY(-5px);
  border-color: var(--cc1, var(--fire));
  box-shadow: 0 12px 30px rgba(0,0,0,0.35);
}
.cat-card:hover::after { opacity: 0.08; }
.cc-icon { font-size: 1.9rem; margin-bottom: 10px; display: block; position: relative; z-index: 1; transition: transform 0.28s; }
.cat-card:hover .cc-icon { transform: scale(1.22) rotate(-6deg); }
.cc-name { font-size: 0.76rem; font-weight: 700; position: relative; z-index: 1; line-height: 1.35; }
.cc-count { font-size: 0.68rem; color: var(--text3); margin-top: 3px; position: relative; z-index: 1; }

/* ─────────────────────────────────────────────
   TRENDING CAROUSEL
───────────────────────────────────────────── */
.scroll-carousel { overflow: hidden; margin: 0 -24px; padding: 0 24px; }
.carousel-inner {
  display: flex; gap: 16px;
  animation: carScroll 42s linear infinite;
  width: max-content;
}
.carousel-inner:hover { animation-play-state: paused; }
@keyframes carScroll {
  from { transform: translateX(0); }
  to { transform: translateX(-50%); }
}
.car-card {
  flex: 0 0 198px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--rad-lg);
  overflow: hidden;
  cursor: none;
  transition: var(--t);
}
.car-card:hover {
  transform: scale(1.04);
  border-color: rgba(155,48,255,0.5);
  box-shadow: 0 12px 38px rgba(155,48,255,0.18);
}
.car-img { height: 186px; overflow: hidden; background: var(--ink3); }
.car-img img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.5s; }
.car-card:hover img { transform: scale(1.1); }
.car-info { padding: 11px 13px; }
.car-name { font-size: 0.79rem; font-weight: 500; margin-bottom: 5px; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; line-height: 1.4; }
.car-price { font-size: 0.88rem; font-weight: 800; color: var(--purple); }

/* ─────────────────────────────────────────────
   CATEGORY LISTING PAGE
───────────────────────────────────────────── */
#page-cat { padding-top: calc(var(--nav-h) + var(--cat-h)); }
.cat-page-header {
  padding: 26px 24px;
  border-bottom: 1px solid var(--border);
  background: linear-gradient(135deg, rgba(255,69,0,0.07), transparent);
}
.cph-icon { font-size: 2.6rem; margin-bottom: 8px; }
.cph-name { font-family: 'Syne', sans-serif; font-size: 1.85rem; font-weight: 800; margin-bottom: 5px; }
.cph-desc { font-size: 0.9rem; color: var(--text2); margin-bottom: 14px; }
.cph-count { font-size: 0.82rem; color: var(--text3); }

.cat-layout {
  display: grid;
  grid-template-columns: 220px 1fr;
}

/* Sidebar */
.cat-sidebar {
  border-right: 1px solid var(--border);
  padding: 24px;
  background: var(--glass);
  position: sticky;
  top: calc(var(--nav-h) + var(--cat-h));
  height: calc(100vh - var(--nav-h) - var(--cat-h));
  overflow-y: auto;
}
.cat-sidebar::-webkit-scrollbar { width: 2px; }
.sb-section { margin-bottom: 28px; }
.sb-title { font-size: 0.78rem; font-weight: 800; letter-spacing: 0.9px; color: var(--text3); text-transform: uppercase; margin-bottom: 14px; }
.filter-opt {
  display: flex; align-items: center; gap: 10px;
  padding: 7px 0;
  cursor: none;
  font-size: 0.84rem;
  color: var(--text2);
  transition: color 0.18s;
}
.filter-opt:hover { color: var(--text); }
.f-check {
  width: 16px; height: 16px; border-radius: 4px;
  border: 1.5px solid var(--border2);
  background: var(--glass);
  display: flex; align-items: center; justify-content: center;
  flex-shrink: 0;
  transition: var(--t);
}
.filter-opt.checked .f-check {
  background: var(--fire);
  border-color: var(--fire);
}
.filter-opt.checked .f-check::after { content: '✓'; font-size: 0.6rem; color: #fff; font-weight: 800; }
.price-range { display: flex; gap: 8px; margin-top: 6px; }
.price-input {
  width: 80px;
  background: var(--surface2);
  border: 1px solid var(--border2);
  border-radius: var(--rad-sm);
  padding: 8px 10px;
  color: var(--text);
  font-size: 0.82rem;
}
.price-input:focus { border-color: rgba(255,69,0,0.5); }
.apply-btn {
  width: 100%; margin-top: 12px; padding: 9px;
  border-radius: 100px;
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff; font-weight: 700; font-size: 0.82rem;
  transition: var(--t); cursor: none;
}
.apply-btn:hover { box-shadow: 0 6px 20px var(--fire-glow); transform: translateY(-1px); }

/* Sort bar */
.sort-bar {
  display: flex; align-items: center; gap: 10px;
  padding: 14px 24px;
  border-bottom: 1px solid var(--border);
  background: var(--glass);
  flex-wrap: wrap;
}
.sort-label { font-size: 0.8rem; color: var(--text3); font-weight: 600; }
.sort-btn {
  padding: 6px 15px; border-radius: 100px;
  font-size: 0.78rem; font-weight: 600;
  color: var(--text2);
  background: var(--glass);
  border: 1px solid var(--border);
  transition: var(--t); cursor: none;
}
.sort-btn.active, .sort-btn:hover {
  background: var(--fire); color: #fff; border-color: transparent;
}
.cat-products { padding: 24px; }

/* ─────────────────────────────────────────────
   PRODUCT DETAIL PAGE
───────────────────────────────────────────── */
#page-prod { padding-top: calc(var(--nav-h) + var(--cat-h)); }
.pd-wrap {
  padding: 28px 24px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 38px;
  max-width: 1100px;
  margin: 0 auto;
}

/* Gallery */
.pd-main-img {
  height: 400px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--rad-lg);
  overflow: hidden;
  cursor: zoom-in;
  position: relative;
  margin-bottom: 12px;
}
.pd-main-img img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.4s; }
.pd-main-img:hover img { transform: scale(1.14); }
.pd-thumbs { display: flex; gap: 9px; flex-wrap: wrap; }
.pd-thumb {
  width: 66px; height: 66px; border-radius: 10px;
  overflow: hidden;
  border: 2px solid transparent;
  cursor: none; transition: var(--t);
  background: var(--surface); flex-shrink: 0;
}
.pd-thumb.active, .pd-thumb:hover { border-color: var(--fire); }
.pd-thumb img { width: 100%; height: 100%; object-fit: cover; }

/* Product info */
.pd-cat-label { font-size: 0.7rem; font-weight: 700; color: var(--fire); letter-spacing: 0.9px; text-transform: uppercase; margin-bottom: 8px; }
.pd-title { font-family: 'Syne', sans-serif; font-size: 1.5rem; font-weight: 700; line-height: 1.26; margin-bottom: 13px; letter-spacing: -0.3px; }
.pd-rating-row { display: flex; align-items: center; gap: 12px; margin-bottom: 18px; flex-wrap: wrap; }
.pd-sold { font-size: 0.77rem; color: var(--text3); }

/* Price block */
.pd-price-block {
  background: linear-gradient(135deg, rgba(255,69,0,0.09), rgba(255,107,53,0.04));
  border: 1px solid rgba(255,69,0,0.16);
  border-radius: var(--rad);
  padding: 16px;
  margin-bottom: 18px;
}
.pd-price-main { font-family: 'Syne', sans-serif; font-size: 2.1rem; font-weight: 800; color: var(--fire); line-height: 1; }
.pd-price-row { display: flex; align-items: baseline; gap: 12px; margin-bottom: 6px; }
.pd-price-old { font-size: 1rem; color: var(--text3); text-decoration: line-through; }
.pd-price-save {
  font-size: 0.8rem; color: var(--success);
  font-weight: 700;
  background: rgba(0,230,118,0.1);
  border-radius: 6px; padding: 2px 8px;
}
.pd-timer { display: flex; align-items: center; gap: 8px; font-size: 0.79rem; color: var(--text2); margin-top: 9px; }
.pd-timer .cd-block { font-size: 0.82rem; padding: 3px 8px; }

/* Stock */
.stock-alert {
  display: flex; align-items: center; gap: 9px;
  background: rgba(255,23,68,0.08);
  border: 1px solid rgba(255,23,68,0.22);
  border-radius: var(--rad-sm);
  padding: 10px 14px;
  font-size: 0.82rem; font-weight: 600; color: #FF5252;
  margin-bottom: 18px;
}
.stock-bar-wrap { margin-bottom: 18px; }
.sb-labels { font-size: 0.73rem; color: var(--text3); margin-bottom: 6px; display: flex; justify-content: space-between; }
.sb-track { height: 5px; background: var(--surface3); border-radius: 3px; overflow: hidden; }
.sb-fill { height: 100%; background: linear-gradient(90deg, var(--fire), var(--fire-lt)); border-radius: 3px; }

/* Variants */
.pd-variants { margin-bottom: 18px; }
.pv-label { font-size: 0.79rem; font-weight: 700; color: var(--text2); margin-bottom: 9px; }
.pv-opts { display: flex; gap: 8px; flex-wrap: wrap; }
.pv-opt {
  padding: 7px 16px; border-radius: 100px;
  border: 1.5px solid var(--border2);
  font-size: 0.8rem; font-weight: 600; color: var(--text2);
  cursor: none; transition: var(--t);
}
.pv-opt:hover, .pv-opt.sel { border-color: var(--fire); color: var(--fire); background: rgba(255,69,0,0.08); }
.pv-color {
  width: 30px; height: 30px; border-radius: 50%;
  border: 2px solid transparent;
  cursor: none; transition: var(--t);
}
.pv-color:hover, .pv-color.sel { border-color: var(--fire); box-shadow: 0 0 0 3px var(--fire-glow); }

/* Qty */
.pd-qty { display: flex; align-items: center; gap: 12px; margin-bottom: 20px; }
.qty-label { font-size: 0.79rem; font-weight: 700; color: var(--text2); }
.qty-ctrl {
  display: flex; align-items: center;
  background: var(--surface2);
  border: 1px solid var(--border2);
  border-radius: 100px; overflow: hidden;
}
.qty-btn {
  width: 36px; height: 36px;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.1rem; cursor: none; color: var(--text2);
  font-weight: 700;
  transition: background 0.18s;
}
.qty-btn:hover { background: var(--surface3); color: var(--text); }
.qty-num { padding: 0 14px; font-size: 0.9rem; font-weight: 700; min-width: 36px; text-align: center; }

/* CTAs */
.pd-ctas { display: flex; gap: 12px; margin-bottom: 22px; }
.btn-add-cart {
  flex: 1; padding: 14px; border-radius: 100px;
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff; font-weight: 800; font-size: 0.95rem;
  transition: var(--t);
  box-shadow: 0 8px 28px var(--fire-glow);
  cursor: none;
}
.btn-add-cart:hover { transform: translateY(-2px); box-shadow: 0 14px 38px rgba(255,69,0,0.48); }
.btn-buy-now {
  flex: 1; padding: 14px; border-radius: 100px;
  background: var(--volt); color: var(--ink);
  font-weight: 800; font-size: 0.95rem;
  transition: var(--t); cursor: none;
}
.btn-buy-now:hover { transform: translateY(-2px); box-shadow: 0 8px 28px rgba(232,255,0,0.32); }
.btn-wish-lg {
  width: 50px; height: 50px; border-radius: 50%;
  background: var(--glass);
  border: 1px solid var(--border2);
  display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem; cursor: none; transition: var(--t); flex-shrink: 0;
}
.btn-wish-lg:hover { background: rgba(255,23,68,0.15); border-color: rgba(255,23,68,0.45); }

/* Trust badges */
.trust-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-bottom: 22px; }
.trust-item {
  display: flex; align-items: center; gap: 9px;
  background: var(--glass);
  border: 1px solid var(--border);
  border-radius: var(--rad-sm);
  padding: 10px 12px;
  font-size: 0.77rem; font-weight: 600; color: var(--text2);
}
.trust-ico { font-size: 1.05rem; flex-shrink: 0; }
.pd-desc { font-size: 0.875rem; color: var(--text2); line-height: 1.76; border-top: 1px solid var(--border); padding-top: 18px; }

/* Sticky ATC */
#sticky-atc {
  position: fixed; bottom: 0; left: 0; right: 0;
  z-index: 6500;
  background: rgba(12,12,20,0.97);
  backdrop-filter: blur(22px);
  border-top: 1px solid var(--border);
  padding: 12px 24px;
  display: flex; align-items: center; gap: 16px;
  transform: translateY(100%);
  transition: transform 0.3s var(--ease);
  box-shadow: 0 -8px 40px rgba(0,0,0,0.44);
}
#sticky-atc.show { transform: translateY(0); }
.satc-info { flex: 1; min-width: 0; }
.satc-name { font-size: 0.875rem; font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.satc-price { font-size: 1rem; font-weight: 800; color: var(--fire); }
.satc-btn {
  padding: 11px 28px; border-radius: 100px;
  background: linear-gradient(135deg, var(--fire), var(--fire-lt));
  color: #fff; font-weight: 800; font-size: 0.875rem;
  white-space: nowrap; transition: var(--t); cursor: none;
}
.satc-btn:hover { box-shadow: 0 6px 20px var(--fire-glow); }

/* ─────────────────────────────────────────────
   REVIEWS
───────────────────────────────────────────── */
.reviews-sec { padding: 36px 24px; border-top: 1px solid var(--border); max-width: 1100px; margin: 0 auto; }
.review-sum {
  display: flex; gap: 32px; align-items: center;
  margin-bottom: 30px; padding: 24px;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--rad-lg);
  flex-wrap: wrap;
}
.rs-big { text-align: center; }
.rs-num { font-family: 'Syne', sans-serif; font-size: 3.5rem; font-weight: 800; line-height: 1; color: var(--fire); }
.rs-stars { font-size: 1.1rem; color: var(--warn); margin: 6px 0; }
.rs-cnt { font-size: 0.78rem; color: var(--text3); }
.rs-bars { flex: 1; min-width: 200px; }
.rsb-row { display: flex; align-items: center; gap: 10px; margin-bottom: 7px; font-size: 0.77rem; color: var(--text3); }
.rsb-track { flex: 1; height: 6px; background: var(--surface3); border-radius: 3px; overflow: hidden; }
.rsb-fill { height: 100%; background: var(--warn); border-radius: 3px; }
.review-cards { display: grid; gap: 16px; }
.rev-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--rad);
  padding: 18px; transition: var(--t);
}
.rev-card:hover { border-color: var(--border2); }
.rev-top { display: flex; align-items: center; gap: 12px; margin-bottom: 10px; }
.rev-av {
  width: 38px; height: 38px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 0.84rem; font-weight: 800; flex-shrink: 0;
}
.rev-name { font-size: 0.875rem; font-weight: 700; }
.rev-date { font-size: 0.74rem; color: var(--text3); }
.rev-body { font-size: 0.845rem; color: var(--text2); line-height: 1.67; }
.rev-imgs { display: flex; gap: 8px; margin-top: 12px; flex-wrap: wrap; }
.rev-img { width: 62px; height: 62px; border-radius: 8px; overflow: hidden; border: 1px solid var(--border); flex-shrink: 0; }
.rev-img img { width: 100%; height: 100%; object-fit: cover; }

/* FBT */
.fbt-sec { padding: 36px 24px; border-top: 1px solid var(--border); max-width: 1100px; margin: 0 auto; }
.fbt-items { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; margin-bottom: 20px; }
.fbt-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--rad); overflow: hidden;
  width: 128px; flex-shrink: 0; cursor: none; transition: var(--t);
}
.fbt-card:hover { border-color: var(--border2); transform: scale(1.03); }
.fbt-card img { width: 100%; height: 96px; object-fit: cover; }
.fbt-info { padding: 8px 10px; }
.fbt-name { font-size: 0.71rem; font-weight: 500; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; margin-bottom: 4px; line-height: 1.35; }
.fbt-price { font-size: 0.8rem; font-weight: 800; color: var(--fire); }
.fbt-plus { font-size: 1.5rem; color: var(--text3); }
.fbt-total { display: flex; align-items: center; gap: 18px; flex-wrap: wrap; }
.fbt-total-price { font-family: 'Syne', sans-serif; font-size: 1.3rem; font-weight: 800; }
.fbt-total-price span { color: var(--fire); }

/* Related */
.related-sec { padding: 36px 24px; border-top: 1px solid var(--border); max-width: 1100px; margin: 0 auto; }

/* ─────────────────────────────────────────────
   FOOTER
───────────────────────────────────────────── */
footer { padding: 56px 24px 28px; border-top: 1px solid var(--border); margin-top: 60px; }
.footer-grid { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 38px; margin-bottom: 40px; }
.f-brand { font-family: 'Syne', sans-serif; font-size: 1.3rem; font-weight: 800; background: linear-gradient(90deg, var(--fire), var(--volt)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 12px; }
.f-desc { font-size: 0.845rem; color: var(--text2); line-height: 1.72; margin-bottom: 18px; }
.f-social { display: flex; gap: 8px; }
.soc-btn { width: 34px; height: 34px; border-radius: 50%; background: var(--glass); border: 1px solid var(--border); display: flex; align-items: center; justify-content: center; font-size: 0.84rem; cursor: none; transition: var(--t); }
.soc-btn:hover { background: rgba(255,69,0,0.16); border-color: rgba(255,69,0,0.36); }
.f-col-title { font-size: 0.82rem; font-weight: 800; margin-bottom: 14px; }
.f-links { display: flex; flex-direction: column; gap: 9px; }
.f-links a { font-size: 0.8rem; color: var(--text2); transition: color 0.18s; cursor: none; }
.f-links a:hover { color: var(--text); }
.footer-bottom { padding-top: 22px; border-top: 1px solid var(--border); display: flex; align-items: center; justify-content: space-between; gap: 14px; flex-wrap: wrap; }
.f-copy { font-size: 0.78rem; color: var(--text3); }
.f-legal { display: flex; gap: 18px; }
.f-legal a { font-size: 0.78rem; color: var(--text3); cursor: none; transition: color 0.18s; }
.f-legal a:hover { color: var(--text2); }

/* ─────────────────────────────────────────────
   SCROLL REVEAL
───────────────────────────────────────────── */
.reveal { opacity: 0; transform: translateY(24px); transition: opacity 0.52s ease, transform 0.52s ease; }
.reveal.in { opacity: 1; transform: translateY(0); }

/* ─────────────────────────────────────────────
   RESPONSIVE
───────────────────────────────────────────── */
@media (max-width: 1024px) {
  .hero-right { display: none; }
  #modal-inner { grid-template-columns: 1fr; }
  .footer-grid { grid-template-columns: 1fr 1fr; }
}
@media (max-width: 768px) {
  nav { padding: 0 16px; gap: 10px; }
  .nav-search { display: none; }
  .cat-bar { padding: 0 16px; }
  .hero { padding: 0 16px 52px; padding-top: calc(var(--nav-h) + var(--cat-h) + 24px); min-height: unset; }
  .hero h1 { font-size: 2.4rem; letter-spacing: -1.5px; }
  .section { padding: 48px 16px; }
  .cat-layout { grid-template-columns: 1fr; }
  .cat-sidebar { display: none; }
  .pd-wrap { grid-template-columns: 1fr; padding: 18px 16px; }
  .trust-grid { grid-template-columns: 1fr; }
  .review-sum { flex-direction: column; }
  footer { padding: 40px 16px 22px; }
  .footer-grid { grid-template-columns: 1fr 1fr; }
  .promo-strip { padding: 10px 16px; }
}
@media (max-width: 480px) {
  .hero h1 { font-size: 2rem; }
  .prod-grid { grid-template-columns: repeat(2, 1fr); gap: 12px; }
  .footer-grid { grid-template-columns: 1fr; }
  .pd-ctas { flex-wrap: wrap; }
  .btn-add-cart, .btn-buy-now { flex: 1 1 45%; }
  .btn-wish-lg { width: 44px; height: 44px; font-size: 1rem; }
}
</style>
</head>
<body>

<!-- Custom cursor -->
<div id="cur"></div>
<div id="cur-r"></div>

<!-- Toast -->
<div id="toast">
  <div id="toast-icon">🛒</div>
  <div id="toast-msg">Added to cart!</div>
</div>

<!-- Quick View Modal -->
<div id="modal-bg" onclick="modalBgClick(event)">
  <div id="modal-box">
    <button class="modal-close-btn" onclick="closeModal()" onmouseenter="H(1)" onmouseleave="H(0)">✕</button>
    <div id="modal-inner"></div>
  </div>
</div>

<!-- Sticky Add to Cart -->
<div id="sticky-atc">
  <div class="satc-info">
    <div class="satc-name" id="satc-name"></div>
    <div class="satc-price" id="satc-price"></div>
  </div>
  <button class="satc-btn" onclick="addCart(); toast('🛒','<strong>Added to cart!</strong> Keep exploring →')" onmouseenter="H(1)" onmouseleave="H(0)">🛒 Add to Cart</button>
</div>

<!-- ═══════════════════════════════
     NAVIGATION
═══════════════════════════════ -->
<nav id="main-nav">
  <div class="nav-logo" onclick="goPage('home')" onmouseenter="H(1)" onmouseleave="H(0)">RareFinds</div>
  <div class="nav-search">
    <span class="nav-search-icon">🔍</span>
    <input type="text" placeholder="Search millions of products..." id="search-input" onkeyup="searchHandler(event)">
  </div>
  <div class="nav-actions">
    <div class="nav-btn" title="Wishlist" onmouseenter="H(1)" onmouseleave="H(0)">
      ❤️<div class="nav-badge" id="wish-badge">0</div>
    </div>
    <div class="nav-btn" title="Cart" onmouseenter="H(1)" onmouseleave="H(0)">
      🛒<div class="nav-badge" id="cart-badge">0</div>
    </div>
    <div class="nav-btn" title="Account" onmouseenter="H(1)" onmouseleave="H(0)">👤</div>
  </div>
</nav>
<div class="cat-bar" id="cat-bar"></div>

<!-- ═══════════════════════════════
     HOME PAGE
═══════════════════════════════ -->
<div class="page active" id="page-home">

  <!-- Hero -->
  <div class="hero">
    <div class="hero-bg"></div>
    <div class="hero-mesh"></div>
    <div class="hero-content">
      <div class="hero-tag"><div class="live-dot"></div>⚡ New drops every 60 minutes</div>
      <h1>Find What<br><em>Everyone</em><br>Is Missing</h1>
      <p>Thousands of rare deals on unique products — curated daily across 11 categories. The best finds at prices that feel impossible.</p>
      <div class="hero-btns">
        <button class="btn-fire" onclick="scrollTo({top:document.getElementById('sec-flash').offsetTop-120,behavior:'smooth'})" onmouseenter="H(1)" onmouseleave="H(0)">Shop Flash Deals ↓</button>
        <button class="btn-outline" onclick="scrollTo({top:document.getElementById('sec-cats').offsetTop-120,behavior:'smooth'})" onmouseenter="H(1)" onmouseleave="H(0)">Browse Categories</button>
      </div>
      <div class="hero-stats">
        <div><div class="stat-num">4.2<span>M+</span></div><div class="stat-label">Happy Shoppers</div></div>
        <div><div class="stat-num">120<span>K+</span></div><div class="stat-label">Products</div></div>
        <div><div class="stat-num">98<span>%</span></div><div class="stat-label">Satisfaction</div></div>
      </div>
    </div>
    <div class="hero-right">
      <div class="hfg" id="hero-floats"></div>
    </div>
  </div>

  <!-- Promo strip -->
  <div class="promo-strip">
    <div class="promo-item"><span class="pi">🚚</span><strong>Free Shipping</strong> over $25</div>
    <div class="promo-item"><span class="pi">⚡</span><strong>Flash deals</strong> every hour</div>
    <div class="promo-item"><span class="pi">🔥</span><strong>247 people</strong> shopping now</div>
    <div class="promo-item"><span class="pi">↩️</span><strong>30-day</strong> easy returns</div>
    <div class="promo-item"><span class="pi">🛡️</span><strong>Buyer Protection</strong> always on</div>
    <div class="promo-item"><span class="pi">⭐</span><strong>4.8/5</strong> average rating</div>
  </div>

  <!-- Flash Sale -->
  <div class="section" id="sec-flash">
    <div class="section-head reveal">
      <div>
        <div class="eyebrow">Limited Time</div>
        <div class="sec-title">⚡ Flash Sale</div>
        <div class="sec-sub">Deals that disappear — grab them before they're gone</div>
      </div>
      <div style="display:flex;align-items:center;gap:16px;flex-wrap:wrap">
        <div class="countdown-row" style="margin:0">
          <div class="cd-label">ENDS IN</div>
          <div class="cd-block" id="fcd-h">02</div>
          <div class="cd-sep">:</div>
          <div class="cd-block" id="fcd-m">47</div>
          <div class="cd-sep">:</div>
          <div class="cd-block" id="fcd-s">33</div>
        </div>
        <a class="see-all" href="#" onmouseenter="H(1)" onmouseleave="H(0)">All deals →</a>
      </div>
    </div>
    <div class="prod-grid reveal" id="grid-flash"></div>
  </div>

  <!-- Categories -->
  <div class="section" id="sec-cats" style="padding-top:0">
    <div class="section-head reveal">
      <div>
        <div class="eyebrow">Explore</div>
        <div class="sec-title">🗂️ Shop by Category</div>
      </div>
      <a class="see-all" href="#" onmouseenter="H(1)" onmouseleave="H(0)">All categories →</a>
    </div>
    <div class="cat-grid-home reveal" id="cats-home"></div>
  </div>

  <!-- Trending Carousel -->
  <div class="section" style="padding-bottom:8px">
    <div class="section-head reveal">
      <div>
        <div class="eyebrow">Hot Right Now</div>
        <div class="sec-title">🔥 Trending Now</div>
      </div>
      <a class="see-all" href="#" onmouseenter="H(1)" onmouseleave="H(0)">View all →</a>
    </div>
    <div class="scroll-carousel reveal">
      <div class="carousel-inner" id="carousel-trending"></div>
    </div>
  </div>

  <!-- New Arrivals -->
  <div class="section" id="sec-new">
    <div class="section-head reveal">
      <div>
        <div class="eyebrow">Just In</div>
        <div class="sec-title">✨ New Arrivals</div>
        <div class="sec-sub">Fresh drops from today's curated selection</div>
      </div>
      <a class="see-all" href="#" onmouseenter="H(1)" onmouseleave="H(0)">See all →</a>
    </div>
    <div class="prod-grid reveal" id="grid-new"></div>
  </div>

  <!-- For You -->
  <div class="section" style="background:linear-gradient(135deg,rgba(155,48,255,0.05),rgba(255,69,0,0.04))">
    <div class="section-head reveal">
      <div>
        <div class="eyebrow" style="color:var(--purple)">AI Curated</div>
        <div class="sec-title">🤖 Recommended For You</div>
        <div class="sec-sub">Personalized picks based on what shoppers like you love</div>
      </div>
      <a class="see-all" href="#" onmouseenter="H(1)" onmouseleave="H(0)">Refresh →</a>
    </div>
    <div class="prod-grid reveal" id="grid-foryou"></div>
  </div>

  <footer>
    <div class="footer-grid">
      <div>
        <div class="f-brand">RareFinds</div>
        <div class="f-desc">Your daily destination for extraordinary deals across thousands of unique products. Find something rare, every single day.</div>
        <div class="f-social">
          <div class="soc-btn" onmouseenter="H(1)" onmouseleave="H(0)">𝕏</div>
          <div class="soc-btn" onmouseenter="H(1)" onmouseleave="H(0)">📘</div>
          <div class="soc-btn" onmouseenter="H(1)" onmouseleave="H(0)">📸</div>
          <div class="soc-btn" onmouseenter="H(1)" onmouseleave="H(0)">▶️</div>
        </div>
      </div>
      <div>
        <div class="f-col-title">Shop</div>
        <div class="f-links">
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Flash Deals</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">New Arrivals</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Best Sellers</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Clearance</a>
        </div>
      </div>
      <div>
        <div class="f-col-title">Help</div>
        <div class="f-links">
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Track Order</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Returns</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Size Guide</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Contact</a>
        </div>
      </div>
      <div>
        <div class="f-col-title">Company</div>
        <div class="f-links">
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">About</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Careers</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Blog</a>
          <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Affiliates</a>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <div class="f-copy">© 2026 RareFinds. All rights reserved.</div>
      <div class="f-legal">
        <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Privacy Policy</a>
        <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Terms of Use</a>
        <a href="#" onmouseenter="H(1)" onmouseleave="H(0)">Cookies</a>
      </div>
    </div>
  </footer>
</div>

<!-- ═══════════════════════════════
     CATEGORY PAGE
═══════════════════════════════ -->
<div class="page" id="page-cat">
  <div class="cat-page-header" id="cph">
    <div class="cph-icon" id="cph-icon"></div>
    <div class="cph-name" id="cph-name"></div>
    <div class="cph-desc" id="cph-desc"></div>
    <div class="cph-count" id="cph-count"></div>
  </div>
  <div class="sort-bar">
    <span class="sort-label">Sort by:</span>
    <button class="sort-btn active" onclick="setSort(this,'pop')" onmouseenter="H(1)" onmouseleave="H(0)">Popular</button>
    <button class="sort-btn" onclick="setSort(this,'pa')" onmouseenter="H(1)" onmouseleave="H(0)">Price ↑</button>
    <button class="sort-btn" onclick="setSort(this,'pd')" onmouseenter="H(1)" onmouseleave="H(0)">Price ↓</button>
    <button class="sort-btn" onclick="setSort(this,'rat')" onmouseenter="H(1)" onmouseleave="H(0)">Top Rated</button>
    <button class="sort-btn" onclick="setSort(this,'new')" onmouseenter="H(1)" onmouseleave="H(0)">Newest</button>
  </div>
  <div class="cat-layout">
    <div class="cat-sidebar">
      <div class="sb-section">
        <div class="sb-title">Price Range</div>
        <div class="price-range">
          <input class="price-input" type="number" placeholder="Min" id="f-min" value="0">
          <input class="price-input" type="number" placeholder="Max" id="f-max" value="500">
        </div>
        <button class="apply-btn" onclick="applyFilters()" onmouseenter="H(1)" onmouseleave="H(0)">Apply Filter</button>
      </div>
      <div class="sb-section">
        <div class="sb-title">Minimum Rating</div>
        <div id="rating-filters"></div>
      </div>
      <div class="sb-section">
        <div class="sb-title">Discount</div>
        <div id="discount-filters"></div>
      </div>
    </div>
    <div class="cat-products">
      <div class="prod-grid" id="grid-cat"></div>
    </div>
  </div>
</div>

<!-- ═══════════════════════════════
     PRODUCT DETAIL PAGE
═══════════════════════════════ -->
<div class="page" id="page-prod">
  <div class="pd-wrap" id="pd-inner"></div>
  <div class="fbt-sec" id="fbt-sec"></div>
  <div class="reviews-sec" id="reviews-sec"></div>
  <div class="related-sec" id="related-sec"></div>
  <footer style="max-width:1100px;margin:0 auto">
    <div class="footer-bottom" style="padding-top:16px">
      <div class="f-copy">© 2026 RareFinds. All rights reserved.</div>
    </div>
  </footer>
</div>

<!-- ═══════════════════════════════
     JAVASCRIPT
═══════════════════════════════ -->
<script>
'use strict';

// ──────────────────────────────────────────────
// DATA
// ──────────────────────────────────────────────
const CATS = [
  { id:'trending', icon:'🔥', name:'Trending Deals',            desc:'The hottest items flying off shelves right now',          c1:'#FF4500', c2:'#FF6B35' },
  { id:'new',      icon:'✨', name:'New Arrivals',               desc:'Fresh drops added today — be the first to discover',      c1:'#9B30FF', c2:'#C06CFF' },
  { id:'flash',    icon:'⚡', name:'Flash Sale',                 desc:'Limited-time deals at impossible prices',                 c1:'#E8FF00', c2:'#B8CC00' },
  { id:'toys',     icon:'🧸', name:'Toys & Hobbies',             desc:'Fun for every age — games, collectibles & crafts',        c1:'#FF4500', c2:'#FF8A3D' },
  { id:'home',     icon:'🌿', name:'Home & Garden',              desc:'Make your space extraordinary',                           c1:'#00C853', c2:'#00E676' },
  { id:'tools',    icon:'🔧', name:'Home Improvement & Tools',   desc:'Upgrade and fix everything around you',                   c1:'#FFC107', c2:'#FFD54F' },
  { id:'outdoors', icon:'⛺', name:'Outdoors',                   desc:'Adventure gear for every explorer',                       c1:'#00BCD4', c2:'#26C6DA' },
  { id:'sports',   icon:'🏋️', name:'Sports & Fitness',           desc:'Gear up and crush your goals',                            c1:'#FF4500', c2:'#FF2D78' },
  { id:'pets',     icon:'🐾', name:'Pets',                       desc:'Everything your furry family deserves',                   c1:'#9B30FF', c2:'#7C3AED' },
  { id:'electronics', icon:'📱', name:'Electronics & Gadgets',  desc:'Cutting-edge tech at shocking prices',                    c1:'#2979FF', c2:'#5C9FFF' },
  { id:'clothing', icon:'👗', name:'Clothing, Shoes & Jewelry',  desc:'Style that turns heads without breaking your bank',       c1:'#FF2D78', c2:'#FF79A8' },
  { id:'beauty',   icon:'💄', name:'Beauty & Personal Care',     desc:'Glow up with premium skincare and beauty',                c1:'#E91E63', c2:'#F06292' },
  { id:'auto',     icon:'🚗', name:'Automotive & Motorcycle',    desc:'Parts, accessories, and upgrades for every ride',         c1:'#546E7A', c2:'#78909C' },
  { id:'other',    icon:'🎲', name:'Other',                      desc:'Hidden gems that defy categorization',                    c1:'#9B30FF', c2:'#FF4500' },
];

// Image helper using Unsplash Source (no API key needed)
const IM  = (id, w=400, h=400) => `https://images.unsplash.com/photo-${id}?w=${w}&h=${h}&fit=crop&auto=format&q=80`;
const IML = (id)               => `https://images.unsplash.com/photo-${id}?w=700&h=700&fit=crop&auto=format&q=85`;

const PRODUCTS = [
  // Electronics
  { id:1,  cat:'electronics', name:'RGB Wireless Gaming Headset Pro',      price:34.99, old:89.99,  img:'1505740420928-5e560c06d30e', img2:'1583394838336-acd977736f90', rating:4.9, reviews:2341, sold:'12.4k', badge:'dis', desc:'Immersive 7.1 surround sound with crystal-clear mic. 20-hour battery. Foldable design. 16M-color RGB lighting that reacts to audio.', variants:{colors:['#1a1a2e','#FF4500','#9B30FF'],sizes:[]},            stock:5,  isNew:false },
  { id:2,  cat:'electronics', name:'30W Wireless Charging Pad Ultra-Fast', price:18.99, old:45.00,  img:'1586953208448-b95a79798f07', img2:'1558618666-fcd25c85cd64', rating:4.7, reviews:1879, sold:'8.1k',  badge:'dis', desc:'Charge any Qi-enabled device at blazing 30W speeds. Sleek aluminum finish. Compatible with iPhone, Samsung, AirPods, and more.',    variants:{colors:['#c0c0c0','#1a1a1a'],sizes:[]},               stock:12, isNew:false },
  { id:3,  cat:'electronics', name:'Portable Mini 4K HD Projector',        price:79.99, old:199.99, img:'1478147427282-58a87a433048', img2:'1580584126903-c17d41830450', rating:4.8, reviews:934,  sold:'3.2k',  badge:'hot', desc:'Turn any wall into a cinema. Native 1080p with 4K input support. Built-in speaker, 3-hour battery. HDMI, USB, and wireless.',          variants:{colors:['#ffffff','#1a1a1a'],sizes:[]},               stock:3,  isNew:false },
  { id:4,  cat:'electronics', name:'TWS Noise-Cancelling Earbuds',         price:29.99, old:89.00,  img:'1560343090-f0409e92791a',   img2:'1583394838336-acd977736f90', rating:4.6, reviews:3102, sold:'18.7k', badge:'dis', desc:'Active noise cancellation + 36-hour total battery life. Hi-Fi audio with deep bass. IPX5 waterproof. Instant pairing.',             variants:{colors:['#000000','#ffffff','#FF4500'],sizes:[]},      stock:20, isNew:true  },
  { id:5,  cat:'electronics', name:'Smart LED Desk Lamp + 4-Port USB Hub', price:22.99, old:55.00,  img:'1507003211169-0a1dd7228f2d', img2:'1513506003901-1e6a35d44fbb', rating:4.5, reviews:678,  sold:'2.4k',  badge:'new', desc:'5 color modes with adjustable brightness. 4-port USB hub built-in. Touch controls. Eye-care flicker-free technology for long sessions.', variants:{colors:['#ffffff','#1a1a1a'],sizes:[]},               stock:15, isNew:true  },
  // Home & Garden
  { id:6,  cat:'home',        name:'Linen Throw Pillow Set of 4',          price:22.99, old:55.00,  img:'1567016432779-094069958ea5', img2:'1555041469-a586c61ea9bc', rating:4.7, reviews:1233, sold:'5.6k',  badge:'dis', desc:'Premium linen-cotton blend covers. Machine washable. Hidden zipper. Perfect for sofas, beds, and cozy reading nooks.',             variants:{colors:['#e8d5b0','#9ca3af','#374151'],sizes:['45cm','50cm','60cm']}, stock:8,  isNew:false },
  { id:7,  cat:'home',        name:'Smart LED Plant Grow Light',           price:27.99, old:69.99,  img:'1416879595882-3373a0480b5b', img2:'1463936575829-25148e1db1b8', rating:4.8, reviews:891,  sold:'4.1k',  badge:'dis', desc:'Full-spectrum LED mimics natural sunlight. Auto on/off timer. Flexible gooseneck. For herbs, succulents, seedlings, and more.',     variants:{colors:['#1a1a1a'],sizes:['Small','Large']},          stock:9,  isNew:false },
  { id:8,  cat:'home',        name:'Japanese Ceramic Tea Set (7 pcs)',     price:36.99, old:88.00,  img:'1556909048-9f3b3b0e33f6',   img2:'1523920853576-e75c9cd22661', rating:4.9, reviews:567,  sold:'1.8k',  badge:'new', desc:'Hand-painted ceramic with 18k gold rim detail. Includes 1 teapot + 6 cups. Microwave and dishwasher safe. Arrives gift-boxed.',        variants:{colors:['#f5f0e8','#888888','#1a237e'],sizes:[]},     stock:14, isNew:true  },
  // Sports & Fitness
  { id:9,  cat:'sports',      name:'Adjustable Dumbbell Set 5–52.5 lbs',  price:89.99, old:220.00, img:'1571019613454-1cb2f99b2d8b', img2:'1534438327276-14e5300c3a48', rating:4.8, reviews:2890, sold:'7.3k',  badge:'hot', desc:'Replaces 15 sets of weights. Dial-select adjustment in seconds. Anti-slip grip. Compact storage tray included. Commercial quality.',  variants:{colors:[],sizes:['5–25 lbs','5–52.5 lbs']},          stock:6,  isNew:false },
  { id:10, cat:'sports',      name:'Ultralight Trail Running Vest 10L',    price:38.99, old:95.00,  img:'1552508744-1696d4464960',   img2:'1539185441755-769473a23570', rating:4.6, reviews:445,  sold:'1.2k',  badge:'new', desc:'2L hydration compatible. 10 pockets. Reflective strips for night safety. Adjustable fit system. Ventilated mesh back panel.',        variants:{colors:['#FF4500','#2979FF','#1a1a1a'],sizes:['XS','S','M','L','XL']}, stock:18, isNew:true  },
  { id:11, cat:'sports',      name:'Pro Resistance Band Set (11 pcs)',     price:19.99, old:48.00,  img:'1598289431512-b97b0917afdd', img2:'1571731956722-edce30001e1d', rating:4.7, reviews:3412, sold:'22.1k', badge:'dis', desc:'5 resistance levels + door anchor + handles + ankle straps + carry bag. Latex-free. 150 lbs max tension. Ideal for home gym.',     variants:{colors:[],sizes:[]},                                  stock:50, isNew:false },
  // Beauty
  { id:12, cat:'beauty',      name:'Hyaluronic Acid Serum Bundle (3 pcs)', price:24.99, old:65.00,  img:'1620916566398-39f1143ab7be', img2:'1556228578-8c89e6adf883', rating:4.8, reviews:4123, sold:'31.4k', badge:'hot', desc:'Clinical-strength 2% HA + Vitamin C + Niacinamide. Plumps, brightens, and minimizes pores. Dermatologist tested and approved.',    variants:{colors:[],sizes:['30ml','60ml']},                     stock:18, isNew:false },
  { id:13, cat:'beauty',      name:'Rose Quartz Gua Sha & Roller Set',     price:14.99, old:38.00,  img:'1576426863848-c21f53c60b19', img2:'1598440947400-2a5a22b86d90', rating:4.6, reviews:2876, sold:'15.2k', badge:'dis', desc:'Rose quartz stone + jade roller. Reduces puffiness, sculpts jawline, boosts circulation. Handcrafted. Velvet gift pouch included.',   variants:{colors:['#f9a8d4','#86efac','#c4b5fd'],sizes:[]},     stock:24, isNew:false },
  { id:14, cat:'beauty',      name:'7-Color LED Face Mask Light Therapy',  price:49.99, old:129.00, img:'1598440947400-2a5a22b86d90', img2:'1576426863848-c21f53c60b19', rating:4.7, reviews:1089, sold:'3.7k',  badge:'hot', desc:'Anti-aging, acne control, and skin rejuvenation. FDA cleared. 20-minute sessions. Rechargeable. Get professional salon results at home.', variants:{colors:['#ffffff'],sizes:[]},                        stock:7,  isNew:true  },
  // Clothing
  { id:15, cat:'clothing',    name:'Oversized Velvet Blazer Jacket',       price:42.99, old:110.00, img:'1594938298603-c8148c4b984f', img2:'1576566588028-4147f3842f27', rating:4.7, reviews:892,  sold:'4.1k',  badge:'dis', desc:'Luxurious crushed velvet fabric. Relaxed oversized silhouette. Fully lined interior. Perfect for evenings, events, or dressed-down layering.', variants:{colors:['#1a0a2e','#2d1b00','#0a1628'],sizes:['XS','S','M','L','XL','XXL']}, stock:6,  isNew:false },
  { id:16, cat:'clothing',    name:'Chunky Platform Sneakers (+5cm)',       price:54.99, old:135.00, img:'1491553895911-0055eca6402d', img2:'1542291026-7eec264c27ff', rating:4.5, reviews:1456, sold:'6.8k',  badge:'dis', desc:'Thick +5cm platform sole. Breathable mesh upper with suede overlay. Memory foam insole. Lace-up closure. Available in unisex sizing.',   variants:{colors:['#ffffff','#1a1a1a','#f5f0dc'],sizes:['US 5','US 6','US 7','US 8','US 9','US 10','US 11','US 12']}, stock:9,  isNew:false },
  // Pets
  { id:17, cat:'pets',        name:'GPS Pet Tracker + Activity Monitor',   price:44.99, old:109.99, img:'1587300003388-59208cc962cb', img2:'1518717758536-85ae29035b6d', rating:4.8, reviews:1678, sold:'8.9k',  badge:'hot', desc:'Real-time GPS tracking. Activity, sleep, and health monitoring. 7-day battery. Waterproof IPX7. Works globally. Fits cats and small dogs.', variants:{colors:['#FF4500','#2979FF','#f9a8d4'],sizes:['Small','Medium','Large']}, stock:10, isNew:false },
  { id:18, cat:'pets',        name:'Elevated Bamboo Dog Bowl Stand Set',   price:29.99, old:72.00,  img:'1596854372786-8be35a94b897', img2:'1587300003388-59208cc962cb', rating:4.6, reviews:934,  sold:'3.2k',  badge:'new', desc:'Natural bamboo stand with 2 premium stainless steel bowls. 3-level adjustable height. Non-slip feet. Promotes healthy posture during meals.',  variants:{colors:['#d4a853'],sizes:['Small','Medium','Large']}, stock:16, isNew:true  },
  // Toys
  { id:19, cat:'toys',        name:'Magnetic Marble Run Set (120 pcs)',    price:39.99, old:99.00,  img:'1558060370-d644479cb6f7',   img2:'1494586994-4a14e7a8ac77', rating:4.9, reviews:3421, sold:'14.6k', badge:'hot', desc:'120-piece magnetic marble run with endless configurations. Builds STEM skills. Glow-in-the-dark balls included. Ages 4 and up.',        variants:{colors:[],sizes:['60pc','120pc','200pc']},            stock:22, isNew:false },
  { id:20, cat:'toys',        name:'Double-Sided RC Stunt Car 360°',       price:27.99, old:69.99,  img:'1558060370-d644479cb6f7',   img2:'1494586994-4a14e7a8ac77', rating:4.7, reviews:2108, sold:'9.4k',  badge:'dis', desc:'360° flips and wall-climbing stunts. Runs on floors, walls, and ceilings. 25 MPH top speed. Rechargeable. 2 controllers. Ages 6+.',        variants:{colors:['#FF1744','#2979FF','#FF6B35'],sizes:[]},     stock:30, isNew:false },
  // Outdoors
  { id:21, cat:'outdoors',    name:'Ultralight 2-Person Hammock',          price:34.99, old:85.00,  img:'1465188035480-cf3a60bb4c0b', img2:'1501854140801-50d01698950b', rating:4.8, reviews:1567, sold:'5.4k',  badge:'dis', desc:'Holds 400 lbs. Sets up in under 60 seconds with triple-stitched seams. Total weight only 3.2 lbs. Includes carabiners and straps.',      variants:{colors:['#16a34a','#1d4ed8','#FF6B35'],sizes:[]},     stock:13, isNew:false },
  { id:22, cat:'outdoors',    name:'Insulated Tumbler 40oz Vacuum Steel',  price:19.99, old:49.99,  img:'1553361371-9b22f78e8b1d',   img2:'1571781926291-c477ebfd024b', rating:4.8, reviews:5632, sold:'42.1k', badge:'dis', desc:'Keeps drinks cold 24hr / hot 12hr. Triple-wall vacuum insulation. Splash-proof lid. Dishwasher safe. BPA-free. Fits all cup holders.',   variants:{colors:['#64748b','#1d4ed8','#f43f5e','#65a30d'],sizes:['20oz','32oz','40oz']}, stock:35, isNew:false },
  // Automotive
  { id:23, cat:'auto',        name:'Dual-Lens 4K Dash Cam WiFi + GPS',    price:54.99, old:139.99, img:'1449965408869-eaa3f722e40d', img2:'1486262715619-67b85e0b08d3', rating:4.7, reviews:1234, sold:'4.8k',  badge:'hot', desc:'4K front + 1080p rear camera. Built-in WiFi for easy phone transfer. GPS tracking with speed data. Advanced night vision mode.', variants:{colors:['#1a1a1a'],sizes:[]},                        stock:8,  isNew:false },
  // Tools
  { id:24, cat:'tools',       name:'21V Cordless Drill Driver Set (26pc)', price:64.99, old:159.99, img:'1530124566582-a618bc2615dc', img2:'1581244533361-d04ac0fa05e8', rating:4.8, reviews:2876, sold:'11.2k', badge:'dis', desc:'21V Li-ion battery. 2-speed gearbox (0–400 / 0–1500 RPM). 25 torque settings. Includes 25-piece bit set and 2 batteries.',         variants:{colors:['#FFD600','#FF1744'],sizes:[]},               stock:11, isNew:false },
  // Other
  { id:25, cat:'other',       name:'Levitating Moon Lamp with Stand',      price:49.99, old:119.99, img:'1507003211169-0a1dd7228f2d', img2:'1478147427282-58a87a433048', rating:4.8, reviews:2234, sold:'9.1k',  badge:'hot', desc:'Magnetic levitation + 360° rotation. Warm/cool LED color modes. Touch control. Wireless charging base. Stunning room centerpiece.', variants:{colors:['#fff'],sizes:['6 inch','8 inch']},           stock:11, isNew:true  },
];

// ──────────────────────────────────────────────
// STATE
// ──────────────────────────────────────────────
let cartCount = 0, wishCount = 0;
let currentCat = null, currentSort = 'pop';
let currentProd = null, qty = 1;
let filterMin = 0, filterMax = 9999, filterRating = 0, filterDiscount = 0;
const wishlisted = new Set();
let toastTimer = null;

// ──────────────────────────────────────────────
// CURSOR
// ──────────────────────────────────────────────
const curEl = document.getElementById('cur');
const curR  = document.getElementById('cur-r');
let mx = 0, my = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  curEl.style.left = mx + 'px';
  curEl.style.top  = my + 'px';
});

(function animCurRing() {
  rx += (mx - rx) * 0.13;
  ry += (my - ry) * 0.13;
  curR.style.left = rx + 'px';
  curR.style.top  = ry + 'px';
  requestAnimationFrame(animCurRing);
})();

function H(on) { document.body.classList.toggle('hov', !!on); }

// Auto-hover on interactive elements
document.addEventListener('mouseover', e => {
  const el = e.target.closest(
    'button, a, .prod-card, .cat-card, .car-card, .nav-btn, .cat-pill, ' +
    '.sort-btn, .filter-opt, .pd-thumb, .fbt-card, .rev-card, .soc-btn, .hf'
  );
  H(!!el);
});

// ──────────────────────────────────────────────
// TOAST
// ──────────────────────────────────────────────
function toast(icon, html) {
  document.getElementById('toast-icon').textContent = icon;
  document.getElementById('toast-msg').innerHTML = html;
  const t = document.getElementById('toast');
  t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => t.classList.remove('show'), 3200);
}

// ──────────────────────────────────────────────
// PAGE ROUTER
// ──────────────────────────────────────────────
function goPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  document.getElementById('sticky-atc').classList.remove('show');
  window.scrollTo({ top: 0, behavior: 'smooth' });
  setTimeout(initReveal, 120);
}

// ──────────────────────────────────────────────
// CART & WISH
// ──────────────────────────────────────────────
function addCart() {
  cartCount++;
  document.getElementById('cart-badge').textContent = cartCount;
}

function toggleWish(id, el) {
  if (wishlisted.has(id)) {
    wishlisted.delete(id);
    el.textContent = '🤍';
    el.classList.remove('on');
    wishCount = Math.max(0, wishCount - 1);
  } else {
    wishlisted.add(id);
    el.textContent = '❤️';
    el.classList.add('on');
    wishCount++;
    toast('❤️', 'Added to <strong>Wishlist!</strong>');
  }
  document.getElementById('wish-badge').textContent = wishCount;
}

// ──────────────────────────────────────────────
// CAT BAR
// ──────────────────────────────────────────────
function buildCatBar() {
  document.getElementById('cat-bar').innerHTML = CATS.map(c =>
    `<div class="cat-pill" data-id="${c.id}" onclick="openCat('${c.id}')" onmouseenter="H(1)" onmouseleave="H(0)">${c.icon} ${c.name}</div>`
  ).join('');
}

// ──────────────────────────────────────────────
// HELPERS
// ──────────────────────────────────────────────
function discPct(p) { return Math.round((1 - p.price / p.old) * 100); }

function starHTML(r) {
  return '★'.repeat(Math.floor(r)) + '☆'.repeat(5 - Math.floor(r));
}

// ──────────────────────────────────────────────
// PRODUCT CARD
// ──────────────────────────────────────────────
function prodCard(p) {
  const d = discPct(p);
  const cat = CATS.find(c => c.id === p.cat);
  const badge = p.badge === 'hot' ? `<div class="badge-hot">🔥 HOT</div>`
              : p.badge === 'new' ? `<div class="badge-new">✨ NEW</div>`
              :                     `<div class="badge-dis">-${d}%</div>`;
  const wOn  = wishlisted.has(p.id) ? 'on' : '';
  const wIco = wishlisted.has(p.id) ? '❤️' : '🤍';
  const safeName = p.name.replace(/'/g, "\\'").slice(0, 30);

  return `<div class="prod-card" onmouseenter="H(1)" onmouseleave="H(0)">
    <div class="pc-img">
      <img src="${IM(p.img)}" alt="${p.name}" loading="lazy">
      <div class="pc-img-alt"><img src="${IM(p.img2)}" alt="${p.name}" loading="lazy"></div>
      ${badge}
      <div class="pc-wish ${wOn}" id="pw${p.id}" onclick="event.stopPropagation();toggleWish(${p.id},this)">${wIco}</div>
      <div class="pc-qv" onclick="openProd(${p.id})">⚡ QUICK VIEW</div>
    </div>
    <div class="pc-body">
      <div class="pc-cat-label">${cat?.icon || ''} ${cat?.name || p.cat}</div>
      <div class="pc-name">${p.name}</div>
      <div class="pc-stars">
        <div class="stars">${starHTML(p.rating)}</div>
        <div class="review-count">${p.rating} (${p.reviews.toLocaleString()})</div>
      </div>
      <div class="pc-price">
        <span class="price-now">$${p.price.toFixed(2)}</span>
        <span class="price-old">$${p.old.toFixed(2)}</span>
      </div>
      <button class="pc-atc"
        onclick="event.stopPropagation();addCart();this.textContent='✓ Added!';this.classList.add('done');setTimeout(()=>{this.textContent='Add to Cart';this.classList.remove('done')},2000);toast('🛒','<strong>${safeName}…</strong> added to cart!')"
        onmouseenter="H(1)" onmouseleave="H(0)">Add to Cart</button>
    </div>
  </div>`;
}

// ──────────────────────────────────────────────
// HOME PAGE BUILD
// ──────────────────────────────────────────────
function buildHome() {
  // Hero floating cards
  const heroProds = [PRODUCTS[0], PRODUCTS[11], PRODUCTS[14], PRODUCTS[18]];
  document.getElementById('hero-floats').innerHTML = heroProds.map((p, i) => {
    const styles = [
      'top:20px;left:78px',
      'top:58px;left:252px',
      'top:225px;left:36px',
      'top:245px;left:236px',
    ];
    return `<div class="hf" onclick="openProd(${p.id})" style="${styles[i]}">
      <img src="${IM(p.img, 300, 160)}" alt="${p.name}">
      <div class="hf-info">
        <div class="hf-name">${p.name}</div>
        <span class="hf-price">$${p.price}</span><span class="hf-old">$${p.old}</span>
      </div>
    </div>`;
  }).join('');

  // Flash sale — sorted by highest discount
  const flash = [...PRODUCTS].sort((a, b) => discPct(b) - discPct(a)).slice(0, 8);
  document.getElementById('grid-flash').innerHTML = flash.map(prodCard).join('');

  // Category grid (exclude meta cats)
  const mainCats = CATS.filter(c => !['trending','new','flash'].includes(c.id));
  document.getElementById('cats-home').innerHTML = mainCats.map(c => `
    <div class="cat-card" onclick="openCat('${c.id}')" style="--cc1:${c.c1};--cc2:${c.c2}" onmouseenter="H(1)" onmouseleave="H(0)">
      <span class="cc-icon">${c.icon}</span>
      <div class="cc-name">${c.name}</div>
      <div class="cc-count">${Math.floor(Math.random() * 20 + 5)}K+ items</div>
    </div>`
  ).join('');

  // Trending carousel (shuffle)
  const shuffled = [...PRODUCTS].sort(() => Math.random() - 0.5);
  const carHTML = shuffled.map(p => `
    <div class="car-card" onclick="openProd(${p.id})" onmouseenter="H(1)" onmouseleave="H(0)">
      <div class="car-img"><img src="${IM(p.img)}" alt="${p.name}" loading="lazy"></div>
      <div class="car-info">
        <div class="car-name">${p.name}</div>
        <div class="car-price">$${p.price.toFixed(2)}
          <span style="font-size:.71rem;color:var(--text3);text-decoration:line-through;font-weight:400;margin-left:5px">$${p.old.toFixed(2)}</span>
        </div>
      </div>
    </div>`
  ).join('');
  document.getElementById('carousel-trending').innerHTML = carHTML + carHTML; // doubled for infinite loop

  // New arrivals
  const newProds = PRODUCTS.filter(p => p.isNew);
  const fillNew  = [...newProds, ...PRODUCTS.filter(p => !p.isNew)].slice(0, 8);
  document.getElementById('grid-new').innerHTML = fillNew.map(prodCard).join('');

  // For you (random)
  const forYou = [...PRODUCTS].sort(() => Math.random() - 0.5).slice(0, 8);
  document.getElementById('grid-foryou').innerHTML = forYou.map(prodCard).join('');
}

// ──────────────────────────────────────────────
// CATEGORY PAGE
// ──────────────────────────────────────────────
function getCatProds(id) {
  if (id === 'trending') return [...PRODUCTS].sort((a, b) => b.reviews - a.reviews);
  if (id === 'new')      return PRODUCTS.filter(p => p.isNew);
  if (id === 'flash')    return [...PRODUCTS].sort((a, b) => discPct(b) - discPct(a));
  return PRODUCTS.filter(p => p.cat === id);
}

function openCat(id) {
  currentCat = id;
  filterRating = 0;
  filterDiscount = 0;
  document.querySelectorAll('.cat-pill').forEach(p => p.classList.toggle('active', p.dataset.id === id));

  const cat = CATS.find(c => c.id === id);
  document.getElementById('cph-icon').textContent  = cat.icon;
  document.getElementById('cph-name').textContent  = cat.name;
  document.getElementById('cph-desc').textContent  = cat.desc;
  document.getElementById('f-min').value = 0;
  document.getElementById('f-max').value = 500;

  const prods = getCatProds(id);
  document.getElementById('cph-count').textContent = `${prods.length} products`;

  // Build filter panels
  document.getElementById('rating-filters').innerHTML = [5, 4, 3].map(r =>
    `<div class="filter-opt" onclick="filterRating=${r};applyFilters()" onmouseenter="H(1)" onmouseleave="H(0)">
      <div class="f-check"></div>
      <span>${starHTML(r)} & up</span>
    </div>`
  ).join('');

  document.getElementById('discount-filters').innerHTML = [50, 30, 10].map(d =>
    `<div class="filter-opt" onclick="filterDiscount=${d};applyFilters()" onmouseenter="H(1)" onmouseleave="H(0)">
      <div class="f-check"></div>
      <span>${d}%+ off</span>
    </div>`
  ).join('');

  renderCatGrid(prods);
  goPage('cat');
}

function applyFilters() {
  filterMin = parseFloat(document.getElementById('f-min').value) || 0;
  filterMax = parseFloat(document.getElementById('f-max').value) || 9999;

  let ps = getCatProds(currentCat).filter(p => p.price >= filterMin && p.price <= filterMax);
  if (filterRating   > 0) ps = ps.filter(p => p.rating >= filterRating);
  if (filterDiscount > 0) ps = ps.filter(p => discPct(p) >= filterDiscount);

  renderCatGrid(sortProds(ps, currentSort));
}

function setSort(el, s) {
  document.querySelectorAll('.sort-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  currentSort = s;
  applyFilters();
}

function sortProds(arr, s) {
  const a = [...arr];
  if (s === 'pa')  return a.sort((x, y) => x.price - y.price);
  if (s === 'pd')  return a.sort((x, y) => y.price - x.price);
  if (s === 'rat') return a.sort((x, y) => y.rating - x.rating);
  if (s === 'new') return a.sort((x, y) => y.isNew - x.isNew);
  return a.sort((x, y) => y.reviews - x.reviews); // 'pop'
}

function renderCatGrid(ps) {
  const g = document.getElementById('grid-cat');
  if (!ps.length) {
    g.innerHTML = `<div style="grid-column:1/-1;text-align:center;padding:60px 24px;color:var(--text3);font-size:1rem">
      😔 No products match your filters.<br><br>
      <button class="btn-outline" onclick="filterRating=0;filterDiscount=0;applyFilters()" onmouseenter="H(1)" onmouseleave="H(0)" style="margin-top:12px">Clear Filters</button>
    </div>`;
    return;
  }
  g.innerHTML = sortProds(ps, currentSort).map(prodCard).join('');
}

// ──────────────────────────────────────────────
// PRODUCT DETAIL PAGE
// ──────────────────────────────────────────────
function openProd(id) {
  currentProd = PRODUCTS.find(p => p.id === id);
  const p   = currentProd;
  qty = 1;
  closeModal();

  const d    = discPct(p);
  const cat  = CATS.find(c => c.id === p.cat);
  const imgs = [p.img, p.img2, p.img, p.img2];

  document.getElementById('pd-inner').innerHTML = `
    <div>
      <div class="pd-main-img">
        <img src="${IML(p.img)}" alt="${p.name}" id="pd-main-img">
      </div>
      <div class="pd-thumbs">
        ${imgs.map((im, i) => `
          <div class="pd-thumb ${i === 0 ? 'active' : ''}" onclick="switchImg('${im}', this)">
            <img src="${IM(im, 120, 120)}" alt="">
          </div>`).join('')}
      </div>
    </div>
    <div>
      <div class="pd-cat-label">${cat?.icon} ${cat?.name}</div>
      <div class="pd-title">${p.name}</div>
      <div class="pd-rating-row">
        <div class="stars" style="font-size:.9rem">${starHTML(p.rating)}</div>
        <span style="font-size:.85rem;color:var(--text2)">${p.rating} · ${p.reviews.toLocaleString()} reviews</span>
        <span class="pd-sold">${p.sold} sold</span>
      </div>
      <div class="pd-price-block">
        <div class="pd-price-row">
          <div class="pd-price-main">$${p.price.toFixed(2)}</div>
          <div class="pd-price-old">$${p.old.toFixed(2)}</div>
          <div class="pd-price-save">-${d}% OFF</div>
        </div>
        <div style="color:var(--success);font-size:.82rem;font-weight:700">You save $${(p.old - p.price).toFixed(2)}</div>
        <div class="pd-timer">
          <span style="color:var(--fire);font-weight:700">⚡ Deal ends in:</span>
          <div class="cd-block" id="pd-h">01</div>
          <div class="cd-sep">:</div>
          <div class="cd-block" id="pd-m">23</div>
          <div class="cd-sep">:</div>
          <div class="cd-block" id="pd-s">44</div>
        </div>
      </div>
      <div class="stock-alert">⚠️ Only ${p.stock} left in stock — order soon!</div>
      <div class="stock-bar-wrap">
        <div class="sb-labels"><span>Stock level</span><span style="color:var(--danger)">${p.stock} remaining</span></div>
        <div class="sb-track"><div class="sb-fill" style="width:${Math.min(100, (p.stock / 50) * 100)}%"></div></div>
      </div>
      ${p.variants.colors.length ? `
        <div class="pd-variants">
          <div class="pv-label">Color</div>
          <div class="pv-opts">
            ${p.variants.colors.map((c, i) => `
              <div class="pv-color ${i === 0 ? 'sel' : ''}" style="background:${c}"
                onclick="document.querySelectorAll('.pv-color').forEach(e=>e.classList.remove('sel'));this.classList.add('sel')"></div>`).join('')}
          </div>
        </div>` : ''}
      ${p.variants.sizes.length ? `
        <div class="pd-variants">
          <div class="pv-label">Size</div>
          <div class="pv-opts">
            ${p.variants.sizes.map((s, i) => `
              <div class="pv-opt ${i === 0 ? 'sel' : ''}"
                onclick="document.querySelectorAll('.pv-opt').forEach(e=>e.classList.remove('sel'));this.classList.add('sel')">${s}</div>`).join('')}
          </div>
        </div>` : ''}
      <div class="pd-qty">
        <span class="qty-label">Quantity:</span>
        <div class="qty-ctrl">
          <button class="qty-btn" onclick="updateQty(-1)" onmouseenter="H(1)" onmouseleave="H(0)">−</button>
          <div class="qty-num" id="qty-display">1</div>
          <button class="qty-btn" onclick="updateQty(1)" onmouseenter="H(1)" onmouseleave="H(0)">+</button>
        </div>
      </div>
      <div class="pd-ctas">
        <button class="btn-add-cart" onclick="addCart();toast('🛒','<strong>${p.name.slice(0,26).replace(/'/g,"\\'")}…</strong> added to cart!')" onmouseenter="H(1)" onmouseleave="H(0)">🛒 Add to Cart</button>
        <button class="btn-buy-now" onclick="addCart();toast('⚡','Redirecting to checkout…')" onmouseenter="H(1)" onmouseleave="H(0)">⚡ Buy Now</button>
        <button class="btn-wish-lg" onclick="toggleWish(${p.id}, this)" onmouseenter="H(1)" onmouseleave="H(0)">${wishlisted.has(p.id) ? '❤️' : '🤍'}</button>
      </div>
      <div class="trust-grid">
        <div class="trust-item"><span class="trust-ico">🔒</span>Secure Checkout</div>
        <div class="trust-item"><span class="trust-ico">🚚</span>Free Shipping +$25</div>
        <div class="trust-item"><span class="trust-ico">↩️</span>30-Day Easy Returns</div>
        <div class="trust-item"><span class="trust-ico">🛡️</span>Buyer Protection</div>
      </div>
      <div class="pd-desc">${p.desc}</div>
    </div>`;

  // Sticky ATC setup
  document.getElementById('satc-name').textContent  = p.name;
  document.getElementById('satc-price').textContent = '$' + p.price.toFixed(2);

  // Frequently Bought Together
  const fbtProds = PRODUCTS.filter(pp => pp.id !== p.id).slice(0, 3);
  const fbtTotal = (p.price + fbtProds.reduce((s, pp) => s + pp.price, 0)).toFixed(2);
  document.getElementById('fbt-sec').innerHTML = `
    <div class="eyebrow" style="margin-bottom:10px">Bundle Deal</div>
    <div class="sec-title" style="font-size:1.4rem;margin-bottom:20px">Frequently Bought Together</div>
    <div class="fbt-items">
      ${[p, ...fbtProds].map((pp, i) => `
        ${i ? '<div class="fbt-plus">+</div>' : ''}
        <div class="fbt-card" onclick="openProd(${pp.id})" onmouseenter="H(1)" onmouseleave="H(0)">
          <img src="${IM(pp.img, 200, 100)}" alt="${pp.name}">
          <div class="fbt-info">
            <div class="fbt-name">${pp.name}</div>
            <div class="fbt-price">$${pp.price.toFixed(2)}</div>
          </div>
        </div>`).join('')}
    </div>
    <div class="fbt-total">
      <div>Bundle total: <span class="fbt-total-price">$<span>${fbtTotal}</span></span></div>
      <button class="btn-fire" onclick="addCart();addCart();addCart();addCart();toast('🛒','Bundle added! Great savings on all 4 items!')" onmouseenter="H(1)" onmouseleave="H(0)">Add All to Cart</button>
    </div>`;

  // Reviews
  const reviewers = [
    { n:'Alex M.',  a:'AM', c:'#FF4500' },
    { n:'Sarah K.', a:'SK', c:'#9B30FF' },
    { n:'James R.', a:'JR', c:'#2979FF' },
    { n:'Priya N.', a:'PN', c:'#E91E63' },
  ];
  const revTexts = [
    'Absolutely incredible quality for the price. Shipped faster than expected and packaging was superb. Already ordered two more for family members!',
    'This completely exceeded my expectations. Looks exactly like the photos and feels genuinely premium in hand. Highly recommend to everyone.',
    'Good product overall. Took a few extra days to arrive but the quality more than makes up for it. Very happy with this purchase.',
    '5 stars — no question about it. Been using it daily for 3 months with zero issues. Outstanding value for money, will buy again.',
  ];
  document.getElementById('reviews-sec').innerHTML = `
    <div class="eyebrow" style="margin-bottom:10px">Customer Feedback</div>
    <div class="sec-title" style="font-size:1.4rem;margin-bottom:22px">Reviews & Ratings</div>
    <div class="review-sum">
      <div class="rs-big">
        <div class="rs-num">${p.rating}</div>
        <div class="rs-stars">${starHTML(p.rating)}</div>
        <div class="rs-cnt">${p.reviews.toLocaleString()} reviews</div>
      </div>
      <div class="rs-bars">
        ${[5,4,3,2,1].map(s => {
          const w = [60, 25, 10, 3, 2][5 - s];
          return `<div class="rsb-row">
            <span>${s}★</span>
            <div class="rsb-track"><div class="rsb-fill" style="width:${w}%"></div></div>
            <span>${w}%</span>
          </div>`;
        }).join('')}
      </div>
    </div>
    <div class="review-cards">
      ${reviewers.map((r, i) => `
        <div class="rev-card">
          <div class="rev-top">
            <div class="rev-av" style="background:linear-gradient(135deg,${r.c},${r.c}88)">${r.a}</div>
            <div>
              <div class="rev-name">${r.n}</div>
              <div class="rev-date">Verified Purchase · ${['2 days ago','1 week ago','3 weeks ago','1 month ago'][i]}</div>
            </div>
            <div class="stars" style="margin-left:auto;font-size:.9rem">${starHTML(i === 2 ? 4 : 5)}</div>
          </div>
          <div class="rev-body">${revTexts[i]}</div>
          ${i < 2 ? `<div class="rev-imgs">
            <div class="rev-img"><img src="${IM(p.img)}" alt="Review photo"></div>
            <div class="rev-img"><img src="${IM(p.img2)}" alt="Review photo"></div>
          </div>` : ''}
        </div>`).join('')}
    </div>`;

  // You May Also Like (same category, then fill)
  const sameCat = PRODUCTS.filter(pp => pp.cat === p.cat && pp.id !== p.id);
  const filled  = [...sameCat, ...PRODUCTS.filter(pp => pp.id !== p.id)].slice(0, 4);
  document.getElementById('related-sec').innerHTML = `
    <div class="eyebrow" style="margin-bottom:10px">More Like This</div>
    <div class="sec-title" style="font-size:1.4rem;margin-bottom:24px">You May Also Like</div>
    <div class="prod-grid">${filled.map(prodCard).join('')}</div>`;

  goPage('prod');

  // Sticky ATC on scroll
  setTimeout(() => {
    const ctasEl = document.querySelector('.pd-ctas');
    if (!ctasEl) return;
    const observer = new IntersectionObserver(([entry]) => {
      document.getElementById('sticky-atc').classList.toggle('show', !entry.isIntersecting);
    }, { threshold: 0 });
    observer.observe(ctasEl);
  }, 400);
}

function switchImg(imgId, el) {
  document.getElementById('pd-main-img').src = IML(imgId);
  document.querySelectorAll('.pd-thumb').forEach(t => t.classList.remove('active'));
  el.classList.add('active');
}

function updateQty(delta) {
  qty = Math.max(1, Math.min(99, qty + delta));
  document.getElementById('qty-display').textContent = qty;
}

// ──────────────────────────────────────────────
// MODAL (QUICK VIEW)
// ──────────────────────────────────────────────
function openModal(p) {
  document.getElementById('modal-inner').innerHTML = `
    <div style="padding:28px;background:var(--surface)">
      <div style="height:320px;border-radius:var(--rad);overflow:hidden;background:var(--ink3)">
        <img src="${IML(p.img)}" style="width:100%;height:100%;object-fit:cover" alt="${p.name}">
      </div>
    </div>
    <div style="padding:28px;overflow-y:auto">
      <div style="font-size:.7rem;font-weight:700;color:var(--fire);text-transform:uppercase;letter-spacing:.9px;margin-bottom:8px">${CATS.find(c => c.id === p.cat)?.name}</div>
      <div style="font-family:'Syne',sans-serif;font-size:1.25rem;font-weight:700;margin-bottom:10px;line-height:1.3">${p.name}</div>
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">
        <span style="color:var(--warn)">${starHTML(p.rating)}</span>
        <span style="font-size:.8rem;color:var(--text2)">${p.reviews.toLocaleString()} reviews</span>
      </div>
      <div style="font-family:'Syne',sans-serif;font-size:1.8rem;font-weight:800;color:var(--fire);margin-bottom:5px">$${p.price.toFixed(2)}</div>
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">
        <span style="text-decoration:line-through;color:var(--text3)">$${p.old.toFixed(2)}</span>
        <span style="background:rgba(0,230,118,.1);color:var(--success);font-size:.78rem;font-weight:700;border-radius:6px;padding:2px 8px">Save $${(p.old - p.price).toFixed(2)}</span>
      </div>
      <div style="font-size:.85rem;color:var(--text2);line-height:1.72;margin-bottom:22px">${p.desc}</div>
      <div style="display:flex;gap:10px">
        <button class="btn-fire" style="flex:1" onclick="closeModal();openProd(${p.id})" onmouseenter="H(1)" onmouseleave="H(0)">View Full Details</button>
        <button class="btn-outline" onclick="addCart();toast('🛒','Added to cart!');closeModal()" onmouseenter="H(1)" onmouseleave="H(0)">🛒 Add to Cart</button>
      </div>
    </div>`;
  document.getElementById('modal-bg').classList.add('open');
}

function closeModal() { document.getElementById('modal-bg').classList.remove('open'); }
function modalBgClick(e) { if (e.target === e.currentTarget) closeModal(); }

// ──────────────────────────────────────────────
// COUNTDOWN TIMERS
// ──────────────────────────────────────────────
let flashSecs = 9753, prodSecs = 5178;

setInterval(() => {
  // Flash sale countdown
  flashSecs--;
  if (flashSecs < 0) flashSecs = 9999;
  const fh = Math.floor(flashSecs / 3600);
  const fm = Math.floor((flashSecs % 3600) / 60);
  const fs = flashSecs % 60;
  const fhEl = document.getElementById('fcd-h');
  if (fhEl) {
    fhEl.textContent                                  = String(fh).padStart(2, '0');
    document.getElementById('fcd-m').textContent     = String(fm).padStart(2, '0');
    document.getElementById('fcd-s').textContent     = String(fs).padStart(2, '0');
  }

  // Product page countdown
  prodSecs--;
  if (prodSecs < 0) prodSecs = 3600;
  const ph = Math.floor(prodSecs / 3600);
  const pm = Math.floor((prodSecs % 3600) / 60);
  const ps = prodSecs % 60;
  const phEl = document.getElementById('pd-h');
  if (phEl) {
    phEl.textContent                              = String(ph).padStart(2, '0');
    document.getElementById('pd-m').textContent  = String(pm).padStart(2, '0');
    document.getElementById('pd-s').textContent  = String(ps).padStart(2, '0');
  }
}, 1000);

// ──────────────────────────────────────────────
// SEARCH
// ──────────────────────────────────────────────
function searchHandler(e) {
  const q = e.target.value.trim().toLowerCase();
  if (q.length < 2 || e.key !== 'Enter') return;

  const results = PRODUCTS.filter(p =>
    p.name.toLowerCase().includes(q) ||
    p.cat.toLowerCase().includes(q) ||
    p.desc.toLowerCase().includes(q)
  );

  document.querySelectorAll('.cat-pill').forEach(p => p.classList.remove('active'));
  document.getElementById('cph-icon').textContent  = '🔍';
  document.getElementById('cph-name').textContent  = `Search: "${e.target.value}"`;
  document.getElementById('cph-desc').textContent  = 'Products matching your search query';
  document.getElementById('cph-count').textContent = `${results.length} result${results.length !== 1 ? 's' : ''} found`;

  if (results.length) {
    document.getElementById('grid-cat').innerHTML = results.map(prodCard).join('');
  } else {
    document.getElementById('grid-cat').innerHTML = `
      <div style="grid-column:1/-1;text-align:center;padding:60px 24px;color:var(--text3)">
        😔 No results found for "<strong style="color:var(--text2)">${e.target.value}</strong>".<br>
        <span style="font-size:.875rem;margin-top:8px;display:block">Try a different keyword or browse our categories.</span>
      </div>`;
  }

  // Hide sidebar for search
  document.querySelector('.cat-sidebar').style.display = 'none';
  goPage('cat');
}

// ──────────────────────────────────────────────
// SCROLL REVEAL
// ──────────────────────────────────────────────
function initReveal() {
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('in');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.07 });

  document.querySelectorAll('.reveal:not(.in)').forEach(el => observer.observe(el));
}

// ──────────────────────────────────────────────
// KEYBOARD SHORTCUTS
// ──────────────────────────────────────────────
document.addEventListener('keydown', e => {
  if (e.key === 'Escape') closeModal();
  if (e.key === '/' && document.activeElement.tagName !== 'INPUT') {
    e.preventDefault();
    document.getElementById('search-input').focus();
  }
});

// ──────────────────────────────────────────────
// INIT
// ──────────────────────────────────────────────
buildCatBar();
buildHome();
initReveal();
</script>
</body>
</html>
