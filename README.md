<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Verificación de Certificado</title>

<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">
<a href="" target="_blank" class="btn-icep">
    <i class="fas fa-graduation-cap"></i>
    INCAEP - SAN MARCOS
</a>

<style>
.btn-icep{
    display:inline-flex;
    align-items:center;
    gap:10px;
    background:#c62828;
    color:white;
    text-decoration:none;
    padding:15px 25px;
    border-radius:10px;
    font-weight:bold;
    transition:0.3s;
}

.btn-icep:hover{
    background:#a91f1f;
    transform:translateY(-2px);
}

.btn-icep i{
    font-size:22px;
}
</style>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4f6f9;
        text-align: center;
        padding: 40px;
    }
    .container {
        background: white;
        padding: 30px;
        border-radius: 12px;
        max-width: 500px;
        margin: auto;
        box-shadow: 0 5px 15px rgba(0,0,0,0.1);
    }
    h2 {
        color: #0d6efd;
    }

    input {
        width: 100%;
        padding: 12px;
        margin-top: 10px;
        border-radius: 6px;
        border: 1px solid #ccc;
    }

    button {
        margin-top: 15px;
        padding: 12px;
        width: 100%;
        background: #0d6efd;
        color: white;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        font-size: 16px;
    }
    .resultado {
        margin-top: 20px;
        padding: 15px;
        border-radius: 6px;
        display: none;
    }
    .ok {
        background: #e7f5ff;
        color: #084298;
    }

    .error {
        background: #fde2e1;
        color: #842029;
    }
    .btn-descargar {
        background: #198754;
        margin-top: 15px;
    }
</style>
</head>

<body>

<div class="container">
    <h2><i class="fa-solid fa-certificate"></i> Verificación de Certificado</h2>

    <input type="text" id="codigo" placeholder="Ingrese DNI, nombre o código">

    <button onclick="verificar()">
        <i class="fa-solid fa-magnifying-glass"></i> Verificar certificado
    </button>

    <div id="resultado" class="resultado"></div>
</div>

<script>
const certificados = [
    {
        codigo: "71766830-1",
        curso: "CAPACITACIÓN DESCENTRALIZADA PARA FORTALECER CAPACIDADES EN INMUNIZACIONES Y MANEJO DE LA CADENA DE FRÍO",
        nombre: "GLORIA DAMARIS, LINARES SÁENZ",
        fecha: "del 09 al 13 de febrero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1nbIll4uz8-AeI-oIZBYqWqSFW6xitbQO"
    },
    
];

function verificar() {
    const valor = document.getElementById("codigo").value.trim().toLowerCase();
    const resultado = document.getElementById("resultado");

    let encontrados = certificados.filter(c =>
        c.codigo.toLowerCase() === valor ||
        c.nombre.toLowerCase().includes(valor)
    );

    resultado.innerHTML = "";
    resultado.style.display = "block";

    if (encontrados.length > 0) {
        resultado.className = "resultado ok";

        resultado.innerHTML += `
            <strong><i class="fa-solid fa-circle-check"></i> ${encontrados.length} certificado(s) encontrado(s)</strong><br><br>
        `;

        encontrados.forEach(data => {
            resultado.innerHTML += `
                <div style="margin-bottom:15px; padding:10px; background:#fff; border-radius:6px;">
                    <b>Curso:</b> ${data.curso}<br>
                    <b>Nombre:</b> ${data.nombre}<br>
                    <b>Fecha:</b> ${data.fecha}<br>

                    <button class="btn-descargar" onclick="descargar('${data.archivo}')">
                        <i class="fa-solid fa-download"></i> Descargar certificado
                    </button>
                </div>
            `;
        });

    } else {
        resultado.className = "resultado error";
        resultado.innerHTML = "<i class='fa-solid fa-circle-xmark'></i> No se encontraron resultados";
    }
}

function descargar(archivo) {
    window.open(archivo, "_blank");
}
</script>

</body>
</html>
