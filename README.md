<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>💕 برای تو</title>
  <link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@700;900&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    html, body { width: 100%; height: 100%; overflow: hidden; direction: rtl; }

    body {
      font-family: 'Vazirmatn', Tahoma, sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #03001a;
    }

    /* ====== BACKGROUND ====== */
    #bg {
      position: fixed; inset: 0; z-index: 0;
      background-image: url('https://images.unsplash.com/photo-1490750967868-88df5691cc4e?w=1920&q=80');
      background-size: cover;
      background-position: center;
      filter: brightness(0.55) saturate(1.8) hue-rotate(200deg);
      transition: filter 1.5s ease;
    }
    #bg.awake { filter: brightness(0.72) saturate(2.2) hue-rotate(210deg); }

    /* Red pulsing vignette */
    #vignette {
      position: fixed; inset: 0; z-index: 1; pointer-events: none;
      background:
        radial-gradient(ellipse 70% 50% at 0% 0%,   rgba(180,0,0,0.50), transparent),
        radial-gradient(ellipse 70% 50% at 100% 100%, rgba(180,0,0,0.50), transparent),
        radial-gradient(ellipse 40% 40% at 50% 50%,  rgba(0,0,0,0.25),  transparent);
      animation: vPulse 3.5s ease-in-out infinite alternate;
    }
    @keyframes vPulse { from { opacity: 0.55; } to { opacity: 1; } }

    /* ====== HEARTS LAYER ====== */
    #hearts { position: fixed; inset: 0; z-index: 100; pointer-events: none; overflow: hidden; }
    .hp {
      position: absolute;
      bottom: -40px;
      opacity: 0;
      animation: heartRise linear forwards;
    }
    @keyframes heartRise {
      0%   { opacity: 0;   transform: translateY(0)      rotate(0deg)   scale(0.5); }
      6%   { opacity: 1; }
      88%  { opacity: 0.8; }
      100% { opacity: 0;   transform: translateY(-115vh) rotate(540deg) scale(1.1); }
    }

    /* ====== SCENE ====== */
    .scene {
      position: relative; z-index: 10;
      width: 360px; height: 500px;
      display: flex; align-items: flex-end; justify-content: center;
    }

    /* ====== BOX WRAPPER ====== */
    .box-wrap {
      position: absolute; bottom: 0; left: 50%;
      transform: translateX(-50%);
      width: 300px;
      cursor: pointer;
      user-select: none;
      -webkit-tap-highlight-color: transparent;
    }

    /* ---- LID ---- */
    .lid {
      width: calc(100% + 10px);
      margin-left: -5px;
      height: 46px;
      background: linear-gradient(150deg, #C06020 0%, #904010 45%, #5C2808 100%);
      border-radius: 12px 12px 0 0;
      border: 3.5px solid #CC0000;
      border-bottom: 2px solid rgba(255,170,80,0.15);
      position: relative;
      box-shadow:
        0 -8px 24px rgba(200,0,0,0.35),
        inset 0 1px 0 rgba(255,200,120,0.25),
        inset 0 -2px 6px rgba(0,0,0,0.35);
      transform-origin: top center;
      transition: transform 0.75s cubic-bezier(0.34, 1.1, 0.64, 1);
    }
    /* wood grain on lid */
    .lid::after {
      content: '';
      position: absolute; inset: 0; border-radius: 10px 10px 0 0;
      background: repeating-linear-gradient(
        87deg, transparent 0, transparent 18px,
        rgba(0,0,0,0.06) 18px, rgba(0,0,0,0.06) 20px
      );
    }
    .box-wrap.open .lid { transform: rotateX(-135deg); }

    /* ---- BODY ---- */
    .body {
      height: 155px;
      background: linear-gradient(165deg, #8B4513 0%, #6A3110 45%, #45200A 100%);
      border-radius: 0 0 16px 16px;
      border: 3.5px solid #CC0000;
      border-top: none;
      box-shadow:
        0 0 48px rgba(200,0,0,0.6),
        0 22px 65px rgba(0,0,0,0.9),
        inset 0 0 30px rgba(0,0,0,0.45),
        inset 3px 0 8px rgba(255,190,100,0.04),
        inset -3px 0 8px rgba(255,190,100,0.04);
      display: flex; align-items: center; justify-content: center;
      padding: 20px; position: relative; overflow: hidden;
      transition: box-shadow 0.35s;
    }
    .box-wrap:hover .body {
      box-shadow:
        0 0 72px rgba(255,60,60,0.75),
        0 22px 65px rgba(0,0,0,0.9),
        inset 0 0 30px rgba(0,0,0,0.45);
    }
    /* wood grain */
    .body::before {
      content: ''; position: absolute; inset: 0;
      background: repeating-linear-gradient(
        89deg, transparent 0, transparent 19px,
        rgba(0,0,0,0.05) 19px, rgba(0,0,0,0.05) 21px
      );
    }
    /* vertical ribbon */
    .rib-v {
      position: absolute; top: 0; left: 50%; bottom: 0; width: 5px;
      background: linear-gradient(to bottom, #CC0000 0%, #8B0000 50%, #CC0000 100%);
      transform: translateX(-50%);
      box-shadow: 0 0 10px rgba(255,0,0,0.55);
    }
    /* horizontal ribbon */
    .rib-h {
      position: absolute; left: 0; right: 0; top: 50%; height: 5px;
      background: linear-gradient(to right, #CC0000 0%, #8B0000 50%, #CC0000 100%);
      transform: translateY(-50%);
      box-shadow: 0 0 10px rgba(255,0,0,0.55);
    }
    /* bow */
    .bow {
      position: absolute; top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      width: 32px; height: 32px;
      background: radial-gradient(circle at 40% 38%, #FF6666, #CC0000 55%);
      border-radius: 50%;
      border: 2.5px solid rgba(255,140,140,0.85);
      box-shadow: 0 0 22px rgba(255,0,0,0.95), 0 0 7px rgba(255,0,0,0.6);
      z-index: 2;
    }

    .box-text {
      color: #FF5050;
      font-size: 1.1rem;
      font-weight: 900;
      text-align: center;
      line-height: 1.9;
      text-shadow:
        0 0 16px rgba(255,50,50,0.95),
        0 0  6px rgba(255,50,50,0.6),
        0 2px 5px rgba(0,0,0,0.9);
      z-index: 3;
      transition: opacity 0.3s;
    }
    .box-wrap.open .box-text { opacity: 0; }

    /* ====== BEAR ====== */
    .bear-wrap {
      position: absolute;
      bottom: 118px; left: 50%;
      transform: translateX(-50%) scale(0) translateY(30px);
      transition: transform 1s cubic-bezier(0.34, 1.6, 0.64, 1);
      display: flex; flex-direction: column; align-items: center; gap: 10px;
      pointer-events: none; z-index: 30;
    }
    .bear-wrap.pop {
      transform: translateX(-50%) scale(1) translateY(-15px);
    }

    /* Speech bubble */
    .bubble {
      background: rgba(255,255,255,0.97);
      border: 3px solid #CC0000;
      border-radius: 22px;
      padding: 11px 26px;
      box-shadow:
        0 6px 35px rgba(204,0,0,0.55),
        0 2px 8px rgba(0,0,0,0.2);
      position: relative;
      opacity: 0;
      transform: scale(0.65) translateY(-8px);
      transition: opacity 0.5s 0.85s, transform 0.5s 0.85s;
    }
    .bear-wrap.pop .bubble { opacity: 1; transform: scale(1) translateY(0); }

    /* bubble tail */
    .bubble::after {
      content: ''; position: absolute;
      bottom: -20px; left: 50%; transform: translateX(-50%);
      border: 10px solid transparent; border-top-color: #CC0000;
    }
    .bubble::before {
      content: ''; position: absolute;
      bottom: -13px; left: 50%; transform: translateX(-50%);
      border: 8px solid transparent; border-top-color: rgba(255,255,255,0.97);
      z-index: 1;
    }

    #phrase {
      color: #7a0000;
      font-size: 0.98rem;
      font-weight: 900;
      white-space: nowrap;
      transition: opacity 0.38s;
      letter-spacing: 0.02em;
    }

    /* Bear face */
    .bear-face {
      font-size: 90px;
      filter: drop-shadow(0 10px 22px rgba(0,0,0,0.7));
      animation: bearBounce 1.1s ease-in-out infinite alternate;
      display: block;
    }
    @keyframes bearBounce {
      from { transform: rotate(-8deg) scale(1);    }
      to   { transform: rotate( 8deg) scale(1.13); }
    }

    /* ====== SHAKE ANIMATION ====== */
    @keyframes shakeBox {
      0%,100% { transform: translateX(-50%); }
      15%     { transform: translateX(calc(-50% - 9px)) rotate(-4deg); }
      35%     { transform: translateX(calc(-50% + 9px)) rotate( 4deg); }
      55%     { transform: translateX(calc(-50% - 6px)) rotate(-2.5deg); }
      75%     { transform: translateX(calc(-50% + 6px)) rotate( 2.5deg); }
    }
    .shaking { animation: shakeBox 0.55s ease; }

    /* ====== SPARKLES ====== */
    .spark {
      position: absolute; pointer-events: none;
      font-size: 20px;
      animation: sparkFly 0.9s ease forwards;
    }
    @keyframes sparkFly {
      from { opacity: 1; transform: scale(0) rotate(0deg);   }
      to   { opacity: 0; transform: scale(1.6) rotate(200deg) translate(var(--tx), var(--ty)); }
    }

    /* ====== TOOLTIP on load ====== */
    #hint {
      position: fixed; bottom: 28px; left: 50%; transform: translateX(-50%);
      background: rgba(0,0,0,0.55); backdrop-filter: blur(8px);
      border: 1px solid rgba(255,80,80,0.4);
      color: rgba(255,160,160,0.9);
      font-family: 'Vazirmatn', Tahoma, sans-serif;
      font-size: 0.78rem; font-weight: 700;
      padding: 7px 20px; border-radius: 50px;
      pointer-events: none; z-index: 200;
      animation: hintPulse 2s ease-in-out infinite alternate;
      letter-spacing: 0.03em;
    }
    @keyframes hintPulse {
      from { opacity: 0.65; }
      to   { opacity: 1; }
    }
    #hint.hide { opacity: 0; transition: opacity 0.5s; }
  </style>
</head>
<body>
  <div id="bg"></div>
  <div id="vignette"></div>
  <div id="hearts"></div>

  <div class="scene">
    <!-- Bear (hidden until box is clicked) -->
    <div class="bear-wrap" id="bearWrap">
      <div class="bubble">
        <p id="phrase">دوست دارم دختر کوچولوم 💕</p>
      </div>
      <span class="bear-face">🐻</span>
    </div>

    <!-- Box -->
    <div class="box-wrap" id="boxWrap" onclick="clickBox()">
      <div class="lid" id="lid"></div>
      <div class="body">
        <div class="rib-v"></div>
        <div class="rib-h"></div>
        <div class="bow"></div>
        <p class="box-text">اگه روم کلیک کنی<br>گازت میگیرم! 😤</p>
      </div>
    </div>
  </div>

  <p id="hint">روی جعبه کلیک کن 🎁</p>

  <script>
    /* =========================================
       LULLABY ENGINE  (Web Audio API)
    ========================================= */
    let ac = null, musicPlaying = false;

    function getAC() {
      if (!ac) ac = new (window.AudioContext || window.webkitAudioContext)();
      if (ac.state === 'suspended') ac.resume();
      return ac;
    }

    function note(hz, tSec, durSec, vol = 0.13) {
      const a   = getAC();
      const now = a.currentTime;

      function voice(freq, v) {
        const o = a.createOscillator();
        const g = a.createGain();
        o.connect(g); g.connect(a.destination);
        o.type = 'sine';
        o.frequency.value = freq;
        const t = now + tSec;
        g.gain.setValueAtTime(0, t);
        g.gain.linearRampToValueAtTime(v, t + 0.07);
        g.gain.exponentialRampToValueAtTime(0.0001, t + durSec * 0.92);
        o.start(t); o.stop(t + durSec + 0.06);
      }

      voice(hz,       vol);          // fundamental
      voice(hz * 2,   vol * 0.22);   // 1st overtone (piano-like)
      voice(hz * 3,   vol * 0.08);   // warmth
    }

    function startLullaby() {
      if (musicPlaying) return;
      musicPlaying = true;

      // Note frequencies
      const C3=130.81, F3=174.61, G3=196;
      const C4=261.63, D4=293.66, E4=329.63, F4=349.23, G4=392, A4=440;

      const q = 0.46; // quarter note = 0.46s → ≈ 130 BPM (lullaby pace)

      // Melody: Twinkle Twinkle (lullaby feel)
      const mel = [
        [C4,0,2],[C4,2,2],[G4,4,2],[G4,6,2],[A4,8,2],[A4,10,2],[G4,12,4],
        [F4,16,2],[F4,18,2],[E4,20,2],[E4,22,2],[D4,24,2],[D4,26,2],[C4,28,4],
        [G4,32,2],[G4,34,2],[F4,36,2],[F4,38,2],[E4,40,2],[E4,42,2],[D4,44,4],
        [G4,48,2],[G4,50,2],[F4,52,2],[F4,54,2],[E4,56,2],[E4,58,2],[D4,60,4],
        [C4,64,2],[C4,66,2],[G4,68,2],[G4,70,2],[A4,72,2],[A4,74,2],[G4,76,4],
        [F4,80,2],[F4,82,2],[E4,84,2],[E4,86,2],[D4,88,2],[D4,90,2],[C4,92,4]
      ].map(([f,b,d]) => [f, b*q, d*q]);

      // Bass (left hand)
      const bass = [
        [C3,0,8],[G3,8,8],[C3,16,8],[G3,24,8],
        [C3,32,8],[G3,40,8],[C3,48,8],[G3,56,8],
        [C3,64,8],[G3,72,4],[G3,76,4],[F3,80,4],[C3,84,4],[C3,88,8]
      ].map(([f,b,d]) => [f, b*q, d*q]);

      const loopMs = 96 * q * 1000;

      (function loop() {
        mel.forEach(([f,t,d])  => note(f, t, d, 0.13));
        bass.forEach(([f,t,d]) => note(f, t, d, 0.07));
        setTimeout(loop, loopMs - 80);
      })();
    }

    // Attempt autoplay immediately (works in some browsers)
    window.addEventListener('load', () => { try { startLullaby(); } catch(e) {} });

    // Guaranteed start on any user gesture
    ['click','touchstart','keydown','pointerdown'].forEach(ev =>
      document.addEventListener(ev, () => startLullaby(), { passive: true })
    );

    /* =========================================
       BOX INTERACTION
    ========================================= */
    let opened = false;

    function clickBox() {
      startLullaby(); // ensure music if not already playing

      if (opened) return;
      opened = true;

      const wrap  = document.getElementById('boxWrap');
      const bear  = document.getElementById('bearWrap');
      const bg    = document.getElementById('bg');
      const hint  = document.getElementById('hint');

      hint.classList.add('hide');
      wrap.style.cursor = 'default';
      wrap.classList.add('shaking');

      // spawn sparkles from box corners
      const dirs = [
        [-55,-55],[55,-55],[-55,-10],[55,-10],[0,-70],[0,-20],[-35,-75],[35,-75]
      ];
      dirs.forEach(([tx,ty], i) => {
        setTimeout(() => {
          const sp = document.createElement('span');
          sp.className = 'spark';
          sp.textContent = ['✨','💫','⭐','🌟','❤️'][Math.floor(Math.random()*5)];
          sp.style.setProperty('--tx', tx + 'px');
          sp.style.setProperty('--ty', ty + 'px');
          sp.style.left = (30 + Math.random()*40) + '%';
          sp.style.top  = (20 + Math.random()*40) + '%';
          wrap.appendChild(sp);
          setTimeout(() => sp.remove(), 950);
        }, i * 65);
      });

      // Open lid → show bear
      setTimeout(() => {
        wrap.classList.add('open');
        bg.classList.add('awake');

        setTimeout(() => {
          bear.classList.add('pop');
          startPhraseLoop();
          startHearts();
        }, 650);
      }, 560);
    }

    /* =========================================
       PHRASE LOOP
    ========================================= */
    const phrases = [
      'دوست دارم دختر کوچولوم 💕',
      '🐻 دوستت دارم 💕',
      'روزت مبارک قشنکککککم 💕',
      '💖 دختر کوچولوم 💖',
      'دوست دارم دختر کوچولوم 💕',
      '🌹 عاشقتم کوچولو 🌹',
    ];

    function startPhraseLoop() {
      const el = document.getElementById('phrase');
      let idx = 0;
      setInterval(() => {
        el.style.opacity = '0';
        setTimeout(() => {
          idx = (idx + 1) % phrases.length;
          el.textContent = phrases[idx];
          el.style.opacity = '1';
        }, 380);
      }, 2300);
    }

    /* =========================================
       HEART RAIN
    ========================================= */
    function startHearts() {
      const container = document.getElementById('hearts');
      const emojis = ['❤️','💕','💖','💗','🌹','💝','🐾','✨','💫'];

      function drop() {
        const el = document.createElement('div');
        el.className = 'hp';
        el.textContent = emojis[Math.floor(Math.random() * emojis.length)];
        el.style.left = Math.random() * 94 + 'vw';
        el.style.fontSize = (13 + Math.random() * 22) + 'px';
        const dur = 3.8 + Math.random() * 4;
        el.style.animationDuration = dur + 's';
        container.appendChild(el);
        setTimeout(() => el.remove(), (dur + 0.5) * 1000);
      }

      setInterval(drop, 460);
    }
  </script>
</body>
</html>
