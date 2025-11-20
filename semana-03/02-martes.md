# 📚 AI-900 | SEMANA 3 - MARTES 19 NOV

## 🔷 Azure AI Vision Service

---

## 🎯 OBJETIVOS DEL DÍA

Al finalizar hoy, serás capaz de:

- ✅ Explicar qué es Azure AI Vision y sus capacidades principales
- ✅ Diferenciar entre los distintos servicios de visión de Azure
- ✅ Identificar cuándo usar cada servicio según el caso de uso
- ✅ Entender las características de OCR (Optical Character Recognition)
- ✅ Conocer las capacidades de Face API
- ✅ Comprender las limitaciones y consideraciones de uso responsable

**Tiempo estimado:** 1.5 horas  
**Nivel de dificultad:** ⭐⭐⭐⚪⚪ (Media)

---

## 📖 PARTE 1: ¿QUÉ ES AZURE AI VISION? (20 min)

### 🔷 Definición

**Azure AI Vision** (anteriormente llamado Computer Vision API) es un **servicio cloud de Microsoft** que proporciona capacidades de Computer Vision mediante APIs, sin necesidad de entrenar modelos propios.

```
TÚ sin Azure AI Vision:
1. Conseguir dataset de imágenes (miles)
2. Etiquetar manualmente (semanas de trabajo)
3. Entrenar modelo de CNN (días/semanas)
4. Optimizar y ajustar
5. Desplegar en producción
= Meses de trabajo + infraestructura costosa

TÚ con Azure AI Vision:
1. Llamar a la API con tu imagen
2. Recibir resultados
= Minutos ⚡
```

### 🎯 Filosofía: Computer Vision as a Service

```
┌─────────────────────────────────────┐
│     TU APLICACIÓN                   │
│  (Web, Mobile, Desktop)             │
└────────────┬────────────────────────┘
             │ Envía imagen
             ↓
┌─────────────────────────────────────┐
│   AZURE AI VISION (Cloud)           │
│                                     │
│  - Modelos pre-entrenados           │
│  - Infraestructura escalable        │
│  - APIs listas para usar            │
└────────────┬────────────────────────┘
             │ Devuelve análisis
             ↓
┌─────────────────────────────────────┐
│     TU APLICACIÓN                   │
│  Muestra resultados al usuario      │
└─────────────────────────────────────┘
```

---

## 📖 PARTE 2: CAPACIDADES PRINCIPALES DE AZURE AI VISION (40 min)

### 1️⃣ IMAGE ANALYSIS (Análisis de Imágenes)

**¿Qué hace?**
Analiza el contenido visual de una imagen y proporciona información estructurada.

#### 📋 Características detectadas:

```
📷 INPUT: Imagen de una playa

🤖 OUTPUT de Azure AI Vision:

{
  "tags": ["playa", "arena", "mar", "cielo", "personas"],
  "description": "Personas en una playa con arena y mar azul",
  "categories": ["outdoor_beach"],
  "color": {
    "dominantColorForeground": "Blue",
    "dominantColorBackground": "Yellow",
    "accentColor": "#3B7FDB"
  },
  "objects": [
    {"object": "persona", "confidence": 0.92, "rectangle": {...}},
    {"object": "sombrilla", "confidence": 0.87, "rectangle": {...}}
  ],
  "faces": [
    {"age": 25, "gender": "female", "faceRectangle": {...}}
  ]
}
```

#### 🔍 Capacidades específicas:

| Capacidad            | Descripción                        | Ejemplo                                   |
| -------------------- | ---------------------------------- | ----------------------------------------- |
| **Tagging**          | Etiquetas de contenido             | "perro", "exterior", "hierba"             |
| **Description**      | Descripción en lenguaje natural    | "Un perro marrón jugando en el parque"    |
| **Categories**       | Categorización de escena           | "outdoor_park", "indoor_office"           |
| **Object Detection** | Detectar y localizar objetos       | Coche en (x:100, y:200, w:80, h:60)       |
| **Faces**            | Detectar rostros (sin identificar) | Rostro en coordenadas, edad aprox, género |
| **Color Analysis**   | Análisis de colores                | Colores dominantes, acento, B/N           |
| **Image Type**       | Tipo de imagen                     | Clip art, foto, dibujo lineal             |
| **Adult Content**    | Contenido adulto/violento          | Flags: isAdultContent, isRacyContent      |

