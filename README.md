<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Elenco Nacional del Folklore de Bolivia</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Montserrat:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --rojo: #C0392B;
    --oro: #D4A017;
    --oro-claro: #F0C040;
    --negro: #0A0A0A;
    --crema: #FAF5E9;
    --marron: #3D1A0A;
    --gris-oscuro: #1A1A1A;
    --gris-medio: #2E2E2E;
    --texto-claro: #EDE8DE;
    --acento: #8B0000;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Montserrat', sans-serif;
    background: var(--negro);
    color: var(--texto-claro);
    overflow-x: hidden;
  }

  /* ─── LOADER ─── */
  #loader {
    position: fixed; inset: 0; z-index: 9999;
    background: var(--negro);
    display: flex; align-items: center; justify-content: center;
    flex-direction: column; gap: 20px;
    transition: opacity 0.8s ease, visibility 0.8s ease;
  }
  #loader.hide { opacity: 0; visibility: hidden; }
  .loader-text {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    letter-spacing: 0.3em;
    color: var(--oro);
    text-transform: uppercase;
    animation: pulse 1.5s ease-in-out infinite;
  }
  .loader-line {
    width: 0; height: 2px;
    background: linear-gradient(90deg, var(--rojo), var(--oro));
    animation: loadLine 1.8s ease forwards;
  }
  @keyframes loadLine { to { width: 200px; } }
  @keyframes pulse { 0%,100%{opacity:.4} 50%{opacity:1} }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; width: 100%; z-index: 1000;
    padding: 18px 60px;
    display: flex; align-items: center; justify-content: space-between;
    background: linear-gradient(180deg, rgba(0,0,0,0.95) 0%, transparent 100%);
    transition: background 0.4s;
  }
  nav.scrolled {
    background: rgba(0,0,0,0.97);
    border-bottom: 1px solid rgba(212,160,23,0.2);
  }
  .nav-logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    font-weight: 700;
    color: var(--oro);
    text-transform: uppercase;
    letter-spacing: 0.15em;
    line-height: 1.2;
  }
  .nav-logo span { display: block; font-size: 0.65rem; color: var(--texto-claro); letter-spacing: 0.4em; font-weight: 300; font-family: 'Montserrat', sans-serif; margin-top: 2px; }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    text-decoration: none; color: var(--texto-claro);
    font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
    font-weight: 500; transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: ''; position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px; background: var(--oro);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--oro); }
  .nav-links a:hover::after { width: 100%; }
  .nav-btn {
    background: transparent; border: 1px solid var(--oro);
    color: var(--oro); padding: 9px 24px;
    font-size: 0.68rem; letter-spacing: 0.2em; text-transform: uppercase;
    cursor: pointer; font-family: 'Montserrat', sans-serif;
    font-weight: 600; transition: all 0.3s;
  }
  .nav-btn:hover { background: var(--oro); color: var(--negro); }

  /* ─── HERO ─── */
  .hero {
    height: 100vh; position: relative;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse at 20% 50%, rgba(192,57,43,0.25) 0%, transparent 60%),
      radial-gradient(ellipse at 80% 30%, rgba(212,160,23,0.15) 0%, transparent 50%),
      linear-gradient(180deg, #0A0A0A 0%, #1A0A05 50%, #0A0A0A 100%);
  }
  .hero-pattern {
    position: absolute; inset: 0; opacity: 0.04;
    background-image:
      repeating-linear-gradient(45deg, var(--oro) 0, var(--oro) 1px, transparent 0, transparent 50%);
    background-size: 30px 30px;
  }
  .hero-decor-left, .hero-decor-right {
    position: absolute; top: 50%; transform: translateY(-50%);
    width: 3px; height: 55vh;
    background: linear-gradient(180deg, transparent, var(--oro), transparent);
    opacity: 0.5;
  }
  .hero-decor-left { left: 60px; }
  .hero-decor-right { right: 60px; }

  .hero-content {
    position: relative; z-index: 2;
    text-align: center; max-width: 900px; padding: 0 40px;
  }
  .hero-eyebrow {
    font-size: 0.65rem; letter-spacing: 0.55em; text-transform: uppercase;
    color: var(--oro); font-weight: 500;
    margin-bottom: 24px;
    opacity: 0; animation: fadeUp 0.8s ease 0.5s forwards;
  }
  .hero-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 7vw, 6.5rem);
    font-weight: 900; line-height: 0.95;
    text-transform: uppercase; letter-spacing: -0.02em;
    color: var(--crema);
    opacity: 0; animation: fadeUp 0.8s ease 0.7s forwards;
  }
  .hero-title .gold { color: var(--oro); display: block; }
  .hero-title .italic-line {
    font-style: italic; font-weight: 400;
    font-size: 0.55em; letter-spacing: 0.1em;
    color: rgba(237,232,222,0.7); display: block; margin-top: 8px;
  }
  .hero-divider {
    width: 80px; height: 2px; margin: 32px auto;
    background: linear-gradient(90deg, transparent, var(--oro), var(--rojo), transparent);
    opacity: 0; animation: fadeUp 0.8s ease 0.9s forwards;
  }
  .hero-subtitle {
    font-size: 0.9rem; line-height: 1.9; letter-spacing: 0.05em;
    color: rgba(237,232,222,0.65); max-width: 600px; margin: 0 auto 44px;
    font-weight: 300;
    opacity: 0; animation: fadeUp 0.8s ease 1.1s forwards;
  }
  .hero-ctas {
    display: flex; gap: 20px; justify-content: center; flex-wrap: wrap;
    opacity: 0; animation: fadeUp 0.8s ease 1.3s forwards;
  }
  .btn-primary {
    background: var(--rojo); color: #fff;
    padding: 16px 44px; border: none; cursor: pointer;
    font-family: 'Montserrat', sans-serif;
    font-size: 0.72rem; letter-spacing: 0.25em; text-transform: uppercase;
    font-weight: 700; transition: all 0.3s;
    text-decoration: none; display: inline-block;
  }
  .btn-primary:hover { background: #a93226; transform: translateY(-2px); box-shadow: 0 8px 30px rgba(192,57,43,0.4); }
  .btn-outline {
    background: transparent; color: var(--texto-claro);
    padding: 15px 44px; border: 1px solid rgba(237,232,222,0.4);
    cursor: pointer; font-family: 'Montserrat', sans-serif;
    font-size: 0.72rem; letter-spacing: 0.25em; text-transform: uppercase;
    font-weight: 500; transition: all 0.3s;
    text-decoration: none; display: inline-block;
  }
  .btn-outline:hover { border-color: var(--oro); color: var(--oro); }

  .hero-scroll {
    position: absolute; bottom: 36px; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    opacity: 0; animation: fadeIn 1s ease 2s forwards;
  }
  .hero-scroll span { font-size: 0.55rem; letter-spacing: 0.4em; text-transform: uppercase; color: rgba(237,232,222,0.4); }
  .scroll-line { width: 1px; height: 50px; background: linear-gradient(180deg, var(--oro), transparent); animation: scrollAnim 2s ease infinite; }
  @keyframes scrollAnim { 0%{opacity:1;transform:scaleY(1)} 100%{opacity:0;transform:scaleY(0) translateY(20px)} }

  @keyframes fadeUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }
  @keyframes fadeIn { from{opacity:0} to{opacity:1} }

  /* ─── STATS BAND ─── */
  .stats-band {
    background: var(--marron);
    border-top: 1px solid rgba(212,160,23,0.3);
    border-bottom: 1px solid rgba(212,160,23,0.3);
    padding: 40px 60px;
    display: flex; justify-content: center; gap: 80px; flex-wrap: wrap;
  }
  .stat-item { text-align: center; }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2.8rem; font-weight: 900; color: var(--oro);
    line-height: 1;
  }
  .stat-label { font-size: 0.62rem; letter-spacing: 0.3em; text-transform: uppercase; color: rgba(237,232,222,0.5); margin-top: 8px; }

  /* ─── SECCIONES GENERALES ─── */
  section { padding: 100px 60px; }

  .section-eyebrow {
    font-size: 0.62rem; letter-spacing: 0.5em; text-transform: uppercase;
    color: var(--oro); font-weight: 500; margin-bottom: 16px;
  }
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.2rem, 4vw, 3.5rem);
    font-weight: 700; line-height: 1.1; color: var(--crema);
    margin-bottom: 24px;
  }
  .section-title em { font-style: italic; color: var(--oro); }
  .section-body {
    font-size: 0.95rem; line-height: 2; color: rgba(237,232,222,0.65);
    font-weight: 300; max-width: 600px;
  }

  /* ─── NOSOTROS ─── */
  .nosotros {
    background: var(--gris-oscuro);
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center;
  }
  .nosotros-visual {
    position: relative; height: 520px;
  }
  .visual-block-main {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #2D0A00 0%, #1A0500 100%);
    border: 1px solid rgba(212,160,23,0.2);
    overflow: hidden;
  }
  .visual-block-main::before {
    content: ''; position: absolute; inset: 0;
    background:
      radial-gradient(ellipse at 50% 50%, rgba(212,160,23,0.12) 0%, transparent 70%),
      url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23D4A017' fill-opacity='0.04'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
  }
  .visual-wiphala {
    position: absolute; right: -20px; bottom: -20px;
    width: 180px; height: 180px;
    display: grid; grid-template-columns: repeat(7,1fr); grid-template-rows: repeat(7,1fr);
    opacity: 0.25; transform: rotate(45deg);
  }
  .visual-wiphala div { }
  .visual-centerpiece {
    position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%);
    text-align: center;
  }
  .visual-centerpiece .big-letter {
    font-family: 'Playfair Display', serif;
    font-size: 11rem; font-weight: 900;
    color: rgba(212,160,23,0.08); line-height: 1;
    user-select: none;
  }
  .visual-tag {
    position: absolute; bottom: 30px; left: 30px;
    border-left: 3px solid var(--oro); padding-left: 16px;
  }
  .visual-tag p { font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase; color: rgba(237,232,222,0.5); }
  .visual-tag strong { font-family: 'Playfair Display', serif; font-size: 1.1rem; color: var(--crema); }

  .nosotros-content { }
  .nosotros-content .section-body { margin-bottom: 32px; }
  .features-list { list-style: none; display: flex; flex-direction: column; gap: 16px; margin-top: 32px; }
  .features-list li {
    display: flex; align-items: flex-start; gap: 14px;
    font-size: 0.85rem; color: rgba(237,232,222,0.6); line-height: 1.6;
  }
  .feat-icon { width: 28px; height: 28px; flex-shrink: 0; display: flex; align-items: center; justify-content: center; background: rgba(212,160,23,0.1); color: var(--oro); font-size: 0.9rem; }

  /* ─── ESPECTÁCULOS ─── */
  .espectaculos { background: var(--negro); }
  .espectaculos-header { text-align: center; margin-bottom: 64px; }
  .espectaculos-header .section-body { margin: 0 auto; }
  .shows-grid {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 2px;
    max-width: 1200px; margin: 0 auto;
  }
  .show-card {
    position: relative; overflow: hidden;
    aspect-ratio: 3/4; cursor: pointer;
    background: var(--gris-medio);
  }
  .show-card-bg {
    position: absolute; inset: 0;
    transition: transform 0.6s ease;
  }
  .show-card:hover .show-card-bg { transform: scale(1.07); }
  .show-card-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(0deg, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.1) 60%);
    transition: background 0.4s;
  }
  .show-card:hover .show-card-overlay { background: linear-gradient(0deg, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.4) 100%); }
  .show-card-info {
    position: absolute; bottom: 0; left: 0; right: 0;
    padding: 30px 28px; transform: translateY(10px); transition: transform 0.4s;
  }
  .show-card:hover .show-card-info { transform: translateY(0); }
  .show-region {
    font-size: 0.58rem; letter-spacing: 0.45em; text-transform: uppercase;
    color: var(--oro); margin-bottom: 8px;
  }
  .show-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem; font-weight: 700; color: var(--crema);
    line-height: 1.2; margin-bottom: 12px;
  }
  .show-desc {
    font-size: 0.78rem; color: rgba(237,232,222,0.55); line-height: 1.7;
    max-height: 0; overflow: hidden; transition: max-height 0.4s ease;
  }
  .show-card:hover .show-desc { max-height: 100px; }
  .show-num {
    position: absolute; top: 24px; right: 24px;
    font-family: 'Playfair Display', serif;
    font-size: 3rem; font-weight: 900; color: rgba(212,160,23,0.15); line-height: 1;
  }

  /* COLORES de las tarjetas de espectáculos */
  .sc-1 .show-card-bg { background: linear-gradient(135deg, #4A0000 0%, #1A0000 100%); }
  .sc-2 .show-card-bg { background: linear-gradient(135deg, #1A0A3D 0%, #0A0020 100%); }
  .sc-3 .show-card-bg { background: linear-gradient(135deg, #003020 0%, #001510 100%); }
  .sc-4 .show-card-bg { background: linear-gradient(135deg, #3D2000 0%, #1A0E00 100%); }
  .sc-5 .show-card-bg { background: linear-gradient(135deg, #300040 0%, #150020 100%); }
  .sc-6 .show-card-bg { background: linear-gradient(135deg, #001A3D 0%, #000A20 100%); }

  .sc-1 .show-card-bg::before,
  .sc-2 .show-card-bg::before,
  .sc-3 .show-card-bg::before,
  .sc-4 .show-card-bg::before,
  .sc-5 .show-card-bg::before,
  .sc-6 .show-card-bg::before {
    content: ''; position: absolute; inset: 0;
    opacity: 0.18;
    background-size: 40px 40px;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='40' height='40'%3E%3Cpath d='M20 2L38 20L20 38L2 20Z' fill='none' stroke='%23D4A017' stroke-width='0.5'/%3E%3C/svg%3E");
  }

  /* ─── GIRA / FUNCIONES ─── */
  .gira { background: var(--marron); }
  .gira-inner { max-width: 1000px; margin: 0 auto; }
  .gira-header { display: flex; justify-content: space-between; align-items: flex-end; margin-bottom: 48px; flex-wrap: wrap; gap: 24px; }
  .eventos-lista { display: flex; flex-direction: column; gap: 0; }
  .evento-item {
    display: grid; grid-template-columns: 90px 1fr auto;
    align-items: center; gap: 40px; padding: 28px 0;
    border-bottom: 1px solid rgba(212,160,23,0.12);
    transition: background 0.3s; cursor: pointer;
  }
  .evento-item:first-child { border-top: 1px solid rgba(212,160,23,0.12); }
  .evento-item:hover { background: rgba(212,160,23,0.04); padding-left: 16px; padding-right: 16px; margin: 0 -16px; }
  .evento-fecha { text-align: center; }
  .fecha-dia { font-family: 'Playfair Display', serif; font-size: 2.2rem; font-weight: 900; color: var(--oro); line-height: 1; }
  .fecha-mes { font-size: 0.6rem; letter-spacing: 0.35em; text-transform: uppercase; color: rgba(237,232,222,0.4); margin-top: 4px; }
  .evento-info { }
  .evento-nombre { font-family: 'Playfair Display', serif; font-size: 1.15rem; color: var(--crema); margin-bottom: 4px; }
  .evento-lugar { font-size: 0.75rem; color: rgba(237,232,222,0.45); letter-spacing: 0.05em; }
  .evento-ciudad { font-size: 0.65rem; text-transform: uppercase; letter-spacing: 0.2em; color: var(--oro); margin-top: 2px; }
  .evento-btn {
    background: transparent; border: 1px solid rgba(212,160,23,0.35);
    color: var(--oro); padding: 10px 24px; cursor: pointer;
    font-family: 'Montserrat', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    font-weight: 600; transition: all 0.3s; white-space: nowrap;
  }
  .evento-btn:hover { background: var(--oro); color: var(--negro); }

  /* ─── CITA DESTACADA ─── */
  .quote-section {
    background: linear-gradient(135deg, var(--acento) 0%, #500000 100%);
    text-align: center; padding: 100px 60px;
    position: relative; overflow: hidden;
  }
  .quote-section::before {
    content: '"'; position: absolute;
    font-family: 'Playfair Display', serif;
    font-size: 30rem; font-weight: 900;
    color: rgba(0,0,0,0.15); line-height: 1;
    top: -60px; left: 40px; pointer-events: none;
  }
  .quote-text {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(1.5rem, 3vw, 2.5rem);
    font-style: italic; font-weight: 300;
    color: var(--crema); max-width: 800px; margin: 0 auto 28px;
    line-height: 1.5; position: relative; z-index: 1;
  }
  .quote-author { font-size: 0.68rem; letter-spacing: 0.4em; text-transform: uppercase; color: rgba(237,232,222,0.5); }

  /* ─── GALERÍA ─── */
  .galeria { background: var(--negro); }
  .galeria-header { text-align: center; margin-bottom: 56px; }
  .galeria-grid {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: repeat(2, 240px);
    gap: 3px; max-width: 1400px; margin: 0 auto;
  }
  .galeria-item {
    overflow: hidden; position: relative; cursor: pointer;
    background: var(--gris-medio);
  }
  .galeria-item:nth-child(1) { grid-column: span 5; }
  .galeria-item:nth-child(2) { grid-column: span 3; }
  .galeria-item:nth-child(3) { grid-column: span 4; }
  .galeria-item:nth-child(4) { grid-column: span 4; }
  .galeria-item:nth-child(5) { grid-column: span 3; }
  .galeria-item:nth-child(6) { grid-column: span 5; }
  .galeria-inner {
    width: 100%; height: 100%;
    transition: transform 0.6s ease;
  }
  .galeria-item:hover .galeria-inner { transform: scale(1.08); }
  .galeria-overlay {
    position: absolute; inset: 0;
    background: rgba(0,0,0,0); transition: background 0.4s;
    display: flex; align-items: center; justify-content: center;
  }
  .galeria-item:hover .galeria-overlay { background: rgba(192,57,43,0.3); }
  .galeria-plus { font-size: 2rem; color: white; opacity: 0; transition: opacity 0.3s; }
  .galeria-item:hover .galeria-plus { opacity: 1; }

  /* COLORES galería */
  .gi-1 .galeria-inner { background: linear-gradient(135deg, #3D0000 30%, #1A0000); }
  .gi-2 .galeria-inner { background: linear-gradient(135deg, #001A3D 30%, #000A1A); }
  .gi-3 .galeria-inner { background: linear-gradient(135deg, #1A3D00 30%, #0A1A00); }
  .gi-4 .galeria-inner { background: linear-gradient(135deg, #3D1A00 30%, #1A0A00); }
  .gi-5 .galeria-inner { background: linear-gradient(135deg, #2D003D 30%, #15001A); }
  .gi-6 .galeria-inner { background: linear-gradient(135deg, #003D2D 30%, #001A15); }

  .galeria-label {
    position: absolute; bottom: 20px; left: 20px;
    font-size: 0.62rem; letter-spacing: 0.35em; text-transform: uppercase;
    color: rgba(212,160,23,0.7); font-weight: 500;
  }

  /* ─── EQUIPO ─── */
  .equipo { background: var(--gris-oscuro); }
  .equipo-header { text-align: center; margin-bottom: 64px; }
  .equipo-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 40px; max-width: 1100px; margin: 0 auto; }
  .persona-card { text-align: center; }
  .persona-foto {
    width: 100%; aspect-ratio: 3/4; margin-bottom: 20px;
    position: relative; overflow: hidden;
  }
  .persona-foto-inner {
    width: 100%; height: 100%;
    transition: transform 0.5s ease;
  }
  .persona-card:hover .persona-foto-inner { transform: scale(1.05); }
  .persona-foto-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(0deg, rgba(0,0,0,0.6) 0%, transparent 50%);
  }
  .p1 .persona-foto-inner { background: linear-gradient(170deg, #3D0000, #1A0000); }
  .p2 .persona-foto-inner { background: linear-gradient(170deg, #1A0A3D, #0A001A); }
  .p3 .persona-foto-inner { background: linear-gradient(170deg, #003020, #001510); }
  .p4 .persona-foto-inner { background: linear-gradient(170deg, #3D2000, #1A0E00); }
  .persona-foto-inner::after {
    content: ''; position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%);
    font-family: 'Playfair Display', serif;
    font-size: 5rem; font-weight: 900; color: rgba(212,160,23,0.15);
  }
  .p1 .persona-foto-inner::after { content: '♦'; }
  .p2 .persona-foto-inner::after { content: '◈'; }
  .p3 .persona-foto-inner::after { content: '⬡'; }
  .p4 .persona-foto-inner::after { content: '✦'; }
  .persona-rol { font-size: 0.58rem; letter-spacing: 0.4em; text-transform: uppercase; color: var(--oro); margin-bottom: 6px; }
  .persona-nombre { font-family: 'Playfair Display', serif; font-size: 1.1rem; color: var(--crema); margin-bottom: 8px; }
  .persona-bio { font-size: 0.78rem; color: rgba(237,232,222,0.45); line-height: 1.6; }

  /* ─── HISTORIA TIMELINE ─── */
  .historia { background: var(--negro); }
  .historia-inner { max-width: 800px; margin: 0 auto; }
  .historia-header { text-align: center; margin-bottom: 64px; }
  .timeline { position: relative; padding-left: 40px; }
  .timeline::before { content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 1px; background: linear-gradient(180deg, var(--oro), transparent); }
  .tl-item { position: relative; padding-bottom: 48px; }
  .tl-dot {
    position: absolute; left: -46px; top: 4px;
    width: 12px; height: 12px;
    border: 1px solid var(--oro); background: var(--negro);
    transform: rotate(45deg);
  }
  .tl-year { font-family: 'Playfair Display', serif; font-size: 1.5rem; font-weight: 700; color: var(--oro); margin-bottom: 8px; }
  .tl-title { font-size: 1rem; font-weight: 600; color: var(--crema); margin-bottom: 8px; }
  .tl-body { font-size: 0.85rem; color: rgba(237,232,222,0.5); line-height: 1.8; }

  /* ─── CONTACTO ─── */
  .contacto {
    background: var(--gris-oscuro);
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: start;
  }
  .contacto-info .section-body { margin-bottom: 40px; }
  .contact-items { display: flex; flex-direction: column; gap: 24px; }
  .contact-item { display: flex; gap: 16px; align-items: flex-start; }
  .contact-icon { width: 36px; height: 36px; border: 1px solid rgba(212,160,23,0.3); display: flex; align-items: center; justify-content: center; color: var(--oro); font-size: 0.9rem; flex-shrink: 0; }
  .contact-item-label { font-size: 0.6rem; letter-spacing: 0.3em; text-transform: uppercase; color: rgba(237,232,222,0.35); margin-bottom: 4px; }
  .contact-item-val { font-size: 0.9rem; color: var(--crema); }
  .social-links { display: flex; gap: 12px; margin-top: 40px; }
  .social-link {
    width: 40px; height: 40px; border: 1px solid rgba(212,160,23,0.25);
    display: flex; align-items: center; justify-content: center;
    color: rgba(237,232,222,0.5); font-size: 0.8rem; font-weight: 700;
    transition: all 0.3s; text-decoration: none; font-family: 'Montserrat', sans-serif;
  }
  .social-link:hover { border-color: var(--oro); color: var(--oro); }

  .contacto-form { }
  .form-group { margin-bottom: 24px; }
  .form-group label { display: block; font-size: 0.62rem; letter-spacing: 0.3em; text-transform: uppercase; color: rgba(237,232,222,0.4); margin-bottom: 8px; }
  .form-group input, .form-group textarea, .form-group select {
    width: 100%; background: rgba(255,255,255,0.04);
    border: 1px solid rgba(212,160,23,0.2);
    color: var(--crema); padding: 14px 16px;
    font-family: 'Montserrat', sans-serif; font-size: 0.85rem;
    transition: border-color 0.3s; outline: none;
  }
  .form-group input:focus, .form-group textarea:focus, .form-group select:focus { border-color: var(--oro); }
  .form-group textarea { height: 120px; resize: vertical; }
  .form-group select { appearance: none; cursor: pointer; }
  .form-group select option { background: var(--negro); }

  /* ─── FOOTER ─── */
  footer {
    background: var(--negro);
    border-top: 1px solid rgba(212,160,23,0.15);
    padding: 60px 60px 36px;
  }
  .footer-top {
    display: grid; grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 60px; margin-bottom: 60px;
  }
  .footer-brand-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem; font-weight: 700; color: var(--oro);
    text-transform: uppercase; letter-spacing: 0.1em; margin-bottom: 4px;
  }
  .footer-brand-sub { font-size: 0.6rem; letter-spacing: 0.35em; text-transform: uppercase; color: rgba(237,232,222,0.3); margin-bottom: 20px; }
  .footer-brand-text { font-size: 0.8rem; color: rgba(237,232,222,0.4); line-height: 1.8; max-width: 280px; }
  .footer-col-title { font-size: 0.62rem; letter-spacing: 0.35em; text-transform: uppercase; color: var(--oro); margin-bottom: 20px; font-weight: 600; }
  .footer-links { list-style: none; display: flex; flex-direction: column; gap: 10px; }
  .footer-links a { text-decoration: none; font-size: 0.8rem; color: rgba(237,232,222,0.4); transition: color 0.3s; }
  .footer-links a:hover { color: var(--crema); }
  .footer-bottom {
    border-top: 1px solid rgba(237,232,222,0.06);
    padding-top: 28px;
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 16px;
  }
  .footer-copy { font-size: 0.7rem; color: rgba(237,232,222,0.25); }
  .footer-flag { display: flex; gap: 4px; align-items: center; }
  .flag-stripe { width: 10px; height: 20px; }
  .flag-r { background: #D52B1E; }
  .flag-y { background: #F9E300; }
  .flag-g { background: #007A3D; }
  .flag-label { font-size: 0.65rem; color: rgba(237,232,222,0.3); margin-left: 8px; letter-spacing: 0.1em; }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 1024px) {
    nav { padding: 18px 30px; }
    .nav-links { display: none; }
    section { padding: 70px 30px; }
    .nosotros { grid-template-columns: 1fr; }
    .shows-grid { grid-template-columns: repeat(2,1fr); }
    .equipo-grid { grid-template-columns: repeat(2,1fr); }
    .contacto { grid-template-columns: 1fr; }
    .footer-top { grid-template-columns: 1fr 1fr; }
    .stats-band { gap: 40px; padding: 40px 30px; }
    .galeria-grid { grid-template-columns: 1fr 1fr; grid-template-rows: auto; }
    .galeria-item:nth-child(n) { grid-column: span 1; }
  }
  @media (max-width: 640px) {
    .shows-grid { grid-template-columns: 1fr; }
    .equipo-grid { grid-template-columns: 1fr 1fr; }
    .footer-top { grid-template-columns: 1fr; }
    .hero-title { font-size: 2.5rem; }
    .gira { padding: 60px 20px; }
    .evento-item { grid-template-columns: 70px 1fr; }
    .evento-btn { display: none; }
  }

  /* ─── SCROLL REVEAL ─── */
  .reveal { opacity: 0; transform: translateY(40px); transition: opacity 0.8s ease, transform 0.8s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }
</style>
</head>
<body>

<!-- LOADER -->
<div id="loader">
  <div class="loader-text">Elenco Nacional del Folklore de Bolivia</div>
  <div class="loader-line"></div>
</div>

<!-- NAV -->
<nav id="navbar">
  <div class="nav-logo">
    Elenco Nacional
    <span>del Folklore de Bolivia</span>
  </div>
  <ul class="nav-links">
    <li><a href="#nosotros">Nosotros</a></li>
    <li><a href="#espectaculos">Espectáculos</a></li>
    <li><a href="#gira">Funciones</a></li>
    <li><a href="#galeria">Galería</a></li>
    <li><a href="#historia">Historia</a></li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
  <button class="nav-btn" onclick="document.getElementById('contacto').scrollIntoView({behavior:'smooth'})">Adquirir Entradas</button>
</nav>

<!-- HERO -->
<section class="hero" id="inicio">
  <div class="hero-bg"></div>
  <div class="hero-pattern"></div>
  <div class="hero-decor-left"></div>
  <div class="hero-decor-right"></div>
  <div class="hero-content">
    <p class="hero-eyebrow">Bolivia · Patrimonio Cultural Viviente</p>
    <h1 class="hero-title">
      <span class="gold">Elenco Nacional</span>
      del Folklore
      <span class="italic-line">de Bolivia</span>
    </h1>
    <div class="hero-divider"></div>
    <p class="hero-subtitle">
      Guardianes de la memoria ancestral. Cada danza es un puente entre el pasado y el presente, entre la tierra y el cielo, entre los pueblos del altiplano, los valles y la amazonia boliviana.
    </p>
    <div class="hero-ctas">
      <a href="#espectaculos" class="btn-primary">Ver Espectáculos</a>
      <a href="#historia" class="btn-outline">Nuestra Historia</a>
    </div>
  </div>
  <div class="hero-scroll">
    <span>Descubrir</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- STATS -->
<div class="stats-band reveal">
  <div class="stat-item">
    <div class="stat-num">70+</div>
    <div class="stat-label">Años de trayectoria</div>
  </div>
  <div class="stat-item">
    <div class="stat-num">120</div>
    <div class="stat-label">Coreografías</div>
  </div>
  <div class="stat-item">
    <div class="stat-num">9</div>
    <div class="stat-label">Regiones culturales</div>
  </div>
  <div class="stat-item">
    <div class="stat-num">40+</div>
    <div class="stat-label">Países visitados</div>
  </div>
  <div class="stat-item">
    <div class="stat-num">5M+</div>
    <div class="stat-label">Espectadores</div>
  </div>
</div>

<!-- NOSOTROS -->
<section class="nosotros" id="nosotros">
  <div class="nosotros-visual reveal">
    <div class="visual-block-main">
      <div class="visual-centerpiece">
        <div class="big-letter">B</div>
      </div>
      <div class="visual-tag">
        <p>Fundado en</p>
        <strong>La Paz, Bolivia</strong>
      </div>
    </div>
  </div>
  <div class="nosotros-content">
    <p class="section-eyebrow reveal">Quiénes somos</p>
    <h2 class="section-title reveal">El alma viva de <em>Bolivia</em> en cada movimiento</h2>
    <p class="section-body reveal">
      El Elenco Nacional del Folklore de Bolivia es la compañía artística más emblemática del país, dedicada a preservar, investigar y difundir las expresiones dancísticas y musicales de las culturas bolivianas. Desde las danzas del altiplano hasta los ritmos tropicales del oriente, somos un museo viviente en movimiento.
    </p>
    <p class="section-body reveal" style="margin-top:16px">
      Nuestro elenco reúne a más de 80 bailarines, músicos y artistas que dan vida a las tradiciones de los pueblos Aymara, Quechua, Guaraní y demás naciones originarias que conforman la diversa Bolivia.
    </p>
    <ul class="features-list">
      <li class="reveal reveal-delay-1">
        <div class="feat-icon">★</div>
        <span>Investigación etnográfica profunda de las 9 regiones culturales de Bolivia</span>
      </li>
      <li class="reveal reveal-delay-2">
        <div class="feat-icon">♪</div>
        <span>Música en vivo con instrumentos andinos originales: zampoñas, charangos y bombos</span>
      </li>
      <li class="reveal reveal-delay-3">
        <div class="feat-icon">◆</div>
        <span>Vestuario artesanal elaborado por comunidades indígenas de todo el país</span>
      </li>
      <li class="reveal reveal-delay-4">
        <div class="feat-icon">✦</div>
        <span>Embajadores culturales en más de 40 países de los 5 continentes</span>
      </li>
    </ul>
  </div>
</section>

<!-- ESPECTÁCULOS -->
<section class="espectaculos" id="espectaculos">
  <div class="espectaculos-header">
    <p class="section-eyebrow reveal">Repertorio</p>
    <h2 class="section-title reveal">Nuestros <em>Espectáculos</em></h2>
    <p class="section-body reveal">Cada producción es un viaje a una región, una época y una cosmovisión diferente.</p>
  </div>
  <div class="shows-grid">
    <div class="show-card sc-1 reveal">
      <div class="show-card-bg"></div>
      <div class="show-card-overlay"></div>
      <div class="show-num">01</div>
      <div class="show-card-info">
        <div class="show-region">Altiplano · Aymara</div>
        <div class="show-name">La Morenada</div>
        <div class="show-desc">La danza más representativa del carnaval de Oruro, declarado Patrimonio Cultural Inmaterial de la Humanidad por la UNESCO.</div>
      </div>
    </div>
    <div class="show-card sc-2 reveal reveal-delay-1">
      <div class="show-card-bg"></div>
      <div class="show-card-overlay"></div>
      <div class="show-num">02</div>
      <div class="show-card-info">
        <div class="show-region">Valles · Quechua</div>
        <div class="show-name">Tinku</div>
        <div class="show-desc">Ritual de encuentro y combate ceremonial que celebra la fertilidad de la tierra y la cosmovisión andina.</div>
      </div>
    </div>
    <div class="show-card sc-3 reveal reveal-delay-2">
      <div class="show-card-bg"></div>
      <div class="show-card-overlay"></div>
      <div class="show-num">03</div>
      <div class="show-card-info">
        <div class="show-region">Altiplano · Puno</div>
        <div class="show-name">Diablada</div>
        <div class="show-desc">El espectacular enfrentamiento entre el bien y el mal, con máscaras talladas a mano y trajes de oro y plata.</div>
      </div>
    </div>
    <div class="show-card sc-4 reveal">
      <div class="show-card-bg"></div>
      <div class="show-card-overlay"></div>
      <div class="show-num">04</div>
      <div class="show-card-info">
        <div class="show-region">Oriente · Santa Cruz</div>
        <div class="show-name">Chovena</div>
        <div class="show-desc">Danza mestiza del oriente boliviano que fusiona influencias indígenas y españolas en un espectáculo colorido y festivo.</div>
      </div>
    </div>
    <div class="show-card sc-5 reveal reveal-delay-1">
      <div class="show-card-bg"></div>
      <div class="show-card-overlay"></div>
      <div class="show-num">05</div>
      <div class="show-card-info">
        <div class="show-region">Chiquitanía · Misiones</div>
        <div class="show-name">Macheteros</div>
        <div class="show-desc">La danza guerrera de los pueblos chiquitanos, expresión de resistencia y conexión espiritual con la naturaleza amazónica.</div>
      </div>
    </div>
    <div class="show-card sc-6 reveal reveal-delay-2">
      <div class="show-card-bg"></div>
      <div class="show-card-overlay"></div>
      <div class="show-num">06</div>
      <div class="show-card-info">
        <div class="show-region">Altiplano · Bolivia</div>
        <div class="show-name">Kullawada</div>
        <div class="show-desc">Danza de los tejedores, símbolo del trabajo y la destreza artesanal del pueblo aymara del Lago Titicaca.</div>
      </div>
    </div>
  </div>
</section>

<!-- CITA -->
<div class="quote-section reveal">
  <p class="quote-text">
    "Bolivia no es un país, es un universo de culturas. El Elenco Nacional es la voz que las hace hablar al mundo entero."
  </p>
  <p class="quote-author">— Dirección Artística · Elenco Nacional del Folklore de Bolivia</p>
</div>

<!-- GIRA -->
<section class="gira" id="gira">
  <div class="gira-inner">
    <div class="gira-header">
      <div>
        <p class="section-eyebrow reveal">Temporada 2025–2026</p>
        <h2 class="section-title reveal">Próximas <em>Funciones</em></h2>
      </div>
      <a href="#contacto" class="btn-outline reveal">Ver todas las fechas</a>
    </div>
    <div class="eventos-lista">
      <div class="evento-item reveal">
        <div class="evento-fecha"><div class="fecha-dia">14</div><div class="fecha-mes">Jun · 2025</div></div>
        <div class="evento-info">
          <div class="evento-nombre">Gala de Apertura — Temporada 2025</div>
          <div class="evento-lugar">Gran Teatro Nacional · La Paz</div>
          <div class="evento-ciudad">Bolivia</div>
        </div>
        <button class="evento-btn">Boletos</button>
      </div>
      <div class="evento-item reveal reveal-delay-1">
        <div class="evento-fecha"><div class="fecha-dia">22</div><div class="fecha-mes">Jun · 2025</div></div>
        <div class="evento-info">
          <div class="evento-nombre">Noche del Folklore Andino</div>
          <div class="evento-lugar">Teatro Municipal · Cochabamba</div>
          <div class="evento-ciudad">Bolivia</div>
        </div>
        <button class="evento-btn">Boletos</button>
      </div>
      <div class="evento-item reveal reveal-delay-2">
        <div class="evento-fecha"><div class="fecha-dia">05</div><div class="fecha-mes">Jul · 2025</div></div>
        <div class="evento-info">
          <div class="evento-nombre">Gira Internacional — Buenos Aires</div>
          <div class="evento-lugar">Teatro Colón · Buenos Aires</div>
          <div class="evento-ciudad">Argentina</div>
        </div>
        <button class="evento-btn">Boletos</button>
      </div>
      <div class="evento-item reveal reveal-delay-3">
        <div class="evento-fecha"><div class="fecha-dia">19</div><div class="fecha-mes">Jul · 2025</div></div>
        <div class="evento-info">
          <div class="evento-nombre">Festival Internacional de Folklore</div>
          <div class="evento-lugar">Auditorio Nacional · Ciudad de México</div>
          <div class="evento-ciudad">México</div>
        </div>
        <button class="evento-btn">Boletos</button>
      </div>
      <div class="evento-item reveal">
        <div class="evento-fecha"><div class="fecha-dia">02</div><div class="fecha-mes">Ago · 2025</div></div>
        <div class="evento-info">
          <div class="evento-nombre">Bolivia en Europa — Gira Continental</div>
          <div class="evento-lugar">Palau de la Música · Barcelona</div>
          <div class="evento-ciudad">España</div>
        </div>
        <button class="evento-btn">Boletos</button>
      </div>
      <div class="evento-item reveal reveal-delay-1">
        <div class="evento-fecha"><div class="fecha-dia">06</div><div class="fecha-mes">Ago · 2025</div></div>
        <div class="evento-info">
          <div class="evento-nombre">Carnaval de Oruro en Gira</div>
          <div class="evento-lugar">Palais des Congrès · París</div>
          <div class="evento-ciudad">Francia</div>
        </div>
        <button class="evento-btn">Boletos</button>
      </div>
    </div>
  </div>
</section>

<!-- GALERÍA -->
<section class="galeria" id="galeria">
  <div class="galeria-header">
    <p class="section-eyebrow reveal">Imágenes</p>
    <h2 class="section-title reveal">Galería de <em>Arte Vivo</em></h2>
  </div>
  <div class="galeria-grid">
    <div class="galeria-item gi-1 reveal">
      <div class="galeria-inner"></div>
      <div class="galeria-overlay"><div class="galeria-plus">+</div></div>
      <div class="galeria-label">La Morenada</div>
    </div>
    <div class="galeria-item gi-2 reveal reveal-delay-1">
      <div class="galeria-inner"></div>
      <div class="galeria-overlay"><div class="galeria-plus">+</div></div>
      <div class="galeria-label">Tinku</div>
    </div>
    <div class="galeria-item gi-3 reveal reveal-delay-2">
      <div class="galeria-inner"></div>
      <div class="galeria-overlay"><div class="galeria-plus">+</div></div>
      <div class="galeria-label">Diablada</div>
    </div>
    <div class="galeria-item gi-4 reveal reveal-delay-1">
      <div class="galeria-inner"></div>
      <div class="galeria-overlay"><div class="galeria-plus">+</div></div>
      <div class="galeria-label">Chovena</div>
    </div>
    <div class="galeria-item gi-5 reveal reveal-delay-2">
      <div class="galeria-inner"></div>
      <div class="galeria-overlay"><div class="galeria-plus">+</div></div>
      <div class="galeria-label">Macheteros</div>
    </div>
    <div class="galeria-item gi-6 reveal reveal-delay-3">
      <div class="galeria-inner"></div>
      <div class="galeria-overlay"><div class="galeria-plus">+</div></div>
      <div class="galeria-label">Kullawada</div>
    </div>
  </div>
</section>

<!-- EQUIPO -->
<section class="equipo" id="equipo">
  <div class="equipo-header">
    <p class="section-eyebrow reveal">Dirección</p>
    <h2 class="section-title reveal">Nuestra <em>Dirección Artística</em></h2>
  </div>
  <div class="equipo-grid">
    <div class="persona-card p1 reveal">
      <div class="persona-foto">
        <div class="persona-foto-inner"></div>
        <div class="persona-foto-overlay"></div>
      </div>
      <div class="persona-rol">Director General</div>
      <div class="persona-nombre">Roberto Mamani Quispe</div>
      <div class="persona-bio">Coreógrafo e investigador con más de 30 años preservando el patrimonio danzístico boliviano.</div>
    </div>
    <div class="persona-card p2 reveal reveal-delay-1">
      <div class="persona-foto">
        <div class="persona-foto-inner"></div>
        <div class="persona-foto-overlay"></div>
      </div>
      <div class="persona-rol">Directora Artística</div>
      <div class="persona-nombre">Carmen Rosa Flores</div>
      <div class="persona-bio">Maestra de danza folklórica boliviana, egresada del Conservatorio Nacional de Música de La Paz.</div>
    </div>
    <div class="persona-card p3 reveal reveal-delay-2">
      <div class="persona-foto">
        <div class="persona-foto-inner"></div>
        <div class="persona-foto-overlay"></div>
      </div>
      <div class="persona-rol">Director Musical</div>
      <div class="persona-nombre">Juan Carlos Apaza</div>
      <div class="persona-bio">Intérprete y compositor especializado en música andina y de las tierras bajas orientales.</div>
    </div>
    <div class="persona-card p4 reveal reveal-delay-3">
      <div class="persona-foto">
        <div class="persona-foto-inner"></div>
        <div class="persona-foto-overlay"></div>
      </div>
      <div class="persona-rol">Diseñadora de Vestuario</div>
      <div class="persona-nombre">Luz María Condori</div>
      <div class="persona-bio">Artesana textil que colabora con comunidades originarias para crear trajes auténticos y únicos.</div>
    </div>
  </div>
</section>

<!-- HISTORIA -->
<section class="historia" id="historia">
  <div class="historia-inner">
    <div class="historia-header">
      <p class="section-eyebrow reveal">Nuestro legado</p>
      <h2 class="section-title reveal">La <em>Historia</em> del Elenco</h2>
    </div>
    <div class="timeline">
      <div class="tl-item reveal">
        <div class="tl-dot"></div>
        <div class="tl-year">1952</div>
        <div class="tl-title">Fundación</div>
        <div class="tl-body">El Elenco Nacional del Folklore de Bolivia nace en La Paz con la misión de preservar las danzas y músicas tradicionales que comenzaban a desaparecer por la urbanización acelerada del país.</div>
      </div>
      <div class="tl-item reveal">
        <div class="tl-dot"></div>
        <div class="tl-year">1965</div>
        <div class="tl-title">Primera gira internacional</div>
        <div class="tl-body">Bolivia lleva su cultura a Argentina, Chile y Perú. El Elenco se convierte en embajador cultural oficial, recibiendo la Medalla al Mérito Cultural del gobierno boliviano.</div>
      </div>
      <div class="tl-item reveal">
        <div class="tl-dot"></div>
        <div class="tl-year">1978</div>
        <div class="tl-title">Sede permanente en el Gran Teatro</div>
        <div class="tl-body">El gobierno nacional otorga al Elenco su sede permanente en el Gran Teatro Nacional de La Paz, consolidándolo como institución cultural de primer orden.</div>
      </div>
      <div class="tl-item reveal">
        <div class="tl-dot"></div>
        <div class="tl-year">2001</div>
        <div class="tl-title">Reconocimiento UNESCO</div>
        <div class="tl-body">El Carnaval de Oruro, cuyas danzas forman parte del repertorio del Elenco, es declarado Patrimonio Cultural Inmaterial de la Humanidad por la UNESCO.</div>
      </div>
      <div class="tl-item reveal">
        <div class="tl-dot"></div>
        <div class="tl-year">2024</div>
        <div class="tl-title">Nueva era digital y expansión global</div>
        <div class="tl-body">El Elenco inicia su transformación digital, llevando el folklore boliviano a plataformas globales y nuevas generaciones, sin perder la esencia de su arte ancestral.</div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACTO -->
<section class="contacto" id="contacto">
  <div class="contacto-info">
    <p class="section-eyebrow reveal">Contacto</p>
    <h2 class="section-title reveal">Conéctate con <em>Nosotros</em></h2>
    <p class="section-body reveal">Para presentaciones, contrataciones, prensa o información general, estamos a tu disposición.</p>
    <div class="contact-items">
      <div class="contact-item reveal">
        <div class="contact-icon">✉</div>
        <div>
          <div class="contact-item-label">Correo electrónico</div>
          <div class="contact-item-val">info@elencofolklorebolivia.bo</div>
        </div>
      </div>
      <div class="contact-item reveal reveal-delay-1">
        <div class="contact-icon">☎</div>
        <div>
          <div class="contact-item-label">Teléfono</div>
          <div class="contact-item-val">+591 2 244-1800</div>
        </div>
      </div>
      <div class="contact-item reveal reveal-delay-2">
        <div class="contact-icon">◈</div>
        <div>
          <div class="contact-item-label">Dirección</div>
          <div class="contact-item-val">Gran Teatro Nacional, Av. Mariscal Santa Cruz, La Paz, Bolivia</div>
        </div>
      </div>
    </div>
    <div class="social-links reveal">
      <a href="#" class="social-link">f</a>
      <a href="#" class="social-link">in</a>
      <a href="#" class="social-link">ig</a>
      <a href="#" class="social-link">yt</a>
    </div>
  </div>
  <div class="contacto-form reveal">
    <div class="form-group">
      <label>Nombre completo</label>
      <input type="text" placeholder="Tu nombre">
    </div>
    <div class="form-group">
      <label>Correo electrónico</label>
      <input type="email" placeholder="tu@correo.com">
    </div>
    <div class="form-group">
      <label>Asunto</label>
      <select>
        <option>Contratación para evento</option>
        <option>Información de boletos</option>
        <option>Prensa y medios</option>
        <option>Alianzas institucionales</option>
        <option>Otro</option>
      </select>
    </div>
    <div class="form-group">
      <label>Mensaje</label>
      <textarea placeholder="Cuéntanos sobre tu proyecto o consulta..."></textarea>
    </div>
    <button class="btn-primary" style="width:100%">Enviar Mensaje</button>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div>
      <div class="footer-brand-name">Elenco Nacional</div>
      <div class="footer-brand-sub">del Folklore de Bolivia</div>
      <p class="footer-brand-text">Preservando la memoria ancestral de Bolivia a través de la danza, la música y el arte. Embajadores culturales de un país plurinacional y diverso.</p>
    </div>
    <div>
      <div class="footer-col-title">Navegación</div>
      <ul class="footer-links">
        <li><a href="#nosotros">Nosotros</a></li>
        <li><a href="#espectaculos">Espectáculos</a></li>
        <li><a href="#gira">Funciones</a></li>
        <li><a href="#galeria">Galería</a></li>
        <li><a href="#historia">Historia</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Información</div>
      <ul class="footer-links">
        <li><a href="#">Prensa</a></li>
        <li><a href="#">Contrataciones</a></li>
        <li><a href="#">Becas y talleres</a></li>
        <li><a href="#">Voluntariado</a></li>
        <li><a href="#">Descargas</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Legal</div>
      <ul class="footer-links">
        <li><a href="#">Política de privacidad</a></li>
        <li><a href="#">Términos de uso</a></li>
        <li><a href="#">Accesibilidad</a></li>
        <li><a href="#">Cookies</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2025 Elenco Nacional del Folklore de Bolivia. Todos los derechos reservados.</div>
    <div class="footer-flag">
      <div class="flag-stripe flag-r"></div>
      <div class="flag-stripe flag-y"></div>
      <div class="flag-stripe flag-g"></div>
      <span class="flag-label">Bolivia</span>
    </div>
  </div>
</footer>

<script>
  // Loader
  window.addEventListener('load', () => {
    setTimeout(() => document.getElementById('loader').classList.add('hide'), 1800);
  });

  // Navbar scroll
  window.addEventListener('scroll', () => {
    document.getElementById('navbar').classList.toggle('scrolled', window.scrollY > 60);
  });

  // Scroll reveal
  const revealEls = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target); } });
  }, { threshold: 0.12 });
  revealEls.forEach(el => observer.observe(el));

  // Wiphala colors (generado programáticamente)
  const wiphalaColors = [
    '#FF0000','#FF7F00','#FFFF00','#00FF00','#0000FF','#4B0082','#8B00FF',
    '#FF7F00','#FFFF00','#00FF00','#0000FF','#4B0082','#8B00FF','#FF0000',
    '#FFFF00','#00FF00','#0000FF','#4B0082','#8B00FF','#FF0000','#FF7F00',
    '#00FF00','#0000FF','#4B0082','#8B00FF','#FF0000','#FF7F00','#FFFF00',
    '#0000FF','#4B0082','#8B00FF','#FF0000','#FF7F00','#FFFF00','#00FF00',
    '#4B0082','#8B00FF','#FF0000','#FF7F00','#FFFF00','#00FF00','#0000FF',
    '#8B00FF','#FF0000','#FF7F00','#FFFF00','#00FF00','#0000FF','#4B0082'
  ];
  const wContainer = document.querySelector('.visual-wiphala');
  if (wContainer) {
    wiphalaColors.forEach(c => {
      const d = document.createElement('div');
      d.style.background = c;
      wContainer.appendChild(d);
    });
  }

  // Smooth scroll for anchors
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      e.preventDefault();
      const target = document.querySelector(a.getAttribute('href'));
      if (target) target.scrollIntoView({ behavior: 'smooth' });
    });
  });
</script>
</body>
</html>
