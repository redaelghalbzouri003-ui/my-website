<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Reda El Ghalbzouri – Master Pastry Chef</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,700;1,400;1,500&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --ivory:#F8F5F0;--champagne:#E8D8B8;--caramel:#CFA675;
    --cocoa:#4A3428;--choc:#1A120F;--cream:#fdfaf6;
  }
  html{scroll-behavior:smooth}
  body{background:var(--ivory);color:var(--cocoa);font-family:'Inter',sans-serif;overflow-x:hidden}

  /* ── HERO ── */
  #hero{
    min-height:100vh;display:grid;grid-template-columns:1fr 1fr;
    position:relative;overflow:hidden;
  }
  .hero-left{
    display:flex;flex-direction:column;justify-content:center;
    padding:80px 60px;z-index:2;
  }
  .hero-tag{
    font-size:.75rem;letter-spacing:.25em;text-transform:uppercase;
    color:var(--caramel);margin-bottom:2rem;opacity:0;
    animation:fadeUp .8s .3s forwards;
  }
  .hero-name{
    font-family:'Playfair Display',serif;font-size:clamp(2.8rem,5vw,5rem);
    font-weight:500;line-height:1.1;color:var(--choc);opacity:0;
    animation:fadeUp .9s .5s forwards;
  }
  .hero-name em{font-style:italic;color:var(--caramel)}
  .hero-tagline{
    margin-top:1.5rem;font-size:1.1rem;font-weight:300;
    color:var(--cocoa);opacity:.75;letter-spacing:.05em;
    opacity:0;animation:fadeUp .9s .75s forwards;
  }
  .hero-sub{
    margin-top:1rem;font-size:.8rem;letter-spacing:.18em;
    text-transform:uppercase;color:var(--caramel);
    opacity:0;animation:fadeUp .9s .95s forwards;
  }
  .scroll-hint{
    margin-top:4rem;display:flex;align-items:center;gap:.75rem;
    font-size:.72rem;letter-spacing:.2em;text-transform:uppercase;
    color:var(--caramel);opacity:0;animation:fadeUp .9s 1.3s forwards;
  }
  .scroll-hint::before{content:'';display:block;width:40px;height:1px;background:var(--caramel)}

  .hero-right{
    position:relative;display:flex;align-items:center;justify-content:center;
    background:linear-gradient(135deg,#f0e8d8 0%,#e8d5b5 100%);overflow:hidden;
  }
  .hero-art{
    width:100%;height:100%;display:flex;align-items:center;justify-content:center;
    opacity:0;animation:fadeIn 1.2s 1s forwards;
  }

  /* warm overlay */
  #hero::after{
    content:'';position:absolute;inset:0;
    background:radial-gradient(ellipse at 70% 50%,rgba(207,166,117,.12) 0%,transparent 70%);
    pointer-events:none;z-index:1;
  }

  /* ── PLATE SECTION ── */
  #plate-section{
    min-height:100vh;display:flex;flex-direction:column;
    align-items:center;justify-content:center;
    padding:80px 20px;position:relative;
  }
  .section-intro{
    text-align:center;margin-bottom:3.5rem;
    opacity:0;transform:translateY(30px);transition:all .9s;
  }
  .section-intro.visible{opacity:1;transform:none}
  .section-intro h2{
    font-family:'Playfair Display',serif;font-size:clamp(1.8rem,3vw,2.8rem);
    font-weight:500;color:var(--choc);
  }
  .section-intro p{
    margin-top:.75rem;font-size:.85rem;letter-spacing:.15em;
    text-transform:uppercase;color:var(--caramel);
  }

  .plate-wrap{
    position:relative;width:min(520px,90vw);height:min(520px,90vw);
    opacity:0;transform:scale(.88);transition:opacity .9s .2s,transform .9s .2s;
  }
  .plate-wrap.visible{opacity:1;transform:scale(1)}

  /* plate SVG bg */
  .plate-bg{
    position:absolute;inset:0;border-radius:50%;
    background:radial-gradient(circle at 38% 35%,#fffdf9 0%,#f5ede0 45%,#e8d5b5 75%,#d4bc95 100%);
    box-shadow:
      0 0 0 2px rgba(207,166,117,.25),
      0 4px 30px rgba(74,52,40,.18),
      0 20px 80px rgba(74,52,40,.1),
      inset 0 -4px 20px rgba(207,166,117,.15);
  }
  /* inner rim */
  .plate-rim{
    position:absolute;inset:14px;border-radius:50%;
    border:1.5px solid rgba(207,166,117,.3);
    box-shadow:inset 0 0 20px rgba(207,166,117,.1);
  }

  /* pastry buttons */
  .pastry{
    position:absolute;width:90px;height:90px;
    transform:translate(-50%,-50%);cursor:pointer;
    transition:transform .35s cubic-bezier(.34,1.56,.64,1),filter .35s;
    z-index:10;
  }
  .pastry:hover{transform:translate(-50%,-50%) translateY(-8px) scale(1.1)}
  .pastry:hover svg{filter:drop-shadow(0 8px 20px rgba(207,166,117,.55))}
  .pastry-label{
    position:absolute;bottom:-28px;left:50%;transform:translateX(-50%);
    font-size:.6rem;letter-spacing:.15em;text-transform:uppercase;
    color:var(--cocoa);white-space:nowrap;opacity:.7;
    font-family:'Inter',sans-serif;transition:opacity .3s;
  }
  .pastry:hover .pastry-label{opacity:1;color:var(--caramel)}

  /* ── MODAL ── */
  .modal-overlay{
    position:fixed;inset:0;background:rgba(26,18,15,.65);backdrop-filter:blur(8px);
    z-index:100;display:flex;align-items:center;justify-content:center;
    opacity:0;pointer-events:none;transition:opacity .4s;
  }
  .modal-overlay.open{opacity:1;pointer-events:all}
  .modal{
    background:var(--cream);max-width:600px;width:90%;max-height:85vh;
    overflow-y:auto;padding:52px 48px;position:relative;
    transform:translateY(30px) scale(.97);transition:transform .4s cubic-bezier(.34,1.2,.64,1);
    border-top:3px solid var(--caramel);
  }
  .modal-overlay.open .modal{transform:none}
  .modal-close{
    position:absolute;top:20px;right:24px;background:none;border:none;
    font-size:1.4rem;cursor:pointer;color:var(--caramel);line-height:1;
  }
  .modal-tag{font-size:.68rem;letter-spacing:.25em;text-transform:uppercase;color:var(--caramel);margin-bottom:.75rem}
  .modal h2{font-family:'Playfair Display',serif;font-size:2rem;color:var(--choc);margin-bottom:1.25rem;font-weight:500}
  .modal p{font-size:.92rem;line-height:1.85;color:var(--cocoa);margin-bottom:1rem;font-weight:300}
  .modal ul{list-style:none;margin:.5rem 0 1rem}
  .modal ul li{
    font-size:.88rem;color:var(--cocoa);padding:.45rem 0;
    border-bottom:1px solid rgba(207,166,117,.2);font-weight:300;
  }
  .modal ul li::before{content:'— ';color:var(--caramel)}

  /* gallery grid */
  .gallery{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-top:1rem}
  .gallery-item{
    aspect-ratio:1;border-radius:4px;display:flex;align-items:center;justify-content:center;
    font-size:2rem;
    background:linear-gradient(135deg,var(--champagne),var(--caramel));
    color:white;font-family:'Playfair Display',serif;
  }

  /* ── INVOICE ── */
  #invoice-section{
    min-height:60vh;display:flex;align-items:center;justify-content:center;
    padding:80px 20px;
  }
  .invoice{
    max-width:480px;width:100%;
    background:linear-gradient(160deg,#fdfaf5 0%,#f5ede0 100%);
    border:1px solid var(--champagne);
    padding:52px 48px;text-align:center;position:relative;
    opacity:0;transform:translateY(50px) rotate(-1deg);
    transition:all 1s cubic-bezier(.34,1.2,.64,1);
    box-shadow:0 20px 80px rgba(74,52,40,.12),0 4px 20px rgba(74,52,40,.08);
  }
  .invoice.visible{opacity:1;transform:none}
  .invoice::before{
    content:'';position:absolute;inset:8px;
    border:1px solid rgba(207,166,117,.25);pointer-events:none;
  }
  .invoice-header{
    font-family:'Playfair Display',serif;font-size:1.1rem;font-style:italic;
    color:var(--caramel);margin-bottom:.5rem;
  }
  .invoice-title{
    font-family:'Playfair Display',serif;font-size:1.9rem;color:var(--choc);
    margin-bottom:.5rem;
  }
  .invoice-date{font-size:.7rem;letter-spacing:.18em;text-transform:uppercase;color:var(--caramel);margin-bottom:2rem}
  .invoice-divider{border:none;border-top:1px solid var(--champagne);margin:1.2rem 0}
  .invoice-row{
    display:flex;justify-content:space-between;align-items:center;
    font-size:.85rem;padding:.4rem 0;color:var(--cocoa);font-weight:300;
  }
  .invoice-row span:last-child{font-style:italic;color:var(--caramel)}
  .invoice-total{
    margin-top:1.5rem;padding-top:1.5rem;border-top:2px solid var(--caramel);
  }
  .invoice-total-label{font-size:.7rem;letter-spacing:.2em;text-transform:uppercase;color:var(--caramel);margin-bottom:.5rem}
  .invoice-total-value{font-family:'Playfair Display',serif;font-size:1.4rem;color:var(--choc);font-style:italic}
  .cta-btn{
    margin-top:2rem;display:inline-block;padding:14px 40px;
    background:var(--choc);color:var(--champagne);border:none;cursor:pointer;
    font-size:.75rem;letter-spacing:.2em;text-transform:uppercase;
    font-family:'Inter',sans-serif;transition:all .3s;text-decoration:none;
  }
  .cta-btn:hover{background:var(--caramel);color:var(--choc)}

  /* ── FOOTER ── */
  footer{
    background:var(--choc);color:var(--champagne);
    padding:48px 40px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:1rem;
  }
  .footer-name{font-family:'Playfair Display',serif;font-size:1.1rem;font-style:italic}
  .footer-title{font-size:.68rem;letter-spacing:.2em;text-transform:uppercase;color:var(--caramel);margin-top:.25rem}
  .footer-links{display:flex;gap:1.5rem;align-items:center}
  .footer-links a{color:var(--champagne);text-decoration:none;font-size:.78rem;letter-spacing:.1em;transition:color .3s}
  .footer-links a:hover{color:var(--caramel)}

  @keyframes fadeUp{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:none}}
  @keyframes fadeIn{from{opacity:0}to{opacity:1}}

  @media(max-width:720px){
    #hero{grid-template-columns:1fr}
    .hero-right{display:none}
    .hero-left{padding:80px 32px 60px}
  }