---

### 2️⃣ OPTICAL CHARACTER RECOGNITION (OCR)

**¿Qué hace?**
Extrae **texto** de imágenes y documentos.

#### 📄 Dos APIs principales:

##### **A) Read API** (Recomendada - moderna)

```
✅ IDEAL PARA:
- Documentos con mucho texto
- Documentos escaneados
- Imágenes con texto complejo
- PDFs
- Múltiples idiomas
- Texto manuscrito (limitado)

📊 CARACTERÍSTICAS:
- Asíncrono (para documentos grandes)
- Mejor precisión
- Optimizado para documentos
- Devuelve líneas de texto completas
```

**Ejemplo de uso:**

```
📷 INPUT: Foto de un libro

🤖 OUTPUT:
{
  "status": "succeeded",
  "analyzeResult": {
    "readResults": [
      {
        "page": 1,
        "lines": [
          {
            "text": "Capítulo 1: Introducción",
            "boundingBox": [120, 50, 400, 50, 400, 80, 120, 80]
          },
          {
            "text": "La inteligencia artificial es...",
            "boundingBox": [120, 100, 500, 100, 500, 130, 120, 130]
          }
        ]
      }
    ]
  }
}
```

##### **B) OCR API** (Legacy - antigua)

```
⚠️ LIMITACIONES:
- Síncrona (respuesta inmediata pero limitada)
- Menos precisa que Read API
- Solo texto impreso (no manuscrito)
- Mejor para textos cortos

🔄 STATUS: Microsoft recomienda migrar a Read API
```

#### 🌍 Idiomas soportados:

- **Read API:** 160+ idiomas (incluyendo español, inglés, chino, árabe, etc.)
- Detección automática de idioma
- Mezcla de idiomas en el mismo documento

---

### 3️⃣ SPATIAL ANALYSIS (Análisis Espacial)

**¿Qué hace?**
Analiza **video en tiempo real** para entender movimiento de personas en espacios físicos.

```
📹 INPUT: Stream de video de una tienda

🤖 ANÁLISIS:
- ¿Cuántas personas hay?
- ¿Dónde están ubicadas?
- ¿Están manteniendo distancia social?
- ¿Cuántas personas cruzaron una línea?
- ¿Cuánto tiempo permanecen en un área?
```

#### 🎯 Casos de uso:

| Industria           | Aplicación                                    |
| ------------------- | --------------------------------------------- |
| 🛒 Retail           | Análisis de tráfico en tienda, colas en cajas |
| 🏥 Salud            | Monitoreo de distanciamiento social           |
| 🏭 Manufactura      | Seguridad en zonas de trabajo                 |
| 🅿️ Estacionamientos | Conteo de vehículos disponibles               |
| 🏢 Oficinas         | Ocupación de salas de reuniones               |

#### ⚠️ Consideraciones importantes:

- Requiere **Azure IoT Edge** (procesamiento en el borde)
- **NO identifica individuos** (privacidad)
- Solo detecta y cuenta personas de forma anónima

---

### 4️⃣ IMAGE GENERATION (Generación de Imágenes)

**¿Qué hace?**
Genera imágenes a partir de descripciones de texto usando **DALL-E** (IA generativa).

```
💬 INPUT (texto): "Un gato astronauta en el espacio, estilo cartoon"

🎨 OUTPUT: Imagen generada
```

#### Características:

- Basado en DALL-E de OpenAI
- Integrado en Azure AI Vision
- Útil para contenido creativo, prototipos, marketing

**Nota:** Esto es IA generativa, tema de Semana 5 del roadmap.

---

## 📖 PARTE 3: OTROS SERVICIOS RELACIONADOS (25 min)

### 🆚 Azure AI Vision vs Face API vs Custom Vision

#### 🔷 **AZURE AI VISION**

```
¿QUÉ ES?
Servicio general de análisis de imágenes

¿CUÁNDO USAR?
- Análisis general de contenido
- Detectar objetos comunes
- Extraer texto (OCR)
- Análisis de color, categorías

MODELOS:
✅ Pre-entrenados
❌ NO personalizables

EJEMPLO:
"Analiza esta foto y dime qué hay en ella"
```

#### 👤 **FACE API**

