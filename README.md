<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Horario USM Simplificado</title>
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
      
      /* --- CAMBIO AQUÍ: Definir un ancho máximo para el contenido principal (formulario, tabla, etc.) --- */
      --content-max-width: 85%; /* Ahora el formulario y la tabla ocuparán un máximo del 85% */
      --form-input-width: 400px; /* Ancho deseado para los inputs/selects del formulario */
      --main-padding: 20px; /* Padding general del body */
    }

    /* Variables CSS para el modo oscuro */
    :root {
      /* --- CAMBIOS AQUÍ para mayor contraste --- */
      --dark-mode-background: #121212; /* Más oscuro */
      --dark-mode-text: #E0E0E0; /* Más claro */
      --dark-mode-input-background: #282828; /* Más oscuro para inputs */
      --dark-mode-input-border: #666; /* Más visible */
      --dark-mode-table-header: #222; /* Más oscuro */
      --dark-mode-table-border: #777; /* Más visible */
      --dark-mode-card-background: #1E1E1E; /* Más oscuro para contenedores */
      --dark-mode-shadow: rgba(0, 0, 0, 0.7); /* Sombra más intensa */
      --usm-blue: #007BFF; /* Azul USM un poco más brillante para contraste */
      --usm-white: #FFFFFF; /* Blanco USM */
    }

    body {
      font-family: 'Roboto', sans-serif; /* Fuente principal */
      background-color: #f5f7fa; /* Fondo suave */
      color: var(--dark-gray);
      padding: var(--main-padding); /* Padding general del body */
      transition: background-color 0.3s ease, color 0.3s ease; /* Transición suave para el modo oscuro */
    }

    h2, h3 {
      font-family: 'Montserrat', sans-serif; /* Fuente para títulos */
      color: var(--primary-color);
      text-align: center;
      margin-bottom: 30px;
      font-weight: 600;
      transition: color 0.3s ease; /* Transición suave para el modo oscuro */
    }
    h3 {
      margin-top: 30px;
    }

    /* Contenedores principales */
    .formulario, #lista-materias, table {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px; /* Bordes más redondeados */
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08); /* Sombra sutil */
        margin-bottom: 25px; /* Más espacio entre secciones */
        width: var(--content-max-width); /* Usar el 85% del ancho de la pantalla */
        margin-left: auto; /* Centrar horizontalmente */
        margin-right: auto; /* Centrar horizontalmente */
        transition: background-color 0.3s ease, box-shadow 0.3s ease; /* Transición suave para el modo oscuro */
    }
    
    .formulario {
        display: flex;
        flex-direction: column; /* Apilar elementos */
        align-items: center; /* Centrar elementos horizontalmente */
        /* --- CAMBIO AQUÍ: El formulario toma el ancho máximo definido --- */
        max-width: var(--content-max-width); 
    }

    table {
      border-collapse: collapse;
      table-layout: fixed; /* Esto ayuda a que las celdas tengan anchos uniformes */
    }
    th, td {
      border: 1px solid var(--table-border-color);
      text-align: center;
      padding: 8px; /* Padding por defecto de las celdas */
      vertical-align: middle;
      height: 50px; /* Altura mínima de la celda */
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
    /* Anchos específicos para las columnas de la tabla */
    table th:first-child, table td:first-child { width: 5%; } /* Bloque */
    table th:nth-child(2), table td:nth-child(2) { width: 10%; } /* Hora */
    table th:nth-child(n+3), table td:nth-child(n+3) { width: 17%; } /* Días (100-5-10)/5 = 17% */


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
        width: 100%; /* Ocupa el 100% del formulario (que ya tiene max-width) */
        /* --- CAMBIO AQUÍ: Ahora el input-group toma el ancho completo del formulario, no un max-width fijo --- */
        /* Eliminamos max-width: var(--form-input-width); para que se estire con el formulario */
        text-align: left; /* Asegura que labels y inputs se alineen a la izquierda dentro de su grupo */
    }

    .formulario input, .formulario select {
      width: 100%; /* Ocupa el 100% de su input-group */
      padding: 10px;
      border: 1px solid var(--border-color);
      border-radius: 5px;
      font-size: 1em;
      margin-top: 5px;
      box-sizing: border-box;
      transition: background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease; /* Transición suave para el modo oscuro */
    }
    .formulario input[type="color"] {
        width: 60px; /* Mantenemos el ancho pequeño para el color */
        padding: 5px;
    }
    
    /* Estilos para el select multiple nativo */
    .formulario select[multiple] {
        height: auto; /* Permite que el alto se ajuste al número de opciones */
        min-height: 100px; /* Altura mínima para que se vean varias opciones */
    }


    .formulario .form-buttons {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 10px;
        width: 100%;
        /* --- CAMBIO AQUÍ: Los botones también se estiran al 100% del formulario --- */
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
    /* Estilos base para ambas materias y topes */
    .celda-materia {
      position: absolute; top: 0; left: 0; width: 100%; height: 100%;
      font-weight: 500;
      display: flex;
      justify-content: center;
      align-items: center;
      box-sizing: border-box; /* Asegura que padding no aumente el tamaño */
      padding: 8px; /* Aumentar el padding para que el contenido tenga más espacio */
      word-break: break-word; /* Rompe palabras largas */
      overflow-wrap: break-word; /* Para mayor compatibilidad con rompimiento de palabras */
      flex-direction: column;
      font-size: 0.85em; /* Tamaño de fuente para materias normales */
      line-height: 1.2; /* Espaciado de línea */
      transition: color 0.3s ease, background-color 0.3s ease; /* Asegurar transición de fondo */
      text-align: center; /* Centrar el texto en la celda */
    }

    /* Estilos específicos para celdas de "tope" */
    .celda-materia.tope { /* Se aplica directamente a la div.celda-materia */
      background-color: var(--danger-color) !important;
      color: white;
    }

    .tope .titulo-tope {
      display: block;
      font-weight: bold;
      font-size: 1.1em; /* Relativo al font-size de .celda-materia */
      margin-bottom: 2px;
      letter-spacing: 0.5px;
      text-transform: uppercase;
      white-space: normal;
      overflow: hidden;
      text-overflow: ellipsis;
      text-align: center;
    }

    .tope .materias-conflicto {
        font-size: 0.9em; /* Relativo al font-size de .celda-materia */
        text-align: center;
        line-height: 1.1;
        white-space: normal;
        word-wrap: break-word;
        overflow-wrap: break-word;
    }

    /* LISTA DE MATERIAS */
    #lista-materias {
        padding: 15px;
        margin-top: 25px; /* Espacio extra porque ahora está debajo */
    }

    #lista-materias .materia-item { /* Nueva clase para cada materia en la lista */
      margin-bottom: 10px;
      padding: 10px;
      border: 1px solid var(--border-color);
      border-radius: 5ppedx;
      display: flex;
      flex-direction: column; /* Cambiado a columna para el contenido y los horarios */
      background-color: var(--light-gray);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
      transition: background-color 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
    }

    #lista-materias .materia-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px; /* Espacio entre el header y los horarios */
    }

    #lista-materias .materia-info {
        display: flex;
        align-items: center;
        gap: 8px;
        font-weight: 400;
        flex-grow: 1;
    }

    #lista-materias .materia-info.oculta span {
        text-decoration: line-through; /* Tachado para materias ocultas */
        opacity: 0.7; /* Ligeramente transparente */
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
        padding-left: 26px; /* Para alinear con el inicio del texto de la materia */
        color: var(--dark-gray);
    }
    #lista-materias .materia-horarios span {
        display: block; /* Cada horario en su propia línea */
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
        background-color: #607D8B; /* Un gris azulado */
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
      /* --- CAMBIO AQUÍ: feedback también respeta el max-width --- */
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
      /* --- CAMBIO AQUÍ: El switch de tema también respeta el max-width --- */
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

    /* --- INICIO DEL CAMBIO CLAVE PARA LA TABLA EN MODO OSCURO --- */
    body.dark-mode table {
      background-color: var(--dark-mode-card-background); /* Fondo general de la tabla en modo oscuro */
      box-shadow: 0 4px 10px var(--dark-mode-shadow);
    }
    
    body.dark-mode th {
      background-color: var(--dark-mode-table-header); /* Fondo de los encabezados de la tabla */
      color: var(--dark-mode-text); /* Color del texto de los encabezados */
      border-color: var(--dark-mode-table-border); /* Color del borde de los encabezados */
    }

    body.dark-mode td {
      background-color: var(--dark-mode-card-background); /* Fondo por defecto de las celdas en modo oscuro */
      color: var(--dark-mode-text); /* Color del texto por defecto de las celdas (para celdas vacías) */
      border-color: var(--dark-mode-table-border); /* Color del borde de las celdas */
    }
    /* --- FIN DEL CAMBIO CLAVE PARA LA TABLA EN MODO OSCURO --- */


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

    /* Ajuste para el texto dentro de .celda-materia en modo oscuro,
       aunque su color de fondo se establece in-line por JS */
    body.dark-mode .celda-materia {
        /* El color de texto se maneja principalmente por getContrastTextColor en JS,
           pero esta regla asegura que cualquier otro texto dentro tenga un color visible */
        color: var(--dark-mode-text); /* Fallback o para texto no afectado por getContrastTextColor */
    }

    body.dark-mode .celda-materia.tope {
        color: var(--usm-white); /* Para el texto del tope, siempre blanco sobre el rojo */
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
        background-color: #555; /* Darker grey for toggle in dark mode */
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

    body.dark-mode .theme-switch-wrapper {
      color: var(--dark-mode-text);
    }

    /* Ajustes responsivos básicos para pantallas más pequeñas */
    @media (max-width: 768px) {
        :root {
            --content-max-width: 100%; /* En móviles, volvemos a 100% para aprovechar el espacio */
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
        #lista-materias .materia-item { /* Usar la nueva clase aquí */
            flex-direction: column;
            align-items: flex-start;
        }
        #lista-materias .materia-header { /* Nuevo */
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
            max-width: 100%; /* Aseguramos que los input-group se estiren en móviles */
        }
        /* Ajuste de celdas de tabla en móviles */
        table th, table td {
            font-size: 0.8em;
            padding: 5px;
            height: 40px;
        }
        table th:first-child, table td:first-child { width: 8%; } /* Bloque */
        table th:nth-child(2), table td:nth-child(2) { width: 15%; } /* Hora */
        table th:nth-child(n+3), table td:nth-child(n+3) { width: 15.4%; } /* Días */
    }
  </style>
