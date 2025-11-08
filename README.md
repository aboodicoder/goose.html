<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>EXTREME DEMO w/ Glitch Sounds — Visual Ransomware Style (PRANK / NOT REAL)</title>
<style>
  :root{
    --bg-black: #040000;
    --deep-red: #2a0000;
    --accent-red: #ff3030;
    --pale: #ffdede;
    --muted: #f0bcbc;
  }
  html,body{height:100%;margin:0;font-family:"Lucida Console", Monaco, monospace;background:var(--bg-black);color:var(--pale);-webkit-font-smoothing:antialiased}
  .wrap{min-height:100vh;display:flex;flex-direction:column;align-items:stretch;justify-content:flex-start;box-sizing:border-box;padding:0;margin:0;position:relative;overflow-x:hidden}
  .backdrop { position:fixed;inset:0;z-index:0;pointer-events:none;
    background:radial-gradient(circle at 20% 20%, rgba(255,0,0,0.06), transparent 6%),
               radial-gradient(circle at 80% 80%, rgba(255,0,0,0.04), transparent 10%);
    mix-blend-mode:screen; animation: slowPulse 3s ease-in-out infinite, screenFlicker 4s steps(6, end) infinite; }
  @keyframes slowPulse { 0%{filter:blur(2px);opacity:0.6} 50%{filter:blur(18px);opacity:1} 100%{filter:blur(2px);opacity:0.6} }
  @keyframes screenFlicker { 0%{opacity:1} 3%{opacity:0.85} 6%{opacity:1} 100%{opacity:1} }

  .container{position:relative;z-index:2;max-width:1200px;margin:28px auto;padding:22px;border-radius:6px;
    background:linear-gradient(180deg, rgba(0,0,0,0.35), rgba(0,0,0,0.65)); border:6px solid rgba(80,0,0,0.7);box-shadow:0 40px 120px rgba(0,0,0,0.8);}
  .toprow{display:flex;gap:18px;align-items:center}
  .title{font-size:28px;color:var(--accent-red);margin:0;letter-spacing:1px}
  .sub{font-size:13px;color:var(--muted);margin:0}

  .main { margin-top:18px;padding:20px;border-radius:8px;background:linear-gradient(180deg, rgba(30,0,0,0.85), rgba(10,0,0,0.95)); display:flex;gap:20px;align-items:flex-start;border:2px solid rgba(255,40,40,0.08); }

  .lock { width:180px;height:180px;flex:0 0 180px;border-radius:10px; display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.08)); border:2px solid rgba(255,255,255,0.03); transform:translateY(0); animation: lockBob 1.8s ease-in-out infinite; }
  @keyframes lockBob { 0%{transform:translateY(0)}50%{transform:translateY(-6px)}100%{transform:translateY(0)} }
  .lock svg{width:120px;height:120px;display:block;stroke:var(--accent-red);fill:none;stroke-width:1.6}
  .message{flex:1}
  .huge{font-size:46px;line-height:1;color:#ffbfbf;margin:0 0 6px;text-transform:uppercase;letter-spacing:2px;text-shadow:0 8px 30px rgba(255,0,0,0.08)}
  .subline{font-size:16px;margin:0 0 12px;color:var(--muted)}
  .filecount{font-size:58px;font-weight:800;color:var(--accent-red);margin:8px 0 6px;text-shadow:0 12px 36px rgba(255,0,0,0.08)}

  .scanlines:before, .scanlines:after{ content:"";position:absolute;left:0;right:0;top:0;height:100%;
    background-image:linear-gradient(transparent 92%, rgba(255,0,0,0.02) 92%); background-size:100% 6px;pointer-events:none;mix-blend-mode:overlay;opacity:0.9;z-index:1; animation: scanMove 6s linear infinite; }
  @keyframes scanMove { 0%{transform:translateY(0)}100%{transform:translateY(6px)} }

  .glitch { position:relative; display:inline-block; }
  .glitch::before, .glitch::after { content: attr(data-text); position:absolute;left:0;top:0; overflow:hidden; clip:rect(0,900px,0,0); }
  .glitch::before { left:2px; text-shadow:-2px 0 rgba(255,0,0,0.7); animation: glitchTop 2.4s infinite linear; opacity:0.9; color:#ffdede }
  .glitch::after { left:-2px; text-shadow:2px 0 rgba(0,255,0,0.05); animation: glitchBot 3s infinite linear; opacity:0.9; color:#ffdede }
  @keyframes glitchTop { 0%{clip:rect(0,9999px,0,0)} 10%{clip:rect(0,9999px,30px,0)} 20%{clip:rect(60px,9999px,90px,0)} 30%{clip:rect(0,9999px,9999px,0)} 100%{clip:rect(0,9999px,0,0)} }
  @keyframes glitchBot { 0%{clip:rect(0,9999px,0,0)} 15%{clip:rect(120px,9999px,160px,0)} 35%{clip:rect(0,9999px,60px,0)} 100%{clip:rect(0,9999px,0,0)} }

  .gibberish { margin-top:18px;height:560px;overflow:auto;padding:14px;border-radius:6px;background:#0b0000;border:1px dashed rgba(255,255,255,0.03); color:#ffdede;font-size:13px;line-height:1.14;white-space:pre-wrap;word-break:break-all;box-shadow:inset 0 0 45px rgba(255,0,0,0.02); }

  .reveal { display:none;margin-top:18px;padding:18px;border-radius:8px;background:linear-gradient(180deg,#063a15,#042916);border:2px solid rgba(0,0,0,0.6); color:#d6f6dc;font-size:16px;box-shadow:0 18px 50px rgba(0,0,0,0.6); }

  .bottom-disclaimer { position:fixed;left:0;right:0;bottom:0;z-index:9999; background:linear-gradient(90deg, rgba(80,0,0,0.98), rgba(160,0,0,0.96)); color:#fff;padding:8px 12px;font-size:13px;display:flex;align-items:center;gap:12px;border-top:3px solid rgba(255,255,255,0.04); box-shadow:0 -10px 30px rgba(0,0,0,0.6); }
  .bottom-disclaimer strong{font-weight:700;letter-spacing:0.6px}
  .bottom-disclaimer small{opacity:0.92;color:#ffdede}

  .controls{margin-top:8px;display:flex;gap:8px}
  button{background:transparent;border:2px solid rgba(255,255,255,0.06);color:var(--pale);padding:10px 14px;border-radius:6px;cursor:pointer;font-family:inherit}
  kbd{background:#111;color:#ffdede;border-radius:4px;padding:2px 6px;font-size:12px;border:1px solid rgba(255,255,255,0.04)}
  .sound-controls{display:flex;gap:8px;align-items:center;margin-left:8px}

  @media (max-width:820px){
    .lock{width:120px;height:120px;flex:0 0 120px}
    .huge{font-size:28px}
    .filecount{font-size:42px}
    .gibberish{height:420px}
    .sound-controls{flex-wrap:wrap}
  }
</style>
</head>
<body>
  <div class="wrap" role="document">
    <div class="backdrop" aria-hidden="true"></div>

    <div class="container scanlines" role="main" aria-labelledby="mainTitle">
      <div class="toprow">
        <div>
          <h1 id="mainTitle" class="title glitch" data-text="SYSTEM ALERT — IMMEDIATE">SYSTEM ALERT — IMMEDIATE</h1>
          <p class="sub">This demo is visual-only. Scroll down to the bottom to reveal the harmless message.</p>
        </div>
      </div>

      <div class="main" role="region" aria-label="Threat display">
        <div class="lock" aria-hidden="true">
          <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="3.5" y="9" width="17" height="11" rx="2.5" stroke="currentColor"/>
            <path d="M8 9V6.8C8 4.2 10.2 2 12.8 2S17.6 4.2 17.6 6.8V9" stroke="currentColor"/>
            <circle cx="12" cy="14.5" r="1.6" fill="currentColor"/>
          </svg>
        </div>

        <div class="message">
          <div class="huge glitch" data-text="YOUR FILES ARE ENCRYPTED">YOUR FILES ARE ENCRYPTED</div>
          <div class="subline">All sensitive data has been locked. System tag: <strong>DEMO-0xEXTREME</strong></div>
          <div id="fileCount" class="filecount">Locked: 0</div>

          <div style="display:flex;gap:10px;align-items:center;justify-content:flex-start;">
            <div class="controls">
              <button id="revealBtn">Reveal now</button>
              <button id="holdBtn">Hold demo</button>
            </div>

            <!-- SOUND CONTROLS -->
            <div class="sound-controls" aria-hidden="false" title="Sound controls">
              <button id="toggleSoundBtn" aria-pressed="false">Enable Sound</button>
              <label style="display:flex;align-items:center;gap:6px;color:var(--muted);font-size:13px">
                Vol
                <input id="volSlider" type="range" min="0" max="100" value="9" step="1" style="width:120px" aria-label="Sound volume">
              </label>
            </div>

            <div style="margin-left:16px;color:var(--muted);font-size:13px">Tip: Press <kbd>Esc</kbd> or scroll to the bottom.</div>
          </div>
        </div>
      </div>

      <div id="gibberish" class="gibberish" aria-hidden="true"></div>

      <div id="revealPanel" class="reveal" role="status" aria-live="polite">
        <h2 style="margin:0 0 8px">🎉 Peace — Harmless Demo!</h2>
        <p style="margin:0 0 8px">This page does not encrypt files, request money, or change anything on your computer. It is a theatrical, local-only demo for fun.</p>
        <p style="margin:0;color:#bfe5c9">If you need me to tone it up/down, swap the lock graphic, or change how the disclaimer looks — say the word.</p>
      </div>
    </div>

    <div style="height:900px;min-height:60vh"></div>

    <div class="bottom-disclaimer" role="note" aria-live="polite">
      <strong>PRANK / DEMO — NOT REAL</strong>
      <small>This is a theatrical visual demo only. It does NOT encrypt, delete, or lock files. Make sure the person seeing this understands it's a harmless demo.</small>
    </div>
  </div>

<script>
/* ---------- Visual behavior (same as before) ---------- */
(function makeGibberish(){
  const el = document.getElementById('gibberish');
  const chars = "!@#$%^&*()_+[]{};:,.<>?/|\\~=-abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
  const out = [];
  out.push(">> INIT: DEMO RENDER PIPELINE START");
  out.push(">> LOADING MODULE: visually_intense_renderer v2.7");
  out.push(">> SUBSYSTEM: encryption-mock (read-only)");
  out.push("");
  for (let i=0;i<1600;i++){
    if (Math.random() < 0.02) {
      let block = "";
      for (let j=0;j<8;j++) block += Math.floor(Math.random()*0xFFFFFFFF).toString(16).padStart(8,'0') + " ";
      out.push(block);
    } else {
      let len = 70 + Math.floor(Math.random()*80);
      let line = "";
      for (let j=0;j<len;j++) line += chars.charAt(Math.floor(Math.random()*chars.length));
      out.push(line);
    }
  }
  out.push("");
  out.push("!!! SYSTEM: CRITICAL VISUAL STATE REACHED !!!");
  el.textContent = out.join("\n");
})();

const cntEl = document.getElementById('fileCount');
let files = 0;
const incr = setInterval(()=>{
  const add = Math.floor(Math.random()*120);
  files += add;
  if (files > 1234567) files = 1234567;
  cntEl.textContent = "Locked: " + files.toLocaleString();
  if (Math.random() < 0.07) files += 500 + Math.floor(Math.random()*2000);
  if (files >= 1234567) clearInterval(incr);
}, 420);

const revealPanel = document.getElementById('revealPanel');
function reveal(reason){
  if (revealPanel.style.display === 'block') return;
  revealPanel.style.display = 'block';
  revealPanel.scrollIntoView({behavior:'smooth', block:'center'});
  for (let i=0;i<40;i++){
    const e = document.createElement('div');
    e.textContent = ['🎉','✨','💚'][Math.floor(Math.random()*3)];
    e.style.position='fixed';
    e.style.left = (Math.random()*70+15) + '%';
    e.style.top = (Math.random()*70+10) + '%';
    e.style.fontSize = (12 + Math.random()*42) + 'px';
    e.style.opacity = Math.random();
    e.style.zIndex = 10001;
    document.body.appendChild(e);
    setTimeout(()=>e.remove(),2600);
  }
}

document.getElementById('revealBtn').addEventListener('click', ()=> reveal('manual'));
document.getElementById('holdBtn').addEventListener('click', ()=> alert('Demo will continue. Scroll to bottom or press Esc to reveal.'));

window.addEventListener('keydown', (e)=> { if (e.key === 'Escape') reveal('esc'); });

window.addEventListener('scroll', ()=>{
  const atBottom = (window.innerHeight + window.scrollY) >= (document.documentElement.scrollHeight - 8);
  if (atBottom) reveal('scrolled');
});

/* ---------- SOUND: Web Audio API Glitch Engine ---------- */
/*
 Behavior:
  - Engine is created but will remain suspended until the user enables sound (or interacts).
  - "Enable Sound" toggles sound on/off.
  - Volume slider adjusts master gain (0 - 100; default 9).
  - Sounds are short, randomized bursts (noise + bandpass + oscillator chirps + clicks).
  - Playbacks occur at random intervals (configurable below).
*/
let audioCtx = null;
let masterGain = null;
let soundEnabled = false;
let glitchTimer = null;
const defaultVol = 0.09; // low default (~9%)
const toggleSoundBtn = document.getElementById('toggleSoundBtn');
const volSlider = document.getElementById('volSlider');

function ensureAudioContext() {
  if (!audioCtx) {
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    masterGain = audioCtx.createGain();
    masterGain.gain.value = defaultVol;
    masterGain.connect(audioCtx.destination);
  }
}

// small helper to create white noise buffer source
function playNoiseBurst(duration = 0.08, freqCenter = 1200, bandQ = 1.5){
  if (!audioCtx) return;
  const buf = audioCtx.createBuffer(1, audioCtx.sampleRate * duration, audioCtx.sampleRate);
  const data = buf.getChannelData(0);
  for (let i=0;i<data.length;i++) data[i] = (Math.random()*2 - 1) * (Math.random() < 0.4 ? 0.9 : 0.35);
  const src = audioCtx.createBufferSource();
  src.buffer = buf;

  const bp = audioCtx.createBiquadFilter();
  bp.type = 'bandpass';
  bp.frequency.value = freqCenter + (Math.random()*400 - 200);
  bp.Q.value = bandQ + Math.random()*1.5;

  const g = audioCtx.createGain();
  g.gain.setValueAtTime(0.0001, audioCtx.currentTime);
  g.gain.exponentialRampToValueAtTime(0.8, audioCtx.currentTime + 0.005 + Math.random()*0.02);
  g.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);

  src.connect(bp);
  bp.connect(g);
  g.connect(masterGain);
  src.start();
  src.stop(audioCtx.currentTime + duration + 0.02);
}

// short oscillator chirp (sine/triangle) for melodic glitch
function playChirp(duration = 0.06, startFreq = 300, endFreq = 1200, type = 'sine'){
  if (!audioCtx) return;
  const o = audioCtx.createOscillator();
  o.type = type;
  o.frequency.setValueAtTime(startFreq * (1 + Math.random()*0.08), audioCtx.currentTime);
  o.frequency.exponentialRampToValueAtTime(endFreq * (1 + Math.random()*0.08), audioCtx.currentTime + duration);

  const g = audioCtx.createGain();
  g.gain.setValueAtTime(0.0001, audioCtx.currentTime);
  g.gain.exponentialRampToValueAtTime(0.9, audioCtx.currentTime + 0.007);
  g.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);

  // optional slight detune + filter to make it glitchy
  const fl = audioCtx.createBiquadFilter();
  fl.type = 'lowpass';
  fl.frequency.value = 800 + Math.random()*2200;

  o.connect(fl);
  fl.connect(g);
  g.connect(masterGain);
  o.start();
  o.stop(audioCtx.currentTime + duration + 0.02);
}

// click / pop using very short noise burst
function playClick(){
  playNoiseBurst(0.03, 5000, 0.7);
}

// one composite glitch event composed of several micro-sounds
function playGlitchEvent(){
  if (!audioCtx) return;
  const pick = Math.random();
  if (pick < 0.25) {
    playNoiseBurst(0.06, 800 + Math.random()*3000, 1 + Math.random()*3);
    setTimeout(()=>{ if (Math.random() < 0.6) playClick(); }, 40 + Math.random()*80);
  } else if (pick < 0.6) {
    playChirp(0.05 + Math.random()*0.08, 220 + Math.random()*160, 800 + Math.random()*2200, Math.random() < 0.5 ? 'sine' : 'triangle');
    if (Math.random() < 0.5) setTimeout(()=>playNoiseBurst(0.04, 1000 + Math.random()*2000, 1.2), 30);
  } else {
    // bursty multi-click cluster
    for (let i=0;i<1 + Math.floor(Math.random()*4); i++){
      setTimeout(()=>playClick(), i * (10 + Math.random()*70));
    }
    if (Math.random() < 0.4) setTimeout(()=>playChirp(0.06, 400, 1200, 'sine'), 80);
  }
}

// start the randomized glitch scheduler
function startGlitchScheduler(){
  if (!audioCtx) ensureAudioContext();
  if (!audioCtx) return;
  if (glitchTimer) clearTimeout(glitchTimer);
  const schedule = () => {
    if (!soundEnabled) return;
    // random interval that favors sparse events but sometimes quick bursts
    const interval = 300 + Math.random()*2200; // ms
    // small chance for an immediate clustered burst
    if (Math.random() < 0.08) {
      for (let i=0;i<1 + Math.floor(Math.random()*4); i++){
        setTimeout(()=>playGlitchEvent(), i * (40 + Math.random()*120));
      }
    } else {
      playGlitchEvent();
    }
    glitchTimer = setTimeout(schedule, interval);
  };
  schedule();
}

// stop scheduler
function stopGlitchScheduler(){
  if (glitchTimer) { clearTimeout(glitchTimer); glitchTimer = null; }
}

// toggle sound on/off (user-triggered)
function setSoundEnabled(on){
  ensureAudioContext();
  if (!audioCtx) return;
  // AudioContext must be resumed after user gesture in many browsers
  if (audioCtx.state === 'suspended') {
    audioCtx.resume().catch(()=>{ /* ignore */ });
  }
  soundEnabled = !!on;
  toggleSoundBtn.setAttribute('aria-pressed', soundEnabled ? 'true' : 'false');
  toggleSoundBtn.textContent = soundEnabled ? 'Sound: On' : 'Enable Sound';
  if (soundEnabled) {
    startGlitchScheduler();
  } else {
    stopGlitchScheduler();
  }
}

// connect volume slider
volSlider.addEventListener('input', (e)=>{
  ensureAudioContext();
  if (!masterGain) return;
  const val = Number(e.target.value) / 100;
  // smooth ramp
  if (audioCtx && masterGain) masterGain.gain.setTargetAtTime(val, audioCtx.currentTime, 0.02);
});

// toggle button handler
toggleSoundBtn.addEventListener('click', () => {
  // user gesture -> ensure audio can start
  ensureAudioContext();
  // if suspended, resume
  if (audioCtx && audioCtx.state === 'suspended') audioCtx.resume().catch(()=>{});
  const wantOn = !soundEnabled;
  setSoundEnabled(wantOn);
});

// default initial volume
volSlider.value = Math.round(defaultVol * 100);
if (!audioCtx) { ensureAudioContext(); }
if (masterGain) masterGain.gain.value = defaultVol;

/* Helpful: resume audio if user interacts anywhere (first interaction starts context) */
function firstGestureStart() {
  ensureAudioContext();
  if (audioCtx && audioCtx.state === 'suspended') {
    audioCtx.resume().catch(()=>{});
  }
  // don't auto-enable sound; just make sure context is unlocked
  window.removeEventListener('click', firstGestureStart);
  window.removeEventListener('keydown', firstGestureStart);
}
window.addEventListener('click', firstGestureStart);
window.addEventListener('keydown', firstGestureStart);

/* Clean up if reveal: keep sounds but you could also stop */
</script>
</body>
</html>
