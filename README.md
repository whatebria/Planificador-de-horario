<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Planificador de horario</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@600&family=Roboto:wght@300;400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    /* VARIABLES CSS para una gestión de colores más fácil */
    :root {
      --primary-color: #2196F3; /* Un azul vibrante */
      --secondary-color: #4CAF50; /* Verde para acciones positivas */
      --danger-color: #f44336; /* Rojo para acciones destructivas/topes */
      --light-gray: #f9f9f9;
      --medium-gray: #e0e0e0;
      --dark-gray: #333;
      --border-color: #ccc;
      --table-border-color: #aaa;
      --content-max-width: 4000px; /* Ancho máximo para el contenido principal */
    }

    /* Variables CSS para el modo oscuro */
    :root {
      --dark-mode-background: #1E1E1E; /* Gris oscuro para el fondo */
      --dark-mode-text: #F8F8F2; /* Blanco hueso para el texto principal */
      --dark-mode-input-background: #333; /* Gris más claro para inputs */
      --dark-mode-input-border: #555;
      --dark-mode-table-header: #333;
      --dark-mode-table-border: #555;
      --dark-mode-card-background: #2C2C2C; /* Gris un poco más claro para contenedores */
      --dark-mode-shadow: rgba(0, 0, 0, 0.5); /* Sombra más intensa */
      --usm-blue: #004AAD; /* Azul característico de la USM */
      --usm-white: #FFFFFF; /* Blanco USM */
    }

    body {
      font-family: 'Roboto', sans-serif; /* Fuente principal */
      background-color: #f5f7fa; /* Fondo suave */
      color: var(--dark-gray);
      padding: 20px; /* Padding general del body para dejar espacio a los lados */
      transition: background-color 0.3s ease, color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    h2 {
      font-family: 'Montserrat', sans-serif; /* Fuente para títulos */
      color: var(--primary-color);
      text-align: center;
      margin-bottom: 30px;
      font-weight: 600;
      transition: color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    /* Contenedores principales */
    .formulario, #lista-materias, table {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px; /* Bordes más redondeados */
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08); /* Sombra sutil */
        margin-bottom: 25px; /* Más espacio entre secciones */
        max-width: var(--content-max-width); /* Limitar el ancho */
        margin-left: auto; /* Centrar horizontalmente */
        margin-right: auto; /* Centrar horizontalmente */
        transition: background-color 0.3s ease, box-shadow 0.3s ease; /* Transición suave para el modo oscuro */
    }

    table {
      border-collapse: collapse;
      width: 100%;
    }
    th, td {
      border: 1px solid var(--table-border-color);
      text-align: center;
      padding: 8px;
      vertical-align: middle;
      height: 50px;
      position: relative;
      overflow: hidden;
      transition: border-color 0.3s ease; /* Transición suave para el modo oscuro */
    }
    th {
      background-color: var(--medium-gray);
      color: var(--dark-gray);
      font-weight: 500;
      transition: background-color 0.3s ease, color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    /* FORMULARIO */
    .formulario label {
      display: block;
      margin-bottom: 5px;
      font-weight: 500;
      color: var(--dark-gray);
      transition: color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    .formulario .input-group {
        margin-bottom: 15px;
    }

    .formulario input, .formulario select {
      width: calc(100% - 18px);
      padding: 10px;
      border: 1px solid var(--border-color);
      border-radius: 5px;
      font-size: 1em;
      margin-top: 5px;
      box-sizing: border-box;
      transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease; /* Transición suave para el modo oscuro */
    }
    .formulario input[type="color"] {
        width: 60px;
        padding: 5px;
    }

    .formulario select[multiple] {
      height: 150px;
    }

    .formulario button {
      padding: 10px 18px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1em;
      font-weight: 500;
      border: none;
      margin-right: 10px;
      transition: background-color 0.3s ease, transform 0.1s ease, box-shadow 0.3s ease, color 0.3s ease;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }

    .formulario button:last-child {
      margin-right: 0;
    }

    .formulario button:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    }

    /* Colores específicos de botones */
    .formulario button:nth-of-type(1) {
        background-color: var(--primary-color);
        color: white;
    }
    .formulario button:nth-of-type(1):hover {
        background-color: #1976D2;
    }
    .formulario button:nth-of-type(2),
    .formulario button:nth-of-type(3) {
        background-color: var(--secondary-color);
        color: white;
    }
    .formulario button:nth-of-type(2):hover,
    .formulario button:nth-of-type(3):hover {
        background-color: #388E3C;
    }
    .formulario button:nth-of-type(4) {
        background-color: #D32F2F;
        color: white;
    }
    .formulario button:nth-of-type(4):hover {
        background-color: #B71C1C;
    }


    /* CELDA MATERIA Y TOPES */
    .celda-materia {
      position: absolute; top: 0; left: 0; width: 100%; height: 100%;
      font-weight: 500;
      display: flex;
      justify-content: center;
      align-items: center;
      box-sizing: border-box;
      padding: 5px;
      word-break: break-word;
      flex-direction: column;
      font-size: 0.9em;
      line-height: 1.2;
      transition: color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    .tope {
      background-color: var(--danger-color) !important;
      color: white;
      font-weight: normal;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 3px;
      font-size: 0.75em;
      line-height: 1.1;
    }

    .tope .titulo-tope {
      display: block;
      font-weight: bold;
      font-size: 1.1em;
      margin-bottom: 2px;
      letter-spacing: 0.5px;
      text-transform: uppercase;
    }

    .tope .materias-conflicto {
        font-size: 0.9em;
        text-align: center;
        line-height: 1.1;
    }

    /* LISTA DE MATERIAS */
    #lista-materias {
        padding: 15px;
    }

    #lista-materias div {
      margin-bottom: 10px;
      padding: 10px;
      border: 1px solid var(--border-color);
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: var(--light-gray);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
      transition: background-color 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease; /* Transición suave */
    }

    #lista-materias .materia-info {
        display: flex;
        align-items: center;
        gap: 8px;
        font-weight: 400;
    }

    #lista-materias .materia-info span { /* Asegura que el texto de la materia en lista también transicione */
      transition: color 0.3s ease;
    }

    #lista-materias .color-indicator {
        width: 18px;
        height: 18px;
        border-radius: 50%;
        border: 1px solid rgba(0,0,0,0.1);
        flex-shrink: 0;
    }

    #lista-materias button {
      padding: 6px 12px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.85em;
      font-weight: 500;
      transition: background-color 0.3s ease, transform 0.1s ease, color 0.3s ease;
      display: inline-flex;
      align-items: center;
      gap: 5px;
    }

    #lista-materias button:first-of-type {
        background-color: var(--primary-color);
        color: white;
        border: none;
    }
    #lista-materias button:first-of-type:hover {
        background-color: #1976D2;
    }
    #lista-materias button:last-of-type {
        background-color: var(--danger-color);
        color: white;
        border: none;
    }
    #lista-materias button:last-of-type:hover {
        background-color: #D32F2F;
    }

    /* FEEDBACK MESSAGE */
    .feedback-message {
      background-color: #e6f7d9;
      color: #388e3c;
      padding: 12px;
      border-radius: 6px;
      margin-top: 15px;
      text-align: center;
      opacity: 0;
      transition: opacity 0.5s ease-in-out, background-color 0.3s ease, color 0.3s ease;
      font-weight: 500;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      max-width: var(--content-max-width);
      margin-left: auto;
      margin-right: auto;
      margin-bottom: 25px;
    }
    .feedback-message.show {
      opacity: 1;
    }
    .feedback-message.error {
      background-color: #fce4ec;
      color: #d32f2f;
    }

    /* >>>>>>> ESTILOS DEL SWITCH DE MODO OSCURO <<<<<<< */
    .theme-switch-wrapper {
      display: flex;
      align-items: center;
      justify-content: flex-end; /* Mover a la derecha */
      margin-bottom: 20px;
      font-size: 0.9em;
      color: var(--dark-gray); /* Color por defecto en modo claro */
      max-width: var(--content-max-width); /* Alinear con el contenido principal */
      margin-left: auto;
      margin-right: auto;
      transition: color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    .theme-switch {
      display: inline-block;
      height: 24px;
      position: relative;
      width: 50px;
      margin-left: 10px;
    }

    .theme-switch input {
      display:none;
    }

    .slider {
      background-color: #ccc;
      bottom: 0;
      cursor: pointer;
      left: 0;
      position: absolute;
      right: 0;
      top: 0;
      transition: .4s;
    }

    .slider:before {
      background-color: #fff;
      bottom: 4px;
      content: "";
      height: 16px;
      left: 4px;
      position: absolute;
      transition: .4s;
      width: 16px;
    }

    input:checked + .slider {
      background-color: var(--primary-color); /* Usar color primario para el switch activado */
    }

    input:focus + .slider {
      box-shadow: 0 0 1px var(--primary-color);
    }

    input:checked + .slider:before {
      transform: translateX(26px);
    }

    /* Rounded sliders */
    .slider.round {
      border-radius: 34px;
    }

    .slider.round:before {
      border-radius: 50%;
    }

    /* >>>>>>> ESTILOS PARA EL MODO OSCURO (CUANDO body TIENE LA CLASE dark-mode) <<<<<<< */
    body.dark-mode {
      background-color: var(--dark-mode-background);
      color: var(--dark-mode-text);
    }

    body.dark-mode h2 {
      color: var(--usm-blue); /* Destacar título con azul USM */
    }

    body.dark-mode .formulario,
    body.dark-mode #lista-materias,
    body.dark-mode table,
    body.dark-mode .feedback-message {
      background-color: var(--dark-mode-card-background);
      color: var(--dark-mode-text);
      box-shadow: 0 4px 10px var(--dark-mode-shadow);
    }

    body.dark-mode th {
      background-color: var(--dark-mode-table-header);
      color: var(--dark-mode-text);
    }

    body.dark-mode td {
      border-color: var(--dark-mode-table-border);
    }

    body.dark-mode .formulario input,
    body.dark-mode .formulario select {
      background-color: var(--dark-mode-input-background);
      color: var(--dark-mode-text);
      border-color: var(--dark-mode-input-border);
    }

    body.dark-mode .formulario label {
      color: var(--dark-mode-text);
    }

    body.dark-mode #lista-materias div {
      background-color: var(--dark-mode-input-background);
      border-color: var(--dark-mode-input-border);
    }

    body.dark-mode #lista-materias .materia-info span {
      color: var(--dark-mode-text);
    }

    body.dark-mode .feedback-message {
      background-color: #2e7d32; /* Verde más oscuro para éxito */
      color: var(--dark-mode-text);
    }
    body.dark-mode .feedback-message.error {
      background-color: #b71c1c; /* Rojo más oscuro para error */
      color: var(--dark-mode-text);
    }

    body.dark-mode .celda-materia {
      color: var(--dark-mode-text); /* Asegurar color de texto en las celdas */
    }
    body.dark-mode .celda-materia.tope { /* Específico para tope en dark mode */
        color: var(--usm-white); /* Texto del tope en blanco USM */
    }

    /* Botones en modo oscuro - ajuste de color de fondo y texto */
    body.dark-mode .formulario button {
      background-color: #444; /* Fondo gris oscuro para botones generales */
      color: var(--dark-mode-text);
      box-shadow: 0 2px 5px var(--dark-mode-shadow);
    }
    body.dark-mode .formulario button:hover {
      background-color: #555;
      box-shadow: 0 4px 8px var(--dark-mode-shadow);
    }

    body.dark-mode .formulario button:nth-of-type(1) { /* Agregar / Actualizar - Destacar con azul USM */
        background-color: var(--usm-blue);
        color: var(--usm-white);
    }
    body.dark-mode .formulario button:nth-of-type(1):hover {
        background-color: #003380; /* Azul más oscuro al pasar el ratón */
    }

    body.dark-mode #lista-materias button {
      background-color: #444; /* Fondo gris oscuro para botones de lista */
      color: var(--dark-mode-text);
    }

    body.dark-mode #lista-materias button:first-of-type { /* Editar - Destacar con azul USM */
        background-color: var(--usm-blue);
        color: var(--usm-white);
    }
    body.dark-mode #lista-materias button:first-of-type:hover {
        background-color: #003380;
    }
    body.dark-mode #lista-materias button:last-of-type { /* Eliminar - Mantener rojo */
        background-color: var(--danger-color);
        color: var(--dark-mode-text);
    }
    body.dark-mode #lista-materias button:last-of-type:hover {
        background-color: #B71C1C;
    }

    body.dark-mode .theme-switch-wrapper {
      color: var(--dark-mode-text);
    }


    /* Ajustes responsivos básicos para pantallas más pequeñas */
    @media (max-width: 768px) {
        :root {
            --content-max-width: 100%; /* En pantallas pequeñas, ocupa todo el ancho */
        }
        body {
            padding: 15px; /* Menos padding en los bordes */
        }
        .formulario input, .formulario select {
            width: 100%; /* Asegura que ocupen todo el ancho disponible */
        }
        .formulario button {
            width: 100%; /* Botones apilados en móvil */
            margin-right: 0;
            margin-bottom: 10px;
        }
        #lista-materias div {
            flex-direction: column; /* Apila info y botones en lista */
            align-items: flex-start;
        }
        #lista-materias div > div { /* Contenedor de botones en lista */
            width: 100%;
            display: flex;
            justify-content: flex-end; /* Alinea los botones a la derecha */
            margin-top: 10px;
            gap: 10px; /* Espacio entre botones */
        }
        .theme-switch-wrapper {
          justify-content: center; /* Centrar el switch en móvil */
          margin-bottom: 25px;
        }
    }
  </style>
