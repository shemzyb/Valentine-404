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

<p id="countdown"></p>

<div class="container">
  <button id="yesBtn">YES ❤️</button>
  <button id="noBtn">NO</button>
</div>

<audio id="music" loop>
  <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_c1c6b5c7e5.mp3?filename=african-love-110624.mp3" type="audio/mpeg">
</audio>

<canvas id="confetti"></canvas>

<script>
  const correctName = "seunmi";
  const input = document.getElementById("nameInput");
  const error = document.getElementById("errorMsg");
  const yesBtn = document.getElementById("yesBtn");
  const noBtn = document.getElementById("noBtn");
  const music = document.getElementById("music");

  let yesScale = 1;

  // Auto-fill from shareable link
  const params = new URLSearchParams(window.location.search);
  if (params.get("name")) {
    input.value = params.get("name");
  }

  function moveNo() {
    navigator.vibrate?.(30);
    noBtn.style.left = Math.random() * (window.innerWidth - 120) + "px";
    noBtn.style.top = Math.random() * (window.innerHeight - 120) + "px";
    yesScale += 0.15;
    yesBtn.style.transform = `scale(${yesScale})`;
  }

  noBtn.addEventListener("mouseenter", moveNo);
  noBtn.addEventListener("touchstart", moveNo);

  yesBtn.addEventListener("click", () => {
    if (input.value.trim().toLowerCase() !== correctName) {
      error.style.display = "block";
      navigator.vibrate?.([100, 50, 100]);
      return;
    }

    music.play();
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

  // Hearts
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
    const d = Math.floor(diff / (1000 * 60 * 60 * 24));
    countdownEl.textContent = `⏳ ${d} days until Valentine’s Day`;
  }, 1000);

  // Confetti
  const canvas = document.getElementById("confetti");
  const ctx = canvas.getContext("2d");
  canvas.width = innerWidth;
  canvas.height = innerHeight;
  let confetti = [];

  function launchConfetti() {
    for (let i = 0; i < 180; i++) {
      confetti.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 6 + 4,
        dx: Math.random() * 4 - 2,
        dy: Math.random() * -6 - 2
      });
    }
    animate();
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    confetti.forEach((c, i) => {
      ctx.beginPath();
      ctx.arc(c.x, c.y, c.r, 0, Math.PI * 2);
      ctx.fillStyle = `hsl(${Math.random() * 360},100%,70%)`;
      ctx.fill();
      c.x += c.dx;
      c.y += c.dy;
      c.dy += 0.15;
      if (c.y > canvas.height) confetti.splice(i, 1);
    });
    if (confetti.length) requestAnimationFrame(animate);
  }
</script>

</body>
</html>
