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
      
      --content-max-width: 85%; 
      --form-input-width: 400px;
      --main-padding: 20px;
    }

    /* Variables CSS para el modo oscuro */
    :root {
      --dark-mode-background: #121212; 
      --dark-mode-text: #E0E0E0; 
      --dark-mode-input-background: #282828; 
      --dark-mode-input-border: #666; 
      --dark-mode-table-header: #222; 
      --dark-mode-table-border: #777; 
      --dark-mode-card-background: #1E1E1E; 
      --dark-mode-shadow: rgba(0, 0, 0, 0.7); 
      --usm-blue: #007BFF; 
      --usm-white: #FFFFFF; 
    }

    body {
      font-family: 'Roboto', sans-serif;
      background-color: #f5f7fa;
      color: var(--dark-gray);
      padding: var(--main-padding);
      transition: background-color 0.3s ease, color 0.3s ease;
    }

    h2, h3 {
      font-family: 'Montserrat', sans-serif;
      color: var(--primary-color);
      text-align: center;
      margin-bottom: 30px;
      font-weight: 600;
      transition: color 0.3s ease;
    }
    h3 {
      margin-top: 30px;
    }

    /* Contenedores principales */
    .formulario, #lista-materias, table {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
        margin-bottom: 25px;
        width: var(--content-max-width);
        margin-left: auto;
        margin-right: auto;
        transition: background-color 0.3s ease, box-shadow 0.3s ease;
    }
    
    .formulario {
        display: flex;
        flex-direction: column;
        align-items: center;
        max-width: var(--content-max-width); 
    }

    table {
      border-collapse: collapse;
      table-layout: fixed;
    }
    th, td {
      border: 1px solid var(--table-border-color);
      text-align: center;
      padding: 8px;
      vertical-align: middle;
      height: 50px;
      position: relative;
      overflow: hidden;
      transition: border-color 0.3s ease;
    }
    th {
      background-color: var(--medium-gray);
      color: var(--dark-gray);
      font-weight: 500;
      transition: background-color 0.3s ease, color 0.3s ease;
    }
    /* Anchos específicos para las columnas de la tabla */
    table th:first-child, table td:first-child { width: 5%; }
    table th:nth-child(2), table td:nth-child(2) { width: 10%; }
    table th:nth-child(n+3), table td:nth-child(n+3) { width: 17%; }


    /* FORMULARIO */
    .formulario label {
      display: block;
      margin-bottom: 5px;
      font-weight: 500;
      color: var(--dark-gray);
      transition: color 0.3s ease;
    }

    .formulario .input-group {
        margin-bottom: 15px;
        width: 100%;
        text-align: left;
    }

    .formulario input, .formulario select {
      width: 100%;
      padding: 10px;
      border: 1px solid var(--border-color);
      border-radius: 5px;
      font-size: 1em;
      margin-top: 5px;
      box-sizing: border-box;
      transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease;
    }
    .formulario input[type="color"] {
        width: 60px;
        padding: 5px;
    }
    
    .formulario select[multiple] {
        height: auto;
        min-height: 100px;
    }


    .formulario .form-buttons {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 10px;
        width: 100%;
        max-width: 100%; 
        margin-top: 15px;
    }

    .formulario button {
      padding: 10px 18px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1em;
      font-weight: 500;
      border: none;
      transition: background-color 0.3s ease, transform 0.1s ease, box-shadow 0.3s ease, color 0.3s ease;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
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
      padding: 8px;
      word-break: break-word;
      overflow-wrap: break-word;
      flex-direction: column;
      font-size: 0.85em;
      line-height: 1.2;
      transition: color 0.3s ease, background-color 0.3s ease; /* Asegurar transición de fondo */
      text-align: center;
    }

    /* Estilos específicos para celdas de "tope" */
    .celda-materia.tope { 
      background-color: var(--danger-color) !important;
      color: white;
    }

    .tope .titulo-tope {
      display: block;
      font-weight: bold;
      font-size: 1.1em;
      margin-bottom: 2px;
      letter-spacing: 0.5px;
      text-transform: uppercase;
      white-space: normal;
      overflow: hidden;
      text-overflow: ellipsis;
      text-align: center;
    }

    .tope .materias-conflicto {
        font-size: 0.9em;
        text-align: center;
        line-height: 1.1;
        white-space: normal;
        word-wrap: break-word;
        overflow-wrap: break-word;
    }

    /* LISTA DE MATERIAS */
    #lista-materias {
        padding: 15px;
        margin-top: 25px;
    }

    #lista-materias .materia-item {
      margin-bottom: 10px;
      padding: 10px;
      border: 1px solid var(--border-color);
      border-radius: 5px;
      display: flex;
      flex-direction: column;
      background-color: var(--light-gray);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
      transition: background-color 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
    }

    #lista-materias .materia-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
    }

    #lista-materias .materia-info {
        display: flex;
        align-items: center;
        gap: 8px;
        font-weight: 400;
        flex-grow: 1;
    }

    #lista-materias .materia-info.oculta span {
        text-decoration: line-through;
        opacity: 0.7;
    }


    #lista-materias .materia-info span {
      transition: color 0.3s ease;
    }

    #lista-materias .color-indicator {
        width: 18px;
        height: 18px;
        border-radius: 50%;
        border: 1px solid rgba(0,0,0,0.1);
        flex-shrink: 0;
    }

    #lista-materias .materia-actions {
        display: flex;
        gap: 8px;
        flex-shrink: 0;
    }

    #lista-materias .materia-horarios {
        font-size: 0.9em;
        padding-left: 26px;
        color: var(--dark-gray);
    }
    #lista-materias .materia-horarios span {
        display: block;
        margin-bottom: 3px;
    }
    #lista-materias .materia-horarios strong {
        color: var(--primary-color);
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

    #lista-materias button.btn-edit {
        background-color: var(--primary-color);
        color: white;
        border: none;
    }
    #lista-materias button.btn-edit:hover {
        background-color: #1976D2;
    }
    #lista-materias button.btn-toggle {
        background-color: #607D8B;
        color: white;
        border: none;
    }
    #lista-materias button.btn-toggle:hover {
        background-color: #455A64;
    }
    #lista-materias button.btn-delete {
        background-color: var(--danger-color);
        color: white;
        border: none;
    }
    #lista-materias button.btn-delete:hover {
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

    /* ESTILOS DEL SWITCH DE MODO OSCURO */
    .theme-switch-wrapper {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      margin-bottom: 20px;
      font-size: 0.9em;
      color: var(--dark-gray);
      max-width: var(--content-max-width); 
      margin-left: auto;
      margin-right: auto;
      transition: color 0.3s ease;
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
      background-color: var(--primary-color);
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

    /* ESTILOS PARA EL MODO OSCURO (CUANDO body TIENE LA CLASE dark-mode) */
    body.dark-mode {
      background-color: var(--dark-mode-background);
      color: var(--dark-mode-text);
    }

    body.dark-mode h2, body.dark-mode h3 {
      color: var(--usm-blue);
    }

    body.dark-mode .formulario,
    body.dark-mode #lista-materias,
    body.dark-mode .feedback-message {
      background-color: var(--dark-mode-card-background);
      color: var(--dark-mode-text);
      box-shadow: 0 4px 10px var(--dark-mode-shadow);
    }

    body.dark-mode table {
      background-color: var(--dark-mode-card-background);
      box-shadow: 0 4px 10px var(--dark-mode-shadow);
    }
    
    body.dark-mode th {
      background-color: var(--dark-mode-table-header);
      color: var(--dark-mode-text);
      border-color: var(--dark-mode-table-border);
    }

    /* INICIO DE AJUSTES PARA CELDAS Y TEXTOS EN MODO OSCURO */
    body.dark-mode td {
      background-color: var(--dark-mode-card-background); /* Fondo para celdas vacías */
      color: var(--dark-mode-text); /* Color del texto para bloques, horas y texto general de la celda */
      border-color: var(--dark-mode-table-border);
    }

    body.dark-mode .celda-materia {
        /* El color de texto de la materia se calcula dinámicamente con getContrastTextColor. */
        /* Este estilo asegura que el texto tenga un buen contraste si el JS falla o en casos específicos. */
        color: var(--dark-mode-text); 
    }

    body.dark-mode .celda-materia.tope {
        background-color: var(--danger-color) !important; /* Mantener el rojo para topes */
        color: var(--usm-white); /* Asegurar texto blanco para topes, para que contraste con el rojo */
    }

    body.dark-mode #lista-materias .materia-horarios {
        color: var(--dark-mode-text); /* Asegura que el texto de los horarios en la lista sea oscuro */
    }
    body.dark-mode #lista-materias .materia-horarios strong {
        color: var(--usm-blue); /* Los días en fuerte seguirán el color USM Blue */
    }
    /* FIN DE AJUSTES PARA CELDAS Y TEXTOS EN MODO OSCURO */

    body.dark-mode .formulario input,
    body.dark-mode .formulario select {
      background-color: var(--dark-mode-input-background);
      color: var(--dark-mode-text);
      border-color: var(--dark-mode-input-border);
    }

    body.dark-mode .formulario label {
      color: var(--dark-mode-text);
    }

    body.dark-mode #lista-materias .materia-item {
      background-color: var(--dark-mode-input-background);
      border-color: var(--dark-mode-input-border);
    }
    body.dark-mode #lista-materias .materia-horarios {
        color: var(--dark-mode-text);
    }
    body.dark-mode #lista-materias .materia-horarios strong {
        color: var(--usm-blue);
    }

    body.dark-mode #lista-materias .materia-info span {
      color: var(--dark-mode-text);
    }

    body.dark-mode .feedback-message {
      background-color: #2e7d32;
      color: var(--dark-mode-text);
    }
    body.dark-mode .feedback-message.error {
      background-color: #b71c1c;
      color: var(--dark-mode-text);
    }

    body.dark-mode .theme-switch-wrapper {
      color: var(--dark-mode-text);
    }

    /* Botones en modo oscuro - ajuste de color de fondo y texto */
    body.dark-mode .formulario button {
      background-color: #444;
      color: var(--dark-mode-text);
      box-shadow: 0 2px 5px var(--dark-mode-shadow);
    }
    body.dark-mode .formulario button:hover {
      background-color: #555;
      box-shadow: 0 4px 8px var(--dark-mode-shadow);
    }

    body.dark-mode .formulario button:nth-of-type(1) {
        background-color: var(--usm-blue);
        color: var(--usm-white);
    }
    body.dark-mode .formulario button:nth-of-type(1):hover {
        background-color: #003380;
    }

    body.dark-mode #lista-materias button {
      background-color: #444;
      color: var(--dark-mode-text);
    }

    body.dark-mode #lista-materias button.btn-edit {
        background-color: var(--usm-blue);
        color: var(--usm-white);
    }
    body.dark-mode #lista-materias button.btn-edit:hover {
        background-color: #003380;
    }
    body.dark-mode #lista-materias button.btn-toggle {
        background-color: #555;
        color: var(--dark-mode-text);
    }
    body.dark-mode #lista-materias button.btn-toggle:hover {
        background-color: #666;
    }
    body.dark-mode #lista-materias button.btn-delete {
        background-color: var(--danger-color);
        color: var(--dark-mode-text);
    }
    body.dark-mode #lista-materias button.btn-delete:hover {
        background-color: #B71C1C;
    }


    /* Ajustes responsivos básicos para pantallas más pequeñas */
    @media (max-width: 768px) {
        :root {
            --content-max-width: 100%;
            --main-padding: 15px;
        }
        body {
            padding: var(--main-padding);
        }
        .formulario input, .formulario select {
            width: 100%;
        }
        .formulario button {
            width: 100%;
            margin-right: 0;
            margin-bottom: 10px;
        }
        #lista-materias .materia-item {
            flex-direction: column;
            align-items: flex-start;
        }
        #lista-materias .materia-header {
            width: 100%;
            flex-direction: column;
            align-items: flex-start;
            margin-bottom: 5px;
        }
        #lista-materias .materia-actions {
            width: 100%;
            display: flex;
            justify-content: flex-end;
            margin-top: 10px;
            gap: 10px;
        }
        .theme-switch-wrapper {
          justify-content: center;
          margin-bottom: 25px;
        }

        .formulario .input-group {
            max-width: 100%;
        }
        table th, table td {
            font-size: 0.8em;
            padding: 5px;
            height: 40px;
        }
        table th:first-child, table td:first-child { width: 8%; }
        table th:nth-child(2), table td:nth-child(2) { width: 15%; }
        table th:nth-child(n+3), table td:nth-child(n+3) { width: 15.4%; }
    }
  </style>