</head>
<body>

<h2>Generador de Horarios USM</h2>

<div class="theme-switch-wrapper">
  <label class="theme-switch" for="checkbox">
    <input type="checkbox" id="checkbox" />
    <div class="slider round"></div>
  </label>
  <em>Modo Oscuro</em>
</div>

<div class="formulario">
  <div class="input-group">
    <label for="materia">Nombre de la materia:</label>
    <input type="text" id="materia" placeholder="Ej: Cálculo I">
  </div>

  <div class="input-group">
    <label for="dia">Día:</label>
    <select id="dia">
      <option value="Lunes">Lunes</option>
      <option value="Martes">Martes</option>
      <option value="Miércoles">Miércoles</option>
      <option value="Jueves">Jueves</option>
      <option value="Viernes">Viernes</option>
    </select>
  </div>

  <div class="input-group">
    <label for="bloques">Bloques (Mantén Ctrl/Cmd para seleccionar múltiples):</label>
    <select multiple id="bloques" size="10" style="width: 100%;"></select>
  </div>

  <div class="input-group">
    <label for="paralelo">Paralelo:</label>
    <input type="text" id="paralelo" placeholder="Ej: 300">
  </div>

  <div class="input-group">
    <label for="color">Color de la materia:</label>
    <input type="color" id="color" value="#90ee90">
  </div>
  <br>
  <button onclick="agregarMateria()"><i class="fas fa-plus-circle"></i> Agregar / Actualizar</button>
  <button onclick="guardarHorario()"><i class="fas fa-save"></i> Guardar</button>
  <button onclick="cargarHorario()"><i class="fas fa-folder-open"></i> Cargar</button>
  <button onclick="exportarPDF()"><i class="fas fa-file-pdf"></i> Exportar a PDF</button>
