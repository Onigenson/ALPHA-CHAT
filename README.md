<!DOCTYPE html>
<html lang="hu">
<head>
  <meta charset="UTF-8">
  <title>Onigen Chat</title>
  <style>
    body {
      margin: 0;
      font-family: Georgia, serif;
      background: url("https://images.unsplash.com/photo-1519608487953-e999c86e7455?auto=format&fit=crop&w=1920&q=80") no-repeat center center fixed;
      background-size: cover;
      color: white;
    }

    .login-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.9);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 10;
    }

    .login-screen input, .login-screen select, .login-screen button {
      padding: 10px;
      margin: 5px;
      font-size: 16px;
      border-radius: 5px;
      border: none;
    }

    .container {
      display: flex;
      flex-direction: row;
      height: 100vh;
      box-sizing: border-box;
      padding: 5px;
      border: 5px solid cyan;
      box-shadow: 0 0 20px cyan;
      background-color: rgba(0, 0, 0, 0.2);
      backdrop-filter: blur(10px);
    }

    .guest-list {
      flex: 1;
      border: 4px solid magenta;
      background-color: rgba(0, 0, 0, 0.2);
      padding: 10px;
      color: cyan;
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-right: 10px;
      box-shadow: 0 0 15px magenta;
    }

    .guest-list h3 {
      font-size: 20px;
      font-weight: bold;
      color: #00ffcc;
    }

    .guest {
      font-family: fantasy;
      font-size: 1.5em;
      margin-top: 30px;
      text-shadow: 0 0 5px #00ffff, 0 0 10px #ff00ff;
    }

    .chat-area {
      flex: 3;
      display: flex;
      flex-direction: column;
      border: 4px solid magenta;
      padding: 10px;
      background-color: rgba(0, 0, 0, 0.2);
      box-shadow: 0 0 15px magenta, 0 0 25px cyan inset;
      backdrop-filter: blur(10px);
    }

    .chat-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-weight: bold;
      font-size: 16px;
      color: white;
    }

    .chat-messages {
      flex-grow: 1;
      margin: 20px 0;
      overflow-y: auto;
      color: white;
    }

    .input-area {
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      padding: 10px;
      display: flex;
      align-items: center;
      color: white;
      font-weight: bold;
      border: 3px solid black;
      box-shadow: 0 0 10px #0ff, 0 0 20px #f0f;
      backdrop-filter: blur(10px);
    }

    .input-area select, .input-area input[type="text"], .input-area input[type="file"] {
      margin-right: 10px;
      padding: 5px;
      border-radius: 5px;
      border: none;
    }

    .input-area input[type="text"] {
      flex-grow: 1;
    }

    .emoji-picker {
      display: flex;
      gap: 5px;
    }

    .emoji-picker span {
      cursor: pointer;
      font-size: 1.2em;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="guest-list">
      <h3>Vendégek</h3>
      <div class="guest">Onigen</div>
    </div>
    <div class="chat-area">
      <div class="chat-header">Onigen Chat</div>
      <div class="chat-messages" id="chat-messages">
        <p><strong>Onigen</strong>: Helló világ! 🌍</p>
      </div>
      <div class="input-area">
        <select id="colorPicker">
          <option value="white">Fehér</option>
          <option value="red">Piros</option>
          <option value="green">Zöld</option>
          <option value="blue">Kék</option>
        </select>
        <input type="text" id="chatInput" placeholder="Írj egy üzenetet...">
        <div class="emoji-picker">
          <span onclick="addEmoji('😊')">😊</span>
          <span onclick="addEmoji('😂')">😂</span>
          <span onclick="addEmoji('🔥')">🔥</span>
          <span onclick="addEmoji('❤️')">❤️</span>
          <span onclick="addEmoji('👍')">👍</span>
        </div>
        <input type="file" accept="image/gif">
      </div>
    </div>
  </div>

  <script>
    const input = document.getElementById("chatInput");
    const messages = document.getElementById("chat-messages");
    const colorPicker = document.getElementById("colorPicker");

    input.addEventListener("keydown", function(event) {
      if (event.key === "Enter" && input.value.trim() !== "") {
        const messageText = input.value.trim();
        const color = colorPicker.value;
        const now = new Date();
        const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
        const dateString = now.toLocaleDateString();
        const messageElement = document.createElement("p");
        messageElement.innerHTML = `<strong style="color:${color}">Onigen</strong> <small>(${dateString} ${timeString})</small>: <span style="color:${color}">${messageText}</span>`;
        messages.appendChild(messageElement);
        input.value = "";
        messages.scrollTop = messages.scrollHeight;
      }
    });

    function addEmoji(emoji) {
      input.value += emoji;
      input.focus();
    }
  </script>
</body>
</html>
