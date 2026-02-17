<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>NayaStudy</title>

<style>
body{
  margin:0;
  font-family:Arial, sans-serif;
  display:flex;
}

/* Barra lateral */
.sidebar{
  width:220px;
  height:100vh;
  background:#d9c6f3;
  padding:15px;
  box-sizing:border-box;
}

.sidebar h2{
  text-align:center;
}

.menu button{
  width:100%;
  margin:8px 0;
  padding:10px;
  border:none;
  border-radius:10px;
  cursor:pointer;
}

/* Área principal */
.main{
  flex:1;
  padding:30px;
  text-align:center;
}

.frase{
  margin-top:40px;
  font-size:20px;
  opacity:0.8;
}

/* Temas */
.theme-lila{ background:#f6f0ff; }
.theme-menta{ background:#e8fff5; }
.theme-gris{ background:#f2f2f2; }

/* Botón tema */
.tema-btn{
  margin-top:10px;
  padding:6px;
  border:none;
  border-radius:8px;
  cursor:pointer;
}
</style>
</head>

<body class="theme-lila">

<div class="sidebar">
  <h2>NayaStudy</h2>

  🔥 Racha: <span id="racha">0</span> días
  <hr>

  <div class="menu">
    <button onclick="mostrar('inicio')">Inicio</button>
    <button onclick="mostrar('temario')">Subir temario</button>
    <button onclick="mostrar('examen')">Exámenes</button>
    <button onclick="mostrar('juegos')">Juegos</button>
    <button onclick="mostrar('repaso')">Repaso</button>
    <button onclick="mostrar('progreso')">Progreso</button>
  </div>

  <hr>
  <b>Ajustes</b><br>
  Tema:
  <br>
  <button class="tema-btn" onclick="cambiarTema('theme-lila')">Lila</button>
  <button class="tema-btn" onclick="cambiarTema('theme-menta')">Menta</button>
  <button class="tema-btn" onclick="cambiarTema('theme-gris')">Gris</button>
</div>

<div class="main">

<div id="inicio" class="pantalla">
  <h1>Bienvenida a NayaStudy</h1>
  <div class="frase" id="fraseMotivadora"></div>
</div>

<div id="temario" class="pantalla" style="display:none">
  <h1>Subir Temario</h1>
  <input type="file">
  <p>Aquí podrás subir PDFs o textos en el futuro.</p>
</div>

<div id="examen" class="pantalla" style="display:none">
  <h1>Exámenes</h1>
  <p>Aquí podrás configurar tus exámenes.</p>
</div>

<div id="juegos" class="pantalla" style="display:none">
  <h1>Juegos</h1>
  <p>Aquí estarán los juegos interactivos.</p>
</div>

<div id="repaso" class="pantalla" style="display:none">
  <h1>Repaso</h1>
  <p>Aquí aparecerán resúmenes y explicaciones.</p>
</div>

<div id="progreso" class="pantalla" style="display:none">
  <h1>Progreso</h1>
  <p>Aquí verás tu avance.</p>
</div>

</div>

<script>

/* Frases motivadoras */
const frases=[
"Vamos por más conocimiento",
"Cada día aprendes algo nuevo",
"Estás más cerca de tu meta",
"Hoy es un buen día para estudiar",
"Pequeños pasos también cuentan"
];

document.getElementById("fraseMotivadora").innerText=
frases[Math.floor(Math.random()*frases.length)];

/* Navegación */
function mostrar(id){
  let pantallas=document.querySelectorAll(".pantalla");
  pantallas.forEach(p=>p.style.display="none");
  document.getElementById(id).style.display="block";
}

/* Temas */
function cambiarTema(tema){
  document.body.className=tema;
  localStorage.setItem("tema",tema);
}

/* Cargar tema guardado */
let temaGuardado=localStorage.getItem("tema");
if(temaGuardado){
  document.body.className=temaGuardado;
}

/* Racha simple */
let racha=localStorage.getItem("racha") || 1;
document.getElementById("racha").innerText=racha;
localStorage.setItem("racha",racha);

</script>

</body>
</html>
