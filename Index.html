#!/data/data/com.termux/files/usr/bin/bash
# Remy's Thoughts - build, push, and enable GitHub Pages in one command
set -e

OWNER="otsum14u"
REPO="otsum14u.github.io"
BRANCH="main"
SRC="$HOME/remys-deploy"

if [ -z "$GH_TOKEN" ]; then
  echo "Set your token first:  export GH_TOKEN=ghp_yourtoken"; exit 1
fi
pkg install -y git curl >/dev/null

rm -rf "$SRC" && mkdir -p "$SRC/.github/workflows" && cd "$SRC"

# ---------- App ----------
cat > index.html << 'EOF'
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#0b0d14">
<meta name="apple-mobile-web-app-capable" content="yes">
<link rel="manifest" href="manifest.json">
<link rel="icon" href="icon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="icon.svg">
<title>Remy's Thoughts</title>
<style>
  :root { --ink:#f4f1ea; --accent:#ffb347; }
  * { box-sizing:border-box; }
  html,body { margin:0; height:100%; overflow:hidden; color:var(--ink);
    background:radial-gradient(ellipse at 50% 25%,#2b3150 0%,#11141f 55%,#07080d 100%);
    font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif; }
  #scene { position:fixed; inset:0; width:100%; height:100%; display:block; touch-action:manipulation; }
  #bubble { position:fixed; left:50%; transform:translateX(-50%);
    top:calc(env(safe-area-inset-top,0px) + 14px); width:min(92vw,520px);
    background:rgba(255,255,255,.08); backdrop-filter:blur(12px); -webkit-backdrop-filter:blur(12px);
    border:1px solid rgba(255,255,255,.15); border-radius:22px; padding:14px 18px;
    font-size:1.08rem; line-height:1.45; text-align:center; min-height:3.2em;
    box-shadow:0 12px 36px rgba(0,0,0,.45); }
  #title { position:fixed; left:0; right:0; text-align:center; font-weight:800; letter-spacing:.08em;
    top:calc(env(safe-area-inset-top,0px) + 4px); font-size:.7rem; opacity:.5; pointer-events:none; }
  #ui { position:fixed; left:0; right:0; bottom:0; padding:12px 12px calc(12px + env(safe-area-inset-bottom,0px));
    background:linear-gradient(transparent,rgba(0,0,0,.65) 45%); display:flex; flex-direction:column; gap:8px; }
  #row { display:flex; gap:8px; }
  input { flex:1; min-width:0; padding:13px 14px; border-radius:14px; border:1px solid rgba(255,255,255,.2);
    background:rgba(0,0,0,.45); color:var(--ink); font-size:1rem; outline:none; }
  button { border:0; border-radius:14px; padding:12px 15px; background:var(--accent); color:#1a1200;
    font-weight:700; font-size:1rem; touch-action:manipulation; cursor:pointer; }
  button.ghost { background:rgba(255,255,255,.12); color:var(--ink); }
  button.listening { background:#ff5e5e; color:#fff; }
  button:disabled { opacity:.35; }
</style>
</head>
<body>
<canvas id="scene"></canvas>
<div id="title">REMY'S THOUGHTS</div>
<div id="bubble">Tap anywhere to wake me up.</div>
<div id="ui">
  <div id="row">
    <button id="thought" class="ghost" title="Hear a thought">Thought</button>
    <button id="mic" class="ghost" title="Ask with your voice">Mic</button>
  </div>
  <form id="form" autocomplete="off" style="margin:0">
    <div id="row">
      <input id="q" placeholder="Ask Remy something..." maxlength="200">
      <button type="submit">Ask</button>
    </div>
  </form>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r160/three.min.js"></script>
<script>
const canvas = document.getElementById('scene');
const renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
renderer.setPixelRatio(Math.min(devicePixelRatio, 2));
renderer.setSize(innerWidth, innerHeight);
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
renderer.toneMapping = THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure = 1.05;
renderer.outputColorSpace = THREE.SRGBColorSpace;

const scene = new THREE.Scene();
scene.fog = new THREE.Fog(0x0b0d14, 9, 24);
const camera = new THREE.PerspectiveCamera(36, innerWidth / innerHeight, 0.1, 100);
camera.position.set(0, 2.3, 7.4);
camera.lookAt(0, 1.6, 0);

scene.add(new THREE.HemisphereLight(0xbfd4ff, 0x221a14, 0.9));
const key = new THREE.DirectionalLight(0xfff1dd, 2.2);
key.position.set(3, 6, 5); key.castShadow = true;
key.shadow.mapSize.set(2048, 2048); key.shadow.bias = -0.0005;
scene.add(key);
const rim = new THREE.DirectionalLight(0x6fa8ff, 1.6); rim.position.set(-5, 3, -4); scene.add(rim);
const warm = new THREE.PointLight(0xffb347, 1.2, 10); warm.position.set(-2, 2, 3); scene.add(warm);

const ground = new THREE.Mesh(new THREE.CircleGeometry(9, 72),
  new THREE.MeshStandardMaterial({ color: 0x161a26, roughness: 0.95 }));
ground.rotation.x = -Math.PI / 2; ground.receiveShadow = true; scene.add(ground);

const M = {
  fur:   new THREE.MeshPhysicalMaterial({ color: 0x111111, roughness: 0.6, clearcoat: 0.35, clearcoatRoughness: 0.35 }),
  dark:  new THREE.MeshStandardMaterial({ color: 0x050505, roughness: 0.9 }),
  white: new THREE.MeshStandardMaterial({ color: 0xffffff, roughness: 0.15 }),
  pupil: new THREE.MeshStandardMaterial({ color: 0x000000, roughness: 0.1 }),
  tongue:new THREE.MeshStandardMaterial({ color: 0xff7a95, roughness: 0.5 }),
  gold:  new THREE.MeshStandardMaterial({ color: 0xd9a441, metalness: 0.8, roughness: 0.25 }),
};
function sph(r, mat, sx = 1, sy = 1, sz = 1) {
  const m = new THREE.Mesh(new THREE.SphereGeometry(r, 40, 28), mat);
  m.scale.set(sx, sy, sz); m.castShadow = true; return m;
}
function put(parent, obj, x = 0, y = 0, z = 0) { obj.position.set(x, y, z); parent.add(obj); return obj; }

const pug = new THREE.Group(); scene.add(pug);
const body = put(pug, sph(1, M.fur, 1.0, 0.95, 1.2), 0, 0.95, 0);
for (const [x, z] of [[-0.5, 0.5], [0.5, 0.5], [-0.5, -0.55], [0.5, -0.55]]) {
  const leg = new THREE.Mesh(new THREE.CylinderGeometry(0.2, 0.18, 0.9, 20), M.fur);
  leg.castShadow = true; put(pug, leg, x, 0.45, z);
  put(pug, sph(0.24, M.fur, 1.1, 0.7, 1.2), x, 0.08, z + 0.12);
}
const head = new THREE.Group(); head.position.set(0, 2.05, 0.55); pug.add(head);
put(head, sph(0.8, M.fur, 1, 0.98, 0.95));
const earL = put(head, sph(0.32, M.fur, 0.7, 1.1, 0.25), -0.62, 0.2, -0.05); earL.rotation.z = 0.35;
const earR = put(head, sph(0.32, M.fur, 0.7, 1.1, 0.25),  0.62, 0.2, -0.05); earR.rotation.z = -0.35;
for (const s of [-1, 1]) {
  const brow = new THREE.Mesh(new THREE.TorusGeometry(0.2, 0.04, 10, 24, Math.PI), M.dark);
  put(head, brow, s * 0.28, 0.42, 0.7);
}
const eyes = [];
for (const s of [-1, 1]) {
  const eg = new THREE.Group(); put(head, eg, s * 0.3, 0.1, 0.66); eyes.push(eg);
  eg.add(sph(0.19, M.white, 1, 1, 0.5));
  put(eg, sph(0.12, M.pupil, 1, 1, 0.5), 0, 0, 0.06);
  put(eg, sph(0.03, M.white), 0.04, 0.05, 0.13);
}
put(head, sph(0.42, M.fur, 1.15, 0.85, 0.95), 0, -0.2, 0.68);
put(head, sph(0.14, M.pupil, 1.5, 0.9, 0.85), 0, 0.0, 1.02);
const jaw = new THREE.Group(); jaw.position.set(0, -0.36, 0.82); head.add(jaw);
put(jaw, sph(0.22, M.fur, 1.4, 0.6, 0.9), 0, -0.04, 0.1);
put(jaw, sph(0.1, M.tongue, 1.2, 0.5, 0.8), 0, -0.1, 0.22);
const tailPivot = new THREE.Group(); tailPivot.position.set(0, 1.3, -1.05); pug.add(tailPivot);
const tail = new THREE.Mesh(new THREE.TorusGeometry(0.32, 0.07, 14, 40, Math.PI * 1.6), M.fur);
tail.rotation.z = Math.PI * 0.2; tail.castShadow = true; tailPivot.add(tail);
const collar = new THREE.Mesh(new THREE.TorusGeometry(0.62, 0.07, 16, 48), M.gold);
collar.rotation.x = Math.PI / 2; put(pug, collar, 0, 1.5, 0.35);
const tag = new THREE.Mesh(new THREE.CylinderGeometry(0.14, 0.14, 0.03, 24), M.gold);
tag.rotation.x = Math.PI / 2; put(pug, tag, 0, 1.3, 0.98);

const clock = new THREE.Clock();
let talking = false, blinkT = -10, nextBlink = 2;
function animate() {
  const t = clock.getElapsedTime();
  body.scale.y = 0.95 + Math.sin(t * 2) * 0.01;
  head.rotation.z = Math.sin(t * 0.9) * 0.05;
  head.rotation.y = Math.sin(t * 0.4) * 0.12;
  tailPivot.rotation.y = Math.sin(t * 6) * 0.35;
  jaw.rotation.x = talking ? 0.15 + Math.abs(Math.sin(t * 16)) * 0.38 : 0.04;
  if (t > nextBlink) { blinkT = t; nextBlink = t + 2 + Math.random() * 4; }
  const b = t - blinkT, k = b < 0.12 ? Math.sin((b / 0.12) * Math.PI) : 0;
  eyes.forEach(e => e.scale.y = 1 - k * 0.9);
  renderer.render(scene, camera);
  requestAnimationFrame(animate);
}
animate();
addEventListener('resize', () => {
  camera.aspect = innerWidth / innerHeight; camera.updateProjectionMatrix();
  renderer.setSize(innerWidth, innerHeight);
});

let ac = null;
function bark(pitch = 1) {
  try {
    ac ||= new (window.AudioContext || window.webkitAudioContext)();
    if (ac.state === 'suspended') ac.resume();
    const t = ac.currentTime;
    const o = ac.createOscillator(), g = ac.createGain(), f = ac.createBiquadFilter();
    o.type = 'sawtooth';
    o.frequency.setValueAtTime(260 * pitch, t);
    o.frequency.exponentialRampToValueAtTime(90 * pitch, t + 0.18);
    f.type = 'lowpass'; f.frequency.value = 900;
    g.gain.setValueAtTime(0, t);
    g.gain.linearRampToValueAtTime(0.5, t + 0.02);
    g.gain.exponentialRampToValueAtTime(0.001, t + 0.22);
    o.connect(f).connect(g).connect(ac.destination);
    o.start(t); o.stop(t + 0.25);
  } catch (e) {}
}

const bubbleEl = document.getElementById('bubble');
let typeTimer, talkTimer;
function typeText(text) {
  clearInterval(typeTimer); bubbleEl.textContent = ''; let i = 0;
  typeTimer = setInterval(() => {
    bubbleEl.textContent = text.slice(0, ++i);
    if (i >= text.length) clearInterval(typeTimer);
  }, 28);
}
function pickVoice() {
  const vs = speechSynthesis.getVoices();
  return vs.find(v => /^en/i.test(v.lang) && /male|david|mark|daniel|george|guy/i.test(v.name))
      || vs.find(v => /^en/i.test(v.lang)) || null;
}
function say(text) {
  typeText(text);
  talking = true;
  clearTimeout(talkTimer);
  talkTimer = setTimeout(() => talking = false, text.length * 75 + 800);
  if (!('speechSynthesis' in window)) return;
  speechSynthesis.cancel();
  const u = new SpeechSynthesisUtterance(text);
  const v = pickVoice(); if (v) u.voice = v;
  u.pitch = 0.55; u.rate = 0.92;
  u.onend = u.onerror = () => talking = false;
  speechSynthesis.speak(u);
}

const THOUGHTS = [
  "Is that a squirrel? No? Okay. I'm still watching it. Don't rush me.",
  "Snacks. I think about snacks. Mostly snacks. Stop looking at me like that.",
  "Nap time is a state of mind, and my mind is always napping. Don't wake me.",
  "Why do they call it a leash? It's a commitment, and I did not agree to it.",
  "I am not short. The floor is just very far away. Quit measuring me.",
  "The mailman came. I was ready. Nobody needs to know I was asleep. Grr.",
  "Belly rubs are a human right. Look it up. Then do it.",
  "Sometimes I stare at the wall. The wall stares back. We have an understanding. It is a bad one.",
  "Everyone says I snore. I call it singing in my sleep. Nobody asked for the harmony.",
  "One sock is missing. I have no regrets. Maybe one regret. Don't ask which."
];
const QA = [
  [/\b(name|who are you)\b/,            ["I'm Remy. Big head, bigger opinions, tiny legs. Next question."]],
  [/\b(hungry|food|eat|snack|treat)\b/, ["Food? Yes. Now? Always. Did you bring snacks, or are you just wasting my time?"]],
  [/\b(walk|outside|park)\b/,           ["Walk? Fine. But if it rains, we're going home, and I'm not apologizing."]],
  [/\b(love|like me|friend)\b/,         ["You, the couch, and tummy rubs. Don't make it weird. Tummy rubs, though. Yes."]],
  [/\b(bath|bathe|shower|wash)\b/,      ["A bath is a crime against fur. I will be filing a complaint with the couch."]],
  [/\b(meaning|purpose)\b.*\b(life)\b|\blife\b.*\b(meaning)\b/, ["A nap in a sunbeam, followed by a snack. You're welcome. Next question."]],
  [/\b(rain|weather|storm|snow)\b/,     ["Rain? I hate rain. Puddles are not for pugs. Unless they're snacks."]],
  [/\b(how are you|how r u|how's it going)\b/, ["Sleepy, grumpy, and extremely handsome. Thanks for asking. Barely."]],
  [/\b(bark|woof)\b/,                   ["Woof. That was a serious woof. Don't test me."]],
  [/\b(sleep|nap|bed)\b/,               ["Sleep is my favorite hobby. I'm very good at it. Don't interrupt."]],
];
const FALLBACK = [
  "Hmm. Good question. I'll think about it from my bed. Don't hold your breath.",
  "I don't know. But my tail thinks yes. My tail is usually wrong.",
  "Let me sleep on it. Literally. Ask me again after my nap, and bring a snack.",
  "That's above my pay grade. My pay is snacks, and I'm underpaid. Hard disagree."
];
const pick = a => a[Math.floor(Math.random() * a.length)];
function answer(q) {
  const s = q.toLowerCase();
  for (const [re, replies] of QA) if (re.test(s)) return pick(replies);
  return pick(FALLBACK);
}

const form = document.getElementById('form'), qInput = document.getElementById('q');
const thoughtBtn = document.getElementById('thought'), micBtn = document.getElementById('mic');
let started = false;
function start() {
  if (started) return;
  started = true;
  bark(1);
  say("Oh! You're here. I was resting my eyes. Ask me anything. Quickly.");
}
addEventListener('pointerdown', start);
function ask(q) {
  const clean = q.trim(); if (!clean) return;
  bark(1.05);
  setTimeout(() => say(answer(clean)), 260);
}
form.addEventListener('submit', e => { e.preventDefault(); ask(qInput.value); qInput.value = ''; });
thoughtBtn.onclick = () => { bark(0.95); say(pick(THOUGHTS)); };
setInterval(() => { if (started && !talking) say(pick(THOUGHTS)); }, 24000);

const ray = new THREE.Raycaster(), ptr = new THREE.Vector2();
canvas.addEventListener('pointerup', e => {
  ptr.x = (e.clientX / innerWidth) * 2 - 1;
  ptr.y = -(e.clientY / innerHeight) * 2 + 1;
  ray.setFromCamera(ptr, camera);
  if (ray.intersectObject(pug, true).length) {
    bark(1.1);
    setTimeout(() => say(pick(["Hey! Personal space. Well... a little petting is okay. Fine.", "Ooh, the head! Yes, right there. Don't stop."])), 250);
  }
});

const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
if (SR) {
  const rec = new SR();
  rec.lang = 'en-US'; rec.interimResults = false; rec.maxAlternatives = 1;
  rec.onresult = e => ask(e.results[0][0].transcript);
  rec.onend = () => micBtn.classList.remove('listening');
  rec.onerror = () => micBtn.classList.remove('listening');
  micBtn.onclick = () => {
    try { micBtn.classList.add('listening'); bark(1.1); rec.start(); }
    catch (e) { micBtn.classList.remove('listening'); }
  };
} else {
  micBtn.disabled = true; micBtn.title = 'Voice input not supported in this browser';
}

if ('serviceWorker' in navigator) navigator.serviceWorker.register('sw.js').catch(() => {});
</script>
</body>
</html>
EOF

cat > manifest.json << 'EOF'
{
  "name": "Remy's Thoughts",
  "short_name": "Remy",
  "description": "An ornery black pug who says what's on his mind and answers your questions.",
  "start_url": "./",
  "scope": "./",
  "display": "standalone",
  "orientation": "portrait",
  "background_color": "#0b0d14",
  "theme_color": "#0b0d14",
  "icons": [
    { "src": "icon.svg", "sizes": "any", "type": "image/svg+xml", "purpose": "any maskable" }
  ]
}
EOF

cat > sw.js << 'EOF'
const CACHE = 'remys-thoughts-v2';
const ASSETS = ['./', './index.html', './manifest.json', './icon.svg'];
self.addEventListener('install', e => {
  e.waitUntil(caches.open(CACHE).then(c => c.addAll(ASSETS)).then(() => self.skipWaiting()));
});
self.addEventListener('activate', e => {
  e.waitUntil(
    caches.keys()
      .then(keys => Promise.all(keys.filter(k => k !== CACHE).map(k => caches.delete(k))))
      .then(() => self.clients.claim())
  );
});
self.addEventListener('fetch', e => {
  if (e.request.method !== 'GET') return;
  e.respondWith(
    caches.match(e.request).then(hit => hit || fetch(e.request).then(res => {
      const copy = res.clone();
      caches.open(CACHE).then(c => c.put(e.request, copy));
      return res;
    }).catch(() => caches.match('./index.html')))
  );
});
EOF

cat > icon.svg << 'EOF'
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
  <rect width="512" height="512" rx="110" fill="#0b0d14"/>
  <circle cx="256" cy="282" r="160" fill="#151515"/>
  <ellipse cx="118" cy="170" rx="58" ry="82" fill="#151515" transform="rotate(-20 118 170)"/>
  <ellipse cx="394" cy="170" rx="58" ry="82" fill="#151515" transform="rotate(20 394 170)"/>
  <circle cx="200" cy="250" r="44" fill="#fff"/>
  <circle cx="312" cy="250" r="44" fill="#fff"/>
  <circle cx="206" cy="256" r="22" fill="#000"/>
  <circle cx="306" cy="256" r="22" fill="#000"/>
  <ellipse cx="256" cy="335" rx="64" ry="48" fill="#222"/>
  <ellipse cx="256" cy="318" rx="26" ry="16" fill="#000"/>
  <path d="M170 392 Q256 430 342 392" stroke="#d9a441" stroke-width="22" fill="none" stroke-linecap="round"/>
  <circle cx="256" cy="420" r="18" fill="#d9a441"/>
</svg>
EOF

touch .nojekyll

cat > README.md << 'EOF'
# Remy's Thoughts

An ornery black pug who says what's on his mind and answers your questions.

**Live site:** https://otsum14u.github.io

- Three.js 3D scene with soft shadows and tone mapping
- Synthesized barks and spoken replies
- Voice input (Chrome) and text input
- Installable PWA that works offline after the first visit
EOF

cat > .github/workflows/pages.yml << 'EOF'
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: .
      - id: deployment
        uses: actions/deploy-pages@v4
EOF

# ---------- Git push ----------
git init -q -b "$BRANCH"
git add -A
git -c user.name="Remy Deploy" -c user.email="remy@example.com" commit -qm "Deploy Remy's Thoughts"
git remote add origin "https://github.com/$OWNER/$REPO.git"
git push -f -q "https://x-access-token:$GH_TOKEN@github.com/$OWNER/$REPO.git" "$BRANCH:$BRANCH"
echo "✅ Code pushed."

# ---------- Turn on GitHub Pages (Actions source) ----------
curl -s -o /dev/null -w "Pages setup: HTTP %{http_code}\n" \
  -X POST "https://api.github.com/repos/$OWNER/$REPO/pages" \
  -H "Authorization: Bearer $GH_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  -d '{"build_type":"workflow"}'
# 201 = enabled now, 409 = already enabled. Both are fine.

echo ""
echo "🐶 Deploy running. Watch it at: https://github.com/$OWNER/$REPO/actions"
echo "Live site (1-2 min): https://$OWNER.github.io"