</head>
<body>

<div class="theme-switch-wrapper">
  <label class="theme-switch" for="checkbox">
    <input type="checkbox" id="checkbox" />
    <div class="slider round"></div>
  </label>
  <em>Modo Oscuro</em>
</div>

<div class="formulario" id="formulario-materia">
  <div class="input-group">
    <label for="materia">Nombre de la materia:</label>
    <input type="text" id="materia" placeholder="Ej: Cálculo I">
  </div>

  <div class="input-group">
    <label for="paralelo">Paralelo:</label>
    <input type="text" id="paralelo" placeholder="Ej: 300">
  </div>

  <div class="input-group">
    <label for="dia-seleccion">Día del horario:</label>
    <select id="dia-seleccion"></select>
  </div>

  <div class="input-group" id="bloques-fijos-container">
    <label for="bloques-seleccion">Bloques del horario:</label>
    <select multiple id="bloques-seleccion"></select>
  </div>

  <div class="input-group">
    <label for="color">Color de la materia:</label>
    <input type="color" id="color" value="#90ee90">
  </div>

  <br>
  <div class="form-buttons">
    <button onclick="agregarActualizarMateriaYHorario()"><i class="fas fa-plus-circle"></i> Agregar/Actualizar Materia y Horario</button>
    <button onclick="guardarHorario()"><i class="fas fa-save"></i> Guardar</button>
    <button onclick="cargarHorario()"><i class="fas fa-folder-open"></i> Cargar</button>
    <button onclick="exportarPDF()" id="export-pdf-btn"><i class="fas fa-file-pdf"></i> Exportar a PDF</button>
    <button onclick="clearLocalStorageData()" style="background-color: orange; color: white;"><i class="fas fa-eraser"></i> Limpiar Datos Guardados</button>
  </div>
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

