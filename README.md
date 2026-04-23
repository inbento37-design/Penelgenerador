<!DOCTYPE html><html lang="es">
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
    }.box {
  background: #111827;
  padding: 20px;
  border-radius: 12px;
  width: 320px;
  box-shadow: 0 0 15px rgba(0,0,0,0.5);
  text-align: center;
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

  </style>
</head>
<body><div class="box" id="loginBox">
  <h2>Acceso Admin</h2>
  <input type="password" id="pass" placeholder="Contraseña admin">
  <button onclick="login()">Entrar</button>
</div><div class="box hidden" id="panel">
  <h2>Generador de Keys</h2>  <select id="days">
    <option value="1">1 Día</option>
    <option value="2">2 Días</option>
    <option value="3">3 Días</option>
    <option value="5">5 Días</option>
  </select><button onclick="generateKey()">Generar Key</button>

  <div class="key" id="result">Aquí aparecerá la key</div>
</div><script>
const ADMIN_PASS = "123456"; // cambia esto

function login() {
  let p = document.getElementById("pass").value;

  if (p === ADMIN_PASS) {
    document.getElementById("loginBox").classList.add("hidden");
    document.getElementById("panel").classList.remove("hidden");
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
  let days = document.getElementById("days").value;

  let key = randomPart() + "-" + randomPart() + "-" + randomPart();

  document.getElementById("result").innerHTML =
    "<b>KEY:</b> " + key + "<br><b>Días:</b> " + days;

  console.log("Key generada:", key, days);
}
</script></body>
</html>