</style>
</head>
<body>

<!-- ═══════════════════ HERO ═══════════════════ -->
<section id="hero">
  <div class="hero-left">
    <div class="hero-tag">The Degustation Menu</div>
    <h1 class="hero-name">Reda<br><em>El Ghalbzouri</em></h1>
    <p class="hero-tagline">Crafting Emotions through Sugar</p>
    <p class="hero-sub">Master Pastry Chef &nbsp;·&nbsp; Chocolate &amp; Modern Desserts</p>
    <div class="scroll-hint">Scroll to begin the tasting</div>
  </div>
  <div class="hero-right">
    <div class="hero-art">
      <!-- Artistic SVG portrait / line art -->
      <svg viewBox="0 0 340 440" width="340" fill="none" xmlns="http://www.w3.org/2000/svg">
        <!-- abstract chef silhouette + pastry elements -->
        <ellipse cx="170" cy="200" rx="95" ry="115" fill="none" stroke="#CFA675" stroke-width="1.2" opacity=".4"/>
        <ellipse cx="170" cy="200" rx="75" ry="95" fill="none" stroke="#CFA675" stroke-width=".6" opacity=".25"/>
        <!-- toque -->
        <rect x="132" y="68" width="76" height="52" rx="8" fill="none" stroke="#4A3428" stroke-width="1.5"/>
        <rect x="120" y="112" width="100" height="12" rx="4" fill="none" stroke="#4A3428" stroke-width="1.5"/>
        <!-- chef waves -->
        <path d="M140 200 Q170 170 200 200 Q170 230 140 200Z" fill="none" stroke="#CFA675" stroke-width="1.2"/>
        <!-- chocolate drip lines -->
        <path d="M60 160 Q55 200 62 240" stroke="#4A3428" stroke-width="1" stroke-linecap="round" opacity=".3"/>
        <path d="M280 160 Q285 200 278 240" stroke="#4A3428" stroke-width="1" stroke-linecap="round" opacity=".3"/>
        <!-- fork / spatula icon -->
        <path d="M48 290 L48 370 M44 290 L44 310 M48 290 L52 290 M52 290 L52 310 M44 310 Q48 320 52 310" stroke="#CFA675" stroke-width="1.2" stroke-linecap="round"/>
        <!-- pastry circles -->
        <circle cx="270" cy="300" r="28" fill="none" stroke="#CFA675" stroke-width="1" opacity=".5"/>
        <circle cx="270" cy="300" r="16" fill="none" stroke="#CFA675" stroke-width=".6" opacity=".3"/>
        <!-- text flourish -->
        <text x="170" y="400" text-anchor="middle" font-family="Playfair Display,serif" font-style="italic" font-size="13" fill="#CFA675" opacity=".6">Chef Pâtissier</text>
        <line x1="90" y1="405" x2="130" y2="405" stroke="#CFA675" stroke-width=".8" opacity=".4"/>
        <line x1="210" y1="405" x2="250" y2="405" stroke="#CFA675" stroke-width=".8" opacity=".4"/>
        <!-- decorative dots -->
        <circle cx="170" cy="340" r="2.5" fill="#CFA675" opacity=".5"/>
        <circle cx="155" cy="348" r="1.5" fill="#CFA675" opacity=".35"/>
        <circle cx="185" cy="348" r="1.5" fill="#CFA675" opacity=".35"/>
      </svg>
    </div>
  </div>