```
¿QUÉ ES?
Servicio especializado en ROSTROS

¿CUÁNDO USAR?
- Detectar rostros y ubicación
- Atributos faciales (edad, emoción, accesorios)
- Verificación facial (¿es la misma persona?)
- Identificación facial (¿quién es esta persona?)

CAPACIDADES:
- Face Detection (detección)
- Face Verification (verificación 1:1)
- Face Identification (identificación 1:N)
- Detectar emociones (feliz, triste, enojado, etc.)
- Detectar accesorios (gafas, barba, maquillaje)

⚠️ USO RESPONSABLE:
- Limitaciones de acceso (requiere aprobación)
- Prohibido en ciertos casos de uso
- Cumplimiento de privacidad
```

**Ejemplo de Face API:**

```
📷 INPUT: Foto de una persona

🤖 OUTPUT:
{
  "faceId": "abc123...",
  "faceRectangle": {"left": 120, "top": 150, "width": 80, "height": 80},
  "faceAttributes": {
    "age": 28,
    "gender": "female",
    "emotion": {
      "happiness": 0.85,
      "sadness": 0.02,
      "neutral": 0.10,
      "anger": 0.01
    },
    "glasses": "ReadingGlasses",
    "facialHair": {
      "moustache": 0.0,
      "beard": 0.0
    }
  }
}
```

#### 🎨 **CUSTOM VISION**

```
¿QUÉ ES?
Servicio para entrenar MODELOS PERSONALIZADOS

¿CUÁNDO USAR?
- Necesitas detectar objetos ESPECÍFICOS de tu negocio
- Azure AI Vision no reconoce tus objetos
- Ejemplo: tipos específicos de productos, defectos en manufactura

PROCESO:
1. Subes tus propias imágenes
2. Etiquetas manualmente
3. Entrenas modelo personalizado
4. Usas el modelo vía API

MODELOS:
❌ NO pre-entrenados
✅ TÚ los entrenas

EJEMPLO:
"Detectar 10 tipos diferentes de piezas de mi fábrica"
```

---

### 📊 TABLA COMPARATIVA:

| Característica          | Azure AI Vision     | Face API         | Custom Vision       |
| ----------------------- | ------------------- | ---------------- | ------------------- |
| **Pre-entrenado**       | ✅ Sí               | ✅ Sí            | ❌ No (tú entrenas) |
| **Objetos generales**   | ✅ Excelente        | ❌ No            | ⚠️ Si los entrenas  |
| **Rostros**             | ⚠️ Detección básica | ✅ Especializado | ⚠️ No recomendado   |
| **OCR/Texto**           | ✅ Sí               | ❌ No            | ❌ No               |
| **Objetos específicos** | ❌ Solo comunes     | ❌ No            | ✅ Sí               |
| **Personalizable**      | ❌ No               | ❌ No            | ✅ Sí               |
| **Facilidad de uso**    | ⭐⭐⭐⭐⭐          | ⭐⭐⭐⭐⚪       | ⭐⭐⭐⚪⚪          |
| **Requiere datos**      | ❌ No               | ❌ No            | ✅ Sí (15-50+ imgs) |

---

## 📖 PARTE 4: CARACTERÍSTICAS TÉCNICAS Y CONSIDERACIONES (20 min)

### 🔧 Cómo usar Azure AI Vision

#### 1️⃣ **Crear recurso en Azure**

```
Azure Portal:
1. Crear recurso "Computer Vision" o "Azure AI services"
2. Elegir región (ej: East US, West Europe)
3. Elegir pricing tier (Free F0 o Paid S1)
4. Obtener:
   - Endpoint URL
   - API Key (para autenticación)
```

#### 2️⃣ **Llamar a la API**

**Ejemplo con REST API:**

```http
POST https://[region].api.cognitive.microsoft.com/vision/v3.2/analyze?visualFeatures=Tags,Description,Objects

Headers:
  Ocp-Apim-Subscription-Key: [tu-api-key]
  Content-Type: application/json

Body:
{
  "url": "https://ejemplo.com/imagen.jpg"
}
```

**Respuesta:**

```json
{
  "tags": [
    { "name": "perro", "confidence": 0.98 },
    { "name": "exterior", "confidence": 0.95 }
  ],
  "description": {
    "captions": [{ "text": "un perro marrón en un parque", "confidence": 0.89 }]
  },
  "objects": [
    {
      "object": "perro",
      "confidence": 0.92,
      "rectangle": { "x": 120, "y": 200, "w": 150, "h": 180 }
    }
  ]
}
```

