# 📈 IA Trend Analyzer
> Powered by Claude claude-opus-4-8 · Anthropic MCP Hackathon

Es una app web con chat en lenguaje natural donde subes cualquier dataset (o la IA lo busca por ti) y Claude lo analiza automáticamente gener…IA Trend Analyzer es una app web con chat en lenguaje natural donde subes cualquier dataset (o la IA lo busca por ti) y Claude lo analiza automáticamente generando gráficas y reportes ejecutivos


## 🗂 Archivos del proyecto

```
ia-trend-analyzer/
├── .env              ← 🔑 Pon aquí tu API Key de Anthropic
├── backend.ipynb     ← 🧠 Backend Flask completo (1 sola celda)
├── frontend.html     ← 🖥  Interfaz web del chat
└── README.md         ← 📖 Este archivo
```

---

## ⚡ Cómo correr el proyecto

### Paso 1 — Pega tu API Key en `.env`
Abre `.env` y reemplaza la línea:
```
ANTHROPIC_API_KEY=sk-ant-XXXXXXX...
```
con tu key real de https://console.anthropic.com/settings/keys

### Paso 2 — Instala las dependencias
Abre la terminal en VS Code y corre **uno por uno**:
```bash
/opt/homebrew/bin/python3 -m pip install flask --break-system-packages
/opt/homebrew/bin/python3 -m pip install flask-cors --break-system-packages
/opt/homebrew/bin/python3 -m pip install anthropic --break-system-packages
/opt/homebrew/bin/python3 -m pip install pandas --break-system-packages
/opt/homebrew/bin/python3 -m pip install openpyxl --break-system-packages
/opt/homebrew/bin/python3 -m pip install google-api-python-client --break-system-packages
/opt/homebrew/bin/python3 -m pip install google-auth-httplib2 --break-system-packages
/opt/homebrew/bin/python3 -m pip install google-auth-oauthlib --break-system-packages
/opt/homebrew/bin/python3 -m pip install python-dotenv --break-system-packages
```

### Paso 3 — Corre el backend
1. Abre `backend.ipynb` en VS Code
2. Selecciona el kernel de Python (esquina superior derecha)
3. Haz clic en **▶ Run Cell** (la celda única)
4. Verás en el output: `🚀 IA Trend Analyzer corriendo en http://localhost:5000`

### Paso 4 — Abre el frontend
- Haz doble clic en `frontend.html` desde el Finder
- O click derecho → *Open with Live Server* si tienes esa extensión

---

## 🎯 Flujo de uso

```
Sube CSV  ──►  Claude confirma datos  ──►  Chat en lenguaje natural
                                                    │
                              ┌─────────────────────┘
                              ▼
                    Análisis + 2 gráficas automáticas
                              │
                    "Genera un reporte"
                              │
                              ▼
                    Google Drive Docs ← Reporte ejecutivo completo
```

---

## 💡 SKILL integrada: Análisis en Lenguaje Natural

La skill principal está en `backend.ipynb`, en la función `ask_claude()` y los `system_prompt` de cada endpoint.

### Sistema de prompts (3 niveles)

**1. Chat conversacional** (`/chat`)
```python
system_prompt = """Eres IA Trend Analyzer, analista de datos experto.
Habla en el idioma del usuario. Usa **negrillas** para métricas.
DATASET ACTUAL: {dataset_summary}"""
```

**2. Generación de reportes** (`/generate_report`)
```
1. RESUMEN EJECUTIVO
2. MÉTRICAS CLAVE (≥5 con valores reales)
3. MEJOR RENDIMIENTO
4. TENDENCIAS
5. PROYECCIONES
6. RECOMENDACIONES
```

**3. Generación de gráficas** (`extract_chart_data`)
```
Claude decide automáticamente qué tipo de gráfica
usar según el contexto del análisis → JSON → Chart.js
```

### Ejemplos de preguntas que maneja

| Pregunta | Acción |
|----------|--------|
| `¿Cuál fue el mejor mes?` | Agrupa por fecha, encuentra máximo |
| `¿Qué producto rinde mejor?` | Compara categorías |
| `Dame proyecciones para Q4` | Estimación con tendencia |
| `Busca datos de ventas retail` | Genera dataset con Claude |
| `Genera un reporte completo` | Pipeline completo → Google Drive |

---

## 🔧 Configurar Google Drive (para guardar reportes)

1. Ve a https://console.cloud.google.com
2. Crea un proyecto nuevo
3. Activa **Google Drive API** + **Google Docs API**
4. Crea credenciales → OAuth 2.0 → Desktop App
5. Descarga el JSON → guárdalo como `credentials.json` en esta carpeta
6. La primera vez que generes un reporte, se abrirá el navegador para autenticarte

> Sin `credentials.json` el chat y análisis funcionan igual, solo falla el guardado en Drive.

---

*Desarrollado para Anthropic MCP Hackathon · El Salvador 🇸🇻*