</section>

<!-- ═══════════════════ PLATE ═══════════════════ -->
<section id="plate-section">
  <div class="section-intro" id="intro-text">
    <h2>The Tasting Menu</h2>
    <p>Six courses · Six stories · One vision</p>
  </div>

  <div class="plate-wrap" id="plateWrap">
    <div class="plate-bg"></div>
    <div class="plate-rim"></div>

    <!-- Pastries positioned in a circle (r≈42% of container) -->
    <!-- positions: top, top-right, bottom-right, bottom, bottom-left, top-left -->
    <div class="pastry" style="left:50%;top:9%" onclick="openModal(0)" aria-label="Who Am I">
      <svg viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
        <!-- meringue kiss -->
        <ellipse cx="45" cy="70" rx="30" ry="10" fill="rgba(207,166,117,.15)"/>
        <path d="M45 65 Q30 50 32 30 Q35 10 45 8 Q55 10 58 30 Q60 50 45 65Z" fill="#FDFAF6" stroke="#E8D8B8" stroke-width="1.2"/>
        <path d="M45 55 Q38 44 39 30 Q41 18 45 16 Q49 18 51 30 Q52 44 45 55Z" fill="white" opacity=".7"/>
        <circle cx="45" cy="9" r="3" fill="#F8F5F0" stroke="#E8D8B8" stroke-width="1"/>
      </svg>
      <div class="pastry-label">Who Am I</div>
    </div>

    <div class="pastry" style="left:82%;top:24%" onclick="openModal(1)" aria-label="My Craft">
      <svg viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
        <!-- caramel macaron -->
        <ellipse cx="45" cy="72" rx="28" ry="9" fill="rgba(207,166,117,.2)"/>
        <ellipse cx="45" cy="62" rx="26" ry="9" fill="#E8C88A"/>
        <ellipse cx="45" cy="62" rx="20" ry="6" fill="rgba(255,255,255,.3)"/>
        <rect x="19" y="56" width="52" height="10" rx="3" fill="#E8D8B8"/>
        <ellipse cx="45" cy="30" rx="26" ry="9" fill="#DDB86A"/>
        <ellipse cx="45" cy="30" rx="20" ry="6" fill="rgba(255,255,255,.25)"/>
        <ellipse cx="45" cy="21" rx="26" ry="9" fill="#E8C88A"/>
      </svg>
      <div class="pastry-label">My Craft</div>
    </div>

    <div class="pastry" style="left:82%;top:67%" onclick="openModal(2)" aria-label="Portfolio">
      <svg viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
        <!-- golden tart -->
        <ellipse cx="45" cy="68" rx="30" ry="8" fill="rgba(207,166,117,.25)"/>
        <path d="M18 60 Q18 45 45 45 Q72 45 72 60 L68 68 Q45 72 22 68Z" fill="#D4A055"/>
        <ellipse cx="45" cy="44" rx="27" ry="7" fill="#E8B865"/>
        <ellipse cx="45" cy="44" rx="20" ry="5" fill="#F0C878" opacity=".8"/>
        <ellipse cx="45" cy="38" rx="16" ry="10" fill="#C8864A"/>
        <ellipse cx="45" cy="36" rx="12" ry="7" fill="#D4956A" opacity=".7"/>
        <circle cx="45" cy="33" r="4" fill="#E8A055" opacity=".8"/>
      </svg>
      <div class="pastry-label">Portfolio</div>
    </div>

    <div class="pastry" style="left:50%;top:82%" onclick="openModal(3)" aria-label="Experience">
      <svg viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
        <!-- milk choc bonbon -->
        <ellipse cx="45" cy="65" rx="26" ry="8" fill="rgba(74,52,40,.2)"/>
        <path d="M20 55 Q20 35 45 33 Q70 35 70 55 Q70 65 45 67 Q20 65 20 55Z" fill="#8B5E3C"/>
        <path d="M28 48 Q28 36 45 35 Q62 36 62 48 Q62 55 45 56 Q28 55 28 48Z" fill="#A0724E" opacity=".8"/>
        <path d="M35 44 Q35 39 45 38 Q55 39 55 44 Q55 48 45 49 Q35 48 35 44Z" fill="rgba(255,255,255,.15)"/>
      </svg>
      <div class="pastry-label">Experience</div>
    </div>

    <div class="pastry" style="left:18%;top:67%" onclick="openModal(4)" aria-label="Philosophy">
      <svg viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
        <!-- dark cocoa dome -->
        <ellipse cx="45" cy="65" rx="28" ry="8" fill="rgba(26,18,15,.25)"/>
        <path d="M17 58 Q17 30 45 28 Q73 30 73 58 Q73 65 45 67 Q17 65 17 58Z" fill="#3D2518"/>
        <path d="M25 52 Q25 32 45 30 Q65 32 65 52 Q65 59 45 60 Q25 59 25 52Z" fill="#4A2E1C" opacity=".7"/>
        <ellipse cx="45" cy="30" rx="20" ry="5" fill="rgba(255,255,255,.06)"/>
        <!-- gold leaf fleck -->
        <ellipse cx="58" cy="38" rx="5" ry="2.5" fill="#CFA675" opacity=".7" transform="rotate(-20 58 38)"/>
      </svg>
      <div class="pastry-label">Philosophy</div>
    </div>

    <div class="pastry" style="left:18%;top:24%" onclick="openModal(5)" aria-label="Contact">
      <svg viewBox="0 0 90 90" xmlns="http://www.w3.org/2000/svg">
        <!-- 80% dark chocolate shard -->
        <ellipse cx="45" cy="68" rx="26" ry="7" fill="rgba(26,18,15,.3)"/>
        <path d="M25 62 L35 22 L58 18 L68 60 Q55 68 45 68 Q32 68 25 62Z" fill="#1A120F"/>
        <path d="M32 58 L40 26 L54 22 L62 56 Q52 63 45 63 Q36 63 32 58Z" fill="#2A1A10" opacity=".7"/>
        <!-- shine -->
        <path d="M38 28 Q42 24 50 26 Q46 32 38 28Z" fill="rgba(255,255,255,.12)"/>
        <!-- gold dust -->
        <circle cx="52" cy="42" r="1.5" fill="#CFA675" opacity=".8"/>
        <circle cx="47" cy="52" r="1" fill="#CFA675" opacity=".6"/>
        <circle cx="56" cy="50" r="1" fill="#CFA675" opacity=".5"/>
      </svg>
      <div class="pastry-label">Contact</div>
    </div>
  </div>

  <p style="margin-top:2.5rem;font-size:.72rem;letter-spacing:.18em;text-transform:uppercase;color:var(--caramel);opacity:.7">
    Select a pastry to explore
  </p>
