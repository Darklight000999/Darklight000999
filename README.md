<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>darklight000999 | Cyber Security</title>
<style>
/* ===== Body ===== */
body {
  margin:0;
  padding:0;
  font-family: 'Fira Code', monospace;
  background: #050507;
  color: #00ff99;
  overflow-x: hidden;
  cursor: none; /* Custom cursor */
}

/* ===== Custom Neon Cursor ===== */
.cursor {
  position: fixed;
  top:0;
  left:0;
  width:12px;
  height:12px;
  border-radius:50%;
  border:2px solid #00ff99;
  pointer-events:none;
  transform:translate(-50%, -50%);
  box-shadow: 0 0 5px #00ff99, 0 0 10px #00ff99, 0 0 20px #00ff99;
  transition: transform 0.05s ease;
  z-index:9999;
}

/* ===== Matrix Background ===== */
canvas {
  position: fixed;
  top:0;
  left:0;
  width:100%;
  height:100%;
  z-index:0;
}

/* ===== Neon Header ===== */
.header {
  position: relative;
  z-index:1;
  text-align:center;
  margin-top:60px;
}
.header h1 {
  font-size:64px;
  color:#00ff99;
  text-shadow: 0 0 5px #00ff99, 0 0 10px #00ff99, 0 0 20px #00ff99, 0 0 40px #00ff99;
  animation:flicker 3s infinite;
}
.header h3 {
  font-size:24px;
  color:#00ff99;
  text-shadow: 0 0 4px #00ff99,0 0 8px #00ff99;
  animation:flicker 3s infinite alternate;
  margin-top:10px;
}
@keyframes flicker {
  0%,19%,21%,23%,25%,54%,56%,100% { opacity:1; }
  20%,22%,24%,55% { opacity:0.4; }
}

/* ===== Tool Carousel ===== */
.carousel-container {
  position: relative;
  width: 100%;
  overflow: hidden;
  margin: 60px 0;
  z-index:1;
}
.carousel {
  display:flex;
  gap:30px;
  animation:scroll 20s linear infinite;
}
.carousel img {
  width:80px;
  height:80px;
  border-radius:12px;
  box-shadow:0 0 10px #00ff99, 0 0 20px #00ff99;
  transition: transform 0.3s;
}
.carousel img:hover { transform: scale(1.3); }
@keyframes scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

/* ===== Sections ===== */
.section {
  position: relative;
  z-index:1;
  text-align:center;
  margin:50px 0;
}
.section img {
  margin:10px;
  border-radius:12px;
  box-shadow:0 0 20px #00ff99;
}

/* ===== Lock Grid ===== */
.lock-container {
  display:flex;
  flex-wrap: wrap;
  justify-content:center;
  gap:4px;
  margin: 40px 0;
  z-index:1;
  position:relative;
}
.lock {
  width:14px;
  height:18px;
  border: 2px solid #00ff99;
  border-radius:2px;
  position: relative;
  overflow:hidden;
  background:#000;
}
.lock::before {
  content:"";
  position:absolute;
  top:-6px;
  left:4px;
  width:6px;
  height:6px;
  border:2px solid #00ff99;
  border-bottom:none;
  border-radius:3px 3px 0 0;
}

/* ===== Code Flow inside Locks ===== */
.code {
  position:absolute;
  top:0;
  left:0;
  width:100%;
  height:100%;
  font-size:8px;
  color:#00ff99;
  line-height:1;
  display:flex;
  flex-direction:column;
  animation:codeFlow 1.5s linear infinite;
  opacity:0.7;
}
@keyframes codeFlow {
  0% { transform:translateY(100%); }
  100% { transform:translateY(-100%); }
}
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>

<canvas id="matrix"></canvas>

<!-- Header -->
<div class="header">
  <h1>darklight000999</h1>
  <h3>Cyber Security and Ethical Hackacknig</h3>
</div>

<!-- Tool Carousel -->
<div class="carousel-container">
  <div class="carousel">
    <img src="https://skillicons.dev/icons?i=kali" alt="Kali Linux">
    <img src="https://skillicons.dev/icons?i=parrot" alt="Parrot OS">
    <img src="https://skillicons.dev/icons?i=nmap" alt="Nmap">
    <img src="https://skillicons.dev/icons?i=metasploit" alt="Metasploit">
    <img src="https://skillicons.dev/icons?i=wireshark" alt="Wireshark">
    <img src="https://skillicons.dev/icons?i=hydra" alt="Hydra">
    <img src="https://skillicons.dev/icons?i=burpsuite" alt="BurpSuite">
    <img src="https://skillicons.dev/icons?i=docker" alt="Docker">
    <img src="https://skillicons.dev/icons?i=cloudflare" alt="Cloudflare">
  </div>
</div>

<!-- GitHub Stats & Quote -->
<div class="section">
  <img src="https://github-readme-stats.vercel.app/api?username=darklight000999&show_icons=true&theme=tokyonight" height="170">
  <img src="https://github-profile-trophy.vercel.app/?username=darklight000999&theme=matrix&no-frame=true&margin-w=15&margin-h=15">
</div>

<div class="section">
  <img src="https://readme-typing-svg.herokuapp.com?font=Courier+Prime&duration=4000&pause=1000&color=FF0000&center=true&vCenter=true&width=800&lines=Hack+the+system+before+it+hacks+you..." alt="Hacker Quote">
</div>

<!-- ===== Lock Animation Grid ===== -->
<div class="lock-container" id="locks"></div>

<!-- ===== Matrix Animation JS ===== -->
<script>
/* ===== Matrix Background ===== */
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()*&^%';
const fontSize = 16;
const columns = canvas.width / fontSize;
const drops = [];
for(let x=0;x<columns;x++) drops[x]=1;

function draw(){
  ctx.fillStyle='rgba(0,0,0,0.05)';
  ctx.fillRect(0,0,canvas.width,canvas.height);
  ctx.fillStyle='#00ff99';
  ctx.font=fontSize+'px monospace';
  for(let i=0;i<drops.length;i++){
    const text = letters.charAt(Math.floor(Math.random()*letters.length));
    ctx.fillText(text,i*fontSize,drops[i]*fontSize);
    if(drops[i]*fontSize>canvas.height && Math.random()>0.975) drops[i]=0;
    drops[i]++;
  }
}
setInterval(draw,35);

/* ===== Generate 200 Locks with Code Flow ===== */
const lockContainer = document.getElementById('locks');
for(let i=0;i<200;i++){
  const lock = document.createElement('div');
  lock.className='lock';
  const codeDiv = document.createElement('div');
  codeDiv.className='code';
  let codeLines='';
  for(let j=0;j<6;j++){
    codeLines += Math.random()>0.5 ? '01' : '10';
    codeLines += '\n';
  }
  codeDiv.innerText = codeLines;
  lock.appendChild(codeDiv);
  lockContainer.appendChild(lock);
}

/* ===== Custom Cursor ===== */
const cursor = document.getElementById('cursor');
document.addEventListener('mousemove', e=>{
  cursor.style.transform=`translate(${e.clientX}px,${e.clientY}px)`;
});
</script>
</body>
</html>
