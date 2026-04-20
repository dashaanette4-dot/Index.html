<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Escáner QR CONALEP</title>

<!-- Librería confiable -->
<script src="https://unpkg.com/html5-qrcode" type="text/javascript"></script>

<style>
body{
    margin:0;
    font-family: Arial;
    text-align:center;
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    color:white;
}
h2{ margin-top:30px; }
#reader{
    width:300px;
    margin:auto;
    border-radius:15px;
    overflow:hidden;
}
#resultado{
    margin-top:20px;
    padding:15px;
    border-radius:10px;
    font-weight:bold;
}
.ok{ background:#00c853; }
.bad{ background:#d50000; }
</style>
</head>

<body>

<h2>🎓 CONALEP 109</h2>
<p>Escanea tu credencial (QR)</p>

<div id="reader"></div>
<div id="resultado">Esperando escaneo...</div>

<script>
function iniciarScanner() {
    const html5QrCode = new Html5Qrcode("reader");

    Html5Qrcode.getCameras().then(cameras => {
        if (cameras && cameras.length) {
            html5QrCode.start(
                cameras[0].id,
                { fps: 10, qrbox: 250 },
                (decodedText) => {
                    validar(decodedText);
                }
            );
        }
    }).catch(err => {
        document.getElementById("resultado").innerText =
        "Error al acceder a la cámara";
    });
}

function validar(texto){
    let res = document.getElementById("resultado");

    if(texto.length >= 6){
        res.innerHTML = "✅ Acceso permitido<br>Matrícula: " + texto;
        res.className = "ok";
    }else{
        res.innerHTML = "❌ Acceso denegado";
        res.className = "bad";
    }
}

iniciarScanner();
</script>

</body>
</html>