---

### 💰 Pricing (Precios)

#### Free Tier (F0):

```
✅ INCLUYE:
- 20 llamadas/minuto
- 5,000 transacciones/mes

⚠️ LIMITACIONES:
- Menor throughput
- No SLA (acuerdo de nivel de servicio)
```

#### Standard Tier (S1):

```
💵 COSTOS (aproximados):
- $1 por 1,000 transacciones (0-1M)
- Descuentos por volumen

✅ INCLUYE:
- Mayor throughput
- SLA del 99.9%
- Mejor para producción
```

---

### ⚡ Límites y cuotas

| Límite              | Free (F0)                | Standard (S1)            |
| ------------------- | ------------------------ | ------------------------ |
| **Llamadas/minuto** | 20                       | 10 por segundo           |
| **Tamaño imagen**   | 6 MB                     | 6 MB                     |
| **Dimensiones**     | 50x50 a 16,000x16,000 px | 50x50 a 16,000x16,000 px |
| **Formatos**        | JPEG, PNG, GIF, BMP      | JPEG, PNG, GIF, BMP      |

---

### 🛡️ Consideraciones de seguridad y privacidad

#### 🔒 Seguridad:

```
✅ BUENAS PRÁCTICAS:
- Guardar API Keys en Azure Key Vault (NO en código)
- Usar Managed Identities cuando sea posible
- Rotar keys periódicamente
- Restringir acceso por IP (opcional)
```

#### 🕵️ Privacidad:

```
⚠️ IMPORTANTE:
- Microsoft NO almacena tus imágenes permanentemente
- Imágenes se procesan y descartan
- NO usar para vigilancia masiva sin consentimiento
- Cumplir con GDPR y regulaciones locales
```

---

### 🌍 Regiones y disponibilidad

**Regiones disponibles:**

- North America: East US, West US, Central US
- Europe: West Europe, North Europe
- Asia: Southeast Asia, East Asia
- Y más...

**Importante:** Elegir región cercana a tus usuarios para menor latencia.

---

## 📖 PARTE 5: CASOS DE USO REALES (15 min)

### 💼 Escenarios empresariales

#### 1️⃣ **E-commerce: Búsqueda visual de productos**

```
PROBLEMA:
Cliente ve un mueble que le gusta pero no sabe cómo buscarlo

SOLUCIÓN:
1. Cliente sube foto del mueble
2. Azure AI Vision analiza: "silla", "madera", "moderna"
3. Sistema busca productos similares
4. Muestra recomendaciones

SERVICIOS USADOS:
- Azure AI Vision (Image Analysis)
- Custom Vision (si tienes catálogo específico)
```

---

#### 2️⃣ **Manufactura: Control de calidad**

```
PROBLEMA:
Inspeccionar 1000 productos/hora manualmente es imposible

SOLUCIÓN:
1. Cámara toma foto de cada producto
2. Custom Vision detecta defectos
3. Productos defectuosos se separan automáticamente

SERVICIOS USADOS:
- Custom Vision (entrenado con fotos de defectos)
- Azure IoT Edge (procesamiento local)
```

---

#### 3️⃣ **Salud: Digitalización de documentos médicos**

```
PROBLEMA:
Miles de historiales médicos en papel

SOLUCIÓN:
1. Escanear documentos
2. Azure AI Vision (Read API) extrae texto
3. Guardar en base de datos
4. Texto buscable y accesible

SERVICIOS USADOS:
- Read API (OCR avanzado)
- Azure Search (para búsqueda de texto)
```

---

#### 4️⃣ **Retail: Análisis de comportamiento en tienda**

```
PROBLEMA:
¿Qué áreas de la tienda tienen más tráfico?

SOLUCIÓN:
1. Cámaras en puntos estratégicos
2. Spatial Analysis cuenta personas
3. Genera heatmaps de tráfico
4. Optimiza ubicación de productos

SERVICIOS USADOS:
- Spatial Analysis (video en tiempo real)
- Power BI (visualización de datos)
```

---

#### 5️⃣ **Banca: Verificación de identidad**

