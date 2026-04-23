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
<?php
include 'db.php';

$data = json_decode(file_get_contents("php://input"));
$key = $data->key;

$sql = "SELECT * FROM keys WHERE license_key='$key'";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
  $row = $result->fetch_assoc();

  if ($row['status'] == "active") {

    if (strtotime($row['expires_at']) > time()) {
      echo json_encode(["valid"=>true]);
    } else {
      echo json_encode(["valid"=>false,"msg"=>"expirada"]);
    }

  } else {
    echo json_encode(["valid"=>false,"msg"=>"usada"]);
  }

} else {
  echo json_encode(["valid"=>false,"msg"=>"no existe"]);
}
?>
body {
  background:#0f172a;
  color:white;
  font-family:Arial;
  display:flex;
  justify-content:center;
  align-items:center;
  height:100vh;
}

.box {
  background:#111827;
  padding:20px;
  border-radius:10px;
  width:300px;
  text-align:center;
}

select,button {
  width:100%;
  padding:10px;
  margin-top:10px;
}
