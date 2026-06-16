<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>cleareyes_fullframes</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Cormorant:ital@0;1&family=Cormorant+Garamond:ital@0;1&display=swap');

  :root{
    --bg:#0a0a0a;
    --bg-2:#111111;
    --fg:#ece8e1;
    --fg-dim:#8a8580;
    --accent:#5c6b73;
    --hair:#262626;
  }

  *{margin:0;padding:0;box-sizing:border-box;}

  html{scroll-behavior:smooth;}

  body{
    background:var(--bg);
    color:var(--fg);
    font-family:'Cormorant Garamond', serif;
    overflow-x:hidden;
  }

  ::selection{background:var(--accent);color:var(--bg);}

  a{color:inherit;text-decoration:none;}

  /* ---------- side nav ---------- */
  .sidenav{
    position:fixed;
    top:0;right:0;
    height:100vh;
    width:14px;
    z-index:100;
    display:flex;
    align-items:center;
    justify-content:center;
  }
  .sidenav .rail{
    width:1px;
    height:60%;
    background:var(--hair);
    transition:width .4s ease, background .4s ease;
  }
  .sidenav:hover{width:160px;}
  .sidenav:hover .rail{display:none;}
  .navlinks{
    display:none;
    flex-direction:column;
    gap:1.4rem;
    padding-right:2rem;
  }
  .sidenav:hover .navlinks{display:flex;}
  .navlinks a{
    font-family:'Bebas Neue', sans-serif;
    font-size:.8rem;
    letter-spacing:.25em;
    color:var(--fg-dim);
    text-align:right;
  }
  .navlinks a:hover{color:var(--fg);}

  .brandmark{
    position:fixed;
    top:2rem;left:2rem;
    z-index:100;
    display:block;
    width:48px;
    opacity:.85;
    filter:grayscale(1) brightness(1.3) contrast(.9);
    transition:opacity .3s ease, transform .3s ease;
  }
  .brandmark img{
    width:100%;
    display:block;
  }
  .brandmark:hover{
    opacity:1;
    transform:scale(1.04);
  }
  @media (max-width:600px){
    .brandmark{width:36px; top:1.4rem; left:1.4rem;}
  }

  /* ---------- hero ---------- */
  .hero{
    height:100vh;
    position:relative;
    display:flex;
    align-items:center;
    justify-content:center;
    overflow:hidden;
    background:#000;
  }
  .hero img{
    position:absolute;
    inset:0;
    width:100%;
    height:100%;
    object-fit:cover;
    filter:grayscale(1) contrast(1.05) brightness(.75);
    opacity:.85;
  }
  .hero::after{
    content:'';
    position:absolute;
    inset:0;
    background:linear-gradient(180deg, rgba(0,0,0,.2) 0%, rgba(0,0,0,.15) 40%, rgba(0,0,0,.55) 100%);
  }
  .hero-mark{
    position:relative;
    z-index:2;
    font-family:'Bebas Neue', sans-serif;
    font-size:clamp(3.2rem, 14vw, 11rem);
    letter-spacing:.04em;
    line-height:.85;
    text-transform:lowercase;
    color:var(--fg);
    width:108%;
    text-align:center;
    mix-blend-mode:difference;
    filter:invert(1);
  }
  .hero-sub{
    position:absolute;
    bottom:3.2rem;
    left:50%;
    transform:translateX(-50%);
    z-index:2;
    font-family:'Cormorant', serif;
    font-style:italic;
    font-size:.95rem;
    color:var(--fg-dim);
    letter-spacing:.04em;
  }
  .scroll-cue{
    position:absolute;
    bottom:1.2rem;
    left:50%;
    transform:translateX(-50%);
    width:1px;height:30px;
    background:var(--fg-dim);
    z-index:2;
    animation:drop 2.2s ease-in-out infinite;
  }
  @keyframes drop{
    0%{opacity:0; transform:translate(-50%,-8px) scaleY(.4);}
    40%{opacity:1; transform:translate(-50%,0) scaleY(1);}
    100%{opacity:0; transform:translate(-50%,10px) scaleY(.4);}
  }

  /* ---------- intro strip ---------- */
  .intro{
    max-width:640px;
    margin:0 auto;
    padding:9rem 2rem 8rem;
    text-align:center;
  }
  .intro .eyebrow{
    font-family:'Bebas Neue', sans-serif;
    font-size:.72rem;
    letter-spacing:.3em;
    color:var(--accent);
    margin-bottom:1.6rem;
    display:block;
  }
  .intro p{
    font-size:1.35rem;
    line-height:1.65;
    color:var(--fg);
    font-style:italic;
  }

  /* ---------- gallery ---------- */
  .gallery-section{
    padding:0 0 6rem;
  }
  .section-label{
    font-family:'Bebas Neue', sans-serif;
    font-size:.75rem;
    letter-spacing:.3em;
    color:var(--fg-dim);
    text-align:center;
    margin-bottom:3.5rem;
  }
  .grid{
    display:grid;
    grid-template-columns:repeat(2,1fr);
    gap:2px;
    max-width:1400px;
    margin:0 auto;
    padding:0 2px;
  }
  .frame{
    position:relative;
    aspect-ratio:3/2;
    overflow:hidden;
    background:#000;
    cursor:pointer;
  }
  .frame img{
    width:100%;height:100%;
    object-fit:cover;
    filter:grayscale(1) contrast(1.05) brightness(.82);
    transition:transform 1.1s cubic-bezier(.22,1,.36,1), filter .6s ease;
    transform:scale(1.02);
  }
  .frame:hover img{
    transform:scale(1.08);
    filter:grayscale(.85) contrast(1.1) brightness(.9);
  }
  .frame-meta{
    position:absolute;
    left:0;bottom:0;right:0;
    padding:1.1rem 1.2rem;
    background:linear-gradient(180deg, transparent, rgba(0,0,0,.75));
    opacity:0;
    transform:translateY(6px);
    transition:opacity .45s ease, transform .45s ease;
  }
  .frame:hover .frame-meta{opacity:1;transform:translateY(0);}
  .frame-meta span{
    display:block;
    font-family:'Cormorant', serif;
    font-style:italic;
    font-size:.85rem;
    color:var(--fg-dim);
    letter-spacing:.02em;
  }
  .frame-meta span.loc{color:var(--fg);margin-top:.15rem;}

  @media (max-width:820px){
    .grid{grid-template-columns:1fr;}
  }

  /* ---------- statement ---------- */
  .statement{
    padding:10rem 2rem;
    text-align:center;
    position:relative;
    border-top:1px solid var(--hair);
    border-bottom:1px solid var(--hair);
  }
  .statement p{
    max-width:780px;
    margin:0 auto;
    font-family:'Bebas Neue', sans-serif;
    text-transform:lowercase;
    font-size:clamp(1.6rem, 4vw, 2.8rem);
    letter-spacing:.02em;
    line-height:1.35;
    color:var(--fg);
  }
  .statement p em{
    font-family:'Cormorant', serif;
    font-style:italic;
    color:var(--accent);
    text-transform:none;
    font-size:.6em;
    display:block;
    margin-top:1.4rem;
    letter-spacing:.04em;
  }

  /* ---------- contact ---------- */
  .contact{
    padding:8rem 2rem 7rem;
    text-align:center;
  }
  .contact .eyebrow{
    font-family:'Bebas Neue', sans-serif;
    font-size:.72rem;
    letter-spacing:.3em;
    color:var(--fg-dim);
    display:block;
    margin-bottom:1.6rem;
  }
  .contact-link{
    font-family:'Bebas Neue', sans-serif;
    font-size:clamp(2rem,7vw,4rem);
    text-transform:lowercase;
    letter-spacing:.03em;
    border-bottom:1px solid transparent;
    transition:border-color .3s ease, color .3s ease;
    padding-bottom:.3rem;
  }
  .contact-link:hover{
    color:var(--accent);
    border-color:var(--accent);
  }
  footer{
    display:flex;
    align-items:center;
    justify-content:center;
    gap:.9rem;
    text-align:center;
    padding:3rem 2rem 2.5rem;
    font-family:'Cormorant', serif;
    font-style:italic;
    font-size:.8rem;
    color:var(--fg-dim);
    border-top:1px solid var(--hair);
  }
  .footer-mark{
    width:22px;
    opacity:.7;
    filter:grayscale(1) brightness(1.3);
  }

  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }

  a:focus-visible, .frame:focus-visible{
    outline:1px solid var(--accent);
    outline-offset:3px;
  }