```
PROBLEMA:
Verificar identidad de clientes remotamente

SOLUCIÓN:
1. Cliente toma selfie
2. Cliente fotografía su ID
3. Face API verifica que coincidan
4. OCR extrae datos del ID

SERVICIOS USADOS:
- Face API (Face Verification)
- Read API (extraer texto del ID)
```

---

## 🎯 CONCEPTOS CLAVE PARA EL EXAMEN

### ⚡ Memoriza esto:

1. **Azure AI Vision** = Análisis general de imágenes (objetos, texto, colores, escenas)
2. **Read API** = OCR moderno y recomendado para extraer texto
3. **Face API** = Especializado en rostros (detección, verificación, identificación)
4. **Custom Vision** = Entrenar modelos personalizados con tus propias imágenes
5. **Spatial Analysis** = Análisis de video en tiempo real para conteo de personas
6. **Tagging** = Etiquetas automáticas de contenido
7. **Object Detection** = Detectar y localizar múltiples objetos
8. **Image Analysis** = Conjunto de capacidades (tags, descripción, objetos, colores)

---

### 📝 Preguntas típicas del examen:

**Pregunta:** "Una empresa necesita extraer texto de miles de documentos escaneados. ¿Qué API de Azure deben usar?"
**Respuesta:** Read API (optimizada para documentos con mucho texto)

**Pregunta:** "Un banco necesita verificar que la foto del cliente coincida con la foto de su identificación oficial. ¿Qué servicio usar?"
**Respuesta:** Face API con Face Verification (compara dos rostros)

**Pregunta:** "Una fábrica necesita detectar 5 tipos específicos de defectos en sus productos. Azure AI Vision no los reconoce. ¿Qué hacer?"
**Respuesta:** Usar Custom Vision para entrenar un modelo personalizado con imágenes de esos defectos específicos

**Pregunta:** "Una tienda quiere contar cuántas personas entran cada hora. ¿Qué servicio usar?"
**Respuesta:** Spatial Analysis (análisis de video en tiempo real)

---

## 🎴 FLASHCARDS (15 tarjetas)

### Tarjeta 1

**P:** ¿Qué es Azure AI Vision?  
**R:** Un servicio cloud de Microsoft que proporciona capacidades de Computer Vision mediante APIs, con modelos pre-entrenados listos para usar.

---

### Tarjeta 2

**P:** ¿Cuáles son las 4 capacidades principales de Azure AI Vision?  
**R:**

1. Image Analysis (análisis de imágenes)
2. OCR (extracción de texto)
3. Spatial Analysis (análisis de video)
4. Image Generation (generar imágenes con DALL-E)

---

### Tarjeta 3

**P:** ¿Qué información puede proporcionar Image Analysis?  
**R:** Tags (etiquetas), descripción en lenguaje natural, categorías, objetos detectados, rostros, colores dominantes, tipo de imagen, contenido adulto.

---

### Tarjeta 4

**P:** ¿Cuál es la diferencia entre Read API y OCR API?  
**R:**

- **Read API:** Moderna, asíncrona, mejor precisión, soporta manuscrito, ideal para documentos largos
- **OCR API:** Legacy, síncrona, solo texto impreso, para textos cortos

---

### Tarjeta 5

**P:** ¿Cuándo usar Azure AI Vision vs Custom Vision?  
**R:**

- **Azure AI Vision:** Objetos comunes (personas, coches, animales)
- **Custom Vision:** Objetos específicos de tu negocio que Azure no reconoce

---

### Tarjeta 6

**P:** ¿Qué hace Face API?  
**R:** Servicio especializado en rostros: detecta ubicación, atributos (edad, emoción), verifica identidad (1:1), identifica personas (1:N).

---

### Tarjeta 7

**P:** ¿Qué es Spatial Analysis?  
**R:** Capacidad de analizar video en tiempo real para contar personas, detectar movimiento, analizar tráfico en espacios físicos, sin identificar individuos.

---

### Tarjeta 8

**P:** Nombra 3 atributos que Face API puede detectar  
**R:**

1. Edad aproximada
2. Emoción (felicidad, tristeza, enojo, etc.)
3. Accesorios (gafas, maquillaje, barba)

---

### Tarjeta 9