</div>

<div id="feedback-message" class="feedback-message" aria-live="polite"></div>

<table>
  <thead>
    <tr>
      <th>Bloque</th><th>Hora</th>
      <th>Lunes</th><th>Martes</th><th>Miércoles</th><th>Jueves</th><th>Viernes</th>
    </tr>
  </thead>
  <tbody id="tabla"></tbody>
</table>

<h3>Materias agregadas</h3>
<div id="lista-materias"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<script>
const bloquesUSM = [
  ["1", "08:15 – 08:50"], ["2", "08:50 – 09:25"], ["3", "09:35 – 10:10"],
  ["4", "10:10 – 10:45"], ["5", "10:55 – 11:30"], ["6", "11:30 – 12:05"],
  ["7", "12:15 – 12:50"], ["8", "12:50 – 13:25"], ["9", "14:30 – 15:05"],
  ["10", "15:05 – 15:40"], ["11", "15:50 – 16:25"], ["12", "16:25 – 17:00"],
  ["13", "17:10 – 17:45"], ["14", "17:45 – 18:20"], ["15", "18:30 – 19:05"],
  ["16", "19:05 – 19:40"], ["17", "19:50 – 20:25"], ["18", "20:25 – 21:00"]
];

const dias = ["Lunes", "Martes", "Miércoles", "Jueves", "Viernes"];
const materias = [];
const tabla = document.getElementById("tabla");
const selectBloques = document.getElementById("bloques");

