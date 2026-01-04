<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>404 Valentine Not Found</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #ffebee;
      color: #c62828;
      text-align: center;
      padding: 50px;
      overflow: hidden;
    }

    h1 {
      font-size: 2.8rem;
    }

    p {
      font-size: 1.4rem;
    }

    .container {
      margin-top: 40px;
      position: relative;
      height: 300px;
    }

    button {
      padding: 15px 30px;
      font-size: 1.2rem;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      position: absolute;
    }

    #yesBtn {
      background-color: #c62828;
      color: white;
      left: 40%;
      top: 150px;
      transition: transform 0.2s;
    }

    #noBtn {
      background-color: #ffcdd2;
      color: #b71c1c;
      left: 55%;
      top: 150px;
    }
  </style>
</head>

<body>
  <h1>404 ERROR: VALENTINE NOT FOUND</h1>

  <p>
    Oops! It looks like you’ve stumbled upon a missing Valentine.<br>
    Would you like to fix the error?
  </p>

  <div class="container">
    <button id="yesBtn">YES ❤️</button>
    <button id="noBtn">NO</button>
  </div>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");

    const noTexts = [
      "NO",
      "Are you sure?",
      "Why though?",
      "Think again 😅",
      "You don't really mean that",
      "Still no?",
      "Okay this is awkward…"
    ];

    let index = 0;
    let yesScale = 1;

    function moveNoButton() {
      const x = Math.random() * (window.innerWidth - 150);
      const y = Math.random() * (window.innerHeight - 150);

      noBtn.style.left = `${x}px`;
      noBtn.style.top = `${y}px`;

      index = (index + 1) % noTexts.length;
      noBtn.textContent = noTexts[index];

      yesScale += 0.1;
      yesBtn.style.transform = `scale(${yesScale})`;
    }

    noBtn.addEventListener("mouseenter", moveNoButton);
    noBtn.addEventListener("touchstart", moveNoButton);

    yesBtn.addEventListener("click", () => {
      document.body.innerHTML = `
        <h1>❤️ ERROR FIXED ❤️</h1>
        <p>You are now officially my Valentine 😌</p>
      `;
    });
  </script>
</body>
</html>