</head>
<body>

<h2>Planificador de horario</h2>

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
    <select id="dia-seleccion"></select> </div>

  <div class="input-group" id="bloques-fijos-container">
    <label for="bloques-seleccion">Bloques del horario:</label>
    <select multiple id="bloques-seleccion"></select> </div>

  <div class="input-group">
    <label for="color">Color de la materia:</label>
    <input type="color" id="color" value="#90ee90">
  </div>

  <br>
  <div class="form-buttons">
    <button onclick="agregarActualizarMateriaYHorario()"><i class="fas fa-plus-circle"></i> Agregar/Actualizar Materia y Horario</button>
    <button onclick="guardarHorario()"><i class="fas fa-save"></i> Guardar</button>
    <button onclick="cargarHorario()"><i class="fas fa-folder-open"></i> Cargar</button>
    <button onclick="exportarPDF()"><i class="fas fa-file-pdf"></i> Exportar a PDF</button>
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

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<script>
console.log("Script iniciado.");

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

// Obtención de referencias a elementos del DOM
const tabla = document.getElementById("tabla");
const inputMateria = document.getElementById("materia");
const inputParalelo = document.getElementById("paralelo");
const inputColor = document.getElementById("color");
const selectDiaSeleccion = document.getElementById("dia-seleccion");
const selectBloquesSeleccion = document.getElementById("bloques-seleccion");
const listaMateriasDiv = document.getElementById("lista-materias");
const feedbackMessageDiv = document.getElementById("feedback-message");
const formularioMateria = document.getElementById("formulario-materia");
const checkbox = document.getElementById("checkbox"); // Para el modo oscuro