<script defer>
// Definiciones de constantes globales
const bloquesUSM = [
  ["1", "08:15 – 08:50"], ["2", "08:50 – 09:25"], ["3", "09:35 – 10:10"],
  ["4", "10:10 – 10:45"], ["5", "10:55 – 11:30"], ["6", "11:30 – 12:05"],
  ["7", "12:15 – 12:50"], ["8", "12:50 – 13:25"], ["9", "14:30 – 15:05"],
  ["10", "15:05 – 15:40"], ["11", "15:50 – 16:25"], ["12", "16:25 – 17:00"],
  ["13", "17:10 – 17:45"], ["14", "17:45 – 18:20"], ["15", "18:30 – 19:05"],
  ["16", "19:05 – 19:40"], ["17", "19:50 – 20:25"], ["18", "20:25 – 21:00"]
];

const dias = ["Lunes", "Martes", "Miércoles", "Jueves", "Viernes"];
const materias = []; // Array principal que almacena las materias

// Objeto para almacenar referencias a elementos DOM, inicializado en DOMContentLoaded
let DOM = {}; 

// Función para obtener elementos DOM de forma segura
function getDOMElements() {
    const elements = {
        tabla: document.getElementById("tabla"),
        inputMateria: document.getElementById("materia"),
        inputParalelo: document.getElementById("paralelo"),
        inputColor: document.getElementById("color"),
        selectDiaSeleccion: document.getElementById("dia-seleccion"),
        selectBloquesSeleccion: document.getElementById("bloques-seleccion"),
        listaMateriasDiv: document.getElementById("lista-materias"),
        feedbackMessageDiv: document.getElementById("feedback-message"),
        formularioMateria: document.getElementById("formulario-materia"),
        checkbox: document.getElementById("checkbox"),
        exportPdfBtn: document.getElementById("export-pdf-btn") // Nuevo
    };

    // Esto nos dará un mensaje si falta algo, pero permitirá que el script siga
    for (const key in elements) {
        if (!elements[key]) {
            console.error(`ERROR DOM: Elemento con ID "${key}" no encontrado.`);
        }
    }
    return elements;
}