const inputMateria = document.getElementById("materia");
const inputParalelo = document.getElementById("paralelo");
const inputColor = document.getElementById("color");
const selectDia = document.getElementById("dia");
const listaMateriasDiv = document.getElementById("lista-materias");
const feedbackMessageDiv = document.getElementById("feedback-message");

// Función para determinar el color del texto (negro o blanco) según el fondo
function getContrastTextColor(hexColor) {
    const r = parseInt(hexColor.slice(1, 3), 16);
    const g = parseInt(hexColor.slice(3, 5), 16);
    const b = parseInt(hexColor.slice(5, 7), 16);
    // Fórmula de luminosidad para determinar el contraste
    const brightness = (r * 299 + g * 587 + b * 114) / 1000;
    
    // Si el modo oscuro está activo, el contraste debe ser con el blanco USM o blanco general.
    // Si el color de fondo es claro, el texto debería ser oscuro (var(--dark-gray))
    // Si el color de fondo es oscuro, el texto debería ser claro (white o var(--usm-white))
    if (document.body.classList.contains('dark-mode')) {
        // En modo oscuro, queremos que el texto sea claro (blanco USM) si el color de la materia es oscuro,
        // o un gris oscuro si la materia es muy clara para evitar el contraste con el fondo oscuro general.
        return (brightness > 180) ? 'black' : 'white'; // En modo oscuro, siempre texto blanco para las materias
    } else {
        // En modo claro, queremos texto oscuro si la materia es clara, y blanco si la materia es oscura.
        return (brightness > 180) ? '#333' : 'white';
    }
}