console.log("Referencias a elementos del DOM obtenidas.");


// Función para determinar el color del texto (negro o blanco) según el fondo
function getContrastTextColor(hexColor) {
    const r = parseInt(hexColor.slice(1, 3), 16);
    const g = parseInt(hexColor.slice(3, 5), 16);
    const b = parseInt(hexColor.slice(5, 7), 16);
    const luminance = (0.2126 * r + 0.7152 * g + 0.0722 * b) / 255;
    
    // Este umbral es crucial para la decisión.
    // Un valor más alto hace que el color claro se use más.
    // Un valor más bajo hace que el color oscuro se use más.
    // Mantener 0.5 es un buen punto de partida.
    const threshold = 0.5;

    // Si el modo oscuro está activo, el fondo de la página es oscuro.
    // Si el color de la materia es claro (luminance > threshold), queremos texto oscuro para buen contraste.
    // Si el color de la materia es oscuro (luminance <= threshold), queremos texto blanco.
    // Esto asegura que el texto dentro de la materia siempre contraste bien,
    // independientemente del modo de la página, ya que el color de la materia puede ser cualquiera.
    return luminance > threshold ? '#333' : 'white';
}


// Carga las opciones de días y bloques al iniciar
function loadFormOptions() {
  console.log("loadFormOptions: Inicializando select de día y bloques.");
  if (!selectDiaSeleccion || !selectBloquesSeleccion) {
      console.error("loadFormOptions: Elementos de selección no encontrados.");
      return;
  }

  // Cargar opciones para el select de un solo día
  selectDiaSeleccion.innerHTML = "";
  dias.forEach(dia => {
    const option = document.createElement("option");
    option.value = dia;
    option.textContent = dia;
    selectDiaSeleccion.appendChild(option);
  });

  // Cargar opciones para el select múltiple de bloques (siempre presente)
  selectBloquesSeleccion.innerHTML = "";
  bloquesUSM.forEach(([numero, hora]) => {
      const option = document.createElement("option");
      option.value = numero;
      option.textContent = `Bloque ${numero} (${hora})`;
      selectBloquesSeleccion.appendChild(option);
  });
  console.log("loadFormOptions: Selects de día y bloques inicializados.");
}