</section>

<!-- ═══════════════════ INVOICE ═══════════════════ -->
<section id="invoice-section">
  <div class="invoice" id="invoiceEl">
    <div class="invoice-header">Restaurant Reda</div>
    <div class="invoice-title">The Tasting Menu</div>
    <div class="invoice-date">Season 2025 · Table Unique</div>
    <hr class="invoice-divider">
    <div class="invoice-row"><span>Passion</span><span>$Priceless</span></div>
    <div class="invoice-row"><span>Creativity</span><span>$Infinite</span></div>
    <div class="invoice-row"><span>Technical Mastery</span><span>Included</span></div>
    <div class="invoice-row"><span>Emotional Depth</span><span>Complimentary</span></div>
    <div class="invoice-row"><span>Years of Devotion</span><span>Cannot be priced</span></div>
    <hr class="invoice-divider">
    <div class="invoice-total">
      <div class="invoice-total-label">Your Investment</div>
      <div class="invoice-total-value">A Partnership for Excellence</div>
    </div>
    <a class="cta-btn" href="mailto:reda@example.com">Contact the Chef</a>
  </div>
</section>

<!-- ═══════════════════ FOOTER ═══════════════════ -->
<footer>
  <div>
    <div class="footer-name">Reda El Ghalbzouri</div>
    <div class="footer-title">Master Pastry Chef</div>
  </div>
  <div class="footer-links">
    <a href="mailto:reda@example.com">✉ Email</a>
    <a href="#" target="_blank">in LinkedIn</a>
    <a href="#" style="font-size:.7rem;opacity:.5">© 2025</a>
  </div>
