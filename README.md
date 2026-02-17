<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NayaStudy</title>

<style>
body{
  margin:0;
  font-family:Segoe UI;
  background:linear-gradient(135deg,#c8d8ff,#e5ccff);
}

nav{
  background:white;
  padding:10px;
  display:flex;
  gap:10px;
  justify-content:center;
  box-shadow:0 4px 10px rgba(0,0,0,0.1);
  flex-wrap:wrap;
}

button{
  border:none;
  padding:8px 12px;
  border-radius:10px;
  background:#7b6cf6;
  color:white;
  font-weight:bold;
  cursor:pointer;
}

.section{
  padding:20px;
  display:none;
}

.active{
  display:block;
}

textarea,input,select{
  width:100%;
  padding:8px;
  margin-top:8px;
  border-radius:10px;
  border:1px solid #ccc;
}

.card{
  background:white;
  padding:15px;
  border-radius:20px;
  box-shadow:0 10px 20px rgba(0,0,0,0.1);
  max-width:500px;
  margin:auto;
}
</style>
</head>

<body>

<nav>
<button onclick="showSection('inicio')">Inicio</button>
<button onclick="showSection('temarios')">Temarios</button>
<button onclick="showSection('examen')">Exámenes</button>
<button onclick="showSection('juegos')">Juegos</button>
<button onclick="showSection('ajustes')">Ajustes</button>
</nav>

<!-- INICIO -->
<div id="inicio" class="section active">
<div class="card">
<h2>Bienvenida a NayaStudy ✨</h2>
<p id="saludo"></p>
</div>
</div>

<!-- TEMARIOS -->
<div id="temarios" class="section">
<div class="card">
<h2>Agregar temario</h2>

<input type="text" id="nombreTema" placeholder="Nombre del tema">
<textarea id="contenidoTema" rows="5" placeholder="Pega aquí el contenido"></textarea>
<button onclick="guardarTema()">Guardar tema</button>

<h3>Temas guardados</h3>
<ul id="listaTemas"></ul>

</div>
</div>

<!-- EXAMEN -->
<div id="examen" class="section">
<div class="card">
<h2>Crear examen</h2>

<label>Selecciona un tema:</label>
<select id="temaSeleccionado"></select>

<label>Cantidad de preguntas:</label>
<input type="number" id="numPreguntas" value="3">

<label>Tipo de preguntas:</label>
<select id="tipoPregunta">
<option value="abierta">Respuesta escrita</option>
<option value="multiple">Selección múltiple</option>
</select>

<button onclick="generarPreguntas()">Generar examen</button>

<div id="preguntas"></div>

</div>
</div>

<!-- JUEGOS -->
<div id="juegos" class="section">
<div class="card">
<h2>Juegos interactivos 🎮</h2>
<p>Próximamente:</p>
<ul>
<li>Tarjetas de memoria</li>
<li>Unir conceptos</li>
<li>Quiz rápido</li>
</ul>
</div>
</div>

<!-- AJUSTES -->
<div id="ajustes" class="section">
<div class="card">
<h2>Cuenta</h2>
<input type="text" id="nombreUsuario" placeholder="Tu nombre">
<button onclick="guardarUsuario()">Guardar</button>
</div>
</div>

<script>

function showSection(id){
  document.querySelectorAll('.section').forEach(sec=>{
    sec.classList.remove('active');
  });
  document.getElementById(id).classList.add('active');
}

function guardarUsuario(){
  let nombre = document.getElementById("nombreUsuario").value;
  localStorage.setItem("usuario", nombre);
  cargarUsuario();
}

function cargarUsuario(){
  let nombre = localStorage.getItem("usuario");
  if(nombre){
    document.getElementById("saludo").innerText =
      "Hola " + nombre + " 💜 lista para estudiar?";
  }
}

function guardarTema(){
  let nombre = document.getElementById("nombreTema").value;
  let contenido = document.getElementById("contenidoTema").value;

  if(!nombre || !contenido){
    alert("Completa el tema");
    return;
  }

  let temas = JSON.parse(localStorage.getItem("temas") || "[]");
  temas.push({nombre, contenido});
  localStorage.setItem("temas", JSON.stringify(temas));

  cargarTemas();
}

function cargarTemas(){
  let temas = JSON.parse(localStorage.getItem("temas") || "[]");

  let lista = document.getElementById("listaTemas");
  let selector = document.getElementById("temaSeleccionado");

  lista.innerHTML = "";
  selector.innerHTML = "";

  temas.forEach((tema, i)=>{
    let li = document.createElement("li");
    li.innerText = tema.nombre;
    lista.appendChild(li);

    let option = document.createElement("option");
    option.value = i;
    option.text = tema.nombre;
    selector.appendChild(option);
  });
}

function generarPreguntas(){
  let cantidad = document.getElementById("numPreguntas").value;
  let tipo = document.getElementById("tipoPregunta").value;

  let contenedor = document.getElementById("preguntas");
  contenedor.innerHTML = "";

  for(let i=1;i<=cantidad;i++){
    let p = document.createElement("p");
    p.innerText = "Pregunta " + i + " sobre el tema.";
    contenedor.appendChild(p);

    if(tipo === "abierta"){
      let input = document.createElement("input");
      contenedor.appendChild(input);
    }else{
      for(let j=1;j<=4;j++){
        let btn = document.createElement("button");
        btn.innerText = "Opción " + j;
        contenedor.appendChild(btn);
      }
    }
  }
}

cargarUsuario();
cargarTemas();

</script>

</body>
</html>
