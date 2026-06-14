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
    {
        codigo: "71766830",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "GLORIA DAMARIS, LINARES SÁENZ",
        fecha: "del 07 al 11 de diciembre del 2025",
        archivo: "https://drive.google.com/uc?export=download&id=1htOKlA-kL_Zl7XLQ0IwkwIFz0KvTUDuL"
    },
    {
        codigo: "LIN02Z",
        curso: "JORNADA NACIONAL DE ACTUALIZACIÓN EN BIOSEGURIDAD, IAAS Y MANEJO SEGURO DE RESIDUOS HOSPITALARIOS",
        nombre: "GLORIA DAMARIS, LINARES SÁENZ",
        fecha: "del 04 al 12 de marzo del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1pb8oFxplbhLt3e_ciNd3k787Y2fapUvZ"
    },
    {
        codigo: "71997181",
        curso: "CAPACITACIÓN DESCENTRALIZADA PARA FORTALECER CAPACIDADES EN INMUNIZACIONES Y MANEJO DE LA CADENA DE FRÍO",
        nombre: "ANGELA LISBETH, PEREZ CADENA",
        fecha: "del 09 al 13 de febrero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1gEQUJ44r7yHvmfch1bV00wzkuLS3hcNH"
    },
    {
        codigo: "45439854",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "KARINA ELIZABETH, LONGA CORTEZ",
        fecha: "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1xqyxkAjMwoUiqH2IUKaQz77JpcgQlKuP"
    },
    {
        codigo: "44577184-1",
        curso: "BIOSEGURIDAD HOSPITALARIA",
        nombre: "MANTILLA CERQUIN, LUIS ALBERTO",
        fecha: "28 de febrero del 2025",
        archivo: "https://drive.google.com/uc?export=download&id=1cF7aFcQQQfcQHbk5Z8FbBSSEKRSfZs50"
    },
    {
        codigo: "72281648-1",
        curso: "BIOSEGURIDAD HOSPITALARIA",
        nombre: "SANCHEZ VILLA, MARISOL",
        fecha: "28 de febrero del 2025",
        archivo: "https://drive.google.com/uc?export=download&id=1Y_bEvRG3Nlik6611VSByQCghgIW0UH31"
    },
    {
        codigo: "72281648-2",
        curso: "PRIMEROS AUXILIOS",
        nombre: "SANCHEZ VILLA, MARISOL",
        fecha: "28 de febrero del 2025",
        archivo: "https://drive.google.com/uc?export=download&id=1bj-oscTIXjwqcprSbLGbP812m9nAcj9I"
    },
     {
        codigo:  "48295755-1",
        curso: "PRIMEROS AUXILIOS",
        nombre: "BARDALES DIAZ, JHIMMY HERMES",
        fecha: "28 de febrero del 2025",
        archivo: "certificado1.pdf"
    },
    {
        codigo: "77133960-1",
        curso: "PRIMEROS AUXILIOS", 
        nombre: "MANTILLA CUEVA, MIGUEL ANGEL", 
        fecha: "03, 04 Y 05 de Marzo del 2025", 
        archivo: "https://drive.google.com/uc?export=download&id=12Zu1YlcEqWv0YItuJAWPTIwowxRJuFDU" 
    }, 
    { 
        codigo:  "46026978",
        curso: "BUENAS PRÁCTICAS EN EL ALMACENAMIENTO, DISTRIBUCIÓN Y TRANSPORTE DE MEDICAMENTOS, DISPOSITIVOS MÉDICOS Y PRODUCTOS SANITARIOS", 
        nombre: "VARGAS CARRASCO, ALEX LENNIN", 
        fecha: "02 al 07 de Marzo del 2026", 
        archivo: "https://drive.google.com/uc?export=download&id=1kNxIPct9O9FvmbuP7vipmqDMWihW1yx4" 
    },
     {
        codigo: "46026978-1",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "VARGAS CARRASCO, ALEX LENNIN",
        fecha:  "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1mVUBV2swzgbzmcdWWgMaypmENFPR6B_6"
    }, 
    { 
        codigo: "46026978-2",
        curso: "ENFERMEDADES METAXÉNICAS", 
        nombre: "VARGAS CARRASCO, ALEX LENNIN", 
        fecha: "del 16 al 22 de setiembre del 2025", 
        archivo: "https://drive.google.com/uc?export=download&id=1EYrlxCyIy-Xhnik4Sd9oe7BQid9RHLG-" 
    },
     {
        codigo: "VAR05",
        curso: "SEGURIDAD Y SALUD EN EL TRABAJO",
        nombre: "VARGAS CARRASCO, ALEX LENNIN",
        fecha:  "del 16 al 24 de febrero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1HplfgOWIihl7FqqyIwtN_J8hIFi55kkb"
    }, 
    { 
        codigo: "46418920-1",
        curso: "BUENAS PRÁCTICAS EN EL ALMACENAMIENTO, DISTRIBUCIÓN Y TRANSPORTE DE MEDICAMENTOS, DISPOSITIVOS MÉDICOS Y PRODUCTOS SANITARIOS", 
        nombre: "CASAS ZELADA, DEYSI MARISOL", 
        fecha: "02 al 07 de Marzo del 2026", 
        archivo: "https://drive.google.com/uc?export=download&id=101VfqZkLn_DCMb50cc4fVMhqQoR4rzA6" 
    },
    {
        codigo: "48318757",
        curso: "BUENAS PRACTICAS EN EL ALMACENAMIENTO, DISTRIBUCIÓN Y TRANSPORTE DE MEDICAMENTOS, DISPOSITIVOS MÉDICOS Y PRODUCTOS SANITARIOS",
        nombre: "HUARIPATA MENDOZA, ROSITA",
        fecha: " DEL 02 AL 07 DE MARZO 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1mn2z72aOY7wiK5rimmXsWm3fj_5Vrjju"
    },
    {
        codigo: "27577469",
        curso: "BUENAS PRACTICAS EN EL ALMACENAMIENTO, DISTRIBUCIÓN Y TRANSPORTE DE MEDICAMENTOS, DISPOSITIVOS MÉDICOS Y PRODUCTOS SANITARIOS",
        nombre: "PAREDES ZAMORA, ROSA ELIZABETH",
        fecha: " DEL 02 AL 07 DE MARZO 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1BpSDWNvEaOMLT0gXn-zCAuRU2OTnCcwH"
    },
    {
        codigo: "PAR05",
        curso: "SEGURIDAD Y SALUD EN EL TRABAJO",
        nombre: "PAREDES ZAMORA, ROSA ELIZABETH",
        fecha:  "del 16 al 24 de febrero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1xjitClhHvwSV1vwePxMl68dd0ryAoxmR"
    }, 
     {
        codigo: "27577469-1",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "PAREDES ZAMORA, ROSA ELIZABETH",
        fecha:  "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1dTkd3JsO-Gy4ltkgoLO1RVSr7QYwnom_"
    }, 
    {
        codigo: "60052013",
        curso: "BUENAS PRACTICAS EN EL ALMACENAMIENTO, DISTRIBUCIÓN Y TRANSPORTE DE MEDICAMENTOS, DISPOSITIVOS MÉDICOS Y PRODUCTOS SANITARIOS",
        nombre: "GOICOCHEA PAREDES, KARLA FIORELLA",
        fecha: " DEL 02 AL 07 DE MARZO 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1eeK7ZzK94bWnCKYp4Ko2B5GBjZbXI6-q"
    },
    {
        codigo: "26724217",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "CERQUIN SAAVEDRA, MARÍA ROSALIA",
        fecha: "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1dkPgI64Dm1qnOkkt_F831SNAEN2WlKx5"
    },
    {
        codigo: "41871474",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "RASCO SALDAÑA LEONILA ROSARIO",
        fecha: "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1hZfbRVPjWzdqIMr8eRid_krUyjyf_LH0" 
    },
    {
        codigo: "42677237",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "VARGAS CARRASCO LUIS ANTONIO",
        fecha: "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1x9xbIwut7hydDM9mfMKI71vCDquIjJpu" 
    }, 
    {
        codigo: "28062728",
        curso: "RCP y Tratamiento Primario de heridas",
        nombre: "TERAN SALDAÑA DORIS MARGARITA",
        fecha: "del 05 al 09 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1Ou0fsV_h3_wH2us473Pp9PvQNnGWr-hA" 
    }, 
    {
        codigo: "41871474-1",
        curso: "Modelo de cuidado integral de salud por curso de vida",
        nombre: "RASCO SALDAÑA LEONILA ROSARIO",
        fecha: "del 18 al 27 de enero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1wOl8Q9Y5fLb7pukVN6EYrpezXQ2xE2Mz" 
    },
    {
        codigo: "41871474-2",
        curso: "Competencias del Técnico en Enfermería",
        nombre: "RASCO SALDAÑA LEONILA ROSARIO",
        fecha: "del 02 al 11 de febrero del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1wNYwcoDHsLF9mD2Y_CDK_TMFgAQOArgf"
    },
    {
        codigo: "44110402-1",
        curso: "BIOSEGURIDAD HOSPITALARIA",
        nombre: "GUTIERREZ CABANILLAS, ORFA NOEMI",
        fecha: "DEL 12 AL 16 de ENERO del 2026",
        archivo: "https://drive.google.com/uc?export=download&id=1hLM1m3Qf4rCc6MnFexbD7DT3Sx3CX6oy"
    }
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