// Carga las opciones de bloques al iniciar
bloquesUSM.forEach(([numero, hora]) => {
  const option = document.createElement("option");
  option.value = numero;
  option.textContent = `Bloque ${numero} (${hora})`;
  selectBloques.appendChild(option);
});


function construirTabla() {
  tabla.innerHTML = "";
  for (let [numero, hora] of bloquesUSM) {
    const fila = document.createElement("tr");
    fila.innerHTML = `<td>${numero}</td><td>${hora}</td>`;
    for (let dia of dias) {
      const celda = document.createElement("td");
      celda.id = `B${numero}-${dia}`;
      fila.appendChild(celda);
    }
    tabla.appendChild(fila);
  }
}

function renderizarMaterias() {
  construirTabla();

  const ocupacion = {};
  for (const mat of materias) {
    for (const bloque of mat.bloques) {
      const clave = `${bloque}-${mat.dia}`;
      if (!ocupacion[clave]) {
        ocupacion[clave] = [];
      }
      ocupacion[clave].push(mat);
    }
  }

  for (let i = 0; i < bloquesUSM.length; i++) {
    const [numeroBloque] = bloquesUSM[i];
    for (let j = 0; j < dias.length; j++) {
      const dia = dias[j];
      const clave = `${numeroBloque}-${dia}`;
      const celda = document.getElementById(`B${numeroBloque}-${dia}`);

      if (!celda) {
        console.warn(`Celda con ID ${clave} no encontrada.`);
        continue;
      }

      celda.innerHTML = "";
      celda.style.display = "";
      celda.rowSpan = 1;
      celda.classList.remove("tope");
      celda.style.backgroundColor = "";
      celda.style.color = "";

      const materiasEnEsteBloque = ocupacion[clave] || [];

      if (materiasEnEsteBloque.length > 1) {
        const contenidoTopes = materiasEnEsteBloque.map(m => `${m.nombre} (P${m.paralelo})`).join("<br>");
        celda.innerHTML = `
          <div class="celda-materia tope">
            <span class="titulo-tope">TOPE DE HORARIO</span>
            <span class="materias-conflicto">${contenidoTopes}</span>
          </div>
        `;
        celda.classList.add("tope");
      } else if (materiasEnEsteBloque.length === 1) {
        const mat = materiasEnEsteBloque[0];
        const textColor = getContrastTextColor(mat.color);
        celda.innerHTML = `
          <div class="celda-materia" style="background-color: ${mat.color}; color: ${textColor};">
            ${mat.nombre}<br>Paralelo ${mat.paralelo}
          </div>
        `;
      }
    }
  }

  listarMaterias();
}