**P:** ¿Cuál es el límite de llamadas en el Free Tier (F0) de Azure AI Vision?  
**R:** 20 llamadas por minuto, máximo 5,000 transacciones por mes.

---

### Tarjeta 10

**P:** ¿Qué necesitas para usar la API de Azure AI Vision?  
**R:**

1. Endpoint URL (región específica)
2. API Key (para autenticación)

---

### Tarjeta 11

**P:** ¿Cuántos idiomas soporta Read API?  
**R:** Más de 160 idiomas, con detección automática de idioma.

---

### Tarjeta 12

**P:** ¿Qué tamaño máximo de imagen soporta Azure AI Vision?  
**R:** 6 MB de tamaño, dimensiones entre 50x50 y 16,000x16,000 píxeles.

---

### Tarjeta 13

**P:** ¿Qué formatos de imagen soporta Azure AI Vision?  
**R:** JPEG, PNG, GIF, BMP

---

### Tarjeta 14

**P:** ¿Microsoft almacena las imágenes que envías a Azure AI Vision?  
**R:** No, las imágenes se procesan y se descartan. No se almacenan permanentemente.

---

### Tarjeta 15

**P:** ¿Cuál es la diferencia entre Face Verification y Face Identification?  
**R:**

- **Verification (1:1):** Verifica si dos rostros son de la misma persona
- **Identification (1:N):** Identifica quién es una persona comparando con un grupo de rostros conocidos

---

## ❓ PREGUNTAS DE AUTOEVALUACIÓN

### Pregunta 1 (Fácil)

**Una biblioteca quiere digitalizar miles de libros antiguos y hacerlos buscables. Necesitan extraer el texto de las páginas escaneadas. ¿Qué API deben usar?**

A) OCR API  
B) Read API  
C) Face API  
D) Custom Vision

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Read API**

**Explicación:** Read API es la solución moderna y recomendada para extraer texto de documentos, especialmente cuando hay mucho texto. Es asíncrona, más precisa, y está optimizada para documentos largos como páginas de libros.

</details>

---

### Pregunta 2 (Media)

**Una empresa de seguridad necesita un sistema que cuente cuántas personas hay en una sala de espera en tiempo real y alerte si se excede la capacidad máxima. NO necesitan identificar a las personas. ¿Qué servicio de Azure es más apropiado?**

A) Azure AI Vision con Object Detection  
B) Face API con Face Identification  
C) Spatial Analysis  
D) Custom Vision

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Spatial Analysis**

**Explicación:** Spatial Analysis está diseñado específicamente para analizar video en tiempo real, contar personas de forma anónima, y detectar si cruzan líneas o permanecen en áreas específicas. No identifica individuos, lo cual es perfecto para este caso de uso que respeta la privacidad.

</details>

---

### Pregunta 3 (Media)

**Un banco implementa un sistema de verificación de identidad. El cliente toma una selfie y una foto de su credencial de elector. El sistema debe: (1) extraer el nombre del documento, (2) verificar que el rostro de la selfie coincida con el de la credencial. ¿Qué servicios necesitan?**

A) Solo Azure AI Vision  
B) Solo Face API  
C) Read API + Face API  
D) Custom Vision + OCR API

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Read API + Face API**

**Explicación:**

- **Read API:** Para extraer el texto (nombre) de la credencial de elector (OCR)
- **Face API:** Para verificar que los dos rostros (selfie vs credencial) pertenecen a la misma persona (Face Verification 1:1)

Se necesitan ambos servicios para completar la tarea.

</details>

---

### Pregunta 4 (Difícil)

**Una empresa de e-commerce quiere implementar una función donde los clientes puedan subir una foto de un producto que vieron en la calle y encontrar productos similares en su catálogo. La empresa tiene 50,000 productos en 200 categorías únicas. ¿Qué estrategia es más apropiada?**

A) Usar solo Azure AI Vision con Object Detection  
B) Entrenar un modelo en Custom Vision con fotos de los 50,000 productos  
C) Usar Azure AI Vision para análisis general + Custom Vision para categorías específicas  
D) Usar Face API para reconocer productos

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Usar Azure AI Vision para análisis general + Custom Vision para categorías específicas**

**Explicación:**

