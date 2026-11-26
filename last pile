
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Traffic Light Challenge</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg,#101d38,#203c65);
  color: white;
  text-align: center;
}
h1 { margin: 25px 0 5px; }
.subtitle { color: #b8c9e5; }
.game {
  max-width: 650px;
  margin: 25px auto;
  padding: 20px;
}
.panel {
  display: flex;
  justify-content: space-around;
  background: #ffffff15;
  padding: 15px;
  border-radius: 15px;
  margin-bottom: 18px;
}
.panel strong { color: #ffd45c; }
.traffic {
  width: 95px;
  padding: 12px;
  background: #161616;
  border-radius: 25px;
  margin: auto;
  box-shadow: 0 8px 20px #0008;
}
.light {
  width: 55px;
  height: 55px;
  border-radius: 50%;
  margin: 8px auto;
  background: #393939;
  opacity: .4;
}
.red.on { background: #ff3434; box-shadow: 0 0 25px red; opacity: 1; }
.yellow.on { background: #ffd52d; box-shadow: 0 0 25px yellow; opacity: 1; }
.green.on { background: #29e66c; box-shadow: 0 0 25px lime; opacity: 1; }

.road {
  height: 210px;
  background: #343a45;
  border-radius: 15px;
  position: relative;
  overflow: hidden;
  margin-top: 20px;
  border: 4px solid #59616e;
}
.road:before {
  content: "";
  position: absolute;
  left: 50%;
  height: 100%;
  border-left: 5px dashed white;
  opacity: .6;
}
.finish {
  position: absolute;
  right: 10px;
  top: 0;
  height: 100%;
  width: 12px;
  background: repeating-linear-gradient(
    0deg, white 0 10px, black 10px 20px
  );
}
.player {
  position: absolute;
  left: 10px;
  top: 78px;
  font-size: 45px;
  transition: left .25s;
}
.status {
  font-size: 21px;
  font-weight: bold;
  margin: 20px;
  color: #ffe16b;
}
button {
  border: none;
  border-radius: 12px;
  padding: 15px 25px;
  margin: 7px;
  font-size: 17px;
  font-weight: bold;
  cursor: pointer;
  transition: .2s;
}
button:hover { transform: scale(1.06); }
.move { background: #32df78; color: #102a1a; }
.start { background: #ffd34f; color: #332500; }
.rules {
  background: #ffffff12;
  padding: 15px;
  border-radius: 15px;
  margin-top: 20px;
  line-height: 1.8;
}
</style>
</head>

<body>
<h1>🚦 TRAFFIC LIGHT CHALLENGE</h1>
<p class="subtitle">신호를 지키고 결승선까지 도착하라!</p>

<div class="game">
  <div class="panel">
    <div>점수<br><strong id="score">0</strong></div>
    <div>이동 거리<br><strong id="distance">0%</strong></div>
    <div>최고 기록<br><strong id="best">0</strong></div>
  </div>

  <div class="traffic">
    <div id="red" class="light red on"></div>
    <div id="yellow" class="light yellow"></div>
    <div id="green" class="light green"></div>
  </div>

  <div class="road">
    <div class="finish"></div>
    <div id="player" class="player">🚗</div>
  </div>

  <div id="status" class="status">게임을 시작하세요!</div>

  <button class="start" onclick="startGame()">▶ 게임 시작</button>
  <button class="move" onclick="moveCar()">🚗 이동하기</button>

  <div class="rules">
    <h3>📖 게임 규칙</h3>
    🟢 초록불 : 이동 가능!<br>
    🟡 노란불 : 이동하면 안 돼요!<br>
    🔴 빨간불 : 반드시 정지!<br>
    🏁 결승선에 도착하면 승리!
  </div>
</div>

<script>
let distance = 0;
let score = 0;
let light = "red";
let playing = false;
let timer;
let best = Number(localStorage.getItem("trafficBest")) || 0;

document.getElementById("best").textContent = best;

function changeLight() {
  const lights = ["red", "green", "yellow"];
  light = lights[Math.floor(Math.random() * 3)];

  lights.forEach(color => {
    document.getElementById(color).classList.toggle(
      "on", color === light
    );
  });

  const messages = {
    red: "🔴 빨간불! 멈춰!",
    yellow: "🟡 노란불! 조심해!",
    green: "🟢 초록불! 출발!"
  };

  document.getElementById("status").textContent =
    messages[light];
}

function startGame() {
  clearInterval(timer);
  distance = 0;
  score = 0;
  playing = true;

  updateDisplay();
  document.getElementById("player").style.left = "10px";

  changeLight();
  document.getElementById("status").textContent =
    "신호를 확인하고 출발하세요!";

  timer = setInterval(changeLight, 2500);
}

function moveCar() {
  if (!playing) {
    document.getElementById("status").textContent =
      "먼저 게임을 시작하세요!";
    return;
  }

  if (light !== "green") {
    playing = false;
    clearInterval(timer);
    document.getElementById("status").textContent =
      "💥 신호 위반! 게임 오버!";
    return;
  }

  distance += 10;
  score += 10;

  updateDisplay();

  if (distance >= 100) {
    distance = 100;
    playing = false;
    clearInterval(timer);
    updateDisplay();

    document.getElementById("status").textContent =
      "🏆 성공! 결승선에 도착했습니다!";

    if (score > best) {
      best = score;
      localStorage.setItem("trafficBest", best);
      document.getElementById("best").textContent = best;
    }
    return;
  }

  document.getElementById("status").textContent =
    "멋져요! 계속 달려보세요! 🚗";
}

function updateDisplay() {
  document.getElementById("score").textContent = score;
  document.getElementById("distance").textContent =
    distance + "%";

  document.getElementById("player").style.left =
    `calc(${distance}% - 20px)`;
}
</script>
</body>
</html>