</footer>

<!-- ═══════════════════ MODAL ═══════════════════ -->
<div class="modal-overlay" id="modalOverlay" onclick="closeModalOutside(event)">
  <div class="modal" id="modalBox">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div class="modal-tag" id="mTag"></div>
    <h2 id="mTitle"></h2>
    <div id="mBody"></div>
  </div>
</div>

<script>
const data=[
  {
    tag:'Course I · Introduction',
    title:'Who Am I?',
    body:`<p>Born from a deep love of flavor and form, Reda El Ghalbzouri discovered pastry not merely as a craft, but as a language — one that speaks directly to the senses and the soul.</p>
    <p>Trained in the classical traditions of French pâtisserie, Reda has spent over a decade refining a style that marries rigorous technique with genuine emotion. Every creation begins with a question: <em>What should the guest feel?</em></p>
    <p>From his earliest memory of a grandmother's sfenj dusted in sugar, to the first chocolate tempered at culinary school, Reda's journey has been one of relentless curiosity and respectful evolution.</p>`
  },
  {
    tag:'Course II · The Art',
    title:'My Craft',
    body:`<p>A complete pastry vision, from the ethereal to the intense:</p>
    <ul>
      <li>Chocolate Work — Ganaches, tempering, sculpted showpieces</li>
      <li>Viennoiserie — Croissants, kouign-amann, laminated doughs</li>
      <li>Entremets & Mousses — Multi-layered modern cakes</li>
      <li>Modern Plated Desserts — Fine dining à la minute service</li>
      <li>Sugar Techniques — Pulled, blown, spun & isomalt work</li>
      <li>Mignardises & Petit Fours — The final impression</li>
    </ul>`
  },
  {
    tag:'Course III · Creations',
    title:'Portfolio',
    body:`<p>A curated selection of signature creations — where technique meets poetry.</p>
    <div class="gallery">
      <div class="gallery-item" style="background:linear-gradient(135deg,#f0e8d8,#e8c88a)">🍮</div>
      <div class="gallery-item" style="background:linear-gradient(135deg,#e8c88a,#d4a055)">🍫</div>
      <div class="gallery-item" style="background:linear-gradient(135deg,#d4a055,#8b5e3c)">🥐</div>
      <div class="gallery-item" style="background:linear-gradient(135deg,#8b5e3c,#3d2518)">🍰</div>
    </div>
    <p style="margin-top:1rem;font-size:.8rem;opacity:.6;font-style:italic">Gallery available upon professional inquiry.</p>`
  },
  {
    tag:'Course IV · Journey',
    title:'Experience',
    body:`<p>A career built in the world's most demanding kitchens, under the guidance of masters:</p>
    <ul>
      <li>5-Star Luxury Hotel, Casablanca — Head Pastry Chef</li>
      <li>Gastronomy Training, Institut Paul Bocuse, Lyon</li>
      <li>Chocolate Atelier, Brussels — Advanced Confectionery</li>
      <li>Michelin-starred Restaurant, Paris — Stagière, Pastry Section</li>
      <li>Private Catering & Events — Bespoke dessert experiences</li>
    </ul>`
  },
  {
    tag:'Course V · Vision',
    title:'Philosophy',
    body:`<p>Reda believes that pastry is one of the few arts capable of triggering memory, emotion, and presence simultaneously. His philosophy rests on four pillars:</p>
    <ul>
      <li><strong>Balance</strong> — No element dominates; all serve the whole</li>
      <li><strong>Emotion</strong> — A dessert must tell a story worth feeling</li>
      <li><strong>Texture</strong> — Contrast is the soul of sensation</li>
      <li><strong>Elegance</strong> — Restraint is the highest form of confidence</li>
    </ul>
    <p>In Reda's kitchen, nothing is accidental. Every crumb, glaze, and garnish is a deliberate act of authorship.</p>`
  },
  {
    tag:'Course VI · Collaborate',
    title:'Contact & Vision',
    body:`<p>Reda is available for creative partnerships, consulting, and collaborative projects that share a commitment to excellence.</p>
    <ul>
      <li>Pastry consulting for restaurants & hotels</li>
      <li>Brand collaborations & product development</li>
      <li>Private events & bespoke tasting menus</li>
      <li>Masterclasses & culinary workshops</li>
    </ul>
    <p><strong>Email:</strong> reda@example.com<br>
    <strong>LinkedIn:</strong> linkedin.com/in/reda-elghalbzouri</p>
    <a class="cta-btn" href="mailto:reda@example.com" style="display:inline-block;margin-top:1rem">Begin the Conversation</a>`
  }
];

function openModal(i){
  const d=data[i];
  document.getElementById('mTag').textContent=d.tag;
  document.getElementById('mTitle').textContent=d.title;
  document.getElementById('mBody').innerHTML=d.body;
  document.getElementById('modalOverlay').classList.add('open');
  document.body.style.overflow='hidden';
}
function closeModal(){
  document.getElementById('modalOverlay').classList.remove('open');
  document.body.style.overflow='';
}
function closeModalOutside(e){
  if(e.target===document.getElementById('modalOverlay'))closeModal();
}

// Intersection Observer for scroll reveals
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting)e.target.classList.add('visible');
  });
},{threshold:.2});
obs.observe(document.getElementById('intro-text'));
obs.observe(document.getElementById('plateWrap'));
obs.observe(document.getElementById('invoiceEl'));

// Keyboard close
document.addEventListener('keydown',e=>{if(e.key==='Escape')closeModal()});
</script>
</body>
</html>
