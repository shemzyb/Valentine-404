<!DOCTYPE html>
<html lang="en">  
<head>  
<meta charset="UTF-8" />  
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>  
<title>404 Valentine Not Found</title>  

<style>
  body {
    margin: 0;
    font-family: "Poppins", Arial, sans-serif;
    background: linear-gradient(135deg, #ffebee, #ffe4ec);
    color: #c62828;
    text-align: center;
    overflow: hidden;
  }

  h1 {
    margin-top: 50px;
    animation: fadeDown 1s ease;
  }

  p {
    font-size: 1.2rem;
    max-width: 500px;
    margin: 15px auto;
  }

  input {
    padding: 12px;
    font-size: 1rem;
    border-radius: 8px;
    border: 2px solid #c62828;
    outline: none;
    width: 220px;
  }

  .error {
    color: #b71c1c;
    margin-top: 10px;
    display: none;
  }

  .spotify-btn {
    display: none;
    margin: 20px auto;
    padding: 12px 22px;
    background: #1db954;
    color: white;
    border-radius: 25px;
    font-size: 0.95rem;
    text-decoration: none;
    width: fit-content;
    box-shadow: 0 8px 20px rgba(29,185,84,0.4);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .spotify-btn:hover {
    transform: scale(1.05);
    box-shadow: 0 12px 28px rgba(29,185,84,0.6);
  }

  button {
    padding: 15px 30px;
    font-size: 1.1rem;
    border-radius: 10px;
    border: none;
    cursor: pointer;
    position: absolute;
  }

  #yesBtn {
    background: #c62828;
    color: white;
    left: 35%;
    top: 220px;
    transition: transform 0.3s ease;
  }

  #noBtn {
    background: #ffcdd2;
    color: #b71c1c;
    left: 55%;
    top: 220px;
  }

  .container {
    position: relative;
    height: 300px;
  }

  .heart {
    position: fixed;
    bottom: -20px;
    font-size: 18px;
    animation: floatUp linear forwards;
    pointer-events: none;
  }

  @keyframes floatUp {
    to { transform: translateY(-110vh); opacity: 0; }
  }

  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  canvas {
    position: fixed;
    top: 0;
    left: 0;
    pointer-events: none;
  }

  /* Easter egg hint */
  #easterEgg {
    position: fixed;
    inset: 0;
    background: rgba(255, 235, 238, 0.95);
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    font-size: 1.5rem;
    color: #c62828;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.8s ease;
    z-index: 9999;
  }

  #easterEgg.show {
    opacity: 1;
    pointer-events: auto;
  }

  #easterEgg span {
    animation: fadeUp 1.2s ease forwards;
  }

  @keyframes fadeUp {
    from { transform: translateY(20px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }
</style>
</head>

<body>

<h1>404 ERROR: VALENTINE NOT FOUND 😌</h1>

<p>
This page is protected.<br>
Only <strong>Seunmi</strong> (aka <strong>Preciousgift</strong>) can fix this error.
</p>

<input id="nameInput" placeholder="Enter your name" />
<div class="error" id="errorMsg">Wrong name 😌 Try again.</div>

<a
  id="spotifyBtn"
  class="spotify-btn"
  href="https://open.spotify.com/playlist/4DbftWuQLJpks6LLT0Orjx"
  target="_blank"
>
  🎧 Press play while reading 😌
</a>

<p id="countdown"></p>

<div class="container">
  <button id="yesBtn">YES ❤️</button>
  <button id="noBtn">NO</button>
</div>

<canvas id="confetti"></canvas>

<!-- Easter egg hint -->
<div id="easterEgg">
  <span>😌 Close! That’s your real name… but I call you something else ❤️</span>
</div>

<script>
const correctName = "seunmi";
const hintName = "preciousgift";
const input = document.getElementById("nameInput");
const error = document.getElementById("errorMsg");
const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const spotifyBtn = document.getElementById("spotifyBtn");
const easterEgg = document.getElementById("easterEgg");

let yesScale = 1;

// Auto-fill from shareable link
const params = new URLSearchParams(window.location.search);
if (params.get("name")) input.value = params.get("name");

// Input listener for validation + Easter egg
input.addEventListener("input", () => {
  const value = input.value.trim().toLowerCase();

  if (value === correctName) {
    error.style.display = "none";
    spotifyBtn.style.display = "inline-block";
    easterEgg.classList.remove("show");
  } else if (value === hintName) {
    error.style.display = "block";
    error.innerText = "😌 Close! That’s your real name… but I call you something else ❤️";
    spotifyBtn.style.display = "none";
    easterEgg.classList.add("show");
    navigator.vibrate?.([50,20,50]);
  } else {
    error.style.display = "block";
    error.innerText = "Wrong name 😌 Try again.";
    spotifyBtn.style.display = "none";
    easterEgg.classList.remove("show");
  }
});

// NO button logic
function moveNo() {
  navigator.vibrate?.(30);
  noBtn.style.left = Math.random() * (window.innerWidth - 120) + "px";
  noBtn.style.top = Math.random() * (window.innerHeight - 120) + "px";
  yesScale += 0.15;
  yesBtn.style.transform = `scale(${yesScale})`;
}
noBtn.addEventListener("mouseenter", moveNo);
noBtn.addEventListener("touchstart", moveNo);

// YES button logic
yesBtn.addEventListener("click", () => {
  if (input.value.trim().toLowerCase() !== correctName) {
    error.style.display = "block";
    navigator.vibrate?.([100,50,100]);
    return;
  }

  launchConfetti();

  document.body.innerHTML = `
    <h1>❤️ ERROR FIXED ❤️</h1>
    <p>
      Seunmi 😌<br>
      You are officially my Valentine.<br>
      Preciousgift indeed 💕
    </p>
  `;
});

// Floating hearts
setInterval(() => {
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "❤️";
  h.style.left = Math.random() * 100 + "vw";
  h.style.animationDuration = 4 + Math.random() * 3 + "s";
  document.body.appendChild(h);
  setTimeout(() => h.remove(), 7000);
}, 450);

// Countdown
const countdownEl = document.getElementById("countdown");
const valentine = new Date("Feb 14, 2026 00:00:00").getTime();
setInterval(() => {
  const now = Date.now();
  const diff = valentine - now;
  const d = Math.floor(diff / (1000*60*60*24));
  countdownEl.textContent = `⏳ ${d} days until Valentine’s Day`;
}, 1000);

// Confetti
const canvas = document.getElementById("confetti");
const ctx = canvas.getContext("2d");
canvas.width = innerWidth;
canvas.height = innerHeight;
let confetti = [];

function launchConfetti() {
  for (let i=0;i<180;i++){
    confetti.push({
      x: Math.random()*canvas.width,
      y: Math.random()*canvas.height,
      r: Math.random()*6+4,
      dx: Math.random()*4-2,
      dy: Math.random()*-6-2
    });
  }
  animate();
}

function animate() {
  ctx.clearRect(0,0,canvas.width,canvas.height);
  confetti.forEach((c,i)=>{
    ctx.beginPath();
    ctx.arc(c.x,c.y,c.r,0,Math.PI*2);
    ctx.fillStyle = `hsl(${Math.random()*360},100%,70%)`;
    ctx.fill();
    c.x += c.dx;
    c.y += c.dy;
    c.dy += 0.15;
    if(c.y > canvas.height) confetti.splice(i,1);
  });
  if(confetti.length) requestAnimationFrame(animate);
}
</script>

</body>
</html>