// Función para determinar el color del texto (negro o blanco) según el fondo
function getContrastTextColor(hexColor) {
    if (!hexColor || hexColor.length !== 7 || hexColor[0] !== '#') {
        console.warn("getContrastTextColor: Color HEX inválido. Usando color por defecto.");
        return '#333'; 
    }
    const r = parseInt(hexColor.slice(1, 3), 16);
    const g = parseInt(hexColor.slice(3, 5), 16);
    const b = parseInt(hexColor.slice(5, 7), 16);
    const luminance = (0.2126 * r + 0.7152 * g + 0.0722 * b) / 255;
    
    const threshold = 0.5; 
    return luminance > threshold ? '#333' : 'white';
}

// Carga las opciones de días y bloques al iniciar
function loadFormOptions() {
  if (DOM.selectDiaSeleccion) {
      DOM.selectDiaSeleccion.innerHTML = "";
      dias.forEach(dia => {
        const option = document.createElement("option");
        option.value = dia;
        option.textContent = dia;
        DOM.selectDiaSeleccion.appendChild(option);
      });
  } else {
      console.warn("loadFormOptions: selectDiaSeleccion no encontrado.");
  }

  if (DOM.selectBloquesSeleccion) {
      DOM.selectBloquesSeleccion.innerHTML = "";
      bloquesUSM.forEach(([numero, hora]) => {
          const option = document.createElement("option");
          option.value = numero;
          option.textContent = `Bloque ${numero} (${hora})`;
          DOM.selectBloquesSeleccion.appendChild(option);
      });
  } else {
      console.warn("loadFormOptions: selectBloquesSeleccion no encontrado.");
  }
}

