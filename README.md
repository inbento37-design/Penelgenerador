<!DOCTYPE html>
<html>
<head>
  <title>Panel Keys</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="box">
  <h2>Admin Panel</h2>

  <select id="days">
    <option value="1">1 Día</option>
    <option value="2">2 Días</option>
    <option value="3">3 Días</option>
    <option value="5">5 Días</option>
  </select>

  <button onclick="gen()">Generar</button>

  <p id="out"></p>
</div>

<script src="script.js"></script>
</body>
</html>
