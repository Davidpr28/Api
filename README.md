---

# 🚀 Simple Gemini AI Web App

Una aplicación web simple que permite a los usuarios interactuar con la API de Google Gemini para generar contenido usando inteligencia artificial. Cuenta con un frontend HTML/CSS/JS y un backend serverless compatible con Vercel.

---

## 📑 Índice

- [📋 Descripción](#-descripción)
- [🧰 Prerrequisitos](#-prerrequisitos)
- [⚙️ Configuración del Entorno](#️-configuración-del-entorno)
- [▶️ Ejecución Local](#️-ejecución-local)
- [📁 Estructura del Proyecto](#-estructura-del-proyecto)
- [💻 Código Fuente Completo](#-código-fuente-completo)
- [☁️ Despliegue en Vercel](#-despliegue-en-vercel)
- [🧪 Preguntas Frecuentes (FAQ)](#-preguntas-frecuentes-faq)
- [👨‍💻 Autor](#-autor)
- [📄 Licencia](#-licencia)

---

## 📋 Descripción

Este proyecto permite hacer solicitudes a la API de Google Gemini y mostrar las respuestas en una interfaz web. Está pensado para aprender sobre inteligencia artificial y cómo integrarla en aplicaciones web simples.

---

## 🧰 Prerrequisitos

- **Node.js y npm**  
  👉 Instalar desde: [https://nodejs.org](https://nodejs.org)

- **Vercel CLI**  
  👉 Instalar con:
  ```bash
  npm install -g vercel
  vercel login
  ```

- **Clave de API Gemini**  
  👉 Obtener desde: [https://makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey)

---

## ⚙️ Configuración del Entorno

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/Davidpr28/Api?tab=readme-ov-file
   cd Api
   ```

2. **Crear archivo `.env` con tu clave API**
   ```env
   GEMINI_API_KEY=TU_CLAVE_DE_API
   ```

3. **Instalar dependencias**
   ```bash
   npm install
   ```

---

## ▶️ Ejecución Local

Ejecuta la app localmente con:

```bash
vercel dev
```

Abre tu navegador en:  
👉 `http://localhost:3000`

---

## 📁 Estructura del Proyecto

```
PRUEBA3/
├── api/
│   └── generate.js
├── public/
│   ├── index.html
│   ├── style.css
│   └── generate.js
├── .env
├── .gitignore
├── vercel.json
├── package.json
└── README.md
```

---

## 💻 Código Fuente Completo

### ✅ `index.html`

```html
<!DOCTYPE html>
<html lang="es">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- Viewport para responsividad -->
  <title>Mi App con Gemini AI</title>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css" rel="stylesheet" />
  <link rel="stylesheet" href="style.css">
</head>

<body>
  <div class="container">
    <h1>Interactúa con Gemini</h1>

    <!-- Sección del Prompt -->
    <div class="prompt-section">
      <textarea class="prompt-area" id="promptInput" placeholder="Escribe tu consulta aquí..."></textarea>
      <div class="button-group">
        <!-- Botón Enviar con Icono -->
        <button id="executeBtn" title="Enviar consulta">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-send" viewBox="0 0 16 16">
            <path d="M15.854.146a.5.5 0 0 1 .11.54l-5.819 14.547a.75.75 0 0 1-1.329.124l-3.178-4.995L.643 7.184a.75.75 0 0 1 .124-1.33L15.314.037a.5.5 0 0 1 .54.11ZM6.636 10.07l2.761 4.338L14.13 2.576zm6.787-8.201L1.591 6.602l4.339 2.76z"/>
          </svg>
          Enviar
        </button>
        <!-- Botón Limpiar con Icono -->
        <button id="clearBtn" title="Limpiar consulta y resultado">
           <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-eraser" viewBox="0 0 16 16">
            <path d="M8.086 2.207a2 2 0 0 1 2.828 0l3.879 3.879a2 2 0 0 1 0 2.828l-5.5 5.5A2 2 0 0 1 7.879 15H5.12a2 2 0 0 1-1.414-.586l-2.5-2.5a2 2 0 0 1 0-2.828zm2.121.707a1 1 0 0 0-1.414 0L4.16 7.547l5.293 5.293 4.633-4.633a1 1 0 0 0 0-1.414zM8.746 13.547 3.453 8.254 1.914 9.793a1 1 0 0 0 0 1.414l2.5 2.5a1 1 0 0 0 .707.293H7.88a1 1 0 0 0 .707-.293z"/>
          </svg>
          Limpiar
        </button>
      </div>
    </div>

    <!-- Sección de Resultados -->
    <div class="result-container">
      <div class="result-header">
          <h3>Respuesta de la IA:</h3>
          <div class="result-actions">
              <!-- Botón Copiar con Icono -->
              <button id="copyBtn" title="Copiar al portapapeles" disabled>
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-clipboard" viewBox="0 0 16 16">
                  <path d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1z"/>
                  <path d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0z"/>
                </svg>
                Copiar
              </button>
              <!-- Botón Guardar con Icono -->
              <button id="saveBtn" title="Guardar como .txt" disabled>
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-download" viewBox="0 0 16 16">
                  <path d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5"/>
                  <path d="M7.646 11.854a.5.5 0 0 0 .708 0l3-3a.5.5 0 0 0-.708-.708L8.5 10.293V1.5a.5.5 0 0 0-1 0v8.793L5.354 8.146a.5.5 0 1 0-.708.708z"/>
                </svg>
                Guardar
              </button>
          </div>
      </div>
      <div id="resultBox" class="result-box">Esperando consulta...</div>
    </div>
  </div>

  <!-- Indicador de carga (spinner) -->
  <div class="loading" id="loading" style="display: none;">
    <div class="spinner"></div>
    <span>Cargando...</span>
  </div>

  <!-- Librerías JavaScript (CDN) -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/components/prism-core.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/plugins/autoloader/prism-autoloader.min.js"></script>

  <!-- TU JavaScript (sin cambios necesarios aquí respecto a la versión anterior) -->
  <script>
    // Referencias a elementos del DOM
    const executeBtn = document.getElementById('executeBtn');
    const clearBtn = document.getElementById('clearBtn');
    const promptInput = document.getElementById('promptInput');
    const resultBox = document.getElementById('resultBox');
    const loadingIndicator = document.getElementById('loading');
    const copyBtn = document.getElementById('copyBtn');
    const saveBtn = document.getElementById('saveBtn');

    // Estado inicial de los botones de acción
    copyBtn.disabled = true;
    saveBtn.disabled = true;

    // Event Listeners
    executeBtn.addEventListener('click', executeQuery);
    clearBtn.addEventListener('click', clearAll);
    copyBtn.addEventListener('click', copyToClipboard);
    saveBtn.addEventListener('click', saveAsTextFile);

    async function executeQuery() {
      const prompt = promptInput.value.trim();
      if (!prompt) {
        alert('Por favor, escribe una consulta.');
        return;
      }
      showLoading();
      resultBox.textContent = 'Procesando...';
      copyBtn.disabled = true;
      saveBtn.disabled = true;
      try {
        const response = await fetch('/api/generate', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ prompt: prompt }),
        });
        if (!response.ok) {
          let errorMsg = 'Error al comunicarse con el servidor.';
          try {
            const errorData = await response.json();
            errorMsg = `Error ${response.status}: ${errorData.error || 'Detalles no disponibles.'}`;
          } catch (e) { errorMsg = `Error ${response.status}: ${response.statusText}`; }
          throw new Error(errorMsg);
        }
        const data = await response.json();
        if (data.candidates && data.candidates.length > 0 && data.candidates[0].content?.parts?.length > 0) {
          const contentPart = data.candidates[0].content.parts[0];
          displayResult(contentPart);
          if (contentPart.text) {
            copyBtn.disabled = false;
            saveBtn.disabled = false;
          }
        } else {
          console.warn('Respuesta inesperada de la API:', data);
          resultBox.textContent = 'No se recibió una respuesta válida del modelo.';
          copyBtn.disabled = true;
          saveBtn.disabled = true;
        }
      } catch (error) {
        console.error('Error en executeQuery:', error);
        resultBox.innerHTML = `<span style="color: var(--danger-color);">Error: ${error.message}</span>`; // Usar variable CSS para color de error
        copyBtn.disabled = false; // Habilitar para copiar el error
        saveBtn.disabled = false; // Habilitar para guardar el error
      } finally {
        hideLoading();
      }
    }

    function displayResult(content) {
      if (content.text) {
        resultBox.innerHTML = marked.parse(content.text);
        Prism.highlightAllUnder(resultBox);
      } else {
        console.warn('Contenido no textual recibido:', content);
        resultBox.textContent = '[Contenido no textual recibido]';
      }
    }

    async function copyToClipboard() {
        const textToCopy = resultBox.innerText;
        if (!textToCopy || resultBox.textContent === 'Esperando consulta...' || resultBox.textContent === 'Procesando...') { return alert('No hay resultado para copiar.'); }
        try {
            await navigator.clipboard.writeText(textToCopy);
            const originalHTML = copyBtn.innerHTML;
            copyBtn.innerHTML = '¡Copiado!';
            copyBtn.disabled = true;
            setTimeout(() => { copyBtn.innerHTML = originalHTML; copyBtn.disabled = false; }, 1500);
        } catch (err) { console.error('Error al copiar:', err); alert('No se pudo copiar el texto.'); }
    }

    function saveAsTextFile() {
        const textToSave = resultBox.innerText;
        if (!textToSave || resultBox.textContent === 'Esperando consulta...' || resultBox.textContent === 'Procesando...') { return alert('No hay resultado para guardar.'); }
        const blob = new Blob([textToSave], { type: 'text/plain;charset=utf-8' });
        const url = URL.createObjectURL(blob);
        const anchor = document.createElement('a');
        anchor.href = url;
        anchor.download = 'gemini-respuesta.txt';
        document.body.appendChild(anchor);
        anchor.click();
        document.body.removeChild(anchor);
        URL.revokeObjectURL(url);
    }

    function showLoading() {
      loadingIndicator.style.display = 'flex';
      executeBtn.disabled = true;
    }
    function hideLoading() {
      loadingIndicator.style.display = 'none';
      executeBtn.disabled = false;
    }
    function clearAll() {
      promptInput.value = '';
      resultBox.innerHTML = 'Esperando consulta...';
      copyBtn.disabled = true;
      saveBtn.disabled = true;
    }
  </script>
</body>
</html>
```

---

### 🎨 `style.css`

```css
/* style.css */

/* 1. Variables CSS (Custom Properties) */
:root {
    /* Paleta de Colores Principal */
    --primary-color: #3498db;          /* Azul principal (Enviar) */
    --primary-color-darker: #2980b9;
    --danger-color: #e74c3c;           /* Rojo (Limpiar, Errores) */
    --danger-color-darker: #c0392b;
    --info-color: #0dcaf0;            /* Azul claro (Copiar) */
    --info-color-darker: #0aa3c2;
    --success-color: #198754;         /* Verde (Guardar) */
    --success-color-darker: #157347;
    --secondary-color: #6c757d;       /* Gris (Deshabilitado Acciones) */
    --disabled-color: #bdc3c7;        /* Gris más claro (Deshabilitado Principal) */
    --disabled-opacity: 0.65;
  
    /* Paleta de Texto y Fondo */
    --text-color-dark: #2c3e50;       /* Títulos oscuros */
    --text-color-medium: #34495e;     /* Subtítulos */
    --text-color-normal: #333;        /* Texto principal */
    --text-color-light: #ccc;         /* Texto en fondo oscuro (código) */
    --text-color-white: #fff;         /* Texto en botones */
  
    --background-color-body: #f4f7f6;
    --background-color-container: #fff;
    --background-color-result: #f9f9f9;
    --background-color-code: #2d2d2d; /* Tema Prism Tomorrow Night */
    --background-color-overlay: rgba(255, 255, 255, 0.7);
  
    /* Bordes */
    --border-color-light: #e0e0e0;     /* Borde caja resultado */
    --border-color-medium: #dcdcdc;    /* Borde textarea */
    --border-radius-standard: 4px;
  
    /* Tipografía y Espaciado */
    --font-family-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    --font-family-mono: "Consolas", "Monaco", monospace;
    --base-font-size: 16px;
    --line-height-normal: 1.6;
    --spacing-unit: 8px; /* Unidad base para márgenes/paddings */
  
    --button-padding-y: 10px;
    --button-padding-x: 20px;
    --button-action-padding-y: 5px;
    --button-action-padding-x: 10px;
  }
  
  /* 2. Reset y Box-Sizing Global */
  html {
    box-sizing: border-box;
  }
  *, *:before, *:after {
    box-sizing: inherit;
  }
  
  body {
    font-family: var(--font-family-sans);
    font-size: var(--base-font-size);
    margin: 0;
    padding: calc(var(--spacing-unit) * 2.5); /* 20px */
    background-color: var(--background-color-body);
    color: var(--text-color-normal);
    line-height: var(--line-height-normal);
  }
  
  /* 3. Estilos del Contenedor Principal */
  .container {
    max-width: 800px;
    margin: calc(var(--spacing-unit) * 2.5) auto; /* 20px auto */
    padding: calc(var(--spacing-unit) * 3);     /* 24px ~= 25px */
    background-color: var(--background-color-container);
    border-radius: calc(var(--border-radius-standard) * 2); /* 8px */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  h1 {
    text-align: center;
    color: var(--text-color-dark);
    margin-top: 0;
    margin-bottom: calc(var(--spacing-unit) * 4); /* 32px ~= 30px */
  }
  
  /* 4. Sección del Prompt */
  .prompt-section {
    margin-bottom: calc(var(--spacing-unit) * 3); /* 24px ~= 25px */
  }
  
  .prompt-area {
    width: 100%;
    padding: calc(var(--spacing-unit) * 1.5); /* 12px */
    border: 1px solid var(--border-color-medium);
    border-radius: var(--border-radius-standard);
    font-size: inherit; /* Heredar del body */
    min-height: 100px;
    resize: vertical;
    margin-bottom: calc(var(--spacing-unit) * 1.25); /* 10px */
    font-family: inherit; /* Asegurar que use la fuente del body */
  }
  
  /* 5. Grupos de Botones */
  .button-group,
  .result-actions {
    display: flex;
    gap: var(--spacing-unit); /* 8px-10px de espacio */
  }
  
  /* Estilo base para TODOS los botones */
  button {
    border: none;
    border-radius: var(--border-radius-standard);
    cursor: pointer;
    transition: background-color 0.2s ease, opacity 0.2s ease;
    display: inline-flex;      /* Para alinear icono y texto */
    align-items: center;       /* Centrar icono y texto verticalmente */
    justify-content: center;   /* Centrar contenido horizontalmente */
    gap: calc(var(--spacing-unit) * 0.6); /* 5px */
    font-size: inherit;        /* Usar tamaño de fuente base */
    color: var(--text-color-white); /* Texto blanco por defecto */
    line-height: 1.2;          /* Ajustar altura de línea para botones */
  }
  
  /* Estilo específico botones principales (Enviar, Limpiar) */
  .button-group button {
    padding: var(--button-padding-y) var(--button-padding-x);
    font-size: var(--base-font-size); /* 16px */
  }
  
  #executeBtn { background-color: var(--primary-color); }
  #executeBtn:hover:not(:disabled) { background-color: var(--primary-color-darker); }
  
  #clearBtn { background-color: var(--danger-color); }
  #clearBtn:hover:not(:disabled) { background-color: var(--danger-color-darker); }
  
  /* Deshabilitado para botones principales */
  .button-group button:disabled {
      background-color: var(--disabled-color);
      cursor: not-allowed;
      opacity: var(--disabled-opacity);
  }
  
  /* Estilo específico botones de acción (Copiar, Guardar) */
  .result-actions button {
    padding: var(--button-action-padding-y) var(--button-action-padding-x);
    font-size: calc(var(--base-font-size) - 2px); /* 14px */
  }
  
  #copyBtn { background-color: var(--info-color); }
  #copyBtn:hover:not(:disabled) { background-color: var(--info-color-darker); }
  
  #saveBtn { background-color: var(--success-color); }
  #saveBtn:hover:not(:disabled) { background-color: var(--success-color-darker); }
  
  /* Deshabilitado para botones de acción */
  .result-actions button:disabled {
    background-color: var(--secondary-color); /* Usar gris secundario */
    cursor: not-allowed;
    opacity: var(--disabled-opacity);
  }
  
  /* Iconos SVG dentro de botones */
  button svg {
    width: 1em;  /* Tamaño relativo al font-size del botón */
    height: 1em;
    vertical-align: middle; /* Ayuda a la alineación */
  }
  
  
  /* 6. Sección de Resultados */
  .result-container {
      margin-top: calc(var(--spacing-unit) * 4); /* 32px ~= 30px */
  }
  
  .result-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--spacing-unit); /* 8px */
    flex-wrap: wrap;
    gap: var(--spacing-unit); /* 8px */
  }
  
  .result-header h3 {
    margin: 0;
    padding: 0;
    color: var(--text-color-medium);
    border-bottom: none;
    flex-grow: 1;
    font-size: calc(var(--base-font-size) + 2px); /* Un poco más grande, ej. 18px */
  }
  
  .result-box {
    padding: calc(var(--spacing-unit) * 2); /* 16px ~= 15px */
    border: 1px solid var(--border-color-light);
    border-radius: var(--border-radius-standard);
    background-color: var(--background-color-result);
    min-height: 100px;
    white-space: pre-wrap;
    word-wrap: break-word;
    font-family: var(--font-family-mono);
    font-size: calc(var(--base-font-size) - 1px); /* 15px */
    overflow-x: auto;
  }
  
  /* >>> Reducción de espacio entre párrafos en el resultado <<< */
  .result-box p {
    margin-top: 0.5em;  /* Espacio reducido arriba */
    margin-bottom: 0.5em; /* Espacio reducido abajo */
  }
  /* Asegurarse que el primer párrafo no tenga margen superior y el último no tenga inferior */
  .result-box p:first-child {
      margin-top: 0;
  }
  .result-box p:last-child {
      margin-bottom: 0;
  }
  
  /* Estilos para bloques de código resaltados por PrismJS */
  pre[class*="language-"] {
    padding: 1em;
    margin: 1em 0; /* Mantener algo de margen vertical para bloques de código */
    overflow: auto;
    border-radius: var(--border-radius-standard);
    background: var(--background-color-code);
    color: var(--text-color-light);
  }
  
  code[class*="language-"] {
     font-family: var(--font-family-mono);
     /* El color suele venir del tema de Prism */
  }
  
  /* 7. Loading Spinner */
  .loading {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: var(--background-color-overlay);
    display: none; /* Cambiado a none por defecto, JS lo cambia a flex */
    justify-content: center;
    align-items: center;
    z-index: 1000;
    flex-direction: column;
    gap: var(--spacing-unit); /* 8px */
    color: var(--text-color-normal);
    font-size: 1.1em;
  }
  
  .spinner {
    border: 4px solid #f3f3f3; /* Mantener gris claro base */
    border-top: 4px solid var(--primary-color); /* Usar color primario para la parte giratoria */
    border-radius: 50%;
    width: 40px;
    height: 40px;
    animation: spin 1s linear infinite;
  }
  
  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
  
  
  /* 8. Media Queries para Responsividad */
  @media (max-width: 768px) {
    body {
      padding: var(--spacing-unit); /* 8px */
    }
  
    .container {
      padding: calc(var(--spacing-unit) * 2); /* 16px */
      margin: var(--spacing-unit) auto; /* 8px auto */
    }
  
    h1 {
       font-size: 1.8em; /* Reducir tamaño en móviles */
       margin-bottom: calc(var(--spacing-unit) * 3); /* 24px */
    }
  
    .button-group {
      flex-direction: column; /* Apilar botones principales */
      align-items: stretch; /* Hacer que ocupen el ancho */
    }
  
    .result-header {
      flex-direction: column; /* Apilar título y botones de acción */
      align-items: flex-start; /* Alinear todo a la izquierda */
    }
  
    .result-actions {
       width: 100%; /* Hacer que los botones de acción ocupen el ancho */
       justify-content: flex-start; /* Alinear botones a la izquierda */
    }
  
    .result-box {
       font-size: calc(var(--base-font-size) - 2px); /* Reducir fuente ligeramente en móvil ej 14px */
    }
  }
  
  @media (max-width: 480px) {
      h1 {
          font-size: 1.5em;
      }
      /* Ajustes adicionales para pantallas muy pequeñas si son necesarios */
  }
```

### 🔧 `api/generate.js`

```javascript
// api/generate.js
// Carga las variables de entorno del archivo .env (solo para desarrollo local)
require('dotenv').config();

const axios = require('axios');

// Middleware simple para CORS (permitir peticiones desde el navegador)
const allowCors = (fn) => async (req, res) => {
  res.setHeader('Access-Control-Allow-Credentials', true);
  res.setHeader('Access-Control-Allow-Origin', '*'); // Permite cualquier origen (para desarrollo)
  // O especifica tu origen local: res.setHeader('Access-Control-Allow-Origin', 'http://localhost:3000');
  res.setHeader('Access-Control-Allow-Methods', 'POST, OPTIONS');
  res.setHeader('Access-Control-Allow-Headers', 'X-CSRF-Token, X-Requested-With, Accept, Accept-Version, Content-Length, Content-MD5, Content-Type, Date, X-Api-Version');

  // Manejar petición OPTIONS (preflight)
  if (req.method === 'OPTIONS') {
    res.status(200).end();
    return;
  }
  // Ejecutar la función principal
  return await fn(req, res);
};

// La función principal que maneja la petición
const handler = async (req, res) => {
  // 1. Verificar que sea método POST
  if (req.method !== 'POST') {
    res.setHeader('Allow', ['POST']);
    return res.status(405).json({ error: 'Método no permitido' });
  }

  // 2. Obtener el prompt del cuerpo de la petición
  const { prompt } = req.body;

  if (!prompt) {
    return res.status(400).json({ error: 'El campo "prompt" es requerido.' });
  }

  // 3. Obtener la API Key de las variables de entorno
  const apiKey = process.env.GOOGLE_API_KEY;

  if (!apiKey) {
    console.error('Error: GOOGLE_API_KEY no está configurada.');
    // No reveles detalles de la API Key al cliente
    return res.status(500).json({ error: 'Error de configuración del servidor.' });
  }

  // 4. Definir la URL de la API de Google Gemini
  // Usa un modelo reciente como 'gemini-1.5-flash-latest'
  const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash-latest:generateContent?key=${apiKey}`;

  try {
    // 5. Realizar la llamada a la API de Google
    const response = await axios.post(apiUrl, {
      // El cuerpo esperado por la API de Gemini
      contents: [{
        parts: [{ text: prompt }]
      }],
      // Opcional: Configuración de generación (ej. para controlar la salida)
      // generationConfig: {
      //   temperature: 0.7,
      //   maxOutputTokens: 2048,
      // }
    }, {
      headers: {
        'Content-Type': 'application/json',
      }
    });

    // 6. Enviar la respuesta de Google de vuelta al frontend
    return res.status(200).json(response.data);

  } catch (error) {
    // 7. Manejar errores de la llamada a la API
    console.error('Error al llamar a la API de Google:', error.response ? error.response.data : error.message);

    // Construir un mensaje de error útil para el frontend
    const statusCode = error.response?.status || 500;
    const errorMessage = error.response?.data?.error?.message || 'Error interno al procesar la consulta con la IA.';

    return res.status(statusCode).json({ error: errorMessage });
  }
};

// Exportar el handler envuelto en el middleware CORS
module.exports = allowCors(handler);
```

---

### 🔐 `.env`

```env
# Pega tu clave API de Google aquí SIN comillas ni espacios extra
GOOGLE_API_KEY=AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

> ⚠️ Este archivo NO debe subirse a GitHub. Asegúrate de incluirlo en `.gitignore`.

---

### 🚫 `.gitignore`

```gitignore
# Dependencias de Node.js
node_modules

# Archivo de variables de entorno local (¡MUY IMPORTANTE!)
.env

# Archivos de sistema operativo
.DS_Store
Thumbs.db

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*
*.log

# Archivos de configuración de Vercel local
.vercel
```

---
## Dependencias 
1. Inicializa npm (crea package.json)
La opción -y acepta todas las configuraciones por defecto
npm init -y

2. Instala las dependencias necesarias (axios, cors, dotenv)
npm install axios cors dotenv

## ☁️ Despliegue en Vercel

1. Inicia sesión:
   ```bash
   vercel login
   ```

2. Ejecuta:
   ```bash
   vercel deploy --prod
   ```

3. Sigue las instrucciones para desplegar tu proyecto. Recibirás una URL pública.

---

## 🧪 Preguntas Frecuentes (FAQ)

### ❓ ¿Dónde consigo la API Key de Gemini?

- Desde: [Google AI Studio](https://makersuite.google.com/app/apikey)

### ❓ ¿Por qué no funciona mi API?

- Verifica el contenido del archivo `.env`
- Asegúrate de que tu cuenta tenga acceso a Gemini
- Reinicia Vercel local: `vercel dev`

### ❓ ¿Puedo publicar esto?

Sí, solo asegúrate de no subir el archivo `.env` a GitHub.

---

## 👨‍💻 Autor

**Julio David**  
Proyecto educativo de demostración para usar IA en aplicaciones web.

## Creditos

**Junacito P. MI MAESTRO😎**
---

## 📄 Licencia

Este proyecto está bajo la licencia MIT.  
Puedes usarlo, modificarlo y compartirlo libremente.

---
