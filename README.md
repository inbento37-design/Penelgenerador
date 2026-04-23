<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Generador de Keys</title>

  <style>
    body {
      margin: 0;
      font-family: Arial;
      background: #0f172a;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      gap: 20px;
    }

    .box {
      background: #111827;
      padding: 20px;
      border-radius: 12px;
      width: 320px;
      text-align: center;
      box-shadow: 0 0 15px rgba(0,0,0,0.5);
    }

    input, select, button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 8px;
      border: none;
      outline: none;
    }

    button {
      background: #3b82f6;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background: #2563eb;
    }

    .hidden {
      display: none;
    }

    .key {
      margin-top: 15px;
      background: #1f2937;
      padding: 10px;
      border-radius: 8px;
      word-break: break-all;
    }

    .side {
      width: 220px;
      background: #111827;
      padding: 15px;
      border-radius: 12px;
      text-align: center;
    }

    .timer {
      margin-top: 10px;
      color: #22c55e;
      font-size: 18px;
    }
  </style>
</head>

<body>

<!-- LOGIN -->
<div class="box" id="loginBox">
  <h2>Acceso Admin</h2>
  <input type="password" id="pass" placeholder="Contraseña">
  <button onclick="login()">Entrar</button>
</div>

<!-- PANEL -->
<div class="box hidden" id="panel">
  <h2>Generador de Keys</h2>

  <!-- ✔ AQUÍ ESTÁ CORREGIDO -->
  <select id="days">
    <option value="1">1 Día</option>
    <option value="2">2 Días</option>
    <option value="3">3 Días</option>
    <option value="5">5 Días</option>
    <option value="7">7 Días</option>
    <option value="15">15 Días</option>
    <option value="30">30 Días</option>
    <option value="90">90 Días</option>
    <option value="180">180 Días</option>
    <option value="365">1 Año</option>
  </select>

  <button onclick="generateKey()">Generar Key</button>

  <div class="key" id="result">Aquí aparecerá la key</div>
</div>

<!-- TIMER -->
<div class="side hidden" id="sidePanel">
  <h3>Tiempo restante</h3>
  <div class="timer" id="timer">--</div>
</div>

<script>
const ADMIN_PASS = "123456";

let expiration = 0;
let interval;

function login() {
  let p = document.getElementById("pass").value;

  if (p === ADMIN_PASS) {
    document.getElementById("loginBox").classList.add("hidden");
    document.getElementById("panel").classList.remove("hidden");
    document.getElementById("sidePanel").classList.remove("hidden");
  } else {
    alert("Contraseña incorrecta");
  }
}

function randomPart() {
  let chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
  let out = "";

  for (let i = 0; i < 4; i++) {
    out += chars[Math.floor(Math.random() * chars.length)];
  }

  return out;
}

function generateKey() {
  let days = parseInt(document.getElementById("days").value);

  let key = randomPart() + "-" + randomPart() + "-" + randomPart();

  expiration = Date.now() + (days * 24 * 60 * 60 * 1000);

  document.getElementById("result").innerHTML =
    "<b>KEY:</b> " + key + "<br><b>Días:</b> " + days;

  startTimer();
}

function startTimer() {
  clearInterval(interval);

  interval = setInterval(() => {
    let diff = expiration - Date.now();

    if (diff <= 0) {
      document.getElementById("timer").innerText = "EXPIRADA";
      clearInterval(interval);
      return;
    }

    let d = Math.floor(diff / (1000 * 60 * 60 * 24));
    let h = Math.floor((diff / (1000 * 60 * 60)) % 24);
    let m = Math.floor((diff / (1000 * 60)) % 60);

    document.getElementById("timer").innerText =
      d + "d " + h + "h " + m + "m";

  }, 1000);
}
</script>

</body>
</html>
