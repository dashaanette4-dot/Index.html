<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Acceso CONALEP</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html5-qrcode/2.3.8/html5-qrcode.min.js"></script>

<style>
body {
    font-family: Arial;
    text-align: center;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
    color: white;
}

#reader {
    width: 300px;
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

<h2>📷 Escaneo de Credencial</h2>
<p>CONALEP 109</p>

<div id="reader"></div>
<div id="status">Esperando escaneo...</div>

<script>
function onScanSuccess(decodedText) {

    // Ejemplo de validación
    if (decodedText.length >= 8) {
        document.getElementById("status").innerText =
        "✅ Acceso permitido\nMatrícula: " + decodedText;
        document.getElementById("status").className = "success";
    } else {
        document.getElementById("status").innerText =
        "❌ Acceso denegado";
        document.getElementById("status").className = "error";
    }
}

let scanner = new Html5QrcodeScanner(
    "reader",
    { fps: 10, qrbox: 250 }
);

scanner.render(onScanSuccess);
</script>

</body>
</html>
