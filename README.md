<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>S\u00daB Z\u00c9R\u00d6 \u2014 Web Designer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
  <style>
    :root {
      --neon: #00f0ff;
      --neon2: #0066ff;
      --neon3: #7b2fff;
      --dark: #020610;
      --dark2: #060d1f;
      --white: #e8f4ff;
      --grey: #3a4a6b;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; }

    body {
      background: var(--dark);
      color: var(--white);
      font-family: 'Space Mono', 'Courier New', Courier, monospace;
      cursor: none;
      overflow-x: hidden;
    }

    /* CURSOR */
    .cursor {
      position: fixed; width: 12px; height: 12px;
      background: var(--neon); border-radius: 50%;
      pointer-events: none; z-index: 9999;
      transform: translate(-50%, -50%);
      transition: width 0.2s, height 0.2s;
      box-shadow: 0 0 12px var(--neon), 0 0 24px var(--neon);
    }
    .cursor-ring {
      position: fixed; width: 36px; height: 36px;
      border: 1.5px solid var(--neon); border-radius: 50%;
      pointer-events: none; z-index: 9998;
      transform: translate(-50%, -50%);
      transition: width 0.3s, height 0.3s, opacity 0.3s;
      opacity: 0.5;
    }

    /* SCANLINES */
    body::before {
      content: ''; position: fixed; inset: 0;
      background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,240,255,0.015) 2px, rgba(0,240,255,0.015) 4px);
      pointer-events: none; z-index: 1000;
    }

    /* NAV */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 500;
      display: flex; justify-content: space-between; align-items: center;
      padding: 1.4rem 3rem;
      background: linear-gradient(180deg, rgba(2,6,16,0.98) 0%, transparent 100%);
      border-bottom: 1px solid rgba(0,240,255,0.08);
    }
    .nav-logo {
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: 1.6rem; letter-spacing: 0.15em;
      color: var(--neon); text-shadow: 0 0 20px var(--neon);
      text-decoration: none; cursor: none;
    }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      color: var(--white); text-decoration: none;
      font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
      position: relative; transition: color 0.3s; cursor: none;
    }
    .nav-links a::after {
      content: ''; position: absolute; bottom: -4px; left: 0;
      width: 0; height: 1px; background: var(--neon);
      box-shadow: 0 0 8px var(--neon); transition: width 0.3s;
    }
    .nav-links a:hover, .nav-links a.active { color: var(--neon); }
    .nav-links a:hover::after, .nav-links a.active::after { width: 100%; }

    /* PAGE SYSTEM */
    .page { display: none; }
    .page.active { display: block; }

    /* ANIMATIONS */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes spin {
      from { transform: translateY(-50%) rotate(0deg); }
      to   { transform: translateY(-50%) rotate(360deg); }
    }
    @keyframes scrollPulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.3; }
    }
    @keyframes marquee {
      from { transform: translateX(0); }
      to   { transform: translateX(-50%); }
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; box-shadow: 0 0 8px #00ff64; }
      50% { opacity: 0.5; box-shadow: 0 0 3px #00ff64; }
    }
    .anim { opacity: 0; animation: fadeUp 0.7s forwards; }

    /* ===================== HOME PAGE ===================== */
    .hero {
      min-height: 100vh; display: flex; flex-direction: column;
      justify-content: center; padding: 0 3rem;
      position: relative; overflow: hidden;
    }
    .hero-bg {
      position: absolute; inset: 0;
      background:
        radial-gradient(ellipse 60% 60% at 70% 50%, rgba(0,102,255,0.12) 0%, transparent 70%),
        radial-gradient(ellipse 40% 40% at 20% 80%, rgba(123,47,255,0.1) 0%, transparent 70%),
        radial-gradient(ellipse 30% 30% at 80% 20%, rgba(0,240,255,0.07) 0%, transparent 70%);
    }
    .hero-grid {
      position: absolute; inset: 0;
      background-image:
        linear-gradient(rgba(0,240,255,0.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,240,255,0.04) 1px, transparent 1px);
      background-size: 60px 60px;
      -webkit-mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 0%, transparent 100%);
      mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 0%, transparent 100%);
    }
    .hero-eyebrow {
      font-size: 0.65rem; letter-spacing: 0.4em;
      color: var(--neon); text-transform: uppercase; margin-bottom: 1.2rem;
      opacity: 0; animation: fadeUp 0.8s 0.3s forwards;
    }
    .hero-name {
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: clamp(5rem, 14vw, 13rem);
      line-height: 0.9; letter-spacing: 0.02em;
      opacity: 0; animation: fadeUp 0.8s 0.5s forwards;
    }
    .hero-name .line1 { display: block; color: var(--white); }
    .hero-name .line2 {
      display: block; color: transparent;
      -webkit-text-stroke: 2px var(--neon);
      filter: drop-shadow(0 0 20px var(--neon));
    }
    .hero-tagline {
      margin-top: 2rem; font-size: 0.75rem; letter-spacing: 0.15em;
      color: var(--grey); max-width: 420px; line-height: 1.8;
      opacity: 0; animation: fadeUp 0.8s 0.7s forwards;
    }
    .hero-tagline span { color: var(--neon); }
    .hero-cta {
      margin-top: 3rem; display: flex; gap: 1.2rem; flex-wrap: wrap;
      opacity: 0; animation: fadeUp 0.8s 0.9s forwards;
    }
    .btn {
      display: inline-block; padding: 0.85rem 2rem;
      font-family: 'Space Mono', 'Courier New', Courier, monospace;
      font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
      text-decoration: none; transition: all 0.3s; cursor: none; border: none;
    }
    .btn-primary {
      background: var(--neon); color: var(--dark); font-weight: 700;
      clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
      -webkit-clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
    }
    .btn-primary:hover {
      background: white;
      box-shadow: 0 0 30px var(--neon), 0 0 60px rgba(0,240,255,0.3);
      transform: translateY(-2px);
    }
    .btn-outline {
      border: 1px solid var(--neon); color: var(--neon);
      clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
      -webkit-clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
    }
    .btn-outline:hover {
      background: rgba(0,240,255,0.08);
      box-shadow: 0 0 20px rgba(0,240,255,0.2);
      transform: translateY(-2px);
    }
    .hero-badge {
      position: absolute; right: 5%; top: 50%; transform: translateY(-50%);
      width: 160px; height: 160px;
      border: 1px solid rgba(0,240,255,0.2); border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      text-align: center; font-size: 0.55rem; letter-spacing: 0.15em;
      text-transform: uppercase; color: var(--neon);
      animation: spin 20s linear infinite, fadeUp 1s 1.1s both;
    }
    .hero-badge::before {
      content: ''; position: absolute; inset: -8px;
      border: 1px dashed rgba(0,240,255,0.15); border-radius: 50%;
      animation: spin 8s linear infinite reverse;
    }
    .hero-badge-inner {
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: 1rem; display: block; margin-bottom: 4px;
    }
    .scroll-hint {
      position: absolute; bottom: 2.5rem; left: 50%; transform: translateX(-50%);
      display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
      font-size: 0.55rem; letter-spacing: 0.25em; color: var(--grey);
      text-transform: uppercase; animation: fadeUp 1s 1.3s both;
    }
    .scroll-line {
      width: 1px; height: 50px;
      background: linear-gradient(var(--neon), transparent);
      animation: scrollPulse 2s ease-in-out infinite;
    }
    .stats-bar {
      background: var(--dark2);
      border-top: 1px solid rgba(0,240,255,0.08);
      border-bottom: 1px solid rgba(0,240,255,0.08);
      padding: 1.5rem 3rem; display: flex; gap: 4rem;
      justify-content: center; flex-wrap: wrap;
    }
    .stat { text-align: center; }
    .stat-num {
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: 2.5rem; color: var(--neon); letter-spacing: 0.05em;
      line-height: 1; text-shadow: 0 0 20px rgba(0,240,255,0.5);
    }
    .stat-label { font-size: 0.55rem; letter-spacing: 0.2em; color: var(--grey); text-transform: uppercase; margin-top: 0.3rem; }
    .marquee-section { padding: 2rem 0; overflow: hidden; border-bottom: 1px solid rgba(0,240,255,0.06); }
    .marquee-track { display: flex; gap: 3rem; animation: marquee 18s linear infinite; white-space: nowrap; }
    .marquee-item {
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: 1.4rem; letter-spacing: 0.15em;
      color: transparent; -webkit-text-stroke: 1px rgba(0,240,255,0.25); flex-shrink: 0;
    }
    .marquee-item.accent { color: var(--neon); -webkit-text-stroke: none; }

    /* ===================== ABOUT PAGE ===================== */
    .page-header {
      padding: 14rem 3rem 5rem; position: relative; overflow: hidden;
    }
    .page-header-bg { position: absolute; inset: 0; }
    .bg-blue { background: radial-gradient(ellipse 50% 80% at 10% 50%, rgba(0,102,255,0.1) 0%, transparent 70%); }
    .bg-purple { background: radial-gradient(ellipse 50% 80% at 90% 50%, rgba(123,47,255,0.1) 0%, transparent 70%); }
    .bg-center { background: radial-gradient(ellipse 60% 80% at 50% 80%, rgba(0,102,255,0.08) 0%, transparent 70%); }
    .page-label { font-size: 0.6rem; letter-spacing: 0.4em; color: var(--neon); text-transform: uppercase; margin-bottom: 1rem; opacity: 0; animation: fadeUp 0.7s 0.2s forwards; }
    .page-title {
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: clamp(4rem, 10vw, 8rem); line-height: 0.9;
      opacity: 0; animation: fadeUp 0.7s 0.4s forwards;
    }
    .page-title span { color: transparent; -webkit-text-stroke: 2px var(--neon); filter: drop-shadow(0 0 15px var(--neon)); }
    .page-sub { margin-top: 1.5rem; font-size: 0.75rem; color: var(--grey); line-height: 1.8; max-width: 500px; opacity: 0; animation: fadeUp 0.7s 0.6s forwards; }
    .page-sub a { color: var(--neon); text-decoration: none; }

    .about-section {
      padding: 5rem 3rem; display: grid;
      grid-template-columns: 1fr 1fr; gap: 6rem; align-items: start;
    }
    .about-photo-box {
      position: relative; width: 100%; aspect-ratio: 3/4;
      background: var(--dark2); border: 1px solid rgba(0,240,255,0.15);
      overflow: hidden;
      clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px));
      -webkit-clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px));
    }
    .about-photo-placeholder {
      width: 100%; height: 100%; display: flex; flex-direction: column;
      align-items: center; justify-content: center; gap: 1rem;
      background: linear-gradient(135deg, var(--dark2), #0a1535);
    }
    .about-photo-icon { font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif; font-size: 6rem; color: rgba(0,240,255,0.15); line-height: 1; }
    .about-photo-label { font-size: 0.55rem; letter-spacing: 0.3em; color: var(--grey); text-transform: uppercase; }
    .photo-corner { position: absolute; width: 30px; height: 30px; border-color: var(--neon); border-style: solid; opacity: 0.6; }
    .photo-corner.tl { top: 8px; left: 8px; border-width: 2px 0 0 2px; }
    .photo-corner.br { bottom: 8px; right: 8px; border-width: 0 2px 2px 0; }
    .about-intro {
      font-size: 1.05rem; line-height: 1.8; color: var(--white); margin-bottom: 2rem;
      font-style: italic; border-left: 2px solid var(--neon); padding-left: 1.5rem;
      opacity: 0; animation: fadeUp 0.7s 0.6s forwards;
    }
    .about-body { font-size: 0.75rem; line-height: 2; color: #8aa0c8; margin-bottom: 3rem; opacity: 0; animation: fadeUp 0.7s 0.8s forwards; }
    .about-body span { color: var(--neon); }
    .skills-title { font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif; font-size: 1.2rem; letter-spacing: 0.15em; color: var(--white); margin-bottom: 1.5rem; opacity: 0; animation: fadeUp 0.7s 1s forwards; }
    .skill-bars { display: flex; flex-direction: column; gap: 1rem; opacity: 0; animation: fadeUp 0.7s 1.1s forwards; }
    .skill-top { display: flex; justify-content: space-between; font-size: 0.6rem; letter-spacing: 0.15em; text-transform: uppercase; margin-bottom: 0.4rem; color: var(--white); }
    .skill-pct { color: var(--neon); }
    .skill-track { height: 3px; background: rgba(0,240,255,0.1); position: relative; clip-path: polygon(4px 0%, 100% 0%, calc(100% - 4px) 100%, 0% 100%); -webkit-clip-path: polygon(4px 0%, 100% 0%, calc(100% - 4px) 100%, 0% 100%); }
    .skill-fill { height: 100%; background: linear-gradient(90deg, var(--neon2), var(--neon)); box-shadow: 0 0 10px var(--neon); width: 0%; transition: width 1.5s cubic-bezier(0.16, 1, 0.3, 1); }

    .services-section { padding: 5rem 3rem; border-top: 1px solid rgba(0,240,255,0.08); }
    .section-label { font-size: 0.6rem; letter-spacing: 0.4em; color: var(--neon); text-transform: uppercase; margin-bottom: 3rem; }
    .services-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; }
    .service-card {
      padding: 2rem; border: 1px solid rgba(0,240,255,0.1);
      background: var(--dark2);
      clip-path: polygon(0 0, calc(100% - 16px) 0, 100% 16px, 100% 100%, 16px 100%, 0 calc(100% - 16px));
      -webkit-clip-path: polygon(0 0, calc(100% - 16px) 0, 100% 16px, 100% 100%, 16px 100%, 0 calc(100% - 16px));
      transition: border-color 0.3s, background 0.3s;
      opacity: 0; animation: fadeUp 0.6s forwards;
    }
    .service-card:nth-child(1) { animation-delay: 0.2s; }
    .service-card:nth-child(2) { animation-delay: 0.35s; }
    .service-card:nth-child(3) { animation-delay: 0.5s; }
    .service-card:hover { border-color: rgba(0,240,255,0.4); background: rgba(0,240,255,0.04); }
    .service-num { font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif; font-size: 3.5rem; color: rgba(0,240,255,0.1); line-height: 1; margin-bottom: 1rem; }
    .service-name { font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif; font-size: 1.3rem; letter-spacing: 0.1em; color: var(--white); margin-bottom: 0.8rem; }
    .service-desc { font-size: 0.65rem; line-height: 1.9; color: var(--grey); }

    /* ===================== PROJECTS PAGE ===================== */
    .filter-bar { padding: 0 3rem 3rem; display: flex; gap: 1rem; flex-wrap: wrap; opacity: 0; animation: fadeUp 0.7s 0.6s forwards; }
    .filter-btn {
      padding: 0.5rem 1.2rem;
      font-family: 'Space Mono', 'Courier New', Courier, monospace;
      font-size: 0.6rem; letter-spacing: 0.15em; text-transform: uppercase;
      background: transparent; border: 1px solid var(--grey); color: var(--grey);
      cursor: none; transition: all 0.3s;
      clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
      -webkit-clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
    }
    .filter-btn:hover, .filter-btn.active { border-color: var(--neon); color: var(--neon); background: rgba(0,240,255,0.05); }
    .projects-section { padding: 0 3rem 6rem; }
    .projects-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 2rem; }
    .project-card {
      position: relative; overflow: hidden;
      border: 1px solid rgba(0,240,255,0.1); background: var(--dark2);
      clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px));
      -webkit-clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px));
      transition: border-color 0.4s, transform 0.4s;
      opacity: 0; animation: fadeUp 0.6s forwards;
    }
    .project-card:nth-child(1) { animation-delay: 0.1s; }
    .project-card:nth-child(2) { animation-delay: 0.2s; }
    .project-card:nth-child(3) { animation-delay: 0.3s; }
    .project-card:nth-child(4) { animation-delay: 0.4s; }
    .project-card:nth-child(5) { animation-delay: 0.5s; }
    .project-card:nth-child(6) { animation-delay: 0.6s; }
    .project-card:hover { border-color: rgba(0,240,255,0.4); transform: translateY(-4px); }
    .project-card.featured { grid-column: span 2; }
    .project-thumb { width: 100%; aspect-ratio: 16/9; background: var(--dark); position: relative; overflow: hidden; display: flex; align-items: center; justify-content: center; }
    .project-card.featured .project-thumb { aspect-ratio: 21/9; }
    .project-thumb-bg {
      position: absolute; inset: 0; display: flex; align-items: center; justify-content: center;
      font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif;
      font-size: 8rem; letter-spacing: 0.1em; transition: transform 0.5s;
    }
    .project-card:hover .project-thumb-bg { transform: scale(1.08); }
    .thumb-1 { background: linear-gradient(135deg, #020a20, #051040); }
    .thumb-1 .project-thumb-bg { color: rgba(0,240,255,0.08); }
    .thumb-2 { background: linear-gradient(135deg, #0a0520, #1a0540); }
    .thumb-2 .project-thumb-bg { color: rgba(123,47,255,0.1); }
    .thumb-3 { background: linear-gradient(135deg, #040a10, #0a1a30); }
    .thumb-3 .project-thumb-bg { color: rgba(0,102,255,0.1); }
    .thumb-4 { background: linear-gradient(135deg, #10050a, #200515); }
    .thumb-4 .project-thumb-bg { color: rgba(255,30,100,0.08); }
    .thumb-5 { background: linear-gradient(135deg, #041510, #082a1a); }
    .thumb-5 .project-thumb-bg { color: rgba(0,255,150,0.06); }
    .thumb-6 { background: linear-gradient(135deg, #080520, #150a35); }
    .thumb-6 .project-thumb-bg { color: rgba(200,100,255,0.08); }
    .thumb-dots { position: absolute; inset: 0; background-image: radial-gradient(circle, rgba(0,240,255,0.12) 1px, transparent 1px); background-size: 24px 24px; }
    .project-overlay { position: absolute; inset: 0; background: rgba(2,6,16,0.8); display: flex; align-items: center; justify-content: center; opacity: 0; transition: opacity 0.3s; }
    .project-card:hover .project-overlay { opacity: 1; }
    .overlay-btn {
      padding: 0.7rem 1.5rem; font-family: 'Space Mono', 'Courier New', Courier, monospace;
      font-size: 0.6rem; letter-spacing: 0.2em; text-transform: uppercase;
      border: 1px solid var(--neon); color: var(--neon); background: transparent; cursor: none;
      clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
      -webkit-clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
      transition: background 0.3s;
    }
    .overlay-btn:hover { background: rgba(0,240,255,0.1); }
    .project-info { padding: 1.5rem; }
    .project-tags { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-bottom: 0.8rem; }
    .project-tag { font-size: 0.5rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--neon); border: 1px solid rgba(0,240,255,0.2); padding: 0.2rem 0.6rem; }
    .project-name { font-family: 'Bebas Neue', Impact, 'Arial Black', sans-serif; font-size: 1.6rem; letter-spacing: 0.08em; color: var(--white); margin-bottom: 0.5rem; transition: color 0.3s; }
    .project-card:hover .project-name { color: var(--neon); }
    .project-desc { font-size: 0.65rem; line-height: 1.8; color: var(--grey); }

    /* ===================== CONTACT PAGE 