function mostrarFeedback(message, type = 'success') {
    feedbackMessageDiv.textContent = "";
    feedbackMessageDiv.classList.remove('success', 'error');

    const icon = document.createElement("i");
    const textSpan = document.createElement("span");
    textSpan.textContent = message;

    if (type === 'error') {
        feedbackMessageDiv.classList.add('error');
        icon.classList.add('fas', 'fa-times-circle');
    } else {
        feedbackMessageDiv.classList.add('success');
        icon.classList.add('fas', 'fa-check-circle');
    }

    feedbackMessageDiv.appendChild(icon);
    feedbackMessageDiv.appendChild(textSpan);

    feedbackMessageDiv.classList.add('show');
    setTimeout(() => {
        feedbackMessageDiv.classList.remove('show');
    }, 3000);
}

function agregarMateria() {
  const nombre = inputMateria.value.trim();
  const paralelo = inputParalelo.value.trim();
  const color = inputColor.value;
  const dia = selectDia.value;
  const bloques = Array.from(selectBloques.selectedOptions).map(opt => opt.value);

  if (!nombre || !paralelo || bloques.length === 0) {
    mostrarFeedback("Completa todos los campos: nombre, paralelo y selecciona al menos un bloque.", 'error');
    return;
  }

  if (isNaN(paralelo)) {
      mostrarFeedback("El paralelo debe ser un valor numérico.", 'error');
      return;
  }

  const existenteIndex = materias.findIndex(m => m.nombre === nombre && m.paralelo === paralelo && m.dia === dia);
  if (existenteIndex !== -1) {
    materias[existenteIndex] = { nombre, paralelo, color, dia, bloques };
    mostrarFeedback("Materia actualizada exitosamente.");
  } else {
    materias.push({ nombre, paralelo, color, dia, bloques });
    mostrarFeedback("Materia agregada exitosamente.");
  }

  inputMateria.value = "";
  inputParalelo.value = "";
  selectBloques.selectedIndex = -1;
  inputColor.value = "#90ee90";

  renderizarMaterias();
}

