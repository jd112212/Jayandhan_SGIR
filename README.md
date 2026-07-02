<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Teekaraman.P — Real Estate</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<script>
tailwind.config = {
  theme: {
    extend: {
      fontFamily: { 'inter': ['Inter', 'sans-serif'] },
      colors: {
        signal: { red: '#E30613', redHover: '#FF1A27' },
        neon: { yellow: '#D4FF00', blue: '#00D4FF' },
      }
    }
  }
}
</script>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: 'Inter', sans-serif; background: #000; color: #fff; overflow-x: hidden; }

  body::after {
    content: '';
    position: fixed; inset: 0; pointer-events: none; z-index: 9999; opacity: 0.035;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
    background-size: 128px 128px;
  }

  .section-zone { transition: all 0.6s ease; }
  .shuffle-out { opacity: 0; transform: scale(0.92) translateY(20px); transition: all 300ms cubic-bezier(0.4, 0, 0.2, 1); }
  .shuffle-in { opacity: 1; transform: scale(1) translateY(0); transition: all 300ms cubic-bezier(0.4, 0, 0.2, 1); }

  .typewriter-cursor { display: inline-block; width: 2px; height: 1.1em; background: #E30613; margin-left: 2px; vertical-align: text-bottom; animation: blink 0.7s infinite; }
  @keyframes blink { 0%,50%{opacity:1} 51%,100%{opacity:0} }

  html { scroll-behavior: smooth; }
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: #000; }
  ::-webkit-scrollbar-thumb { background: #E30613; border-radius: 3px; }

  .hero-overlay { background: linear-gradient(135deg, rgba(0,0,0,0.85) 0%, rgba(0,0,0,0.4) 50%, rgba(227,6,19,0.15) 100%); }
  .glow-line { height: 2px; background: linear-gradient(90deg, transparent, #E30613, #00D4FF, transparent); box-shadow: 0 0 12px rgba(227,6,19,0.5); }

  .property-card { transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94); }
  .property-card:hover { transform: translateY(-6px); box-shadow: 0 20px 60px rgba(227,6,19,0.15); }
  .property-card:hover .card-img { transform: scale(1.05); }

  .nav-blur { backdrop-filter: blur(16px) saturate(180%); -webkit-backdrop-filter: blur(16px) saturate(180%); }

  .fade-up { opacity: 0; transform: translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .fade-up.visible { opacity: 1; transform: translateY(0); }

  .pulse-ring { animation: pulseRing 2s infinite; }
  @keyframes pulseRing { 0% { box-shadow: 0 0 0 0 rgba(227,6,19,0.5); } 70% { box-shadow: 0 0 0 15px rgba(227,6,19,0); } 100% { box-shadow: 0 0 0 0 rgba(227,6,19,0); } }

  /* Admin Panel */
  .admin-overlay { position: fixed; inset: 0; z-index: 10000; background: rgba(0,0,0,0.85); backdrop-filter: blur(8px); opacity: 0; pointer-events: none; transition: opacity 0.3s; }
  .admin-overlay.active { opacity: 1; pointer-events: auto; }
  .admin-panel { position: fixed; top: 0; right: -600px; width: 580px; max-width: 95vw; height: 100vh; z-index: 10001; background: #0a0a0a; border-left: 1px solid rgba(255,255,255,0.1); overflow-y: auto; transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
  .admin-panel.active { right: 0; }
  .admin-panel::-webkit-scrollbar { width: 4px; }
  .admin-panel::-webkit-scrollbar-thumb { background: #E30613; border-radius: 2px; }

  .admin-input { width: 100%; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 0.75rem; padding: 0.75rem 1rem; color: #fff; font-size: 0.875rem; transition: border-color 0.2s; outline: none; font-family: 'Inter', sans-serif; }
  .admin-input:focus { border-color: rgba(227,6,19,0.5); }
  .admin-input::placeholder { color: rgba(255,255,255,0.2); }
  .admin-select { appearance: none; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='rgba(255,255,255,0.4)' viewBox='0 0 16 16'%3E%3Cpath d='M8 11L3 6h10l-5 5z'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 12px center; padding-right: 36px; }
  .admin-select option { background: #111; color: #fff; }

  .admin-list-item { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); border-radius: 1rem; overflow: hidden; transition: border-color 0.2s; }
  .admin-list-item:hover { border-color: rgba(227,6,19,0.3); }

  .img-upload-zone { border: 2px dashed rgba(255,255,255,0.15); border-radius: 1rem; padding: 2rem; text-align: center; cursor: pointer; transition: all 0.3s; position: relative; overflow: hidden; }
  .img-upload-zone:hover { border-color: rgba(227,6,19,0.5); background: rgba(227,6,19,0.03); }
  .img-upload-zone img { max-height: 180px; object-fit: cover; border-radius: 0.5rem; }

  .admin-btn { padding: 0.625rem 1.25rem; border-radius: 0.75rem; font-size: 0.875rem; font-weight: 500; transition: all 0.2s; cursor: pointer; display: inline-flex; align-items: center; gap: 0.5rem; font-family: 'Inter', sans-serif; }
  .admin-btn-primary { background: #E30613; color: #fff; border: none; }
  .admin-btn-primary:hover { background: #FF1A27; transform: translateY(-1px); }
  .admin-btn-ghost { background: transparent; color: rgba(255,255,255,0.5); border: 1px solid rgba(255,255,255,0.1); }
  .admin-btn-ghost:hover { color: #fff; border-color: rgba(255,255,255,0.3); background: rgba(255,255,255,0.05); }
  .admin-btn-danger { background: transparent; color: #f87171; border: 1px solid rgba(248,113,113,0.2); }
  .admin-btn-danger:hover { background: rgba(248,113,113,0.1); border-color: rgba(248,113,113,0.4); }
  .admin-btn-sm { padding: 0.375rem 0.75rem; font-size: 0.75rem; border-radius: 0.5rem; }

  .admin-tab { padding: 0.625rem 1.25rem; font-size: 0.8125rem; font-weight: 500; color: rgba(255,255,255,0.4); border-bottom: 2px solid transparent; cursor: pointer; transition: all 0.2s; background: none; border-top: none; border-left: none; border-right: none; font-family: 'Inter', sans-serif; }
  .admin-tab:hover { color: rgba(255,255,255,0.7); }
  .admin-tab.active { color: #fff; border-bottom-color: #E30613; }

  .confirm-modal { position: fixed; inset: 0; z-index: 10002; background: rgba(0,0,0,0.85); display: flex; align-items: center; justify-content: center; opacity: 0; pointer-events: none; transition: opacity 0.3s; }
  .confirm-modal.active { opacity: 1; pointer-events: auto; }

  /* Big visible manage bar */
  .manage-bar { background: linear-gradient(135deg, rgba(227,6,19,0.1) 0%, rgba(0,212,255,0.05) 100%); border: 1px solid rgba(227,6,19,0.2); border-radius: 1rem; padding: 1rem 1.5rem; display: flex; align-items: center; justify-content: space-between; gap: 1rem; flex-wrap: wrap; }
  .manage-bar:hover { border-color: rgba(227,6,19,0.4); background: linear-gradient(135deg, rgba(227,6,19,0.15) 0%, rgba(0,212,255,0.08) 100%); }
  .manage-big-btn { background: #E30613; color: #fff; border: none; padding: 0.75rem 1.5rem; border-radius: 0.75rem; font-size: 0.9375rem; font-weight: 600; cursor: pointer; display: flex; align-items: center; gap: 0.5rem; transition: all 0.2s; font-family: 'Inter', sans-serif; }
  .manage-big-btn:hover { background: #FF1A27; transform: translateY(-2px); box-shadow: 0 8px 25px rgba(227,6,19,0.3); }
</style>
</head>
<body>

<!-- ========== NAVIGATION ========== -->
<nav id="mainNav" class="fixed top-0 left-0 right-0 z-50 nav-blur bg-black/70 border-b border-white/5 transition-all duration-500">
  <div class="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
    <a href="#" class="flex items-center gap-3 group">
      <div class="w-10 h-10 bg-signal-red rounded-lg flex items-center justify-center font-black text-white text-lg group-hover:bg-signal-redHover transition-colors">T</div>
      <div>
        <span class="text-white font-bold text-lg tracking-tight">TEEKARAMAN</span>
        <span class="text-signal-red font-light text-lg">.P</span>
        <div class="text-[10px] text-white/40 uppercase tracking-[0.25em] -mt-0.5">Real Estate</div>
      </div>
    </a>
    <div class="hidden md:flex items-center gap-8">
      <a href="#about" class="text-sm text-white/60 hover:text-white transition-colors">About</a>
      <a href="#listings" class="text-sm text-white/60 hover:text-white transition-colors">Listings</a>
      <a href="#contact" class="bg-signal-red hover:bg-signal-redHover text-white text-sm font-medium px-5 py-2.5 rounded-lg transition-all hover:scale-105 hover:shadow-lg hover:shadow-signal-red/20">Contact</a>
    </div>
    <button id="mobileMenuBtn" class="md:hidden text-white/70 hover:text-white"><i data-lucide="menu" class="w-6 h-6"></i></button>
  </div>
  <div id="mobileMenu" class="md:hidden hidden bg-black/95 border-t border-white/5 px-6 py-6 space-y-4">
    <a href="#about" class="block text-white/70 hover:text-white py-2">About</a>
    <a href="#listings" class="block text-white/70 hover:text-white py-2">Listings</a>
    <a href="#contact" class="block bg-signal-red text-white text-center py-3 rounded-lg font-medium">Contact</a>
  </div>
</nav>

<!-- ========== HERO ========== -->
<section id="hero-section" class="relative min-h-screen flex items-center pt-20 overflow-hidden">
  <div class="absolute inset-0">
    <div class="w-full h-full bg-cover bg-center" style="background-image: url('hero-bg.jpg');"></div>
    <div class="hero-overlay absolute inset-0"></div>
  </div>
  <div class="absolute left-0 top-1/2 -translate-y-1/2 w-1 h-48 bg-signal-red rounded-r-full shadow-[0_0_20px_rgba(227,6,19,0.5)]"></div>
  <div class="relative z-10 max-w-7xl mx-auto px-6 w-full">
    <div class="grid lg:grid-cols-2 gap-12 items-center">
      <div class="space-y-8">
        <div class="inline-flex items-center gap-2 bg-white/5 border border-white/10 rounded-full px-4 py-1.5">
          <span class="w-2 h-2 bg-neon-yellow rounded-full animate-pulse"></span>
          <span class="text-xs font-medium text-white/70 uppercase tracking-wider">Now Accepting Clients</span>
        </div>
        <h1 class="text-5xl sm:text-6xl lg:text-7xl font-black leading-[0.95] tracking-tight">
          <span class="text-white">YOUR</span><br><span class="text-signal-red">DREAM</span><br><span class="text-white">PROPERTY</span><br><span class="text-white/30 text-4xl sm:text-5xl lg:text-6xl font-light">STARTS HERE.</span>
        </h1>
        <p class="text-lg text-white/50 max-w-md leading-relaxed font-light">Trusted real estate expertise by <span class="text-white font-medium">Teekaraman.P</span> — helping you find the perfect property with transparency and conviction.</p>
        <div class="flex flex-wrap gap-4">
          <a href="#listings" class="bg-signal-red hover:bg-signal-redHover text-white font-semibold px-8 py-4 rounded-xl transition-all hover:scale-105 hover:shadow-xl hover:shadow-signal-red/25 flex items-center gap-2"><span>View Listings</span><i data-lucide="arrow-right" class="w-5 h-5"></i></a>
          <a href="tel:9962699649" class="border border-white/15 hover:border-white/30 text-white font-medium px-8 py-4 rounded-xl transition-all hover:bg-white/5 flex items-center gap-2"><i data-lucide="phone" class="w-4 h-4"></i><span>Call Now</span></a>
        </div>
        <div class="flex gap-10 pt-4">
          <div><div class="text-3xl font-black text-white">150<span class="text-signal-red">+</span></div><div class="text-xs text-white/40 uppercase tracking-wider mt-1">Properties Sold</div></div>
          <div><div class="text-3xl font-black text-white">8<span class="text-signal-red">+</span></div><div class="text-xs text-white/40 uppercase tracking-wider mt-1">Years Experience</div></div>
          <div><div class="text-3xl font-black text-white">98<span class="text-signal-red">%</span></div><div class="text-xs text-white/40 uppercase tracking-wider mt-1">Client Satisfaction</div></div>
        </div>
      </div>
      <div class="hidden lg:flex justify-center">
        <div class="relative group">
          <div class="absolute -inset-4 bg-gradient-to-br from-signal-red/20 via-transparent to-neon-blue/10 rounded-3xl blur-2xl opacity-0 group-hover:opacity-100 transition-opacity duration-700"></div>
          <div class="relative bg-white/5 border border-white/10 rounded-2xl p-8 backdrop-blur-sm">
            <div class="w-72 h-80 rounded-xl overflow-hidden border-2 border-white/10">
              <img src="teekaraman.jpeg" alt="Teekaraman.P" class="w-full h-full object-cover" style="filter: contrast(1.15) brightness(0.95);"
                onerror="this.src='https://picsum.photos/seed/teekaraman-portrait/600/700.jpg'">
            </div>
            <div class="mt-5 text-center">
              <h3 class="text-xl font-bold text-white">Teekaraman.P</h3>
              <p class="text-signal-red text-sm font-medium mt-1">Senior Real Estate Consultant</p>
              <div class="flex justify-center gap-4 mt-4">
                <a href="tel:9962699649" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-signal-red hover:border-signal-red transition-all"><i data-lucide="phone" class="w-4 h-4 text-white/70"></i></a>
                <a href="mailto:pandavlogs@gmail.com" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-neon-blue hover:border-neon-blue transition-all"><i data-lucide="mail" class="w-4 h-4 text-white/70"></i></a>
                <a href="https://wa.me/919962699649" target="_blank" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-green-600 hover:border-green-600 transition-all"><i data-lucide="message-circle" class="w-4 h-4 text-white/70"></i></a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 animate-bounce">
    <span class="text-[10px] text-white/30 uppercase tracking-[0.3em]">Scroll</span>
    <i data-lucide="chevron-down" class="w-4 h-4 text-white/30"></i>
  </div>
</section>

<div class="glow-line w-full"></div>

<!-- ========== ABOUT ========== -->
<section id="about" class="section-zone py-24 px-6 relative" data-brand="neon-blue">
  <div class="max-w-7xl mx-auto">
    <div class="grid lg:grid-cols-5 gap-16 items-start">
      <div class="lg:col-span-2 fade-up">
        <div class="relative group">
          <div class="absolute -inset-2 bg-gradient-to-b from-neon-blue/10 to-transparent rounded-2xl blur-xl group-hover:blur-2xl transition-all duration-500"></div>
          <div class="relative aspect-[3/4] rounded-2xl overflow-hidden border border-white/10">
            <img src="teekaraman.jpeg" alt="Teekaraman.P" class="w-full h-full object-cover" style="filter: contrast(1.2) brightness(0.9);"
              onerror="this.src='https://picsum.photos/seed/teekaraman-about/600/800.jpg'">
            <div class="absolute inset-0 bg-gradient-to-t from-black via-transparent to-transparent"></div>
            <div class="absolute bottom-0 left-0 right-0 p-6">
              <div class="text-xs uppercase tracking-[0.3em] text-neon-blue font-semibold mb-2">About Me</div>
              <div class="text-2xl font-black text-white">Teekaraman.P</div>
            </div>
          </div>
        </div>
      </div>
      <div class="lg:col-span-3 space-y-8 fade-up" style="transition-delay: 150ms;">
        <div>
          <span class="text-xs uppercase tracking-[0.3em] text-signal-red font-semibold">The Person Behind The Deals</span>
          <h2 class="text-4xl sm:text