</style>
</head>
<body>

<nav class="sidenav" aria-label="Section navigation">
  <div class="rail"></div>
  <div class="navlinks">
    <a href="#work">work</a>
    <a href="#about">about</a>
    <a href="#contact">contact</a>
  </div>
</nav>

<a href="#" class="brandmark" aria-label="Cleareyes Fullframes home">
  <img src="img/logo.png" alt="Cleareyes Fullframes logo">
</a>

<section class="hero">
  <img src="img/IMG_5160.jpeg" alt="">
  <div class="hero-mark">cleareyes<br>_fullframes</div>
  <div class="hero-sub">portraits, mostly. people, always.</div>
  <div class="scroll-cue"></div>
</section>

<section class="intro" id="about">
  <span class="eyebrow">no filter, no noise</span>
  <p>i shoot what's already there. no direction, no performance — just the second before someone remembers the camera is on them.</p>
</section>

<section class="gallery-section" id="work">
  <span class="section-label">selected frames</span>
  <div class="grid">
    <div class="frame" tabindex="0">
      <img src="img/IMG_5160.jpeg" alt="Thumbs up, go-kart helmet">
      <div class="frame-meta"><span>indoor track</span><span class="loc">houston, tx</span></div>
    </div>
    <div class="frame" tabindex="0">
      <img src="img/IMG_5131.jpeg" alt="Go-kart, profile">
      <div class="frame-meta"><span>motion, low light</span><span class="loc">houston, tx</span></div>
    </div>
    <div class="frame" tabindex="0">
      <img src="img/IMG_5121.jpeg" alt="Victory Lane signage">
      <div class="frame-meta"><span>detail</span><span class="loc">indianapolis</span></div>
    </div>
    <div class="frame" tabindex="0">
      <img src="img/IMG_5120.jpeg" alt="Candid, exodus cap">
      <div class="frame-meta"><span>candid, arcade light</span><span class="loc">houston, tx</span></div>
    </div>
  </div>
</section>

<section class="statement">
  <p>the frame holds still. <em>everything else doesn't have to.</em></p>
</section>

<section class="contact" id="contact">
  <span class="eyebrow">inquiries</span>
  <a class="contact-link" href="mailto:hello@cleareyesfullframes.com">hello@cleareyesfullframes.com</a>
</section>

<footer>
  <img src="img/logo.png" alt="" class="footer-mark">
  <span>cleareyes_fullframes — houston, tx</span>
</footer>

</body>
</html>
