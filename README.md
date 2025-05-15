<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tap Clicker Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
      color: #fff;
      animation: backgroundScroll 30s linear infinite;
      background: linear-gradient(270deg, #ff8a00, #e52e71, #9b00e8, #00bfff);
      background-size: 800% 800%;
    }

    @keyframes backgroundScroll {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    #counter {
      font-size: 2em;
      margin: 20px 0;
    }

    #clickBtn {
      padding: 15px 30px;
      font-size: 1.5em;
      cursor: pointer;
      background: #222;
      color: #fff;
      border: none;
      border-radius: 10px;
    }

    #objects {
      margin-top: 20px;
      min-height: 50px;
    }

    #congrats, #bottomText {
      font-size: 1.5em;
      color: #0f0;
      margin-top: 20px;
      display: none;
    }

    #bottomText {
      position: fixed;
      bottom: 10px;
      width: 100%;
    }

    .auto-btn {
      margin: 10px;
      padding: 10px 20px;
      cursor: pointer;
      background: #444;
      color: white;
      border: none;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <h1>Tap Clicker Game</h1>
  <div id="counter">Taps: 0</div>
  <button id="clickBtn">Tap!</button>

  <div>
    <button class="auto-btn" onclick="buyAutoClicker(1000, 100)">Buy Slow Auto-Clicker (100 taps)</button>
    <button class="auto-btn" onclick="buyAutoClicker(333, 500)">Buy Medium Auto-Clicker (500 taps)</button>
    <button class="auto-btn" onclick="buyAutoClicker(100, 2500)">Buy Fast Auto-Clicker (2500 taps)</button>
  </div>

  <div id="objects"></div>
  <div id="congrats">Congrats! You reached 100,000 taps!</div>
  <div id="bottomText">Congrats! You reached 100,000 taps!</div>

  <script>
    let taps = 0;
    const counter = document.getElementById('counter');
    const objects = document.getElementById('objects');
    const congrats = document.getElementById('congrats');
    const bottomText = document.getElementById('bottomText');

    const emojis = [];
    for (let i = 128512; i <= 128512 + 1000; i++) {
      emojis.push(String.fromCodePoint(i));
    }

    function updateCounter() {
      counter.textContent = `Taps: ${taps}`;
      if (taps >= 100000) {
        congrats.style.display = 'block';
        bottomText.style.display = 'block';
      }
    }

    function addTap() {
      taps++;
      updateCounter();

      const newEmoji = document.createElement('span');
      newEmoji.textContent = emojis[Math.floor(Math.random() * emojis.length)];
      newEmoji.style.margin = "0 5px";
      objects.appendChild(newEmoji);
    }

    document.getElementById('clickBtn').addEventListener('click', addTap);

    function buyAutoClicker(speed, cost) {
      if (taps < cost) {
        alert(`Not enough taps! You need ${cost}.`);
        return;
      }

      taps -= cost;
      updateCounter();

      const intervalId = setInterval(addTap, speed);
      setTimeout(() => clearInterval(intervalId), 30 * 60 * 1000); // 30 mins
    }
  </script>
</body>
</html>