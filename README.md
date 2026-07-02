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

  /* Admin Panel Styles */
  .admin-overlay { position: fixed; inset: 0; z-index: 10000; background: rgba(0,0,0,0.8); backdrop-filter: blur(8px); opacity: 0; pointer-events: none; transition: opacity 0.3s; }
  .admin-overlay.active { opacity: 1; pointer-events: auto; }
  .admin-panel { position: fixed; top: 0; right: -600px; width: 580px; max-width: 95vw; height: 100vh; z-index: 10001; background: #0a0a0a; border-left: 1px solid rgba(255,255,255,0.1); overflow-y: auto; transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
  .admin-panel.active { right: 0; }
  .admin-panel::-webkit-scrollbar { width: 4px; }
  .admin-panel::-webkit-scrollbar-thumb { background: #E30613; border-radius: 2px; }

  .admin-input { width: 100%; background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 0.75rem; padding: 0.75rem 1rem; color: #fff; font-size: 0.875rem; transition: border-color 0.2s; outline: none; }
  .admin-input:focus { border-color: rgba(227,6,19,0.5); }
  .admin-input::placeholder { color: rgba(255,255,255,0.2); }
  .admin-select { appearance: none; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='rgba(255,255,255,0.4)' viewBox='0 0 16 16'%3E%3Cpath d='M8 11L3 6h10l-5 5z'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 12px center; padding-right: 36px; }

  .admin-list-item { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); border-radius: 1rem; overflow: hidden; transition: border-color 0.2s; }
  .admin-list-item:hover { border-color: rgba(227,6,19,0.3); }

  .img-upload-zone { border: 2px dashed rgba(255,255,255,0.15); border-radius: 1rem; padding: 2rem; text-align: center; cursor: pointer; transition: all 0.3s; position: relative; overflow: hidden; }
  .img-upload-zone:hover { border-color: rgba(227,6,19,0.5); background: rgba(227,6,19,0.03); }
  .img-upload-zone img { max-height: 200px; object-fit: cover; border-radius: 0.5rem; }

  .admin-btn { padding: 0.625rem 1.25rem; border-radius: 0.75rem; font-size: 0.875rem; font-weight: 500; transition: all 0.2s; cursor: pointer; display: inline-flex; align-items: center; gap: 0.5rem; }
  .admin-btn-primary { background: #E30613; color: #fff; border: none; }
  .admin-btn-primary:hover { background: #FF1A27; transform: translateY(-1px); }
  .admin-btn-ghost { background: transparent; color: rgba(255,255,255,0.5); border: 1px solid rgba(255,255,255,0.1); }
  .admin-btn-ghost:hover { color: #fff; border-color: rgba(255,255,255,0.3); background: rgba(255,255,255,0.05); }
  .admin-btn-danger { background: transparent; color: #f87171; border: 1px solid rgba(248,113,113,0.2); }
  .admin-btn-danger:hover { background: rgba(248,113,113,0.1); border-color: rgba(248,113,113,0.4); }
  .admin-btn-sm { padding: 0.375rem 0.75rem; font-size: 0.75rem; border-radius: 0.5rem; }

  .admin-tab { padding: 0.625rem 1.25rem; font-size: 0.8125rem; font-weight: 500; color: rgba(255,255,255,0.4); border-bottom: 2px solid transparent; cursor: pointer; transition: all 0.2s; }
  .admin-tab:hover { color: rgba(255,255,255,0.7); }
  .admin-tab.active { color: #fff; border-bottom-color: #E30613; }

  /* Floating manage button */
  .manage-fab { position: fixed; bottom: 24px; left: 24px; z-index: 100; width: 52px; height: 52px; border-radius: 50%; background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.15); color: rgba(255,255,255,0.6); display: flex; align-items: center; justify-content: center; cursor: pointer; transition: all 0.3s; backdrop-filter: blur(12px); }
  .manage-fab:hover { background: #E30613; border-color: #E30613; color: #fff; transform: scale(1.1); box-shadow: 0 8px 30px rgba(227,6,19,0.3); }

  /* Delete confirmation */
  .confirm-modal { position: fixed; inset: 0; z-index: 10002; background: rgba(0,0,0,0.85); display: flex; align-items: center; justify-content: center; opacity: 0; pointer-events: none; transition: opacity 0.3s; }
  .confirm-modal.active { opacity: 1; pointer-events: auto; }
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
          <h2 class="text-4xl sm:text-5xl font-black text-white mt-3 leading-tight">I Don't Just Sell Properties.<br><span class="text-white/20">I Sell Convictions.</span></h2>
        </div>
        <div class="space-y-4 text-white/50 text-lg leading-relaxed font-light">
          <p>With over <span class="text-white font-medium">8 years</span> in the real estate industry, I've built my reputation on one principle: <span class="text-neon-yellow font-medium">never recommend what I wouldn't buy myself</span>. Every property I present has been personally inspected, researched, and vetted.</p>
          <p>From luxury apartments in Chennai's prime corridors to investment plots with high appreciation potential — I bring the same level of rigor whether you're spending ₹20 lakhs or ₹5 crores.</p>
          <p>My approach is simple: <span class="text-white font-medium">deep research, honest opinions, zero pressure</span>. I'd rather lose a deal than lose your trust.</p>
        </div>
        <div class="grid sm:grid-cols-2 gap-4 pt-4">
          <div class="bg-white/[0.03] border border-white/[0.06] rounded-xl p-5 hover:border-signal-red/30 transition-colors">
            <div class="flex items-center gap-3 mb-3"><div class="w-10 h-10 rounded-lg bg-signal-red/10 flex items-center justify-center"><i data-lucide="phone-call" class="w-5 h-5 text-signal-red"></i></div><span class="text-xs uppercase tracking-wider text-white/40">Phone</span></div>
            <a href="tel:9962699649" class="text-white font-semibold text-lg hover:text-signal-red transition-colors">+91 99626 99649</a>
          </div>
          <div class="bg-white/[0.03] border border-white/[0.06] rounded-xl p-5 hover:border-neon-blue/30 transition-colors">
            <div class="flex items-center gap-3 mb-3"><div class="w-10 h-10 rounded-lg bg-neon-blue/10 flex items-center justify-center"><i data-lucide="mail" class="w-5 h-5 text-neon-blue"></i></div><span class="text-xs uppercase tracking-wider text-white/40">Email</span></div>
            <a href="mailto:pandavlogs@gmail.com" class="text-white font-semibold text-lg hover:text-neon-blue transition-colors break-all">pandavlogs@gmail.com</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="glow-line w-full"></div>

<!-- ========== LISTINGS ========== -->
<section id="listings" class="section-zone py-24 px-6 relative" data-brand="signal-red">
  <div class="max-w-7xl mx-auto">
    <div class="flex flex-col sm:flex-row sm:items-end sm:justify-between gap-6 mb-12 fade-up">
      <div>
        <span class="text-xs uppercase tracking-[0.3em] text-signal-red font-semibold">Property Library</span>
        <h2 class="text-4xl sm:text-5xl font-black text-white mt-3">Featured Listings</h2>
      </div>
      <div class="flex flex-wrap gap-2" id="filterBtns">
        <button data-filter="all" class="filter-btn active bg-signal-red text-white text-sm font-medium px-5 py-2 rounded-lg transition-all">All</button>
        <button data-filter="apartment" class="filter-btn bg-white/5 text-white/60 text-sm font-medium px-5 py-2 rounded-lg border border-white/10 hover:border-signal-red/40 hover:text-white transition-all">Apartments</button>
        <button data-filter="villa" class="filter-btn bg-white/5 text-white/60 text-sm font-medium px-5 py-2 rounded-lg border border-white/10 hover:border-signal-red/40 hover:text-white transition-all">Villas</button>
        <button data-filter="plot" class="filter-btn bg-white/5 text-white/60 text-sm font-medium px-5 py-2 rounded-lg border border-white/10 hover:border-signal-red/40 hover:text-white transition-all">Plots</button>
        <button data-filter="commercial" class="filter-btn bg-white/5 text-white/60 text-sm font-medium px-5 py-2 rounded-lg border border-white/10 hover:border-signal-red/40 hover:text-white transition-all">Commercial</button>
      </div>
    </div>
    <div id="propertyGrid" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6"></div>
    <div id="emptyState" class="hidden text-center py-20">
      <i data-lucide="home" class="w-16 h-16 text-white/10 mx-auto mb-4"></i>
      <p class="text-white/30 text-lg">No listings yet. Click the manage button to add properties.</p>
    </div>
  </div>
</section>

<div class="glow-line w-full"></div>

<!-- ========== CONTACT ========== -->
<section id="contact" class="section-zone py-24 px-6 relative" data-brand="signal-red">
  <div class="max-w-7xl mx-auto">
    <div class="grid lg:grid-cols-2 gap-16">
      <div class="fade-up">
        <span class="text-xs uppercase tracking-[0.3em] text-signal-red font-semibold">Stay Updated</span>
        <h2 class="text-4xl font-black text-white mt-3 mb-4">Get New Listings First</h2>
        <p class="text-white/40 text-lg font-light mb-8">I send curated property picks every week. No spam, no fluff.</p>
        <form id="newsletterForm" class="space-y-4" onsubmit="return false;">
          <input type="text" id="newsletterName" placeholder="Your Name" class="w-full bg-white/5 border border-white/10 rounded-xl px-5 py-4 text-white placeholder:text-white/20 focus:outline-none focus:border-signal-red/50 transition-colors text-lg">
          <div class="relative">
            <input type="email" id="newsletterEmail" placeholder="" class="w-full bg-white/5 border border-white/10 rounded-xl px-5 py-4 text-white placeholder:text-white/20 focus:outline-none focus:border-signal-red/50 transition-colors text-lg" required>
            <span class="typewriter-cursor" id="typewriterCursor"></span>
          </div>
          <button type="submit" id="newsletterBtn" class="w-full bg-signal-red hover:bg-signal-redHover text-white font-semibold py-4 rounded-xl transition-all hover:scale-[1.02] hover:shadow-xl hover:shadow-signal-red/20 text-lg flex items-center justify-center gap-2"><span>Subscribe</span><i data-lucide="arrow-right" class="w-5 h-5"></i></button>
          <div id="newsletterMsg" class="hidden text-center py-3 rounded-xl text-sm font-medium"></div>
        </form>
      </div>
      <div class="fade-up" style="transition-delay: 150ms;">
        <span class="text-xs uppercase tracking-[0.3em] text-neon-blue font-semibold">Direct Line</span>
        <h2 class="text-4xl font-black text-white mt-3 mb-8">Talk to Teekaraman</h2>
        <div class="space-y-4">
          <a href="tel:9962699649" class="flex items-center gap-5 bg-white/[0.03] border border-white/[0.06] rounded-xl p-5 hover:border-signal-red/30 transition-all group">
            <div class="w-14 h-14 rounded-xl bg-signal-red/10 flex items-center justify-center flex-shrink-0 pulse-ring"><i data-lucide="phone" class="w-6 h-6 text-signal-red"></i></div>
            <div><div class="text-xs text-white/30 uppercase tracking-wider mb-1">Call Now</div><div class="text-xl font-bold text-white group-hover:text-signal-red transition-colors">+91 99626 99649</div></div>
            <i data-lucide="arrow-up-right" class="w-5 h-5 text-white/20 ml-auto group-hover:text-signal-red transition-colors"></i>
          </a>
          <a href="mailto:pandavlogs@gmail.com" class="flex items-center gap-5 bg-white/[0.03] border border-white/[0.06] rounded-xl p-5 hover:border-neon-blue/30 transition-all group">
            <div class="w-14 h-14 rounded-xl bg-neon-blue/10 flex items-center justify-center flex-shrink-0"><i data-lucide="mail" class="w-6 h-6 text-neon-blue"></i></div>
            <div><div class="text-xs text-white/30 uppercase tracking-wider mb-1">Email</div><div class="text-xl font-bold text-white group-hover:text-neon-blue transition-colors break-all">pandavlogs@gmail.com</div></div>
            <i data-lucide="arrow-up-right" class="w-5 h-5 text-white/20 ml-auto group-hover:text-neon-blue transition-colors"></i>
          </a>
          <a href="https://wa.me/919962699649?text=Hi%20Teekaraman%2C%20I%27m%20interested%20in%20your%20property%20listings." target="_blank" class="flex items-center gap-5 bg-white/[0.03] border border-white/[0.06] rounded-xl p-5 hover:border-green-500/30 transition-all group">
            <div class="w-14 h-14 rounded-xl bg-green-500/10 flex items-center justify-center flex-shrink-0"><i data-lucide="message-circle" class="w-6 h-6 text-green-500"></i></div>
            <div><div class="text-xs text-white/30 uppercase tracking-wider mb-1">WhatsApp</div><div class="text-xl font-bold text-white group-hover:text-green-500 transition-colors">Send a Message</div></div>
            <i data-lucide="arrow-up-right" class="w-5 h-5 text-white/20 ml-auto group-hover:text-green-500 transition-colors"></i>
          </a>
        </div>
        <div class="mt-8 flex items-center gap-3 bg-neon-yellow/5 border border-neon-yellow/20 rounded-xl p-4">
          <span class="w-3 h-3 bg-neon-yellow rounded-full animate-pulse"></span>
          <span class="text-neon-yellow text-sm font-medium">Available for site visits today • Call to schedule</span>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="glow-line w-full"></div>

<!-- ========== FOOTER ========== -->
<footer class="py-16 px-6 bg-black">
  <div class="max-w-7xl mx-auto">
    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-10 mb-12">
      <div>
        <div class="flex items-center gap-3 mb-4"><div class="w-10 h-10 bg-signal-red rounded-lg flex items-center justify-center font-black text-white text-lg">T</div><div><span class="text-white font-bold text-lg">TEEKARAMAN</span><span class="text-signal-red font-light">.P</span></div></div>
        <p class="text-white/30 text-sm leading-relaxed">Honest real estate opinions. No BS. Just properties I'd actually recommend.</p>
      </div>
      <div>
        <h4 class="text-xs uppercase tracking-[0.2em] text-white/50 font-semibold mb-4">Navigate</h4>
        <ul class="space-y-3"><li><a href="#about" class="text-white/30 text-sm hover:text-white transition-colors">About</a></li><li><a href="#listings" class="text-white/30 text-sm hover:text-white transition-colors">Listings</a></li><li><a href="#contact" class="text-white/30 text-sm hover:text-white transition-colors">Contact</a></li></ul>
      </div>
      <div>
        <h4 class="text-xs uppercase tracking-[0.2em] text-white/50 font-semibold mb-4">Contact</h4>
        <ul class="space-y-3"><li><a href="tel:9962699649" class="text-white/30 text-sm hover:text-signal-red transition-colors">+91 99626 99649</a></li><li><a href="mailto:pandavlogs@gmail.com" class="text-white/30 text-sm hover:text-neon-blue transition-colors">pandavlogs@gmail.com</a></li><li><a href="https://wa.me/919962699649" target="_blank" class="text-white/30 text-sm hover:text-green-500 transition-colors">WhatsApp</a></li></ul>
      </div>
    </div>
    <div class="border-t border-white/5 pt-8 flex flex-col sm:flex-row justify-between items-center gap-4">
      <p class="text-white/20 text-sm">© 2025 Teekaraman.P Real Estate. All rights reserved.</p>
      <p class="text-white/10 text-xs">Built with conviction, not templates.</p>
    </div>
  </div>
</footer>

<!-- ========== FLOATING MANAGE BUTTON ========== -->
<button class="manage-fab" id="manageFab" title="Manage Listings">
  <i data-lucide="settings" class="w-5 h-5"></i>
</button>

<!-- ========== ADMIN OVERLAY ========== -->
<div class="admin-overlay" id="adminOverlay"></div>

<!-- ========== ADMIN PANEL ========== -->
<div class="admin-panel" id="adminPanel">
  <!-- Header -->
  <div class="sticky top-0 bg-[#0a0a0a] border-b border-white/10 z-10 px-6 py-5">
    <div class="flex items-center justify-between">
      <div>
        <h2 class="text-xl font-bold text-white">Manage Listings</h2>
        <p class="text-white/40 text-xs mt-0.5">Add, edit, or remove properties</p>
      </div>
      <button id="adminClose" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-white/10 transition-colors">
        <i data-lucide="x" class="w-5 h-5 text-white/60"></i>
      </button>
    </div>
    <!-- Tabs -->
    <div class="flex gap-4 mt-4 -mb-5">
      <button class="admin-tab active" data-tab="list">All Properties</button>
      <button class="admin-tab" data-tab="form">Add New</button>
    </div>
  </div>

  <!-- Tab: Property List -->
  <div id="tabList" class="p-6 space-y-4">
    <div id="adminPropertyList"></div>
    <div id="adminEmpty" class="hidden text-center py-16">
      <i data-lucide="inbox" class="w-12 h-12 text-white/10 mx-auto mb-3"></i>
      <p class="text-white/30 text-sm">No properties added yet.</p>
      <button class="admin-btn admin-btn-primary mt-4 admin-tab-switch" data-tab="form">+ Add First Property</button>
    </div>
  </div>

  <!-- Tab: Add/Edit Form -->
  <div id="tabForm" class="p-6 hidden">
    <form id="propertyForm" class="space-y-5">
      <input type="hidden" id="editId" value="">

      <!-- Image Upload -->
      <div>
        <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Property Image</label>
        <div class="img-upload-zone" id="imgUploadZone">
          <div id="imgPlaceholder">
            <i data-lucide="image-plus" class="w-10 h-10 text-white/20 mx-auto mb-2"></i>
            <p class="text-white/30 text-sm">Click or drag image here</p>
            <p class="text-white/15 text-xs mt-1">JPG, PNG — under 2MB recommended</p>
          </div>
          <img id="imgPreview" class="hidden mx-auto" alt="Preview">
          <input type="file" id="imgInput" accept="image/*" class="absolute inset-0 w-full h-full opacity-0 cursor-pointer">
        </div>
      </div>

      <!-- Title -->
      <div>
        <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Property Title *</label>
        <input type="text" id="formTitle" class="admin-input" placeholder="e.g. Skyline Tower 3BHK" required>
      </div>

      <!-- Location -->
      <div>
        <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Location *</label>
        <input type="text" id="formLocation" class="admin-input" placeholder="e.g. OMR, Chennai" required>
      </div>

      <!-- Type + Area Row -->
      <div class="grid grid-cols-2 gap-4">
        <div>
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Type *</label>
          <select id="formType" class="admin-input admin-select" required>
            <option value="">Select</option>
            <option value="apartment">Apartment</option>
            <option value="villa">Villa</option>
            <option value="plot">Plot</option>
            <option value="commercial">Commercial</option>
          </select>
        </div>
        <div>
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Area</label>
          <input type="text" id="formArea" class="admin-input" placeholder="e.g. 1450 sq.ft">
        </div>
      </div>

      <!-- Badge + Color Row -->
      <div class="grid grid-cols-2 gap-4">
        <div>
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Badge Label</label>
          <input type="text" id="formBadge" class="admin-input" placeholder="e.g. New, Hot, Premium">
        </div>
        <div>
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Badge Color</label>
          <select id="formBadgeColor" class="admin-input admin-select">
            <option value="signal-red">Red</option>
            <option value="neon-yellow">Yellow</option>
            <option value="neon-blue">Blue</option>
          </select>
        </div>
      </div>

      <!-- Divider -->
      <div class="border-t border-white/5 pt-5">
        <p class="text-xs uppercase tracking-wider text-neon-blue font-semibold mb-4">Enquiry Details (per property)</p>

        <!-- Enquiry Phone -->
        <div class="mb-4">
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Enquiry Phone</label>
          <input type="text" id="formEnqPhone" class="admin-input" placeholder="+91 99626 99649" value="+91 99626 99649">
          <p class="text-white/20 text-xs mt-1">Leave default to use your number</p>
        </div>

        <!-- Enquiry Email -->
        <div class="mb-4">
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">Enquiry Email</label>
          <input type="email" id="formEnqEmail" class="admin-input" placeholder="pandavlogs@gmail.com" value="pandavlogs@gmail.com">
        </div>

        <!-- Enquiry WhatsApp Message -->
        <div>
          <label class="block text-xs uppercase tracking-wider text-white/40 font-semibold mb-2">WhatsApp Message</label>
          <textarea id="formEnqMsg" class="admin-input" rows="2" placeholder="Hi, I'm interested in [PROPERTY_NAME]">Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details.</textarea>
          <p class="text-white/20 text-xs mt-1">Use [PROPERTY_NAME] as placeholder — it auto-replaces</p>
        </div>
      </div>

      <!-- Buttons -->
      <div class="flex gap-3 pt-2">
        <button type="submit" class="admin-btn admin-btn-primary flex-1" id="formSubmitBtn">
          <i data-lucide="plus" class="w-4 h-4"></i>
          <span>Add Property</span>
        </button>
        <button type="button" class="admin-btn admin-btn-ghost" id="formCancelBtn">Cancel</button>
      </div>
    </form>
  </div>
</div>

<!-- ========== DELETE CONFIRMATION ========== -->
<div class="confirm-modal" id="confirmModal">
  <div class="bg-[#111] border border-white/10 rounded-2xl p-8 max-w-sm mx-4 text-center">
    <div class="w-14 h-14 rounded-full bg-red-500/10 flex items-center justify-center mx-auto mb-4">
      <i data-lucide="trash-2" class="w-7 h-7 text-red-400"></i>
    </div>
    <h3 class="text-xl font-bold text-white mb-2">Delete Property?</h3>
    <p class="text-white/40 text-sm mb-6" id="confirmText">This action cannot be undone.</p>
    <div class="flex gap-3">
      <button class="admin-btn admin-btn-ghost flex-1" id="confirmCancel">Cancel</button>
      <button class="admin-btn admin-btn-danger flex-1" id="confirmDelete" style="background:rgba(248,113,113,0.1)">
        <i data-lucide="trash-2" class="w-4 h-4"></i> Delete
      </button>
    </div>
  </div>
</div>

<!-- Toast -->
<div id="toast" class="fixed bottom-6 right-6 z-[9998] bg-white/10 backdrop-blur-xl border border-white/20 rounded-xl px-6 py-4 text-white text-sm font-medium shadow-2xl transform translate-y-20 opacity-0 transition-all duration-400 pointer-events-none flex items-center gap-3">
  <i data-lucide="check-circle" class="w-5 h-5 text-neon-yellow"></i>
  <span id="toastMsg">Success!</span>
</div>

<script>
// ==================== DEFAULT PROPERTY DATA ====================
const defaultProperties = [
  { id: 1, title: "Skyline Tower 3BHK", location: "OMR, Chennai", type: "apartment", area: "1450 sq.ft", badge: "New", badgeColor: "signal-red", img: "", enqPhone: "+91 99626 99649", enqEmail: "pandavlogs@gmail.com", enqMsg: "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details." },
  { id: 2, title: "Palm Villa Phase II", location: "ECR, Chennai", type: "villa", area: "3200 sq.ft", badge: "Premium", badgeColor: "neon-yellow", img: "", enqPhone: "+91 99626 99649", enqEmail: "pandavlogs@gmail.com", enqMsg: "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details." },
  { id: 3, title: "DTCP Approved Plot", location: "Oragadam, Chennai", type: "plot", area: "2400 sq.ft", badge: "Hot", badgeColor: "signal-red", img: "", enqPhone: "+91 99626 99649", enqEmail: "pandavlogs@gmail.com", enqMsg: "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details." },
  { id: 4, title: "Prestige Tech Park Office", location: "Guindy, Chennai", type: "commercial", area: "2000 sq.ft", badge: "Investment", badgeColor: "neon-blue", img: "", enqPhone: "+91 99626 99649", enqEmail: "pandavlogs@gmail.com", enqMsg: "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details." },
  { id: 5, title: "Green Valley 2BHK", location: "Porur, Chennai", type: "apartment", area: "1050 sq.ft", badge: "Budget", badgeColor: "neon-yellow", img: "", enqPhone: "+91 99626 99649", enqEmail: "pandavlogs@gmail.com", enqMsg: "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details." },
  { id: 6, title: "Lake View Villa", location: "Navalur, Chennai", type: "villa", area: "2800 sq.ft", badge: "Featured", badgeColor: "neon-blue", img: "", enqPhone: "+91 99626 99649", enqEmail: "pandavlogs@gmail.com", enqMsg: "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details." },
];

// ==================== LOAD FROM LOCALSTORAGE ====================
function loadProperties() {
  const saved = localStorage.getItem('tp_properties');
  if (saved) {
    try { return JSON.parse(saved); } catch(e) {}
  }
  return JSON.parse(JSON.stringify(defaultProperties));
}

function saveProperties(data) {
  localStorage.setItem('tp_properties', JSON.stringify(data));
}

let properties = loadProperties();
let nextId = properties.length > 0 ? Math.max(...properties.map(p => p.id)) + 1 : 1;

// ==================== RENDER PROPERTY CARDS ====================
const grid = document.getElementById('propertyGrid');
const emptyState = document.getElementById('emptyState');

function getImgSrc(p) {
  if (p.img && p.img.startsWith('data:')) return p.img;
  if (p.img && !p.img.startsWith('http') && !p.img.startsWith('data:')) return p.img;
  return `https://picsum.photos/seed/${p.title.replace(/\s+/g, '-').toLowerCase()}/800/500.jpg`;
}

function buildEnquiryLink(p) {
  const phone = (p.enqPhone || '+91 99626 99649').replace(/\D/g, '');
  const msg = (p.enqMsg || "Hi, I'm interested in [PROPERTY_NAME].").replace('[PROPERTY_NAME]', p.title);
  return `https://wa.me/${phone}?text=${encodeURIComponent(msg)}`;
}

function renderProperties(filter = 'all') {
  const filtered = filter === 'all' ? properties : properties.filter(p => p.type === filter);
  grid.querySelectorAll('.property-card').forEach(c => c.classList.add('shuffle-out'));

  setTimeout(() => {
    grid.innerHTML = '';
    if (filtered.length === 0) {
      emptyState.classList.remove('hidden');
    } else {
      emptyState.classList.add('hidden');
    }

    filtered.forEach((p, i) => {
      const card = document.createElement('div');
      card.className = 'property-card shuffle-out bg-white/[0.03] border border-white/[0.06] rounded-2xl overflow-hidden cursor-pointer';
      card.innerHTML = `
        <div class="relative aspect-[16/10] overflow-hidden">
          <img src="${getImgSrc(p)}" alt="${p.title}" class="card-img w-full h-full object-cover transition-transform duration-700" style="filter: contrast(1.15) brightness(0.9);"
            onerror="this.src='https://picsum.photos/seed/${encodeURIComponent(p.title)}/800/500.jpg'">
          <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent"></div>
          ${p.badge ? `<span class="absolute top-3 left-3 bg-${p.badgeColor} text-black text-[10px] font-bold uppercase tracking-wider px-3 py-1 rounded-md">${p.badge}</span>` : ''}
          ${p.area ? `<div class="absolute bottom-3 left-3 right-3 flex justify-end items-end"><div class="text-xs text-white/60 bg-black/50 backdrop-blur-sm rounded px-2 py-1">${p.area}</div></div>` : ''}
        </div>
        <div class="p-5">
          <h3 class="text-lg font-bold text-white mb-1">${p.title}</h3>
          <div class="flex items-center gap-1.5 text-white/40 text-sm">
            <i data-lucide="map-pin" class="w-3.5 h-3.5"></i>
            <span>${p.location}</span>
          </div>
          <div class="flex items-center justify-between mt-4 pt-4 border-t border-white/5">
            <span class="text-xs text-white/30 uppercase tracking-wider">${p.type}</span>
            <a href="${buildEnquiryLink(p)}" target="_blank" class="text-signal-red text-xs font-semibold hover:underline flex items-center gap-1">
              Enquire <i data-lucide="external-link" class="w-3 h-3"></i>
            </a>
          </div>
        </div>
      `;
      grid.appendChild(card);
      setTimeout(() => {
        card.classList.remove('shuffle-out');
        card.classList.add('shuffle-in');
        lucide.createIcons();
      }, 50 + i * 60);
    });
  }, 300);
}

// Filter buttons
document.getElementById('filterBtns').addEventListener('click', (e) => {
  const btn = e.target.closest('.filter-btn');
  if (!btn) return;
  document.querySelectorAll('.filter-btn').forEach(b => {
    b.classList.remove('active', 'bg-signal-red', 'text-white');
    b.classList.add('bg-white/5', 'text-white/60', 'border', 'border-white/10');
  });
  btn.classList.add('active', 'bg-signal-red', 'text-white');
  btn.classList.remove('bg-white/5', 'text-white/60');
  renderProperties(btn.dataset.filter);
});

renderProperties();

// ==================== ADMIN PANEL LOGIC ====================
const adminOverlay = document.getElementById('adminOverlay');
const adminPanel = document.getElementById('adminPanel');
const manageFab = document.getElementById('manageFab');

function openAdmin() { adminOverlay.classList.add('active'); adminPanel.classList.add('active'); document.body.style.overflow = 'hidden'; renderAdminList(); }
function closeAdmin() { adminOverlay.classList.remove('active'); adminPanel.classList.remove('active'); document.body.style.overflow = ''; }

manageFab.addEventListener('click', openAdmin);
document.getElementById('adminClose').addEventListener('click', closeAdmin);
adminOverlay.addEventListener('click', closeAdmin);

// Tabs
document.querySelectorAll('.admin-tab').forEach(tab => {
  tab.addEventListener('click', () => {
    document.querySelectorAll('.admin-tab').forEach(t => t.classList.remove('active'));
    tab.classList.add('active');
    const target = tab.dataset.tab;
    document.getElementById('tabList').classList.toggle('hidden', target !== 'list');
    document.getElementById('tabForm').classList.toggle('hidden', target !== 'form');
    if (target === 'form' && !document.getElementById('editId').value) resetForm();
  });
});
// Tab switch buttons inside panels
document.querySelectorAll('.admin-tab-switch').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.admin-tab').forEach(t => { if (t.dataset.tab === btn.dataset.tab) t.classList.add('active'); else t.classList.remove('active'); });
    document.getElementById('tabList').classList.toggle('hidden', btn.dataset.tab !== 'list');
    document.getElementById('tabForm').classList.toggle('hidden', btn.dataset.tab !== 'form');
    resetForm();
  });
});

// Render admin property list
function renderAdminList() {
  const list = document.getElementById('adminPropertyList');
  const empty = document.getElementById('adminEmpty');
  if (properties.length === 0) { list.innerHTML = ''; empty.classList.remove('hidden'); return; }
  empty.classList.add('hidden');
  list.innerHTML = properties.map(p => `
    <div class="admin-list-item">
      <div class="flex gap-4 p-4">
        <div class="w-20 h-14 rounded-lg overflow-hidden flex-shrink-0 bg-white/5">
          <img src="${getImgSrc(p)}" alt="${p.title}" class="w-full h-full object-cover" style="filter: contrast(1.1) brightness(0.9);"
            onerror="this.src='https://picsum.photos/seed/${encodeURIComponent(p.title)}/200/140.jpg'">
        </div>
        <div class="flex-1 min-w-0">
          <h4 class="text-white font-semibold text-sm truncate">${p.title}</h4>
          <p class="text-white/30 text-xs mt-0.5">${p.location} • ${p.type} ${p.area ? '• ' + p.area : ''}</p>
          <p class="text-white/15 text-xs mt-0.5">Enquiry: ${p.enqPhone || 'Default'}</p>
        </div>
        <div class="flex flex-col gap-2 flex-shrink-0">
          <button class="admin-btn admin-btn-ghost admin-btn-sm" onclick="editProperty(${p.id})">
            <i data-lucide="pencil" class="w-3 h-3"></i> Edit
          </button>
          <button class="admin-btn admin-btn-danger admin-btn-sm" onclick="confirmDeleteProperty(${p.id})">
            <i data-lucide="trash-2" class="w-3 h-3"></i> Delete
          </button>
        </div>
      </div>
    </div>
  `).join('');
  lucide.createIcons();
}

// ==================== IMAGE UPLOAD ====================
const imgInput = document.getElementById('imgInput');
const imgPreview = document.getElementById('imgPreview');
const imgPlaceholder = document.getElementById('imgPlaceholder');
let currentImageData = '';

imgInput.addEventListener('change', function() {
  const file = this.files[0];
  if (!file) return;
  if (file.size > 3 * 1024 * 1024) { showToast('Image too large. Please use under 3MB.'); return; }
  const reader = new FileReader();
  reader.onload = function(e) {
    currentImageData = e.target.result;
    imgPreview.src = currentImageData;
    imgPreview.classList.remove('hidden');
    imgPlaceholder.classList.add('hidden');
  };
  reader.readAsDataURL(file);
});

// Drag and drop
const imgUploadZone = document.getElementById('imgUploadZone');
imgUploadZone.addEventListener('dragover', (e) => { e.preventDefault(); imgUploadZone.style.borderColor = 'rgba(227,6,19,0.6)'; imgUploadZone.style.background = 'rgba(227,6,19,0.05)'; });
imgUploadZone.addEventListener('dragleave', () => { imgUploadZone.style.borderColor = ''; imgUploadZone.style.background = ''; });
imgUploadZone.addEventListener('drop', (e) => {
  e.preventDefault(); imgUploadZone.style.borderColor = ''; imgUploadZone.style.background = '';
  const file = e.dataTransfer.files[0];
  if (file && file.type.startsWith('image/')) {
    const dt = new DataTransfer(); dt.items.add(file); imgInput.files = dt.files;
    imgInput.dispatchEvent(new Event('change'));
  }
});

// ==================== FORM: ADD / EDIT ====================
function resetForm() {
  document.getElementById('editId').value = '';
  document.getElementById('formTitle').value = '';
  document.getElementById('formLocation').value = '';
  document.getElementById('formType').value = '';
  document.getElementById('formArea').value = '';
  document.getElementById('formBadge').value = '';
  document.getElementById('formBadgeColor').value = 'signal-red';
  document.getElementById('formEnqPhone').value = '+91 99626 99649';
  document.getElementById('formEnqEmail').value = 'pandavlogs@gmail.com';
  document.getElementById('formEnqMsg').value = "Hi Teekaraman, I'm interested in [PROPERTY_NAME]. Please share details.";
  currentImageData = '';
  imgPreview.classList.add('hidden'); imgPreview.src = '';
  imgPlaceholder.classList.remove('hidden');
  imgInput.value = '';
  document.getElementById('formSubmitBtn').innerHTML = '<i data-lucide="plus" class="w-4 h-4"></i><span>Add Property</span>';
  lucide.createIcons();
}

function editProperty(id) {
  const p = properties.find(x => x.id === id);
  if (!p) return;
  // Switch to form tab
  document.querySelectorAll('.admin-tab').forEach(t => { t.dataset.tab === 'form' ? t.classList.add('active') : t.classList.remove('active'); });
  document.getElementById('tabList').classList.add('hidden');
  document.getElementById('tabForm').classList.remove('hidden');

  document.getElementById('editId').value = p.id;
  document.getElementById('formTitle').value = p.title;
  document.getElementById('formLocation').value = p.location;
  document.getElementById('formType').value = p.type;
  document.getElementById('formArea').value = p.area || '';
  document.getElementById('formBadge').value = p.badge || '';
  document.getElementById('formBadgeColor').value = p.badgeColor || 'signal-red';
  document.getElementById('formEnqPhone').value = p.enqPhone || '+91 99626 99649';
  document.getElementById('formEnqEmail').value = p.enqEmail || 'pandavlogs@gmail.com';
  document.getElementById('formEnqMsg').value = p.enqMsg || "Hi, I'm interested in [PROPERTY_NAME].";

  if (p.img && p.img.startsWith('data:')) {
    currentImageData = p.img;
    imgPreview.src = p.img;
    imgPreview.classList.remove('hidden');
    imgPlaceholder.classList.add('hidden');
  } else {
    currentImageData = p.img || '';
    imgPreview.classList.add('hidden');
    imgPlaceholder.classList.remove('hidden');
    if (p.img) imgPlaceholder.innerHTML = `<i data-lucide="image" class="w-10 h-10 text-neon-blue/50 mx-auto mb-2"></i><p class="text-neon-blue/60 text-sm">Using file: ${p.img}</p><p class="text-white/20 text-xs mt-1">Upload new to replace</p>`;
    else imgPlaceholder.innerHTML = `<i data-lucide="image-plus" class="w-10 h-10 text-white/20 mx-auto mb-2"></i><p class="text-white/30 text-sm">Click or drag image here</p><p class="text-white/15 text-xs mt-1">JPG, PNG — under 2MB recommended</p>`;
    lucide.createIcons();
  }

  document.getElementById('formSubmitBtn').innerHTML = '<i data-lucide="check" class="w-4 h-4"></i><span>Update Property</span>';
  lucide.createIcons();
}

document.getElementById('formCancelBtn').addEventListener('click', () => {
  document.querySelectorAll('.admin-tab').forEach(t => { t.dataset.tab === 'list' ? t.classList.add('active') : t.classList.remove('active'); });
  document.getElementById('tabList').classList.remove('hidden');
  document.getElementById('tabForm').classList.add('hidden');
  resetForm();
});

document.getElementById('propertyForm').addEventListener('submit', function(e) {
  e.preventDefault();
  const editId = document.getElementById('editId').value;
  const data = {
    title: document.getElementById('formTitle').value.trim(),
    location: document.getElementById('formLocation').value.trim(),
    type: document.getElementById('formType').value,
    area: document.getElementById('formArea').value.trim(),
    badge: document.getElementById('formBadge').value.trim(),
    badgeColor: document.getElementById('formBadgeColor').value,
    enqPhone: document.getElementById('formEnqPhone').value.trim() || '+91 99626 99649',
    enqEmail: document.getElementById('formEnqEmail').value.trim() || 'pandavlogs@gmail.com',
    enqMsg: document.getElementById('formEnqMsg').value.trim() || "Hi, I'm interested in [PROPERTY_NAME].",
    img: currentImageData || (editId ? (properties.find(p => p.id == editId)?.img || '') : ''),
  };

  if (!data.title || !data.location || !data.type) { showToast('Please fill in Title, Location, and Type.'); return; }

  if (editId) {
    const idx = properties.findIndex(p => p.id == editId);
    if (idx > -1) { data.id = parseInt(editId); properties[idx] = data; }
    showToast('Property updated successfully!');
  } else {
    data.id = nextId++;
    properties.push(data);
    showToast('Property added successfully!');
  }

  saveProperties(properties);
  renderProperties(getCurrentFilter());
  renderAdminList();
  resetForm();

  // Switch back to list
  document.querySelectorAll('.admin-tab').forEach(t => { t.dataset.tab === 'list' ? t.classList.add('active') : t.classList.remove('active'); });
  document.getElementById('tabList').classList.remove('hidden');
  document.getElementById('tabForm').classList.add('hidden');
});

function getCurrentFilter() {
  const active = document.querySelector('.filter-btn.active');
  return active ? active.dataset.filter : 'all';
}

// ==================== DELETE ====================
let deleteTargetId = null;

function confirmDeleteProperty(id) {
  deleteTargetId = id;
  const p = properties.find(x => x.id === id);
  document.getElementById('confirmText').textContent = `Delete "${p?.title}"? This cannot be undone.`;
  document.getElementById('confirmModal').classList.add('active');
}

document.getElementById('confirmCancel').addEventListener('click', () => {
  document.getElementById('confirmModal').classList.remove('active');
  deleteTargetId = null;
});

document.getElementById('confirmDelete').addEventListener('click', () => {
  if (deleteTargetId !== null) {
    properties = properties.filter(p => p.id !== deleteTargetId);
    saveProperties(properties);
    renderProperties(getCurrentFilter());
    renderAdminList();
    showToast('Property deleted.');
  }
  document.getElementById('confirmModal').classList.remove('active');
  deleteTargetId = null;
});

// ==================== TYPEWRITER ====================
const typewriterEl = document.getElementById('newsletterEmail');
const cursorEl = document.getElementById('typewriterCursor');
const pitches = ["yourname@email.com", "get weekly property picks...", "exclusive deals, first access...", "no spam, just real estate..."];
let pitchIdx = 0, charIdx = 0, isDeleting = false, typewriterTimeout;
function typewrite() {
  const c = pitches[pitchIdx];
  if (!isDeleting) { typewriterEl.placeholder = c.substring(0, charIdx + 1); charIdx++; if (charIdx === c.length) { isDeleting = true; typewriterTimeout = setTimeout(typewrite, 2000); return; } typewriterTimeout = setTimeout(typewrite, 80); }
  else { typewriterEl.placeholder = c.substring(0, charIdx - 1); charIdx--; if (charIdx === 0) { isDeleting = false; pitchIdx = (pitchIdx + 1) % pitches.length; typewriterTimeout = setTimeout(typewrite, 400); return; } typewriterTimeout = setTimeout(typewrite, 40); }
}
typewrite();
typewriterEl.addEventListener('focus', () => { cursorEl.style.display = 'none'; clearTimeout(typewriterTimeout); typewriterEl.placeholder = ''; });
typewriterEl.addEventListener('blur', () => { cursorEl.style.display = 'inline-block'; typewrite(); });

// ==================== NEWSLETTER ====================
document.getElementById('newsletterForm').addEventListener('submit', function(e) {
  e.preventDefault();
  const name = document.getElementById('newsletterName').value.trim();
  const email = document.getElementById('newsletterEmail').value.trim();
  const msgEl = document.getElementById('newsletterMsg');
  const btn = document.getElementById('newsletterBtn');
  if (!email) { msgEl.className = 'text-center py-3 rounded-xl text-sm font-medium bg-signal-red/10 text-signal-red border border-signal-red/20'; msgEl.textContent = 'Please enter your email.'; msgEl.classList.remove('hidden'); return; }
  btn.innerHTML = '<span class="animate-pulse">Subscribing...</span>'; btn.disabled = true;
  setTimeout(() => {
    btn.innerHTML = '<span>Subscribed!</span><svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>';
    btn.classList.remove('bg-signal-red','hover:bg-signal-redHover'); btn.classList.add('bg-green-600');
    msgEl.className = 'text-center py-3 rounded-xl text-sm font-medium bg-green-600/10 text-green-400 border border-green-600/20';
    msgEl.textContent = `Welcome${name ? ', ' + name : ''}! Check your inbox.`; msgEl.classList.remove('hidden');
    showToast('Subscribed!');
    setTimeout(() => { btn.innerHTML = '<span>Subscribe</span><svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h14M12 5l7 7-7 7"/></svg>'; btn.classList.add('bg-signal-red','hover:bg-signal-redHover'); btn.classList.remove('bg-green-600'); btn.disabled = false; document.getElementById('newsletterName').value = ''; document.getElementById('newsletterEmail').value = ''; }, 3000);
  }, 1200);
});

// ==================== TOAST ====================
function showToast(msg) { const t = document.getElementById('toast'); document.getElementById('toastMsg').textContent = msg; t.style.transform = 'translateY(0)'; t.style.opacity = '1'; t.style.pointerEvents = 'auto'; setTimeout(() => { t.style.transform = 'translateY(20px)'; t.style.opacity = '0'; t.style.pointerEvents = 'none'; }, 3500); }

// ==================== SCROLL EFFECTS ====================
const nav = document.getElementById('mainNav');
const brandColors = { 'signal-red': { accent: '#E30613', glow: 'rgba(227,6,19,0.3)' }, 'neon-blue': { accent: '#00D4FF', glow: 'rgba(0,212,255,0.3)' }, 'neon-yellow': { accent: '#D4FF00', glow: 'rgba(212,255,0,0.3)' } };
const obs = new IntersectionObserver((entries) => { entries.forEach(entry => { if (entry.isIntersecting) { const c = brandColors[entry.target.dataset.brand]; if (c) { nav.style.borderBottomColor = c.accent + '20'; nav.style.boxShadow = `0 4px 30px ${c.glow}`; } } }); }, { threshold: 0.3 });
document.querySelectorAll('.section-zone').forEach(s => obs.observe(s));

const fadeObs = new IntersectionObserver((entries) => { entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); }); }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
document.querySelectorAll('.fade-up').forEach(el => fadeObs.observe(el));

document.getElementById('mobileMenuBtn').addEventListener('click', () => { document.getElementById('mobileMenu').classList.toggle('hidden'); });
document.querySelectorAll('#mobileMenu a').forEach(l => l.addEventListener('click', () => { document.getElementById('mobileMenu').classList.add('hidden'); }));
window.addEventListener('scroll', () => { nav.style.background = window.pageYOffset > 100 ? 'rgba(0,0,0,0.85)' : 'rgba(0,0,0,0.7)'; });

lucide.createIcons();
</script>
</body>
</html>
