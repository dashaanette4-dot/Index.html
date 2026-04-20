<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Control de Acceso CONALEP</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html5-qrcode/2.3.8/html5-qrcode.min.js"></script>

<style>
body {
    margin: 0;
    font-family: Arial;
    text-align: center;
    background: linear-gradient(135deg, #1e3c72, #2a5298);
    color: white;
}

.container {
    margin-top: 40px;
}

#reader {
    width: 280px;
    margin: auto;
    border-radius: 15px;
    overflow: hidden;
}

#status {
    margin-top: 20px;
    padding: 15px;
    border-radius: 10px;
    font-weight: bold;
}

.success { background: #00c853; }
.error { background: #d50000; }
</style>
</head>

<body>

<div class="container">
    <h2>🎓 CONALEP 109</h2>
    <p>Escanea tu credencial</p>

    <div id="reader"></div>
    <div id="status">Esperando escaneo...</div>
</div>

<script>
function onScanSuccess(texto) {

    if (texto.length >= 6) {
        document.getElementById("status").innerHTML =
        "✅ Acceso permitido<br>Matrícula: " + texto;
        document.getElementById("status").className = "success";
    } else {
        document.getElementById("status").innerHTML =
        "❌ Acceso denegado";
        document.getElementById("status").className = "error";
    }
}

let scanner = new Html5QrcodeScanner(
    "reader",
    { fps: 10, qrbox: 200 }
);

scanner.render(onScanSuccess);
</script>

</body>
</html>
