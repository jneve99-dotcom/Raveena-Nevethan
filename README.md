<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>I Love You ❤️</title>
  <style>
    :root{
      --bg1:#ff7aa2;
      --bg2:#ffd1dc;
      --card:#ffffffcc;
      --text:#1f1f1f;
      --accent:#ff2e6d;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      min-height:100vh;
      display:grid;
      place-items:center;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color:var(--text);
      background: radial-gradient(circle at 20% 20%, var(--bg2), transparent 55%),
                  radial-gradient(circle at 80% 30%, #ffe9ef, transparent 50%),
                  linear-gradient(135deg, var(--bg1), var(--bg2));
      overflow:hidden;
    }
    .card{
      width:min(680px, 92vw);
      background:var(--card);
      backdrop-filter: blur(10px);
      border:1px solid #ffffff80;
      border-radius:24px;
      padding:28px 22px;
      box-shadow: 0 18px 50px rgba(0,0,0,.18);
      text-align:center;
      position:relative;
    }
    h1{
      margin:0 0 8px;
      font-size: clamp(34px, 6vw, 56px);
      letter-spacing:-.02em;
    }
    p{
      margin: 6px auto;
      font-size: clamp(16px, 2.6vw, 18px);
      line-height:1.5;
      max-width: 56ch;
    }
    .name{
      font-weight:700;
      color:var(--accent);
    }
    .heart-wrap{
      display:grid;
      place-items:center;
      margin: 18px 0 12px;
    }
    .heart{
      width:72px;
      height:72px;
      background:var(--accent);
      transform: rotate(45deg);
      position:relative;
      animation: beat 1.1s infinite;
      filter: drop-shadow(0 10px 18px rgba(255,46,109,.35));
    }
    .heart:before,
    .heart:after{
      content:"";
      position:absolute;
      width:72px;
      height:72px;
      background:var(--accent);
      border-radius:50%;
    }
    .heart:before{ left:-36px; top:0; }
    .heart:after{ left:0; top:-36px; }
    @keyframes beat{
      0%, 100%{ transform: rotate(45deg) scale(1); }
      50%{ transform: rotate(45deg) scale(1.12); }
    }

    .actions{
      display:flex;
      gap:10px;
      justify-content:center;
      flex-wrap:wrap;
      margin-top:18px;
    }
    button{
      border:0;
      padding:12px 16px;
      border-radius:999px;
      font-weight:700;
      cursor:pointer;
      background:var(--accent);
      color:white;
      transition: transform .08s ease, opacity .2s ease;
      box-shadow: 0 10px 24px rgba(255,46,109,.25);
    }
    button:active{ transform: scale(.98); }
    .secondary{
      background: transparent;
      color: var(--accent);
      border: 2px solid var(--accent);
      box-shadow:none;
    }
    .reveal{
      margin-top:16px;
      display:none;
      padding:14px 14px;
      border-radius:16px;
      background: #fff;
      border: 1px solid #00000010;
    }
    .tiny{
      opacity:.75;
      font-size:14px;
      margin-top:10px;
    }

    /* floating hearts background */
    .float{
      position:absolute;
      inset:-10vh -10vw;
      pointer-events:none;
      z-index:-1;
    }
    .float span{
      position:absolute;
      font-size:18px;
      opacity:.55;
      animation: drift linear infinite;
      filter: blur(.2px);
    }
    @keyframes drift{
      from { transform: translateY(110vh) translateX(0) rotate(0deg); }
      to   { transform: translateY(-20vh) translateX(40px) rotate(20deg); }
    }
  </style>
</head>
<body>
  <div class="float" aria-hidden="true" id="float"></div>

  <main class="card">
    <h1>I love you, <span class="name" id="gfName">my love</span> ❤️</h1>
    <p id="line1">You make my days brighter, my stress quieter, and my life better just by being in it.</p>

    <div class="heart-wrap">
      <div class="heart" title="always"></div>
    </div>

    <p id="line2">I’m grateful for you — today, tomorrow, and all the days after that.</p>

    <div class="actions">
      <button id="revealBtn">Tap for a secret message</button>
      <button class="secondary" id="copyBtn">Copy this page link/text</button>
    </div>

    <div class="reveal" id="revealBox">
      <p style="margin:0;font-weight:700;">If you ever forget:</p>
      <p style="margin:6px 0 0;">I choose you. I’m proud of you. And I’m always on your team. 💖</p>
    </div>

    <div class="tiny" id="tinyNote">Made with love ✨</div>
  </main>

  <script>
    // ✍️ Customize these:
    const GIRLFRIEND_NAME = "Babe";  // change this
    const CUSTOM_LINE_1   = "You make my days brighter, my stress quieter, and my life better just by being in it.";
    const CUSTOM_LINE_2   = "I’m grateful for you — today, tomorrow, and all the days after that.";

    // Apply customization
    document.getElementById("gfName").textContent = GIRLFRIEND_NAME;
    document.getElementById("line1").textContent = CUSTOM_LINE_1;
    document.getElementById("line2").textContent = CUSTOM_LINE_2;

    // Reveal message
    const btn = document.getElementById("revealBtn");
    const box = document.getElementById("revealBox");
    btn.addEventListener("click", () => {
      const showing = box.style.display === "block";
      box.style.display = showing ? "none" : "block";
      btn.textContent = showing ? "Tap for a secret message" : "Hide message";
    });

    // Copy text (works even if not hosted)
    document.getElementById("copyBtn").addEventListener("click", async () => {
      const text = `I love you, ${GIRLFRIEND_NAME} ❤️\n\n${CUSTOM_LINE_1}\n${CUSTOM_LINE_2}\n\n(Secret: I choose you. I'm always on your team. 💖)`;
      try {
        await navigator.clipboard.writeText(text);
        document.getElementById("tinyNote").textContent = "Copied 💌 Now send it to her!";
      } catch (e) {
        document.getElementById("tinyNote").textContent = "Couldn’t copy automatically—select and copy the text on screen 💌";
      }
    });

    // Floating hearts background
    const float = document.getElementById("float");
    const hearts = ["💖","💕","💘","💗","❤️","✨"];
    for (let i = 0; i < 22; i++){
      const s = document.createElement("span");
      s.textContent = hearts[Math.floor(Math.random()*hearts.length)];
      s.style.left = Math.random()*100 + "vw";
      s.style.animationDuration = (8 + Math.random()*10) + "s";
      s.style.animationDelay = (-Math.random()*10) + "s";
      s.style.fontSize = (14 + Math.random()*18) + "px";
      float.appendChild(s);
    }
  </script>
</body>
</html>
