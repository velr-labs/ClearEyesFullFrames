<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cleareyes Fullframes</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@400;500;600&display=swap');

  :root{
    --bg:#0d0c0a;
    --panel:#161410;
    --fg:#f5f1e8;
    --fg-dim:#9a9388;
    --gold:#c9a368;
    --hair:#2a2622;
  }

  *{margin:0;padding:0;box-sizing:border-box;}
  html,body{height:100%;}
  body{
    background:var(--bg);
    color:var(--fg);
    font-family:'Inter', sans-serif;
    overflow:hidden;
  }
  a{color:inherit;text-decoration:none;}
  button{font-family:inherit;border:none;background:none;color:inherit;cursor:pointer;}

  ::selection{background:var(--gold);color:#1a1208;}

  .app{
    height:100vh;
    display:flex;
    flex-direction:column;
  }

  /* ---------- top bar ---------- */
  .topbar{
    height:64px;
    flex-shrink:0;
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:0 1.4rem;
    border-bottom:1px solid var(--hair);
    background:var(--bg);
    z-index:20;
  }
  .brand{
    display:flex;
    align-items:center;
    gap:.6rem;
  }
  .brand img{height:30px;width:30px;}
  .brand span{
    font-family:'Bebas Neue', sans-serif;
    font-size:1.05rem;
    letter-spacing:.04em;
  }
  .brand span em{
    color:var(--gold);
    font-style:normal;
  }
  .tabs{
    display:flex;
    gap:.3rem;
    background:var(--panel);
    border:1px solid var(--hair);
    border-radius:999px;
    padding:3px;
  }
  .tab{
    font-size:.78rem;
    font-weight:500;
    letter-spacing:.02em;
    padding:.5rem 1.1rem;
    border-radius:999px;
    color:var(--fg-dim);
    transition:background .25s ease, color .25s ease;
  }
  .tab.active{
    background:var(--gold);
    color:#1a1208;
  }
  .tab:not(.active):hover{color:var(--fg);}

  .contact-btn{
    font-size:.78rem;
    font-weight:600;
    padding:.55rem 1.2rem;
    border-radius:999px;
    border:1px solid var(--gold);
    color:var(--gold);
    transition:background .25s ease, color .25s ease;
  }
  .contact-btn:hover{background:var(--gold);color:#1a1208;}

  /* ---------- main view swap ---------- */
  .view{
    flex:1;
    overflow:hidden;
    position:relative;
  }
  .panel{
    position:absolute;
    inset:0;
    display:none;
    flex-direction:column;
  }
  .panel.active{display:flex;}

  /* ---------- WORK panel ---------- */
  .stage{
    flex:1;
    position:relative;
    display:flex;
    align-items:center;
    justify-content:center;
    background:#000;
    overflow:hidden;
  }
  .stage img{
    max-width:100%;
    max-height:100%;
    object-fit:contain;
    opacity:0;
    position:absolute;
    transition:opacity .45s ease;
  }
  .stage img.show{opacity:1;}

  .stage-nav{
    position:absolute;
    top:50%;
    transform:translateY(-50%);
    width:42px;height:42px;
    border-radius:50%;
    background:rgba(13,12,10,.55);
    border:1px solid var(--hair);
    display:flex;
    align-items:center;
    justify-content:center;
    color:var(--fg);
    font-size:1.1rem;
    transition:background .2s ease, border-color .2s ease;
    z-index:5;
  }
  .stage-nav:hover{background:rgba(201,163,104,.18);border-color:var(--gold);}
  .stage-nav.prev{left:1rem;}
  .stage-nav.next{right:1rem;}

  .stage-meta{
    position:absolute;
    bottom:1.1rem;
    left:1.4rem;
    z-index:5;
    font-size:.78rem;
    color:var(--fg-dim);
  }
  .stage-meta strong{color:var(--fg);font-weight:500;}

  .filmstrip{
    flex-shrink:0;
    display:flex;
    gap:.5rem;
    padding:.8rem 1.2rem;
    border-top:1px solid var(--hair);
    overflow-x:auto;
  }
  .thumb{
    flex-shrink:0;
    width:78px;height:54px;
    border-radius:6px;
    overflow:hidden;
    border:2px solid transparent;
    opacity:.55;
    transition:opacity .25s ease, border-color .25s ease;
  }
  .thumb img{width:100%;height:100%;object-fit:cover;display:block;}
  .thumb.active{opacity:1;border-color:var(--gold);}
  .thumb:hover{opacity:.9;}

  /* ---------- ABOUT panel ---------- */
  .about-panel{
    align-items:center;
    justify-content:center;
    padding:2rem;
  }
  .about-inner{
    max-width:480px;
    text-align:center;
  }
  .about-inner .aperture{
    width:54px;height:54px;
    margin:0 auto 1.6rem;
    border-radius:50%;
    border:2px solid var(--gold);
    display:flex;
    align-items:center;
    justify-content:center;
    color:var(--gold);
    font-family:'Bebas Neue', sans-serif;
    font-size:1.1rem;
    transition:transform .6s ease;
  }
  .about-inner:hover .aperture{transform:rotate(90deg);}
  .about-inner h2{
    font-family:'Bebas Neue', sans-serif;
    font-size:1.6rem;
    letter-spacing:.03em;
    margin-bottom:1rem;
  }
  .about-inner p{
    font-size:.95rem;
    line-height:1.65;
    color:var(--fg-dim);
  }
  .about-inner p + p{margin-top:.9rem;}

  /* ---------- CONTACT panel ---------- */
  .contact-panel{
    align-items:center;
    justify-content:center;
  }
  .contact-inner{
    text-align:center;
  }
  .contact-inner .label{
    font-size:.75rem;
    letter-spacing:.2em;
    color:var(--fg-dim);
    margin-bottom:1rem;
    display:block;
  }
  .contact-inner a{
    font-family:'Bebas Neue', sans-serif;
    font-size:clamp(1.6rem,6vw,3rem);
    color:var(--fg);
    border-bottom:1px solid transparent;
    transition:color .25s ease, border-color .25s ease;
    padding-bottom:.2rem;
  }
  .contact-inner a:hover{color:var(--gold);border-color:var(--gold);}
  .contact-inner .sub{
    margin-top:1.2rem;
    font-size:.82rem;
    color:var(--fg-dim);
  }

  /* ---------- mobile ---------- */
  @media (max-width:640px){
    .brand span{display:none;}
    .tabs{gap:.2rem;}
    .tab{padding:.45rem .8rem;font-size:.72rem;}
    .contact-btn{display:none;}
    .stage-nav{width:36px;height:36px;font-size:1rem;}
    .thumb{width:60px;height:42px;}
  }

  @media (prefers-reduced-motion: reduce){
    *{transition:none !important;}
  }

  button:focus-visible, a:focus-visible{
    outline:1px solid var(--gold);
    outline-offset:2px;
  }
</style>
</head>
<body>

<div class="app">

  <div class="topbar">
    <div class="brand">
      <img src="img/logo.png" alt="">
      <span>cleareyes<em>fullframes</em></span>
    </div>
    <div class="tabs" role="tablist">
      <button class="tab active" data-panel="work">Work</button>
      <button class="tab" data-panel="about">About</button>
    </div>
    <button class="contact-btn" data-panel="contact">Contact</button>
  </div>

  <div class="view">

    <section class="panel active" id="panel-work">
      <div class="stage">
        <button class="stage-nav prev" aria-label="Previous photo">&#8249;</button>
        <img src="img/IMG_5160.jpeg" alt="Thumbs up, go-kart helmet" class="show" data-meta="indoor track · houston, tx">
        <img src="img/IMG_5131.jpeg" alt="Go-kart, profile" data-meta="motion, low light · houston, tx">
        <img src="img/IMG_5121.jpeg" alt="Victory Lane signage" data-meta="detail · indianapolis">
        <img src="img/IMG_5120.jpeg" alt="Candid, exodus cap" data-meta="candid, arcade light · houston, tx">
        <button class="stage-nav next" aria-label="Next photo">&#8250;</button>
        <div class="stage-meta"><strong id="meta-text">indoor track</strong> <span id="meta-sub">· houston, tx</span></div>
      </div>
      <div class="filmstrip" role="tablist" aria-label="Photo selector">
        <div class="thumb active" data-index="0"><img src="img/IMG_5160.jpeg" alt=""></div>
        <div class="thumb" data-index="1"><img src="img/IMG_5131.jpeg" alt=""></div>
        <div class="thumb" data-index="2"><img src="img/IMG_5121.jpeg" alt=""></div>
        <div class="thumb" data-index="3"><img src="img/IMG_5120.jpeg" alt=""></div>
      </div>
    </section>

    <section class="panel about-panel" id="panel-about">
      <div class="about-inner">
        <div class="aperture">CF</div>
        <h2>portraits, mostly. people, always.</h2>
        <p>i shoot what's already there. no direction, no performance — just the second before someone remembers the camera is on them.</p>
        <p>based in houston, shooting wherever the light's worth chasing.</p>
      </div>
    </section>

    <section class="panel contact-panel" id="panel-contact">
      <div class="contact-inner">
        <span class="label">INQUIRIES</span>
        <a href="mailto:hello@cleareyesfullframes.com">hello@cleareyesfullframes.com</a>
        <div class="sub">houston, tx</div>
      </div>
    </section>

  </div>

</div>

<script>
  const tabs = document.querySelectorAll('.tab, .contact-btn[data-panel]');
  const panels = document.querySelectorAll('.panel');

  function showPanel(name){
    panels.forEach(p => p.classList.toggle('active', p.id === 'panel-' + name));
    document.querySelectorAll('.tab').forEach(t => t.classList.toggle('active', t.dataset.panel === name));
  }

  tabs.forEach(t => t.addEventListener('click', () => showPanel(t.dataset.panel)));

  // gallery stage logic
  const images = document.querySelectorAll('.stage img[data-meta]');
  const thumbs = document.querySelectorAll('.thumb');
  const metaText = document.getElementById('meta-text');
  const metaSub = document.getElementById('meta-sub');
  let current = 0;

  function setSlide(i){
    current = (i + images.length) % images.length;
    images.forEach((img, idx) => img.classList.toggle('show', idx === current));
    thumbs.forEach((th, idx) => th.classList.toggle('active', idx === current));
    const [main, sub] = images[current].dataset.meta.split(' · ');
    metaText.textContent = main;
    metaSub.textContent = '· ' + sub;
  }

  document.querySelector('.stage-nav.prev').addEventListener('click', () => setSlide(current - 1));
  document.querySelector('.stage-nav.next').addEventListener('click', () => setSlide(current + 1));
  thumbs.forEach(th => th.addEventListener('click', () => setSlide(parseInt(th.dataset.index))));

  document.addEventListener('keydown', e => {
    if(!document.getElementById('panel-work').classList.contains('active')) return;
    if(e.key === 'ArrowLeft') setSlide(current - 1);
    if(e.key === 'ArrowRight') setSlide(current + 1);
  });
</script>

</body>
</html>
