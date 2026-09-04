!doctype html>
<html lang="tr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#0b0b09">
<meta name="description" content="PARLE — Modern gastronomi, zamansız bir atmosfer ve unutulmaz sofralar.">
<title>PARLE — Dining, Reimagined</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300&family=Playfair+Display:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
<style>
:root{--bg:#0a0a08;--paper:#eee9df;--muted:#a9a398;--line:rgba(238,233,223,.16);--gold:#c6aa78;--ease:cubic-bezier(.16,1,.3,1)}
*{box-sizing:border-box}html{scroll-behavior:smooth}body{margin:0;background:var(--bg);color:var(--paper);font-family:"DM Sans",sans-serif;font-weight:300;overflow-x:hidden}body.lock{overflow:hidden}a{color:inherit;text-decoration:none}button{font:inherit;color:inherit}

/* Custom Cursor & Noise */
.noise{position:fixed;inset:0;z-index:50;pointer-events:none;opacity:.035;background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 180 180' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E")}
.cursor{position:fixed;width:18px;height:18px;border:1px solid rgba(255,255,255,.65);border-radius:50%;pointer-events:none;z-index:1000;transform:translate(-50%,-50%);transition:width .25s,height .25s,background .25s;mix-blend-mode:difference}
.cursor.big{width:72px;height:72px;background:#fff}

/* Preloader */
.preloader{position:fixed;inset:0;z-index:999;background:#090907;display:grid;place-items:center;transition:opacity 1s var(--ease),visibility 1s}
.preloader.hide{opacity:0;visibility:hidden}
.loader{width:min(360px,70vw);text-align:center}
.loader-brand{font-family:"Playfair Display",serif;font-size:clamp(52px,10vw,110px);letter-spacing:.18em;margin-left:.18em;font-weight:400}
.loader-line{height:1px;background:#292923;margin-top:28px;overflow:hidden}
.loader-line span{display:block;width:0;height:100%;background:var(--paper);transition:width 1.6s var(--ease)}
.loader-meta{display:flex;justify-content:space-between;margin-top:12px;font-size:9px;letter-spacing:.22em;text-transform:uppercase;color:#77736b}

/* Topbar & Mobile Nav */
.topbar{position:fixed;z-index:100;left:0;right:0;top:0;height:84px;padding:0 4vw;display:flex;align-items:center;justify-content:space-between;background:linear-gradient(#080806cc,transparent);transition:.5s var(--ease)}
.topbar.scrolled{height:68px;background:#090907ee;backdrop-filter:blur(14px);border-bottom:1px solid var(--line)}
.brand{font-family:"Playfair Display",serif;font-size:28px;letter-spacing:.2em;margin-left:.2em}
.nav{display:flex;gap:34px;font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:#c6c1b8}
.nav a{transition:.3s}.nav a:hover{color:#fff}
.top-cta{border:1px solid var(--line);border-radius:100px;padding:11px 18px;font-size:9px;letter-spacing:.2em;text-transform:uppercase;cursor:pointer;background:none;transition:.35s}
.top-cta:hover{background:var(--paper);color:#0b0b09}
.menu-toggle{display:none;border:0;background:none;color:#fff;font-size:24px;cursor:pointer;z-index:101}
.mobile-overlay{position:fixed;inset:0;background:#090907;z-index:99;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:30px;opacity:0;pointer-events:none;transition:.5s var(--ease)}
.mobile-overlay.open{opacity:1;pointer-events:all}
.mobile-overlay a{font-family:"Playfair Display",serif;font-size:32px;letter-spacing:.1em;color:var(--paper)}

/* Immersive Hero Video Canvas */
.hero{height:100svh;min-height:720px;position:relative;display:grid;place-items:center;overflow:hidden}
.hero-video-wrap{position:absolute;inset:-5%;overflow:hidden}
.hero-video-wrap video{width:100%;height:100%;object-fit:cover;transform:scale(1.08);will-change:transform;transition:transform .1s linear;filter:brightness(.6) contrast(1.1)}
.hero-vignette{position:absolute;inset:0;background:radial-gradient(circle at center,rgba(0,0,0,0.2) 0%,#050504 90%)}
.hero-center{position:relative;z-index:4;text-align:center;max-width:820px;padding:0 24px;transform:translateY(2vh)}
.kicker{font-size:9px;letter-spacing:.5em;text-transform:uppercase;color:var(--gold);margin-bottom:26px}
.hero h1{font-family:"Playfair Display",serif;font-size:clamp(86px,16vw,230px);font-weight:400;line-height:.72;letter-spacing:.06em;margin:0 0 35px}
.hero-copy{font-size:12px;line-height:1.9;color:#c4c0b8;max-width:470px;margin:0 auto 35px}
.pill{display:inline-flex;align-items:center;gap:16px;border:1px solid #ffffff48;border-radius:100px;padding:15px 24px;font-size:9px;letter-spacing:.22em;text-transform:uppercase;transition:.4s var(--ease);background:rgba(255,255,255,0.05);backdrop-filter:blur(10px)}
.pill:hover{background:#f1ece2;color:#0a0a08;transform:translateY(-3px)}
.scroll-note{position:absolute;z-index:5;bottom:28px;left:4vw;font-size:8px;letter-spacing:.3em;text-transform:uppercase;color:#8c877e;display:flex;gap:12px;align-items:center}
.scroll-note i{width:42px;height:1px;background:#8c877e}

/* Floating Interactive Dishes (3D Depth) */
.side-dishes{position:absolute;inset:0;z-index:3;pointer-events:none}
.dish{position:absolute;width:min(245px,18vw);aspect-ratio:.72;overflow:hidden;border:1px solid #ffffff25;background:#10100e;box-shadow:0 25px 70px #00000080;transition:transform .8s var(--ease),border-color .4s;pointer-events:all;cursor:pointer}
.dish:after{content:"";position:absolute;inset:0;background:linear-gradient(0deg,#070706f5 0%,transparent 60%)}
.dish img{width:100%;height:100%;object-fit:cover;filter:saturate(.82);transition:transform 1.1s var(--ease)}
.dish:hover img{transform:scale(1.1)}
.dish-info{position:absolute;z-index:2;left:18px;right:18px;bottom:17px}
.dish-tag{font-size:8px;letter-spacing:.2em;text-transform:uppercase;color:var(--gold)}
.dish-name{font-family:"Playfair Display",serif;font-size:24px;margin-top:5px}
.dish-price{font-size:9px;color:#aaa59b;margin-top:4px}
.d1{left:3.3vw;top:20%;transform:rotate(-6deg)}
.d2{left:9vw;bottom:7%;transform:rotate(5deg) scale(.82)}
.d3{right:3.3vw;top:20%;transform:rotate(6deg)}
.d4{right:9vw;bottom:7%;transform:rotate(-5deg) scale(.82)}

/* General Sections */
.section{padding:150px 7vw}
.section-head{display:flex;justify-content:space-between;gap:40px;align-items:flex-end;margin-bottom:70px}
.eyebrow{font-size:9px;letter-spacing:.34em;text-transform:uppercase;color:#958d80;margin-bottom:18px}
.display{font-family:"Playfair Display",serif;font-size:clamp(54px,7vw,110px);font-weight:400;line-height:.9;margin:0;letter-spacing:-.02em}
.intro{display:grid;grid-template-columns:1.1fr .9fr;gap:10vw;align-items:end}
.intro-copy{font-size:18px;line-height:1.7;color:#c5c0b7;max-width:590px}
.micro{font-size:10px;line-height:1.9;color:#817c74}

/* Interactive Tour (Video Walkthrough) Section */
.tour-section{position:relative;padding:0;height:100vh;background:#000;display:grid;place-items:center;overflow:hidden}
.tour-video{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.5}
.tour-overlay{position:relative;z-index:2;text-align:center;max-width:700px;padding:0 20px}

/* Menu Section with 3D Tilt Cards */
.menu-section{background:#0d0d0b}
.filters{display:flex;gap:10px;flex-wrap:wrap}
.filter{border:1px solid var(--line);background:transparent;padding:10px 16px;border-radius:100px;font-size:9px;letter-spacing:.16em;text-transform:uppercase;cursor:pointer;color:var(--paper);transition:.3s}
.filter.active,.filter:hover{background:var(--paper);color:#0a0a08}
.menu-grid{display:grid;grid-template-columns:repeat(12,1fr);gap:20px}
.card{position:relative;overflow:hidden;background:#151512;min-height:450px;grid-column:span 4;border:1px solid var(--line);transform-style:preserve-3d;perspective:1000px;transition:transform .2s ease-out, border-color .3s}
.card:hover{border-color:var(--gold)}
.card.wide{grid-column:span 6}
.card:nth-child(2){margin-top:70px}
.card:nth-child(5){margin-top:-45px}
.card-media{height:100%;min-height:450px;overflow:hidden}
.card img{width:100%;height:100%;object-fit:cover;filter:saturate(.8);transition:1s var(--ease)}
.card:hover img{transform:scale(1.08)}
.card:after{content:"";position:absolute;inset:0;background:linear-gradient(transparent 30%,#050504e8 90%)}
.card-content{position:absolute;z-index:2;left:28px;right:28px;bottom:28px;transform:translateZ(30px)}
.card-index{font-size:9px;color:var(--gold);letter-spacing:.15em}
.card h3{font-family:"Playfair Display",serif;font-size:38px;font-weight:400;margin:6px 0}
.card p{font-size:10px;color:#bbb6ad;margin:0;line-height:1.6}

/* Experience & Stats */
.experience{display:grid;grid-template-columns:.85fr 1.15fr;gap:8vw;align-items:center}
.experience-photo{height:720px;overflow:hidden;position:relative}
.experience-photo img{width:100%;height:100%;object-fit:cover;transform:scale(1.05);transition:1.2s var(--ease)}
.experience-photo:hover img{transform:scale(1)}
.quote{font-family:"Playfair Display",serif;font-size:clamp(24px,3vw,42px);line-height:1.3;color:#d9d2c7;margin:35px 0;font-style:italic}
.stat-row{display:grid;grid-template-columns:repeat(3,1fr);border-top:1px solid var(--line);margin-top:55px}
.stat{padding:25px 20px 0 0;border-right:1px solid var(--line)}
.stat:last-child{border:0;padding-left:20px}
.stat b{display:block;font-family:"Playfair Display",serif;font-size:42px;font-weight:400;color:var(--paper)}
.stat span{font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:#8f8a82}

/* Reservation CTA Section */
.reserve-section{min-height:85vh;display:grid;place-items:center;text-align:center;position:relative;overflow:hidden;background:linear-gradient(#050504aa,#050504e8),url('https://images.unsplash.com/photo-1414235077428-338989a2e8c0?auto=format&fit=crop&w=2400&q=90') center/cover fixed}
.reserve-section .display{font-size:clamp(60px,10vw,150px)}
.reserve-section p{color:#bbb6ad;max-width:470px;line-height:1.8;margin:25px auto 35px}

/* Footer & Modals */
.footer{padding:80px 7vw 25px;background:#070706}
.footer-main{display:flex;justify-content:space-between;gap:60px;padding-bottom:80px}
.footer-brand{font-family:"Playfair Display",serif;font-size:78px;letter-spacing:.08em}
.footer-cols{display:flex;gap:80px}
.footer h4{font-size:9px;letter-spacing:.22em;text-transform:uppercase;font-weight:500;margin:0 0 16px;color:var(--gold)}
.footer p,.footer a{font-size:11px;color:#88847d;line-height:1.9;margin:0}
.footer a:hover{color:#eee}
.footer-bottom{border-top:1px solid var(--line);padding-top:20px;display:flex;justify-content:space-between;font-size:9px;color:#67635d;letter-spacing:.08em}

.reveal{opacity:0;transform:translateY(45px);transition:opacity 1s var(--ease),transform 1s var(--ease)}
.reveal.visible{opacity:1;transform:none}

.modal{position:fixed;inset:0;z-index:800;background:#050504d9;backdrop-filter:blur(18px);display:none;place-items:center;padding:20px}
.modal.open{display:grid}
.modal-box{width:min(680px,100%);background:#12120f;border:1px solid var(--line);padding:42px;position:relative;box-shadow:0 40px 120px #000}
.close{position:absolute;right:20px;top:18px;border:0;background:none;font-size:24px;cursor:pointer;color:#aaa}
.modal-title{font-family:"Playfair Display",serif;font-size:48px;font-weight:400;margin:0 0 8px}
.form{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:30px}
.field{display:flex;flex-direction:column;gap:8px}
.field.full{grid-column:1/-1}
.field label{font-size:8px;letter-spacing:.18em;text-transform:uppercase;color:#8f8a81}
.field input,.field select{border:1px solid var(--line);background:#0c0c0a;color:#eee;padding:14px;outline:0}
.submit{grid-column:1/-1;border:1px solid #eee;background:#eee;color:#0b0b09;padding:15px;cursor:pointer;letter-spacing:.18em;text-transform:uppercase;font-size:9px;transition:.3s}
.submit:hover{background:var(--gold);border-color:var(--gold);color:#000}
.toast{position:fixed;z-index:900;right:24px;bottom:24px;background:var(--paper);color:#111;padding:15px 20px;font-size:10px;letter-spacing:.1em;transform:translateY(120px);transition:.5s var(--ease)}
.toast.show{transform:none}

/* Media Queries */
@media(max-width:1050px){
  .nav{display:none}.menu-toggle{display:block}
  .dish{width:180px}.d2,.d4{display:none}
  .intro,.experience{grid-template-columns:1fr}
  .experience-photo{height:520px}.footer-cols{gap:35px}
}
@media(max-width:700px){
  .topbar{height:68px}.brand{font-size:23px}.top-cta{display:none}
  .hero{min-height:760px}.hero-center{padding:0 24px}.hero h1{font-size:76px}
  .hero-copy{font-size:11px}
  .dish{width:120px;aspect-ratio:.7}
  .d1{left:-20px;top:20%}.d3{right:-20px;top:20%}
  .dish-info{left:10px;right:10px;bottom:10px}.dish-name{font-size:16px}.dish-price{display:none}
  .section{padding:90px 6vw}.section-head{display:block;margin-bottom:45px}.filters{margin-top:25px}
  .menu-grid{display:block}.card,.card.wide{height:420px;min-height:420px;margin:0 0 16px!important}
  .experience-photo{height:380px}.stat b{font-size:32px}
  .footer-main{display:block}.footer-brand{font-size:55px;margin-bottom:45px}
  .footer-cols{display:grid;grid-template-columns:1fr 1fr}.footer-bottom{display:block;line-height:2}
  .form{grid-template-columns:1fr}.field.full,.submit{grid-column:auto}
  .modal-box{padding:30px 20px}.modal-title{font-size:36px}.cursor{display:none}
}
</style>
</head>
<body class="lock">
<div class="noise"></div>
<div class="cursor" id="cursor"></div>

<div class="preloader" id="preloader">
  <div class="loader">
    <div class="loader-brand">PARLE</div>
    <div class="loader-line"><span id="loadbar"></span></div>
    <div class="loader-meta"><span>Maison de cuisine</span><span id="loadpct">00</span></div>
  </div>
</div>

<div class="mobile-overlay" id="mobileNav">
  <a href="#story" onclick="toggleMobileMenu()">Hikâye</a>
  <a href="#tour" onclick="toggleMobileMenu()">Atmosfer</a>
  <a href="#menu" onclick="toggleMobileMenu()">Menü</a>
  <a href="#experience" onclick="toggleMobileMenu()">Deneyim</a>
  <a href="#contact" onclick="toggleMobileMenu()">İletişim</a>
</div>

<header class="topbar" id="topbar">
  <a class="brand" href="#top">PARLE</a>
  <nav class="nav">
    <a href="#story">Hikâye</a>
    <a href="#tour">Atmosfer</a>
    <a href="#menu">Menü</a>
    <a href="#experience">Deneyim</a>
    <a href="#contact">İletişim</a>
  </nav>
  <button class="top-cta" data-open>Rezervasyon</button>
  <button class="menu-toggle" id="menuBtn" aria-label="Menüyü aç/kapat">☰</button>
</header>

<main id="top">
  <section class="hero">
    <div class="hero-video-wrap">
      <video id="heroVideo" autoplay loop muted playsinline poster="https://images.unsplash.com/photo-1515003197210-e0cd71810b5f?auto=format&fit=crop&w=2400&q=90">
        <source src="https://assets.mixkit.co/videos/preview/mixkit-top-view-of-a-restaurant-table-with-food-41619-large.mp4" type="video/mp4">
      </video>
    </div>
    <div class="hero-vignette"></div>

    <div class="side-dishes" id="dishes">
      <article class="dish d1"><img src="https://images.unsplash.com/photo-1547592180-85f173990554?auto=format&fit=crop&w=900&q=85" alt="Burrata"><div class="dish-info"><div class="dish-tag">01 · Başlangıç</div><div class="dish-name">Burrata</div><div class="dish-price">Mevsim Dokunuşu</div></div></article>
      <article class="dish d2"><img src="https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=900&q=85" alt="Prime Cut"><div class="dish-info"><div class="dish-tag">02 · Ana Yemek</div><div class="dish-name">Prime Cut</div><div class="dish-price">Şef Seçimi</div></div></article>
      <article class="dish d3"><img src="https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?auto=format&fit=crop&w=900&q=85" alt="Signature"><div class="dish-info"><div class="dish-tag">03 · İmza</div><div class="dish-name">Signature</div><div class="dish-price">Parle Dokunuşu</div></div></article>
      <article class="dish d4"><img src="https://images.unsplash.com/photo-1551024506-0bccd828d307?auto=format&fit=crop&w=900&q=85" alt="Tatlı"><div class="dish-info"><div class="dish-tag">04 · Tatlı</div><div class="dish-name">Paris-Brest</div><div class="dish-price">Final Dokunuşu</div></div></article>
    </div>

    <div class="hero-center">
      <div class="kicker">Dining · Art · Atmosphere</div>
      <h1>PARLE</h1>
      <p class="hero-copy">Lüksün ve lezzetin buluştuğu zamansız bir atmosfer. Sizi gastronominin derinliklerine davet ediyoruz.</p>
      <a href="#menu" class="pill">Menüyü Keşfet <span>↗</span></a>
    </div>
    <div class="scroll-note"><i></i> Kaydırın</div>
  </section>

  <section class="section" id="story">
    <div class="intro reveal">
      <div>
        <div class="eyebrow">01 · Felsefe</div>
        <h2 class="display">Sofranın<br>ötesinde.</h2>
      </div>
      <div>
        <p class="intro-copy">Parle, sıradan bir akşam yemeğinin ötesinde duygulara hitap eden bir sahnedir. Işık, mimari, servis ve tatlar uyum içinde hareket eder.</p>
        <p class="micro">Her tabak mevsime göre şekillenir. İçeri adım attığınız andan itibaren zamanın ritmi değişir.</p>
      </div>
    </div>
  </section>

  <section class="tour-section" id="tour">
    <video autoplay loop muted playsinline class="tour-video">
      <source src="https://assets.mixkit.co/videos/preview/mixkit-chef-preparing-a-dish-in-a-restaurant-kitchen-41615-large.mp4" type="video/mp4">
    </video>
    <div class="hero-vignette"></div>
    <div class="tour-overlay reveal">
      <div class="eyebrow" style="color:var(--gold)">02 · İç Mekân & Mutfak</div>
      <h2 class="display" style="font-size:clamp(40px,6vw,90px)">Açık Mutfak,<br>Canlı Ritme Şahit Olun.</h2>
      <p style="color:#ccc; margin-top:20px;">Şeflerimizin tutkulu çalışmalarına ve restoranın sıcak atmosferine yakından göz atın.</p>
    </div>
  </section>

  <section class="section menu-section" id="menu">
    <div class="section-head reveal">
      <div>
        <div class="eyebrow">03 · Mutfak</div>
        <h2 class="display">Parle<br>Seçkisi.</h2>
      </div>
      <div class="filters">
        <button class="filter active" data-filter="all">Tümü</button>
        <button class="filter" data-filter="start">Başlangıç</button>
        <button class="filter" data-filter="main">Ana Yemek</button>
        <button class="filter" data-filter="dessert">Tatlı</button>
      </div>
    </div>

    <div class="menu-grid" id="menuGrid">
      <article class="card wide reveal" data-cat="start">
        <div class="card-media"><img src="https://images.unsplash.com/photo-1547592180-85f173990554?auto=format&fit=crop&w=1400&q=90" alt="Burrata"></div>
        <div class="card-content"><span class="card-index">01 / STARTER</span><h3>Taze Burrata</h3><p>Konfi domatesler, taze fesleğen yağı ve sızma zeytinyağı</p></div>
      </article>
      <article class="card reveal" data-cat="main">
        <div class="card-media"><img src="https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=1200&q=90" alt="Prime Cut"></div>
        <div class="card-content"><span class="card-index">02 / MAIN</span><h3>Prime Cut Ribeye</h3><p>Közlenmiş mevsim sebzeleri, özel demi-glace sos</p></div>
      </article>
      <article class="card reveal" data-cat="main">
        <div class="card-media"><img src="https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?auto=format&fit=crop&w=1200&q=90" alt="Signature Pizza"></div>
        <div class="card-content"><span class="card-index">03 / SIGNATURE</span><h3>Trüflü Signature</h3><p>Özel hamur, trüf kreması, yaban mantarları</p></div>
      </article>
      <article class="card reveal" data-cat="start">
        <div class="card-media"><img src="https://images.unsplash.com/photo-1540420773420-3366772f4999?auto=format&fit=crop&w=1200&q=90" alt="Garden Salad"></div>
        <div class="card-content"><span class="card-index">04 / STARTER</span><h3>Garden Greens</h3><p>Mevsim yeşillikleri, narenciye sosu ve kıtır ceviz</p></div>
      </article>
      <article class="card wide reveal" data-cat="dessert">
        <div class="card-media"><img src="https://images.unsplash.com/photo-1551024506-0bccd828d307?auto=format&fit=crop&w=1400&q=90" alt="Paris-Brest"></div>
        <div class="card-content"><span class="card-index">05 / DESSERT</span><h3>Paris-Brest</h3><p>Kavrulmuş fındık pralini, pralin krema ve karamel</p></div>
      </article>
    </div>
  </section>

  <section class="section" id="experience">
    <div class="experience">
      <div class="experience-photo reveal">
        <img src="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1500&q=90" alt="Parle Atmosfer">
      </div>
      <div class="experience-copy reveal">
        <div class="eyebrow">04 · Deneyim</div>
        <h2 class="display">Gecenin<br>Ruhu.</h2>
        <p class="quote">“Bazı akşamlar sadece yemek yemek için değil, unutulmaz kılınmak için yaşanır.”</p>
        <p class="micro">Loş ışıklar, özenle seçilmiş müzikler ve kusursuz servis. Parle'da her detay duyularınıza hitap etmek için tasarlandı.</p>
        <div class="stat-row">
          <div class="stat"><b>01</b><span>Özel Atmosfer</span></div>
          <div class="stat"><b>24</b><span>Mevsimsel Lezzet</span></div>
          <div class="stat"><b>100%</b><span>Unutulmaz Anlar</span></div>
        </div>
      </div>
    </div>
  </section>

  <section class="reserve-section" id="reservation">
    <div class="reveal">
      <div class="eyebrow">05 · Rezervasyon</div>
      <h2 class="display">Masanızı<br>Ayırın.</h2>
      <p>Bu eşsiz lezzet ve atmosfer deneyiminin bir parçası olun. Tarihinizi belirleyin, gerisini bize bırakın.</p>
      <button class="pill" data-open>Rezervasyon Oluştur <span>→</span></button>
    </div>
  </section>
</main>

<footer class="footer" id="contact">
  <div class="footer-main">
    <div class="footer-brand">PARLE</div>
    <div class="footer-cols">
      <div><h4>Lokasyon</h4><p>Parle Restaurant<br>İstanbul / Türkiye</p></div>
      <div><h4>İletişim</h4><p><a href="tel:+905426464219">+90 542 646 42 19</a><br>Her Gün · 12:00 — 00:00</p></div>
      <div><h4>Sosyal Medya</h4><p><a href="#">Instagram</a><br><a href="#">Google</a></p></div>
    </div>
  </div>
  <div class="footer-bottom">
    <span>© 2026 PARLE MAISON</span>
    <span>Gastronomy with Intention.</span>
  </div>
</footer>

<div class="modal" id="modal" aria-hidden="true">
  <div class="modal-box">
    <button class="close" id="close" aria-label="Kapat">×</button>
    <div class="eyebrow">PARLE · MAISON</div>
    <h2 class="modal-title">Masa Ayır.</h2>
    <div class="micro">Bilgilerinizi bırakın, ekibimiz talebinizi onaylamak için iletişime geçsin.</div>
    <form class="form" id="booking">
      <div class="field"><label>Ad Soyad</label><input required name="name" placeholder="Adınız Soyadınız"></div>
      <div class="field"><label>Kişi Sayısı</label><select name="people"><option>2 Kişi</option><option>3 Kişi</option><option>4 Kişi</option><option>5+ Kişi</option></select></div>
      <div class="field"><label>Tarih</label><input required type="date" name="date"></div>
      <div class="field"><label>Saat</label><select name="time"><option>19:00</option><option>19:30</option><option>20:00</option><option>20:30</option><option>21:00</option></select></div>
      <div class="field full"><label>Özel İstekler</label><input name="note" placeholder="Diyet kısıtlamaları veya özel kutlamalar..."></div>
      <button class="submit" type="submit">Rezervasyon Talebi Gönder</button>
    </form>
  </div>
</div>

<div class="toast" id="toast">Talebiniz başarıyla alındı. Parle ekibi en kısa sürede sizinle iletişime geçecektir.</div>

<script>
const $=s=>document.querySelector(s), $$=s=>[...document.querySelectorAll(s)];

// Preloader Script
const pre=$('#preloader'), bar=$('#loadbar'), pct=$('#loadpct');
let p=0;
const timer=setInterval(()=>{
  p=Math.min(100,p+Math.floor(Math.random()*14)+7);
  bar.style.width=p+'%';
  pct.textContent=String(p).padStart(2,'0');
  if(p>=100){
    clearInterval(timer);
    setTimeout(()=>{pre.classList.add('hide');document.body.classList.remove('lock')},350);
  }
},80);

// Video Zoom / Paralaks Efekti (Sayfa Kaydırıldıkça Mekana Yakınlaşma)
const heroVideo = $('#heroVideo');
const topbar = $('#topbar');
const dishes = $$('#dishes .dish');

window.addEventListener('scroll', ()=>{
  const scrollY = window.scrollY;
  topbar.classList.toggle('scrolled', scrollY > 40);
  
  if(heroVideo) {
    // Sayfa aşağı kaydırıldıkça videoyu yumuşakça büyütüp mekanın içine girme hissi oluşturur
    const scale = 1.08 + (scrollY * 0.0005);
    heroVideo.style.transform = `scale(${Math.min(scale, 1.45)}) translateY(${scrollY * 0.05}px)`;
  }
}, {passive:true});

// Custom Cursor
const cursor=$('#cursor');
addEventListener('pointermove',e=>{
  cursor.style.left=e.clientX+'px';
  cursor.style.top=e.clientY+'px';
});
$$('a, button, .dish, .card').forEach(el=>{
  el.addEventListener('mouseenter',()=>cursor.classList.add('big'));
  el.addEventListener('mouseleave',()=>cursor.classList.remove('big'));
});

// Parallax Dish Motion (Fareye Duyarlı 3D Yüzen Tabaklar)
addEventListener('pointermove',e=>{
  if(innerWidth<900)return;
  const x=(innerWidth/2 - e.clientX)/35;
  const y=(innerHeight/2 - e.clientY)/35;
  dishes.forEach((d,i)=>{
    const factor = (i % 2 === 0 ? 1 : -1) * (i + 1) * 0.4;
    d.style.transform = `translate3d(${x * factor}px, ${y * factor}px, 0px)`;
  });
},{passive:true});

// Reveal Animations (Intersection Observer)
const io=new IntersectionObserver(es=>es.forEach(e=>{
  if(e.isIntersecting){
    e.target.classList.add('visible');
    io.unobserve(e.target);
  }
}),{threshold:.12});
$$('.reveal').forEach(x=>io.observe(x));

// Menu Filtering
$$('.filter').forEach(btn=>btn.onclick=()=>{
  $$('.filter').forEach(x=>x.classList.remove('active'));
  btn.classList.add('active');
  const f=btn.dataset.filter;
  $$('.card').forEach(c=>{
    c.style.display=(f==='all'||c.dataset.cat===f)?'block':'none';
  });
});

// 3D Card Tilt Effect (Menü Kartları Eğilme Efekti)
$$('.card').forEach(card => {
  card.addEventListener('mousemove', e => {
    const rect = card.getBoundingClientRect();
    const x = e.clientX - rect.left - rect.width/2;
    const y = e.clientY - rect.top - rect.height/2;
    card.style.transform = `rotateY(${x / 20}deg) rotateX(${-y / 20}deg)`;
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = 'rotateY(0deg) rotateX(0deg)';
  });
});

// Mobil Menü Mantığı
const menuBtn = $('#menuBtn');
const mobileNav = $('#mobileNav');
function toggleMobileMenu(){
  const isOpen = mobileNav.classList.toggle('open');
  menuBtn.textContent = isOpen ? '✕' : '☰';
  document.body.classList.toggle('lock', isOpen);
}
if(menuBtn) menuBtn.onclick = toggleMobileMenu;

// Modal & Form Handler
const modal=$('#modal');
const open=()=>{modal.classList.add('open');modal.setAttribute('aria-hidden','false');document.body.classList.add('lock')};
const close=()=>{modal.classList.remove('open');modal.setAttribute('aria-hidden','true');document.body.classList.remove('lock')};
$$('[data-open]').forEach(x=>x.onclick=open);
$('#close').onclick=close;
modal.onclick=e=>{if(e.target===modal)close()};
addEventListener('keydown',e=>{if(e.key==='Escape')close()});

$('#booking').onsubmit=e=>{
  e.preventDefault();
  close();
  const t=$('#toast');
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),4500);
};
</script>
</body>
</html>