- **Azure AI Vision** puede detectar características generales (colores, formas, categorías amplias como "mueble", "ropa")
- **Custom Vision** se entrena con las categorías específicas de la empresa (200 categorías)
- Esta combinación aprovecha lo mejor de ambos: el poder de los modelos pre-entrenados de Azure + la especialización de Custom Vision para productos específicos
- Entrenar con 50,000 productos sería excesivo; es mejor usar categorías y subcategorías

Face API es completamente inapropiado (es para rostros, no productos).

</details>

---

### Pregunta 5 (Media)

**¿Cuál de las siguientes afirmaciones sobre el Free Tier (F0) de Azure AI Vision es INCORRECTA?**

A) Permite 20 llamadas por minuto  
B) Incluye hasta 5,000 transacciones por mes  
C) Tiene las mismas capacidades funcionales que el Standard Tier  
D) Incluye SLA (acuerdo de nivel de servicio) del 99.9%

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: D) Incluye SLA (acuerdo de nivel de servicio) del 99.9%**

**Explicación:** El Free Tier (F0) NO incluye SLA. Solo el Standard Tier (S1) incluye SLA del 99.9%. El Free Tier tiene las mismas capacidades funcionales pero con límites de throughput y sin garantías de disponibilidad, por lo que no es recomendado para producción.

</details>

---

### Pregunta 6 (Fácil)

**Una fábrica de automóviles necesita detectar 8 tipos específicos de defectos en piezas metálicas. Estos defectos son únicos de su proceso de manufactura y Azure AI Vision no los reconoce. ¿Qué servicio deben usar?**

A) Azure AI Vision con Image Analysis  
B) Custom Vision  
C) Face API  
D) Read API

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Custom Vision**

**Explicación:** Custom Vision permite entrenar modelos personalizados con imágenes específicas de tu negocio. Como los defectos son únicos de esta fábrica y no son objetos comunes que Azure AI Vision reconozca, necesitan entrenar su propio modelo con imágenes de piezas defectuosas y no defectuosas.

</details>

---

### Pregunta 7 (Difícil - Estilo Microsoft)

**Scenario:** Una cadena de supermercados quiere optimizar la disposición de productos en sus tiendas. Necesitan:

1. Identificar qué pasillos tienen más tráfico de clientes
2. Medir cuánto tiempo los clientes pasan mirando ciertos productos
3. Detectar si hay productos mal ubicados o caídos en los estantes

¿Qué combinación de servicios sería óptima?

A) Solo Spatial Analysis para todo  
B) Spatial Analysis (tráfico) + Azure AI Vision (productos mal ubicados)  
C) Azure AI Vision (todo) + Face API (identificar clientes frecuentes)  
D) Custom Vision para entrenar detección de todos los productos

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Spatial Analysis (tráfico) + Azure AI Vision (productos mal ubicados)**

**Explicación:**

- **Spatial Analysis:** Perfecto para (1) analizar tráfico de personas en tiempo real y (2) medir cuánto tiempo permanecen en áreas específicas. No identifica individuos, solo los cuenta y rastrea de forma anónima.
- **Azure AI Vision:** Puede detectar objetos (productos) y sus orientaciones para (3) identificar productos caídos o mal ubicados mediante Object Detection.

La opción C es inapropiada porque Face API para identificar clientes frecuentes plantea serios problemas de privacidad y probablemente no estaría permitido sin consentimiento explícito. La opción D sería excesiva e innecesaria.

</details>

---

### Pregunta 8 (Media)

**¿Cuál de las siguientes tareas NO puede realizar Azure AI Vision directamente (sin usar otros servicios)?**

A) Detectar si una imagen contiene contenido adulto  
B) Extraer texto de un documento PDF de 50 páginas  
C) Entrenar un modelo para reconocer 10 especies específicas de plantas de tu jardín  
D) Generar una descripción en lenguaje natural de una foto

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Entrenar un modelo para reconocer 10 especies específicas de plantas de tu jardín**

**Explicación:** Azure AI Vision usa modelos pre-entrenados que NO puedes personalizar. Para entrenar modelos con tus propias categorías específicas (como especies de plantas específicas), necesitas usar **Custom Vision**, que es un servicio separado.

Las otras opciones SÍ son capacidades directas de Azure AI Vision:

- A) Adult Content detection (parte de Image Analysis)
- B) Read API para OCR de documentos largos
- D) Description generation (parte de Image Analysis)

</details>

---

## ✅ CHECKLIST DEL DÍA

