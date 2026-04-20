<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Escáner Código de Barras</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/quagga/0.12.1/quagga.min.js"></script>

<style>
body {
    font-family: Arial;
    text-align: center;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
    color: white;
} 
    
#scanner {
    width: 300px;
    height: 200px;
    margin: auto;
    border: 3px solid white;
    border-radius: 10px;
}

#resultado {
    margin-top: 20px;
    font-size: 18px;
    font-weight: bold;
}
</style>
</head>

<body>

<h2>📷 Escanear Credencial</h2>
<p>CONALEP 109</p>

<div id="scanner"></div>
<div id="resultado">Esperando escaneo...</div>

<script>
Quagga.init({
    inputStream: {
        type: "LiveStream",
        target: document.querySelector('#scanner'),
        constraints: {
            facingMode: "environment"
        }
    },
    decoder: {
        readers: ["code_128_reader", "ean_reader", "ean_8_reader"]
    }
}, function(err) {
    if (err) {
        console.log(err);
        return;
    }
    Quagga.start();
});

Quagga.onDetected(function(data) {
    let codigo = data.codeResult.code;

    if (codigo.length >= 6) {
        document.getElementById("resultado").innerHTML =
        "✅ Acceso permitido<br>Código: " + codigo;
    } else {
        document.getElementById("resultado").innerHTML =
        "❌ Acceso denegado";
    }
});
</script>

</body>
</html>
