<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Lì Xì Tết 2026 - Chúc Mừng Năm Mới</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Roboto:wght@400;700&display=swap');

    body {
      margin: 0;
      padding: 0;
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(to bottom, #ff5e3a, #ff2d00);
      color: #fff;
      min-height: 100vh;
      overflow-x: hidden;
      position: relative;
    }

    .snow { 
      position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none;
      background: transparent url('https://www.transparenttextures.com/patterns/arabesque.png');
      opacity: 0.1;
    }

    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 20px;
      text-align: center;
      position: relative;
      z-index: 2;
    }

    h1 {
      font-family: 'Dancing Script', cursive;
      font-size: 3.5em;
      margin: 30px 0;
      text-shadow: 3px 3px 10px rgba(0,0,0,0.5);
    }

    .envelope {
      width: 280px;
      height: 180px;
      margin: 50px auto;
      background: #d40000;
      position: relative;
      border-radius: 10px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.5);
      cursor: pointer;
      transition: transform 0.4s;
    }

    .envelope:hover { transform: scale(1.1); }

    .envelope::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 90px;
      background: #ffed4e;
      clip-path: polygon(0 0, 100% 0, 50% 100%);
    }

    .envelope::after {
      content: 'Lì Xì May Mắn';
      position: absolute;
      top: 60px;
      left: 0; right: 0;
      font-size: 1.8em;
      font-weight: bold;
      color: #d40000;
      text-shadow: 2px 2px #fff;
    }

    .open .envelope::before {
      transform: rotateX(180deg);
      transition: transform 0.6s;
    }

    .message {
      display: none;
      margin: 40px auto;
      padding: 30px;
      background: rgba(255,255,255,0.95);
      color: #d40000;
      border-radius: 15px;
      max-width: 500px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.3);
    }

    .message h2 { margin: 0 0 20px; font-size: 2.2em; }
    .message p { font-size: 1.4em; line-height: 1.6; }

    input, textarea {
      width: 80%;
      max-width: 400px;
      padding: 12px;
      margin: 15px 0;
      border: none;
      border-radius: 8px;
      font-size: 1.1em;
    }

    button {
      padding: 12px 30px;
      font-size: 1.2em;
      background: #ffed4e;
      color: #d40000;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    }

    button:hover { background: #ffd700; transform: translateY(-3px); }

    .share-link {
      margin: 30px 0;
      font-size: 1.3em;
      word-break: break-all;
      background: rgba(255,255,255,0.2);
      padding: 15px;
      border-radius: 10px;
    }

    .fireworks {
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    footer {
      margin-top: 100px;
      font-size: 0.9em;
      opacity: 0.8;
    }
  </style>
</head>
<body>
  <div class="snow"></div>
  <canvas class="fireworks"></canvas>

  <div class="container" id="home">
    <h1>Chúc Mừng Năm Mới 2026</h1>
    <p>Gửi bao lì xì may mắn đến người thân yêu 💕</p>

    <input type="text" id="sender" placeholder="Tên bạn (người gửi)" />
    <textarea id="wish" rows="4" placeholder="Lời chúc Tết thật ấm áp..."></textarea>
    <br/>
    <button onclick="createEnvelope()">Tạo Bao Lì Xì 🎉</button>

    <div id="linkArea" style="display:none;">
      <p>Chia sẻ link này để người nhận mở lì xì:</p>
      <div class="share-link" id="shareLink"></div>
      <button onclick="copyLink()">Copy Link</button>
    </div>
  </div>

  <div class="container" id="receive" style="display:none;">
    <h1>Click vào bao để mở lì xì!</h1>
    <div class="envelope" id="envelope" onclick="openEnvelope()"></div>

    <div class="message" id="message">
      <h2>Chúc Mừng Năm Mới!</h2>
      <p id="wishText"></p>
      <p><strong>Gửi từ: <span id="senderName"></span></strong></p>
      <p style="font-size:1.6em;">🍊 Năm mới Phát Tài - Vạn Sự Như Ý 🍊</p>
    </div>
  </div>

  <footer>
    Made with ❤️ by Grok - Chúc mọi người một cái Tết thật ấm áp và may mắn!
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/tsparticles-confetti@2.12.0/tsparticles.confetti.min.js"></script>
  <script>
    const urlParams = new URLSearchParams(window.location.search);
    const id = urlParams.get('id');

    if (id) {
      // Trang nhận lì xì
      document.getElementById('home').style.display = 'none';
      document.getElementById('receive').style.display = 'block';

      const data = JSON.parse(localStorage.getItem(id) || '{}');
      if (data.sender && data.wish) {
        document.getElementById('senderName').textContent = data.sender;
        document.getElementById('wishText').textContent = data.wish;
      } else {
        document.getElementById('message').innerHTML = "<h2>Ôi không! Bao lì xì đã hết hạn hoặc chưa được tạo 😢</h2>";
      }
    }

    function createEnvelope() {
      const sender = document.getElementById('sender').value.trim() || "Bạn thân mến";
      const wish = document.getElementById('wish').value.trim() || "Chúc bạn năm mới mạnh khỏe, hạnh phúc và thật nhiều tài lộc!";

      const uniqueId = Date.now().toString(36) + Math.random().toString(36).substr(2);

      const data = { sender, wish };
      localStorage.setItem(uniqueId, JSON.stringify(data));

      const link = window.location.origin + window.location.pathname + '?id=' + uniqueId;
      document.getElementById('shareLink').textContent = link;
      document.getElementById('linkArea').style.display = 'block';

      confettiBurst();
    }

    function openEnvelope() {
      document.getElementById('envelope').classList.add('open');
      setTimeout(() => {
        document.getElementById('message').style.display = 'block';
        confettiBurst();
      }, 800);
    }

    function copyLink() {
      const link = document.getElementById('shareLink').textContent;
      navigator.clipboard.writeText(link).then(() => {
        alert('Đã copy link thành công! 🎉');
      });
    }

    function confettiBurst() {
      const duration = 3 * 1000;
      const end = Date.now() + duration;

      (function frame() {
        confetti({
          particleCount: 5,
          angle: 60,
          spread: 55,
          origin: { x: 0 },
          colors: ['#ffed4e', '#d40000', '#fff']
        });
        confetti({
          particleCount: 5,
          angle: 120,
          spread: 55,
          origin: { x: 1 },
          colors: ['#ffed4e', '#d40000', '#fff']
        });

        if (Date.now() < end) {
          requestAnimationFrame(frame);
        }
      }());
    }
  </script>
</body>
</html>