Marca cada item al completarlo:

- [ ] Leí y entendí qué es Azure AI Vision
- [ ] Entiendo las capacidades de Image Analysis (tags, description, objects, etc.)
- [ ] Comprendo la diferencia entre Read API y OCR API
- [ ] Sé qué hace Face API y cuándo usarlo
- [ ] Entiendo qué es Custom Vision y cuándo es necesario
- [ ] Sé qué hace Spatial Analysis
- [ ] Puedo diferenciar cuándo usar cada servicio según el caso de uso
- [ ] Revisé las 15 flashcards
- [ ] Intenté las 8 preguntas de autoevaluación
- [ ] Entiendo consideraciones de pricing y privacidad

---

## 🎯 PREPARACIÓN PARA MAÑANA

**Miércoles 20 Nov: Face API y Custom Vision (Profundización)**

Mañana profundizaremos más en:

- Capacidades avanzadas de Face API
- Cómo funciona Custom Vision en detalle
- Proceso de entrenamiento de modelos personalizados

Asegúrate de entender bien hoy:

- La diferencia entre los 3 servicios principales (Vision, Face, Custom)
- Cuándo usar cada uno según el escenario

---

## 📚 RECURSOS DE MICROSOFT LEARN

### 🔗 Módulos recomendados para HOY:

1. **"Analyze images with the Azure AI Vision service"**
   - URL: https://learn.microsoft.com/training/modules/analyze-images-computer-vision/
   - Duración: 45 min
   - Nivel: Beginner

2. **"Read text in images and documents with the Azure AI Vision service"**
   - URL: https://learn.microsoft.com/training/modules/read-text-images-documents-with-computer-vision-service/
   - Duración: 38 min
   - Nivel: Beginner

3. **"Detect faces and facial attributes with Azure AI Face"**
   - URL: https://learn.microsoft.com/training/modules/detect-analyze-faces/
   - Duración: 30 min
   - Nivel: Beginner

### 📖 Documentación adicional:

- [Azure AI Vision overview](https://learn.microsoft.com/azure/ai-services/computer-vision/overview)
- [Face API documentation](https://learn.microsoft.com/azure/ai-services/computer-vision/overview-identity)
- [Custom Vision overview](https://learn.microsoft.com/azure/ai-services/custom-vision-service/overview)

---

## 📌 NOTAS IMPORTANTES

### 💡 Tips para el examen:

1. **Enfócate en CASOS DE USO:** El examen te dará escenarios y tendrás que elegir el servicio correcto
2. **Diferencia clave:**
   - Azure AI Vision = Objetos comunes + OCR
   - Face API = Solo rostros
   - Custom Vision = Objetos específicos (tú entrenas)
3. **Read API vs OCR API:** Siempre recomienda Read API (es la moderna)
4. **Privacidad:** Face API tiene restricciones de uso y requiere aprobación para ciertos casos

### 🎓 Conceptos críticos:

- **Image Analysis** proporciona tags, description, objects, colors, faces (básico)
- **Read API** es asíncrona y mejor para documentos largos
- **Spatial Analysis** es para video en tiempo real, NO para imágenes estáticas
- **Custom Vision** requiere que TÚ proporciones y etiquetes las imágenes de entrenamiento
- **Face Verification** = comparar 2 rostros (1:1)
- **Face Identification** = identificar quién es alguien en un grupo (1:N)

---

## 🔗 CONEXIÓN CON EL DÍA ANTERIOR

**Ayer aprendiste:**

- Conceptos fundamentales de Computer Vision
- Classification, Object Detection, Segmentation
- Cómo funcionan las CNNs

**Hoy aprendiste:**

- Cómo AZURE implementa esos conceptos en servicios cloud
- Qué servicio usar según el caso de uso
- Diferencias entre Vision, Face y Custom Vision

**Mañana aprenderás:**

- Detalles técnicos de Face API
- Cómo entrenar modelos en Custom Vision paso a paso

---

**🎉 ¡Excelente progreso! Ya dominas los servicios principales de Computer Vision en Azure.**

**Siguiente sesión:** Miércoles 20 Nov - Face API y Custom Vision (Deep Dive)

---

_Documento creado: Martes 19 de Noviembre, 2025_  
_Roadmap: Semana 3 de 6 | AI-900 Certification Prep_