function construirTabla() {
  if (!DOM.tabla) {
      console.error("construirTabla: Elemento 'tabla' no encontrado. No se puede construir.");
      return;
  }
  DOM.tabla.innerHTML = ""; 
  for (let [numero, hora] of bloquesUSM) {
    const fila = document.createElement("tr");
    fila.innerHTML = `<td>${numero}</td><td>${hora}</td>`;
    for (let dia of dias) {
      const celda = document.createElement("td");
      celda.id = `B${numero}-${dia}`;
      fila.appendChild(celda);
    }
    DOM.tabla.appendChild(fila);
  }
}

function renderizarMaterias() {
  construirTabla(); 

  const ocupacion = {}; 
  
  for (const mat of materias) {
    if (!mat.oculto) {
      const horariosArray = Array.isArray(mat.horarios) ? mat.horarios : (mat.horarios ? [mat.horarios] : []);
      
      for (const horario of horariosArray) {
        if (horario && horario.dia && Array.isArray(horario.bloques)) {
            for (const bloque of horario.bloques) {
              const clave = `${bloque}-${horario.dia}`;
              if (!ocupacion[clave]) {
                ocupacion[clave] = [];
              }
              ocupacion[clave].push(mat); 
            }
        }
      }
    }
  }

  for (let i = 0; i < bloquesUSM.length; i++) {
    const [numeroBloque] = bloquesUSM[i];
    for (let j = 0; j < dias.length; j++) {
      const dia = dias[j];
      const clave = `${numeroBloque}-${dia}`;
      const celda = document.getElementById(`B${numeroBloque}-${dia}`); 

      if (!celda) {
        console.warn(`renderizarMaterias: Celda con ID ${clave} no encontrada.`);
        continue;
      }

      celda.innerHTML = "";
      celda.style.display = "";
      celda.rowSpan = 1;
      celda.style.backgroundColor = ""; 
      celda.style.color = ""; 

      const materiasEnEsteBloque = ocupacion[clave] || [];

      if (materiasEnEsteBloque.length > 1) {
        const contenidoTopes = [...new Set(materiasEnEsteBloque.map(m => `${m.nombre} (P${m.paralelo})`))].join("<br>");
        celda.innerHTML = `
          <div class="celda-materia tope">
            <span class="titulo-tope">TOPE DE HORARIO</span>
            <span class="materias-conflicto">${contenidoTopes}</span>
          </div>
        `;
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
    if (!DOM.feedbackMessageDiv) {
        // Si el feedback div no está, solo loguear el mensaje
        console.warn(`Feedback no mostrado (div no encontrado): ${message}`);
        return;
    }
    DOM.feedbackMessageDiv.textContent = "";
    DOM.feedbackMessageDiv.classList.remove('success', 'error');

    const icon = document.createElement("i");
    const textSpan = document.createElement("span");
    textSpan.textContent = message;

    if (type === 'error') {
        DOM.feedbackMessageDiv.classList.add('error');
        icon.classList.add('fas', 'fa-times-circle');
    } else if (type === 'info') {
        DOM.feedbackMessageDiv.classList.add('info');
        icon.classList.add('fas', 'fa-info-circle');
    } else { 
        DOM.feedbackMessageDiv.classList.add('success');
        icon.classList.add('fas', 'fa-check-circle');
    }

    DOM.feedbackMessageDiv.appendChild(icon);
    DOM.feedbackMessageDiv.appendChild(textSpan);

    DOM.feedbackMessageDiv.classList.add('show');
    setTimeout(() => {
        DOM.feedbackMessageDiv.classList.remove('show');
    }, 3000);
}

function agregarActualizarMateriaYHorario() {
  if (!DOM.inputMateria || !DOM.inputParalelo || !DOM.inputColor || !DOM.selectDiaSeleccion || !DOM.selectBloquesSeleccion) {
      mostrarFeedback("Error: Elementos del formulario no disponibles.", 'error');
      return;
  }

  const nombre = DOM.inputMateria.value.trim();
  const paralelo = DOM.inputParalelo.value.trim();
  const color = DOM.inputColor.value;
  
  const diaSeleccionado = DOM.selectDiaSeleccion.value;
  const bloquesSeleccionados = Array.from(DOM.selectBloquesSeleccion.selectedOptions).map(option => option.value);

  if (!nombre || !paralelo) { 
    mostrarFeedback("Completa los campos de nombre y paralelo.", 'error');
    return;
  }
  if (!diaSeleccionado || bloquesSeleccionados.length === 0) {
      mostrarFeedback("Selecciona un día y al menos un bloque para el horario.", 'error');
      return;
  }

  if (isNaN(paralelo)) {
      mostrarFeedback("El paralelo debe ser un valor numérico.", 'error');
      return;
  }

  const nuevoHorario = { dia: diaSeleccionado, bloques: bloquesSeleccionados };

  let materiaExistenteIndex = materias.findIndex(m => m.nombre === nombre && m.paralelo === paralelo);

  if (materiaExistenteIndex !== -1) {
    let materiaExistente = materias[materiaExistenteIndex];
    materiaExistente.color = color;
    materiaExistente.horarios = [nuevoHorario];
    mostrarFeedback(`Materia "${nombre}" y horario actualizados.`);
  } else {
    materias.push({ 
      nombre, 
      paralelo, 
      color, 
      horarios: [nuevoHorario],
      oculto: false 
    });
    mostrarFeedback("Materia y horario agregados exitosamente.");
  }

  if (DOM.inputMateria) DOM.inputMateria.value = "";
  if (DOM.inputParalelo) DOM.inputParalelo.value = "";
  if (DOM.inputColor) DOM.inputColor.value = "#90ee90";
  if (DOM.selectDiaSeleccion) DOM.selectDiaSeleccion.value = "";
  if (DOM.selectBloquesSeleccion) {
      Array.from(DOM.selectBloquesSeleccion.options).forEach(option => option.selected = false);
  }

  renderizarMaterias();
}

function listarMaterias() {
  if (!DOM.listaMateriasDiv) {
      console.warn("listarMaterias: Elemento listaMateriasDiv no encontrado.");
      return;
  }
  DOM.listaMateriasDiv.innerHTML = "";
  materias.forEach((mat, i) => {
    const div = document.createElement("div");
    div.classList.add('materia-item');

    const horarioDisplay = mat.horarios && mat.horarios.length > 0 ? mat.horarios[0] : { dia: 'N/A', bloques: [] };
    const horariosHtml = `<span><strong>${horarioDisplay.dia}:</strong> Bloques ${horarioDisplay.bloques.join(", ")}</span>`;

    div.innerHTML = `
      <div class="materia-header">
        <div class="materia-info ${mat.oculto ? 'oculta' : ''}">
          <span class="color-indicator" style="background-color: ${mat.color};"></span>
          <span>
            <strong>${mat.nombre}</strong> (P${mat.paralelo})
          </span>
        </div>
        <div class="materia-actions">
          <button class="btn-toggle" onclick="toggleOcultarMateria(${i})">
              <i class="fas ${mat.oculto ? 'fa-eye' : 'fa-eye-slash'}"></i> ${mat.oculto ? 'Mostrar' : 'Ocultar'}
          </button>
          <button class="btn-edit" onclick="editarMateria(${i})"><i class="fas fa-edit"></i> Editar</button>
          <button class="btn-delete" onclick="eliminarMateria(${i})"><i class="fas fa-trash-alt"></i> Eliminar</button>
        </div>
      </div>
      <div class="materia-horarios">
        ${horariosHtml}
      </div>
    `;
    DOM.listaMateriasDiv.appendChild(div);
  });
}

function editarMateria(index) {
  const mat = materias[index];
  
  if (!DOM.inputMateria || !DOM.inputParalelo || !DOM.inputColor || !DOM.selectDiaSeleccion || !DOM.selectBloquesSeleccion || !DOM.formularioMateria) {
      mostrarFeedback("Error: Elementos del formulario no disponibles para editar.", 'error');
      return;
  }

  DOM.inputMateria.value = mat.nombre;
  DOM.inputParalelo.value = mat.paralelo;
  DOM.inputColor.value = mat.color;
  
  DOM.selectDiaSeleccion.value = "";
  Array.from(DOM.selectBloquesSeleccion.options).forEach(option => option.selected = false);

  if (mat.horarios && mat.horarios.length > 0) {
    const horarioEditar = mat.horarios[0];
    if (horarioEditar.dia) {
        DOM.selectDiaSeleccion.value = horarioEditar.dia;
    }
    if (Array.isArray(horarioEditar.bloques)) {
        horarioEditar.bloques.forEach(bloque => {
            const optionToSelect = DOM.selectBloquesSeleccion.querySelector(`option[value="${bloque}"]`);
            if (optionToSelect) {
                optionToSelect.selected = true;
            }
        });
    }
  }

  DOM.formularioMateria.scrollIntoView({ behavior: 'smooth', block: 'start' });
}

function eliminarMateria(index) {
  if (confirm("¿Estás seguro de que quieres eliminar esta materia (incluyendo su horario)?")) {
    materias.splice(index, 1);
    renderizarMaterias();
    mostrarFeedback("Materia eliminada correctamente.");
  }
}

function toggleOcultarMateria(index) {
    if (index >= 0 && index < materias.length) {
        materias[index].oculto = !materias[index].oculto;
        renderizarMaterias();
        mostrarFeedback(`Materia "${materias[index].nombre}" ${materias[index].oculto ? 'ocultada' : 'mostrada'} correctamente.`);
    } else {
        mostrarFeedback("Error: No se pudo ocultar/mostrar la materia.", 'error');
    }
}

function guardarHorario() {
  localStorage.setItem("horarioUSM", JSON.stringify(materias));
  mostrarFeedback("Horario guardado en el navegador.");
}

function cargarHorario() {
  let datos = [];
  try {
    const storedData = localStorage.getItem("horarioUSM");
    if (storedData) {
        datos = JSON.parse(storedData);
    }
  } catch (e) {
    console.error("Error al cargar horario desde localStorage:", e);
    mostrarFeedback("Error al cargar horario guardado. Se ha borrado el horario corrupto.", 'error');
    localStorage.removeItem("horarioUSM"); 
    datos = []; 
  }
  
  materias.length = 0; 
  datos.forEach(m => {
      let saneadoHorario = null;
      if (m.horarios && Array.isArray(m.horarios) && m.horarios.length > 0) {
          let h = m.horarios[0];
          if (h && typeof h === 'object' && h.dia && Array.isArray(h.bloques)) {
              saneadoHorario = { dia: h.dia, bloques: h.bloques.map(String) };
          } else if (h && typeof h === 'object' && h.dia && h.bloques) {
              saneadoHorario = { dia: h.dia, bloques: [String(h.bloques)].filter(Boolean) };
          }
      } else if (m.dia && m.bloques) {
          saneadoHorario = {
              dia: m.dia,
              bloques: Array.isArray(m.bloques) ? m.bloques.map(String) : [String(m.bloques)].filter(Boolean)
          };
      }
      
      const finalHorarios = saneadoHorario ? [saneadoHorario] : [];

      if (typeof m.oculto === 'undefined') {
          m.oculto = false;
      }
      
      materias.push({
          nombre: m.nombre,
          paralelo: m.paralelo,
          color: m.color,
          horarios: finalHorarios,
          oculto: m.oculto
      });
  });
  renderizarMaterias();
  if (datos.length > 0) {
      mostrarFeedback("Horario cargado desde el navegador.");
  } else {
      mostrarFeedback("No se encontró horario guardado o los datos estaban corruptos (limpiados).", 'info');
  }
}

function exportarPDF() {
  mostrarFeedback("Exportar a PDF no disponible. La librería `html2pdf.js` no se pudo cargar.", 'error');
  // Se podría considerar cargar la librería aquí dinámicamente si se necesita
  // o simplemente mantener el botón deshabilitado / funcionalidad no disponible
}

function clearLocalStorageData() {
    if (confirm("¿Estás seguro de que quieres borrar TODOS los datos del horario guardados? Esta acción no se puede deshacer.")) {
        localStorage.removeItem("horarioUSM");
        localStorage.removeItem("darkMode"); 
        materias.length = 0; 
        renderizarMaterias(); 
        if (DOM.checkbox) {
            DOM.checkbox.checked = false;
        }
        document.body.classList.remove('dark-mode'); 
        mostrarFeedback("Datos guardados limpiados.", 'success');
    }
}

function setupDarkMode() {
    if (!DOM.checkbox) {
        console.warn("setupDarkMode: Elemento checkbox para modo oscuro no encontrado.");
        return;
    }

    const body = document.body;
    const isDarkMode = localStorage.getItem('darkMode'); 

    if (isDarkMode === null || isDarkMode === 'true') { 
      body.classList.add('dark-mode');
      DOM.checkbox.checked = true;
    } else {
      body.classList.remove('dark-mode');
      DOM.checkbox.checked = false;
    }

    DOM.checkbox.addEventListener('change', () => {
      body.classList.toggle('dark-mode');
      localStorage.setItem('darkMode', DOM.checkbox.checked); 
      renderizarMaterias(); 
    });
}


// --- INICIALIZACIÓN FINAL: Asegura que todo se ejecute cuando el DOM esté listo ---
document.addEventListener('DOMContentLoaded', () => {
    DOM = getDOMElements(); 

    // Si el botón de PDF existe, lo deshabilitamos ya que la librería no está cargada
    if (DOM.exportPdfBtn) {
        DOM.exportPdfBtn.disabled = true;
    }

    // Estas funciones deben ejecutarse siempre que sus respectivos elementos DOM existan.
    // La función `getDOMElements` ya maneja los errores de no encontrar un ID.
    loadFormOptions(); 
    construirTabla(); 
    setupDarkMode(); 
    cargarHorario(); 
    
    // Un feedback para confirmar que el script se inicializó
    mostrarFeedback("Página cargada. ¡A planificar!", 'info');
});

</script>
</body>
</html>