function listarMaterias() {
  listaMateriasDiv.innerHTML = "";
  materias.forEach((mat, i) => {
    const div = document.createElement("div");
    div.innerHTML = `
      <div class="materia-info">
        <span class="color-indicator" style="background-color: ${mat.color};"></span>
        <span>
          <strong>${mat.nombre}</strong> (P${mat.paralelo}) - ${mat.dia}, Bloques: ${mat.bloques.join(", ")}
        </span>
      </div>
      <div>
        <button onclick="editarMateria(${i})"><i class="fas fa-edit"></i> Editar</button>
        <button onclick="eliminarMateria(${i})"><i class="fas fa-trash-alt"></i> Eliminar</button>
      </div>
    `;
    listaMateriasDiv.appendChild(div);
  });
}

function editarMateria(index) {
  const mat = materias[index];
  inputMateria.value = mat.nombre;
  inputParalelo.value = mat.paralelo;
  inputColor.value = mat.color;
  selectDia.value = mat.dia;

  Array.from(selectBloques.options).forEach(opt => opt.selected = false);

  for (const opt of selectBloques.options) {
    opt.selected = mat.bloques.includes(opt.value);
  }
}

function eliminarMateria(index) {
  if (confirm("¿Estás seguro de que quieres eliminar esta materia?")) {
    materias.splice(index, 1);
    renderizarMaterias();
    mostrarFeedback("Materia eliminada correctamente.");
  }
}

function guardarHorario() {
  localStorage.setItem("horarioUSM", JSON.stringify(materias));
  mostrarFeedback("Horario guardado en el navegador.");
}

function cargarHorario() {
  const datos = JSON.parse(localStorage.getItem("horarioUSM") || "[]");
  materias.length = 0;
  materias.push(...datos);
  renderizarMaterias();
  mostrarFeedback("Horario cargado desde el navegador.");
}

function exportarPDF() {
  mostrarFeedback("Generando PDF...");
  const opt = {
    margin:       10,
    filename:     'horario_usm.pdf',
    image:        { type: 'jpeg', quality: 0.98 },
    html2canvas:  { scale: 2, logging: true, dpi: 192, letterRendering: true },
    jsPDF:        { unit: 'mm', format: 'a4', orientation: 'landscape' }
  };
  
  const exportContainer = document.createElement('div');
  exportContainer.style.width = '100%';
  exportContainer.style.padding = '20px';

  const h2ForPdf = document.querySelector('h2').cloneNode(true);
  const tableForPdf = document.querySelector('table').cloneNode(true);

  const pdfCells = tableForPdf.querySelectorAll('td');

  pdfCells.forEach(cell => {
      const celdaMateriaDiv = cell.querySelector('.celda-materia');
      if (celdaMateriaDiv) {
          cell.innerHTML = celdaMateriaDiv.innerHTML;
          cell.style.backgroundColor = celdaMateriaDiv.style.backgroundColor;
          cell.style.color = celdaMateriaDiv.style.color;
          cell.style.position = 'static'; // Important for PDF
          cell.style.display = '';
      }
      if (cell.style.display === 'none') {
          cell.style.display = '';
          cell.innerHTML = '';
      }
  });


  exportContainer.appendChild(h2ForPdf);
  exportContainer.appendChild(tableForPdf);

  html2pdf().set(opt).from(exportContainer).save();
}

// >>>>> Lógica del Modo Oscuro <<<<<
const checkbox = document.getElementById("checkbox");
const body = document.body;

// Comprobar si hay una preferencia guardada al cargar la página
const isDarkMode = localStorage.getItem('darkMode') === 'true';
if (isDarkMode) {
  body.classList.add('dark-mode');
  checkbox.checked = true;
}

// Escuchar el cambio en el checkbox para alternar el modo oscuro
checkbox.addEventListener('change', () => {
  body.classList.toggle('dark-mode');
  localStorage.setItem('darkMode', checkbox.checked); // Guardar la preferencia
  renderizarMaterias(); // Volver a renderizar materias para recalcular colores de texto si es necesario
});


// Inicialización:
construirTabla();
cargarHorario();
</script>
</body>
</html>