function construirTabla() {
  console.log("construirTabla: Iniciando construcción de la tabla.");
  if (!tabla) {
      console.error("construirTabla: Elemento 'tabla' no encontrado.");
      return;
  }
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
  console.log("construirTabla: Tabla construida.");
}

function renderizarMaterias() {
  console.log("renderizarMaterias: Iniciando renderizado de materias en la tabla y lista.");
  construirTabla(); // Asegura que la tabla esté fresca

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
        console.warn(`renderizarMaterias: Celda con ID ${clave} no encontrada. Esto puede indicar un problema en construirTabla.`);
        continue;
      }

      celda.innerHTML = "";
      celda.style.display = "";
      celda.rowSpan = 1;
      // Remueve los estilos in-line de fondo y color directamente de la celda TD
      // para que el CSS (incluido el de dark-mode) pueda aplicar el color de fondo por defecto
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
  console.log("renderizarMaterias: Renderizado completado.");
}

function mostrarFeedback(message, type = 'success') {
    console.log(`Feedback: ${message} (Type: ${type})`);
    if (!feedbackMessageDiv) {
        console.error("mostrarFeedback: Elemento feedbackMessageDiv no encontrado.");
        return;
    }
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

function agregarActualizarMateriaYHorario() {
  console.log("agregarActualizarMateriaYHorario: Iniciado.");
  const nombre = inputMateria.value.trim();
  const paralelo = inputParalelo.value.trim();
  const color = inputColor.value;
  
  const diaSeleccionado = selectDiaSeleccion.value;
  const bloquesSeleccionados = Array.from(selectBloquesSeleccion.selectedOptions).map(option => option.value);

  if (!nombre || !paralelo) { 
    mostrarFeedback("Completa los campos de nombre y paralelo.", 'error');
    console.log("agregarActualizarMateriaYHorario: Error - Campos nombre/paralelo vacíos.");
    return;
  }
  if (!diaSeleccionado || bloquesSeleccionados.length === 0) {
      mostrarFeedback("Selecciona un día y al menos un bloque para el horario.", 'error');
      console.log("agregarActualizarMateriaYHorario: Error - Día o bloques no seleccionados.");
      return;
  }

  if (isNaN(paralelo)) {
      mostrarFeedback("El paralelo debe ser un valor numérico.", 'error');
      console.log("agregarActualizarMateriaYHorario: Error - Paralelo no numérico.");
      return;
  }

  // Objeto de horario para la materia
  const nuevoHorario = { dia: diaSeleccionado, bloques: bloquesSeleccionados };

  let materiaExistenteIndex = materias.findIndex(m => m.nombre === nombre && m.paralelo === paralelo);

  if (materiaExistenteIndex !== -1) {
    // Materia ya existe, actualiza sus datos y horario
    let materiaExistente = materias[materiaExistenteIndex];
    materiaExistente.color = color;
    // Asigna el nuevo horario (o actualiza el existente)
    materiaExistente.horarios = [nuevoHorario]; // Simplificamos a un array con un solo horario
    mostrarFeedback(`Materia "${nombre}" y horario actualizados.`);
  } else {
    // Materia no existe, crea una nueva
    materias.push({ 
      nombre, 
      paralelo, 
      color, 
      horarios: [nuevoHorario], // Almacenamos el horario como un array con un solo elemento
      oculto: false 
    });
    mostrarFeedback("Materia y horario agregados exitosamente.");
  }

  // Limpiar el formulario
  inputMateria.value = "";
  inputParalelo.value = "";
  inputColor.value = "#90ee90";
  selectDiaSeleccion.value = ""; // Deseleccionar el día
  Array.from(selectBloquesSeleccion.options).forEach(option => option.selected = false); // Deseleccionar todos los bloques

  renderizarMaterias();
  console.log("agregarActualizarMateriaYHorario: Finalizado.");
}

function listarMaterias() {
  console.log("listarMaterias: Iniciado.");
  if (!listaMateriasDiv) {
      console.error("listarMaterias: Elemento listaMateriasDiv no encontrado.");
      return;
  }
  listaMateriasDiv.innerHTML = "";
  materias.forEach((mat, i) => {
    const div = document.createElement("div");
    div.classList.add('materia-item');

    // Asumimos que ahora solo hay un horario por materia, o es el primer elemento del array
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
    listaMateriasDiv.appendChild(div);
  });
  console.log("listarMaterias: Finalizado.");
}

function editarMateria(index) {
  console.log(`editarMateria: Editando materia en índice ${index}.`);
  const mat = materias[index];
  inputMateria.value = mat.nombre;
  inputParalelo.value = mat.paralelo;
  inputColor.value = mat.color;
  
  if (!selectDiaSeleccion || !selectBloquesSeleccion) {
      console.error("editarMateria: Elementos de selección no encontrados.");
      return;
  }

  // Limpiar selección de día y bloques
  selectDiaSeleccion.value = "";
  Array.from(selectBloquesSeleccion.options).forEach(option => option.selected = false);
  console.log("editarMateria: Selects deseleccionados en el formulario.");

  if (mat.horarios && mat.horarios.length > 0) {
    const horarioEditar = mat.horarios[0]; // Tomamos el primer (y único) horario
    if (horarioEditar.dia) {
        selectDiaSeleccion.value = horarioEditar.dia;
    }
    if (Array.isArray(horarioEditar.bloques)) {
        horarioEditar.bloques.forEach(bloque => {
            const optionToSelect = selectBloquesSeleccion.querySelector(`option[value="${bloque}"]`);
            if (optionToSelect) {
                optionToSelect.selected = true;
                console.log(`editarMateria: Bloque ${bloque} seleccionado.`);
            }
        });
    }
  }
  console.log("editarMateria: Día y bloques de la materia preseleccionados.");

  if (formularioMateria) {
      formularioMateria.scrollIntoView({ behavior: 'smooth', block: 'start' });
  } else {
      console.warn("editarMateria: Elemento formularioMateria no encontrado para scroll.");
  }
  console.log("editarMateria: Finalizado.");
}

function eliminarMateria(index) {
  if (confirm("¿Estás seguro de que quieres eliminar esta materia (incluyendo su horario)?")) {
    materias.splice(index, 1);
    renderizarMaterias();
    mostrarFeedback("Materia eliminada correctamente.");
  }
}

function toggleOcultarMateria(index) {
    materias[index].oculto = !materias[index].oculto;
    renderizarMaterias();
    mostrarFeedback(`Materia "${materias[index].nombre}" ${materias[index].oculto ? 'ocultada' : 'mostrada'} correctamente.`);
}


function guardarHorario() {
  localStorage.setItem("horarioUSM", JSON.stringify(materias));
  mostrarFeedback("Horario guardado en el navegador.");
}

function cargarHorario() {
  console.log("cargarHorario: Iniciando carga desde localStorage.");
  let datos = [];
  try {
    const storedData = localStorage.getItem("horarioUSM");
    if (storedData) {
        datos = JSON.parse(storedData);
        console.log("cargarHorario: Datos cargados exitosamente de localStorage.");
    } else {
        console.log("cargarHorario: No se encontraron datos en localStorage.");
    }
  } catch (e) {
    console.error("cargarHorario: Error al cargar horario desde localStorage:", e);
    mostrarFeedback("Error al cargar horario guardado. Se ha borrado el horario corrupto.", 'error');
    localStorage.removeItem("horarioUSM"); 
    datos = []; 
  }
  
  materias.length = 0; 
  datos.forEach(m => {
      // --- Saneamiento de datos para el formato simplificado ---
      let saneadoHorario = null;
      if (m.horarios && Array.isArray(m.horarios) && m.horarios.length > 0) {
          // Si ya es un array de horarios, tomamos el primero
          let h = m.horarios[0];
          if (h && typeof h === 'object' && h.dia && Array.isArray(h.bloques)) {
              saneadoHorario = { dia: h.dia, bloques: h.bloques.map(String) };
          } else if (h && typeof h === 'object' && h.dia && h.bloques) {
              // Si bloques no es array (ej. de una versión antigua que era string/número)
              saneadoHorario = { dia: h.dia, bloques: [String(h.bloques)].filter(Boolean) };
          }
      } else if (m.dia && m.bloques) {
          // Compatibilidad con formato antiguo donde 'dia' y 'bloques' estaban directamente en la materia
          saneadoHorario = {
              dia: m.dia,
              bloques: Array.isArray(m.bloques) ? m.bloques.map(String) : [String(m.bloques)].filter(Boolean)
          };
      }
      
      // La materia ahora siempre tendrá un array 'horarios' con un máximo de un elemento
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
  // Solo mostrar feedback si la carga fue realmente exitosa o manejada
  if (datos.length > 0) {
      mostrarFeedback("Horario cargado desde el navegador.");
  } else {
      mostrarFeedback("No se encontró horario guardado o los datos estaban corruptos (limpiados).", 'info');
  }
  console.log("cargarHorario: Finalizada la carga. Materias:", materias);
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

  // Clonar la tabla y el título para la exportación
  const h2ForPdf = document.querySelector('h2').cloneNode(true);
  const tableForPdf = document.querySelector('table').cloneNode(true);

  // Asegurar que las celdas de la tabla clonada mantengan el estilo original de las materias
  const pdfCells = tableForPdf.querySelectorAll('td');
  pdfCells.forEach(cell => {
      const celdaMateriaDiv = cell.querySelector('.celda-materia');
      if (celdaMateriaDiv) {
          // Copiar el contenido interno y los estilos de fondo/color de texto
          cell.innerHTML = celdaMateriaDiv.innerHTML;
          cell.style.backgroundColor = celdaMateriaDiv.style.backgroundColor;
          cell.style.color = celdaMateriaDiv.style.color;
          cell.style.position = 'static'; // Esencial para PDF, remueve el posicionamiento absoluto
          cell.style.display = ''; // Asegurar que sea visible
      }
      // Si la celda fue ocultada (por ejemplo, por rowspan en una versión anterior),
      // asegurarse de que no haya contenido si no hay materia.
      if (cell.style.display === 'none') {
          cell.style.display = '';
          cell.innerHTML = '';
      }
  });


  exportContainer.appendChild(h2ForPdf);
  exportContainer.appendChild(tableForPdf);

  if (typeof html2pdf !== 'undefined') {
    html2pdf().set(opt).from(exportContainer).save()
        .then(() => console.log("PDF generado y guardado exitosamente."))
        .catch(err => {
            console.error("Error al generar PDF:", err);
            mostrarFeedback("Error al generar PDF. Revisa la consola.", 'error');
        });
  } else {
      console.error("html2pdf no está definido. Asegúrate de que la librería se haya cargado correctamente.");
      mostrarFeedback("Error: La función de exportar a PDF no está disponible.", 'error');
  }
}

// Lógica para limpiar datos de localStorage
function clearLocalStorageData() {
    if (confirm("¿Estás seguro de que quieres borrar TODOS los datos del horario guardados? Esta acción no se puede deshacer.")) {
        localStorage.removeItem("horarioUSM");
        localStorage.removeItem("darkMode"); 
        materias.length = 0; 
        renderizarMaterias(); 
        mostrarFeedback("Datos guardados limpiados. Recarga la página si persisten los problemas.", 'success');
        console.log("localStorage limpiado.");
    }
}

---
### Lógica del Modo Oscuro
---

const body = document.body;

// Comprobar si hay una preferencia guardada al cargar la página
// Si no hay preferencia o es 'true', activa el modo oscuro.
// Esto permite que el usuario pueda desactivarlo y que esa preferencia se respete.
const isDarkMode = localStorage.getItem('darkMode'); 

// Si no se ha guardado nada O si la preferencia guardada es 'true'
if (isDarkMode === null || isDarkMode === 'true') { 
  body.classList.add('dark-mode');
  if (checkbox) checkbox.checked = true;
} else { // Si la preferencia guardada es 'false' (modo claro)
  body.classList.remove('dark-mode');
  if (checkbox) checkbox.checked = false;
}

// Escuchar el cambio en el checkbox para alternar el modo oscuro
if (checkbox) {
    checkbox.addEventListener('change', () => {
      body.classList.toggle('dark-mode');
      localStorage.setItem('darkMode', checkbox.checked); 
      renderizarMaterias(); 
    });
} else {
    console.warn("Elemento checkbox para modo oscuro no encontrado.");
}


  
    console.log("DOMContentLoaded: El DOM ha sido completamente cargado.");
    loadFormOptions(); 
    construirTabla(); // Asegura que la tabla esté presente incluso sin datos cargados
    cargarHorario(); 
console.log("Fin del script principal.");
</script>
</body>
</html>
