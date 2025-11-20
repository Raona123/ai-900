# 📚 AI-900 | SEMANA 3 - MIÉRCOLES 20 NOV

## 👤🎨 Face API y Custom Vision (Deep Dive)

---

## 🎯 OBJETIVOS DEL DÍA

Al finalizar hoy, serás capaz de:

- ✅ Explicar en detalle las capacidades de Face API
- ✅ Diferenciar entre Face Detection, Verification e Identification
- ✅ Entender el proceso completo de Custom Vision
- ✅ Saber cuándo y cómo entrenar modelos personalizados
- ✅ Conocer las consideraciones éticas y de uso responsable de IA
- ✅ Identificar casos de uso apropiados para cada servicio

**Tiempo estimado:** 1.5 horas  
**Nivel de dificultad:** ⭐⭐⭐⭐⚪ (Media-Alta)

---

## 📖 PARTE 1: FACE API EN PROFUNDIDAD (45 min)

### 👤 ¿Qué es Face API?

**Face API** es un servicio de Azure especializado en **detectar, analizar, verificar e identificar rostros humanos** en imágenes.

```
AZURE AI VISION dice:
"Hay un rostro en esta imagen"

FACE API dice:
"Hay un rostro en (x:120, y:150), es una mujer de ~28 años,
sonriendo (85% feliz), usa gafas de lectura, sin barba,
con maquillaje ligero"
```

---

### 🔍 CAPACIDAD 1: FACE DETECTION (Detección de Rostros)

**¿Qué hace?**
Detecta **dónde están los rostros** en una imagen y proporciona **atributos faciales**.

#### 📊 Información que devuelve:

```json
{
  "faceId": "abc123-456def-789ghi", // ID único temporal (24h)
  "faceRectangle": {
    "left": 120,
    "top": 150,
    "width": 80,
    "height": 80
  },
  "faceLandmarks": {
    // Puntos clave del rostro (opcional)
    "pupilLeft": { "x": 140, "y": 170 },
    "pupilRight": { "x": 170, "y": 170 },
    "noseTip": { "x": 155, "y": 185 },
    "mouthLeft": { "x": 140, "y": 200 },
    "mouthRight": { "x": 170, "y": 200 }
  },
  "faceAttributes": {
    "age": 28,
    "gender": "female",
    "smile": 0.85,
    "facialHair": {
      "moustache": 0.0,
      "beard": 0.0,
      "sideburns": 0.0
    },
    "glasses": "ReadingGlasses", // NoGlasses, ReadingGlasses, Sunglasses, SwimmingGoggles
    "emotion": {
      "happiness": 0.85,
      "sadness": 0.02,
      "neutral": 0.1,
      "anger": 0.01,
      "contempt": 0.01,
      "disgust": 0.0,
      "fear": 0.0,
      "surprise": 0.01
    },
    "makeup": {
      "eyeMakeup": true,
      "lipMakeup": true
    },
    "accessories": [{ "type": "glasses", "confidence": 0.98 }],
    "hair": {
      "bald": 0.05,
      "invisible": false,
      "hairColor": [
        { "color": "brown", "confidence": 0.9 },
        { "color": "black", "confidence": 0.8 }
      ]
    },
    "headPose": {
      "roll": 0.5, // Inclinación lateral
      "yaw": -10.2, // Rotación izquierda/derecha
      "pitch": 5.3 // Inclinación arriba/abajo
    },
    "occlusion": {
      "foreheadOccluded": false,
      "eyeOccluded": false,
      "mouthOccluded": false
    },
    "blur": {
      "blurLevel": "low", // low, medium, high
      "value": 0.15
    },
    "exposure": {
      "exposureLevel": "goodExposure", // underExposure, goodExposure, overExposure
      "value": 0.65
    },
    "noise": {
      "noiseLevel": "low",
      "value": 0.1
    }
  }
}
```

#### 🎯 Atributos importantes:

| Atributo       | Valores posibles                | Uso típico                          |
| -------------- | ------------------------------- | ----------------------------------- |
| **age**        | 0-100 (estimado)                | Restricción de edad, estadísticas   |
| **gender**     | male, female                    | Personalización, estadísticas       |
| **emotion**    | 8 emociones (0-1)               | Análisis de sentimiento, UX         |
| **glasses**    | None, Reading, Sun, Swimming    | Control de acceso, verificación     |
| **facialHair** | 0-1 (barba, bigote, patillas)   | Descripción, búsqueda               |
| **makeup**     | true/false (ojos, labios)       | Análisis de belleza                 |
| **headPose**   | roll, yaw, pitch (-180 a 180)   | Calidad de foto, alerta de atención |
| **blur**       | low, medium, high               | Control de calidad de imagen        |
| **occlusion**  | true/false (frente, ojos, boca) | Calidad de foto, seguridad          |

---

### 🔐 CAPACIDAD 2: FACE VERIFICATION (Verificación 1:1)

**¿Qué hace?**
Verifica si **dos rostros pertenecen a la misma persona**.

#### 💡 Caso de uso típico:

```
ESCENARIO: Login con reconocimiento facial

1. Usuario registrado toma foto (Foto A)
2. Sistema guarda faceId de Foto A
3. Usuario intenta hacer login con nueva selfie (Foto B)
4. Face Verification compara Foto A vs Foto B
5. Resultado: ¿Son la misma persona?
```

#### 📊 Respuesta de la API:

```json
{
  "isIdentical": true, // ¿Son la misma persona?
  "confidence": 0.87 // Nivel de confianza (0-1)
}
```

#### 🎚️ Umbral de confianza:

```
Confianza > 0.5  → Probablemente la misma persona
Confianza > 0.7  → Muy probablemente la misma persona
Confianza > 0.9  → Casi seguro que es la misma persona

IMPORTANTE: TÚ decides el umbral según tu caso de uso
- Alto umbral (0.9): Más seguro, pero más falsos negativos
- Bajo umbral (0.6): Más flexible, pero más falsos positivos
```

#### 🔄 Proceso completo:

```
┌─────────────────────────────────────┐
│ PASO 1: Registrar usuario          │
│                                     │
│ 📷 Usuario toma foto de registro   │
│     ↓                               │
│ 🔍 Face API detecta rostro          │
│     ↓                               │
│ 💾 Guarda faceId: "abc123"          │
└─────────────────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│ PASO 2: Login posterior            │
│                                     │
│ 📷 Usuario toma nueva selfie        │
│     ↓                               │
│ 🔍 Face API detecta nuevo rostro    │
│     ↓                               │
│ 🆚 Compara nuevo faceId vs "abc123" │
│     ↓                               │
│ ✅ Confidence: 0.89 → Acceso OK     │
└─────────────────────────────────────┘
```

---

### 🎯 CAPACIDAD 3: FACE IDENTIFICATION (Identificación 1:N)

**¿Qué hace?**
Identifica **quién es una persona** comparando contra un grupo de rostros conocidos.

#### 💡 Caso de uso típico:

```
ESCENARIO: Control de acceso en oficina

Person Group: "Empleados de la empresa"
- Persona 1: Juan (faceId: aaa111)
- Persona 2: María (faceId: bbb222)
- Persona 3: Pedro (faceId: ccc333)
- ... (hasta 10,000 personas)

1. Cámara captura rostro en entrada
2. Face Identification busca en el Person Group
3. Resultado: "Es María con 92% confianza"
4. Puerta se abre automáticamente
```

#### 🏗️ Estructura de datos:

```
PERSON GROUP
│
├── Person 1: "Juan Pérez"
│   ├── Face 1 (frontal)
│   ├── Face 2 (perfil izquierdo)
│   ├── Face 3 (perfil derecho)
│   └── Face 4 (con gafas)
│
├── Person 2: "María García"
│   ├── Face 1 (sonriendo)
│   ├── Face 2 (seria)
│   └── Face 3 (con sombrero)
│
└── Person 3: "Pedro López"
    ├── Face 1 (foto de perfil)
    └── Face 2 (foto casual)
```

#### 📊 Respuesta de la API:

```json
{
  "candidates": [
    {
      "personId": "person-maria-123",
      "faceId": "bbb222",
      "confidence": 0.92
    },
    {
      "personId": "person-lucia-456",
      "faceId": "ddd444",
      "confidence": 0.32 // Segunda opción menos probable
    }
  ]
}
```

#### 🔢 Límites:

| Tier              | Max Person Groups | Max Personas por Group | Max Faces por Persona |
| ----------------- | ----------------- | ---------------------- | --------------------- |
| **Free (F0)**     | 1,000             | 1,000                  | 248                   |
| **Standard (S0)** | 1,000,000         | 10,000                 | 248                   |

---

### 📊 COMPARACIÓN: Detection vs Verification vs Identification

| Característica        | Detection             | Verification                  | Identification                 |
| --------------------- | --------------------- | ----------------------------- | ------------------------------ |
| **Pregunta**          | ¿Hay rostros?         | ¿Son la misma persona?        | ¿Quién es?                     |
| **Input**             | 1 imagen              | 2 rostros (faceIds)           | 1 rostro + Person Group        |
| **Output**            | Atributos faciales    | isIdentical + confidence      | personId + confidence          |
| **Comparación**       | No compara            | 1:1                           | 1:N                            |
| **Requiere registro** | ❌ No                 | ❌ No                         | ✅ Sí (Person Group)           |
| **Uso típico**        | Análisis demográfico  | Login facial, verificación ID | Control de acceso, búsqueda    |
| **Privacidad**        | 🟢 Baja (no almacena) | 🟡 Media                      | 🔴 Alta (almacena identidades) |

---

### ⚠️ CONSIDERACIONES DE USO RESPONSABLE

#### 🚫 Restricciones de acceso:

```
⚠️ IMPORTANTE: Face API tiene acceso limitado

Face API NO está disponible libremente para todos.
Microsoft requiere APROBACIÓN para:
- Face Identification
- Casos de uso sensibles

PROCESO:
1. Aplicar para acceso
2. Describir caso de uso
3. Microsoft revisa y aprueba/rechaza
4. Solo entonces puedes usar ciertas funcionalidades
```

#### 🛡️ Usos PROHIBIDOS:

❌ **NO permitido:**

- Vigilancia masiva sin consentimiento
- Discriminación basada en atributos faciales
- Inferir emociones en contextos de empleo o educación
- Sistemas de crédito social
- Identificación de menores sin consentimiento parental
- Aplicaciones policiales sin transparencia

✅ **Permitido (con aprobación):**

- Verificación de identidad en banca (con consentimiento)
- Control de acceso en empresas (empleados informados)
- Búsqueda de personas desaparecidas (con autoridad legal)
- Personalización de experiencias (con opt-in explícito)

#### 🔒 Mejores prácticas:

```
1. ✅ TRANSPARENCIA: Informar a usuarios que se usa reconocimiento facial
2. ✅ CONSENTIMIENTO: Obtener permiso explícito
3. ✅ PROPÓSITO LIMITADO: Solo para el propósito declarado
4. ✅ SEGURIDAD: Proteger datos biométricos
5. ✅ RETENCIÓN LIMITADA: faceIds expiran en 24h (no almacenar indefinidamente)
6. ✅ NO INFERIR: No asumir emociones = estados mentales
7. ✅ DIVERSIDAD: Probar con diferentes demografías
```

---

## 📖 PARTE 2: CUSTOM VISION EN PROFUNDIDAD (45 min)

### 🎨 ¿Qué es Custom Vision?

**Custom Vision** es un servicio que te permite **entrenar modelos de Computer Vision personalizados** sin necesidad de experiencia en Machine Learning.

```
PROBLEMA:
"Necesito detectar 5 tipos específicos de defectos en mis productos,
pero Azure AI Vision no los reconoce"

SOLUCIÓN:
Custom Vision → Tú subes imágenes + etiquetas = Modelo entrenado
```

---

### 🆚 ¿Cuándo usar Custom Vision?

#### ✅ USA Custom Vision cuando:

```
1. Objetos ESPECÍFICOS de tu negocio
   Ejemplo: Detectar 10 modelos de tornillos de tu fábrica

2. Categorías MUY ESPECÍFICAS
   Ejemplo: Distinguir entre 20 especies de orquídeas

3. Azure AI Vision no reconoce tus objetos
   Ejemplo: Piezas de maquinaria especializadas

4. Necesitas alta precisión en dominio específico
   Ejemplo: Detectar tipos específicos de células en microscopía
```

#### ❌ NO uses Custom Vision cuando:

```
1. Objetos COMUNES que Azure AI Vision ya reconoce
   Ejemplo: personas, coches, perros, gatos → Usa Azure AI Vision

2. Solo necesitas OCR
   Ejemplo: Extraer texto de documentos → Usa Read API

3. Análisis de ROSTROS
   Ejemplo: Detectar emociones → Usa Face API

4. Muy pocas imágenes de entrenamiento (<15 por categoría)
   Resultado: Modelo con overfitting, baja precisión
```

---

### 🎯 DOS TIPOS DE PROYECTOS

#### 1️⃣ IMAGE CLASSIFICATION

**¿Qué hace?**
Asigna **una etiqueta** a cada imagen completa.

```
INPUT: Foto de una fruta
OUTPUT: "Manzana" (una etiqueta)

EJEMPLOS:
- Clasificar tipo de producto
- Diagnosticar enfermedad en planta (sana/enferma)
- Clasificar tipo de documento
```

**Subtipos:**

| Tipo           | Descripción                      | Ejemplo                                        |
| -------------- | -------------------------------- | ---------------------------------------------- |
| **Multiclass** | Una imagen = UNA etiqueta        | "Esta fruta es: manzana"                       |
| **Multilabel** | Una imagen = MÚLTIPLES etiquetas | "Esta imagen tiene: manzana, plátano, naranja" |

#### 2️⃣ OBJECT DETECTION

**¿Qué hace?**
Detecta **múltiples objetos** y sus ubicaciones con bounding boxes.

```
INPUT: Foto de una tienda
OUTPUT:
  - Producto A (x:100, y:200, w:50, h:60)
  - Producto B (x:300, y:150, w:70, h:80)
  - Producto C (x:500, y:250, w:60, h:70)

EJEMPLOS:
- Detectar y contar productos en estante
- Encontrar defectos en piezas metálicas
- Localizar tumores en radiografías
```

---

### 🔨 PROCESO COMPLETO DE CUSTOM VISION

#### 📋 PASO 1: CREAR PROYECTO

```
1. Ir a Custom Vision Portal: customvision.ai
2. Crear nuevo proyecto
3. Elegir:
   - Nombre del proyecto
   - Tipo: Classification o Object Detection
   - Dominio: General, Food, Retail, etc.
```

#### 🎨 Dominios disponibles:

| Dominio          | Descripción         | Uso                          |
| ---------------- | ------------------- | ---------------------------- |
| **General**      | Propósito general   | Default, cualquier cosa      |
| **General [A1]** | Versión compacta    | Dispositivos móviles/edge    |
| **Food**         | Comida y bebidas    | Aplicaciones de restaurantes |
| **Landmarks**    | Lugares famosos     | Apps de turismo              |
| **Retail**       | Productos en tienda | E-commerce, inventario       |
| **Logo**         | Logos de marcas     | Detección de marcas          |

---

#### 🖼️ PASO 2: SUBIR Y ETIQUETAR IMÁGENES

##### Para IMAGE CLASSIFICATION:

```
REQUERIMIENTOS MÍNIMOS:
- Mínimo 15 imágenes por categoría
- Recomendado: 50+ imágenes por categoría
- Máximo: 10,000 imágenes por proyecto (Free), 100,000 (Paid)

EJEMPLO: Clasificar frutas
├── Categoría "Manzana": 50 imágenes
├── Categoría "Plátano": 50 imágenes
├── Categoría "Naranja": 50 imágenes
└── Categoría "Uva": 50 imágenes
```

**Proceso:**

```
1. Subir lote de imágenes (hasta 64 a la vez)
2. Asignar etiqueta: "Manzana"
3. Subir siguiente lote
4. Asignar etiqueta: "Plátano"
5. Repetir para todas las categorías
```

##### Para OBJECT DETECTION:

```
REQUERIMIENTOS:
- Mínimo 15 imágenes con objetos etiquetados
- Recomendado: 50+ instancias del objeto
- Puedes tener múltiples objetos en una imagen

EJEMPLO: Detectar productos en estante
Imagen 1:
├── Producto A (dibujar caja)
├── Producto B (dibujar caja)
└── Producto C (dibujar caja)
```

**Proceso:**

```
1. Subir imagen
2. Para cada objeto:
   a. Dibujar bounding box (rectángulo)
   b. Asignar etiqueta
3. Guardar
4. Repetir con todas las imágenes
```

---

#### 🚀 PASO 3: ENTRENAR MODELO

```
1. Clic en botón "Train" (Entrenar)
2. Elegir tipo de entrenamiento:
   - Quick Training (rápido, ~5 min)
   - Advanced Training (mejor, ~1 hora)
3. Esperar a que termine
4. Revisar métricas de rendimiento
```

#### 📊 Métricas de evaluación:

##### Para CLASSIFICATION:

| Métrica                    | Qué mide                                                            | Ideal |
| -------------------------- | ------------------------------------------------------------------- | ----- |
| **Precision**              | De los que predice como "Manzana", ¿cuántos son realmente manzanas? | >90%  |
| **Recall**                 | De todas las manzanas reales, ¿cuántas detectó?                     | >90%  |
| **AP (Average Precision)** | Promedio de precision across all categories                         | >90%  |

##### Para OBJECT DETECTION:

| Métrica                          | Qué mide                                           | Ideal |
| -------------------------------- | -------------------------------------------------- | ----- |
| **Precision**                    | De los objetos detectados, ¿cuántos son correctos? | >85%  |
| **Recall**                       | De todos los objetos reales, ¿cuántos detectó?     | >85%  |
| **mAP (mean Average Precision)** | Promedio de precisión considerando IoU             | >0.50 |

#### 🎯 Interpretación de resultados:

```
EJEMPLO:
Precision: 95%  ✅ Muy bien, pocas falsas alarmas
Recall: 60%     ❌ Problema, está perdiendo muchos objetos

SOLUCIÓN:
- Agregar más imágenes de entrenamiento
- Mejorar calidad de etiquetado
- Agregar más variedad (ángulos, iluminación)
```

---

#### 🧪 PASO 4: PROBAR MODELO

```
QUICK TEST:
1. Clic en "Quick Test"
2. Subir imagen nueva (nunca vista por el modelo)
3. Ver predicción

RESULTADO:
"Manzana" - 98% confidence ✅
"Plátano" - 1% confidence
"Naranja" - 1% confidence
```

**Recomendaciones de prueba:**

```
✅ PROBAR CON:
- Imágenes de diferentes ángulos
- Diferentes condiciones de luz
- Fondo diferente al de entrenamiento
- Objetos parcialmente ocultos
- Múltiples objetos en la misma imagen

❌ NO PROBAR SOLO CON:
- Imágenes casi idénticas a las de entrenamiento
- Siempre misma iluminación
- Siempre mismo fondo
```

---

#### 🔄 PASO 5: ITERAR Y MEJORAR

```
SI PRECISIÓN ES BAJA:

1️⃣ Agregar más imágenes (especialmente de casos fallidos)
2️⃣ Mejorar etiquetado (revisar etiquetas incorrectas)
3️⃣ Balancear dataset (misma cantidad por categoría)
4️⃣ Agregar variedad:
   - Diferentes ángulos
   - Diferentes iluminaciones
   - Diferentes fondos
   - Objetos a diferentes distancias
5️⃣ Re-entrenar modelo
6️⃣ Volver a probar
```

**Técnica de data augmentation:**

```
IMAGEN ORIGINAL: 1 foto de manzana

GENERAR VARIACIONES:
├── Rotar 15° izquierda
├── Rotar 15° derecha
├── Aumentar brillo +20%
├── Reducir brillo -20%
├── Flip horizontal
├── Agregar ruido
└── Cambiar saturación

RESULTADO: 1 imagen → 8 imágenes de entrenamiento
```

---

#### 🌐 PASO 6: PUBLICAR Y USAR

```
1. PUBLICAR MODELO:
   - Darle nombre a la iteración
   - Publicar a "Prediction endpoint"

2. OBTENER CREDENCIALES:
   - Prediction URL
   - Prediction Key

3. INTEGRAR EN TU APP:
   - Llamar API con imagen
   - Recibir predicciones
```

**Ejemplo de uso de API:**

```http
POST https://[region].api.cognitive.microsoft.com/customvision/v3.0/Prediction/[projectId]/classify/iterations/[iteration-name]/image

Headers:
  Prediction-Key: [tu-prediction-key]
  Content-Type: application/json

Body:
{
  "Url": "https://ejemplo.com/fruta.jpg"
}

Response:
{
  "predictions": [
    {"tagName": "Manzana", "probability": 0.98},
    {"tagName": "Plátano", "probability": 0.01},
    {"tagName": "Naranja", "probability": 0.01}
  ]
}
```

---

### 💡 MEJORES PRÁCTICAS

#### 📸 Calidad de imágenes:

```
✅ USAR:
- Alta resolución (mínimo 256x256)
- Buena iluminación
- Objetos claramente visibles
- Variedad de ángulos y contextos

❌ EVITAR:
- Imágenes borrosas
- Muy oscuras o sobre-expuestas
- Objetos muy pequeños (<5% de la imagen)
- Todas las fotos idénticas
```

#### 🎯 Dataset balanceado:

```
✅ CORRECTO:
Manzana: 50 imágenes
Plátano: 50 imágenes
Naranja: 50 imágenes
Uva: 50 imágenes

❌ INCORRECTO (desbalanceado):
Manzana: 200 imágenes
Plátano: 10 imágenes
Naranja: 10 imágenes
Uva: 5 imágenes

PROBLEMA: Modelo aprenderá a predecir "Manzana" siempre
```

#### 🔄 Negative images (imágenes negativas):

```
CONCEPTO:
Agregar imágenes que NO pertenecen a ninguna categoría

EJEMPLO: Clasificador de frutas
├── Manzana: 50 imgs
├── Plátano: 50 imgs
└── Negative: 20 imgs (sillas, mesas, personas, etc.)

BENEFICIO: Modelo aprende a decir "no es ninguna categoría conocida"
```

---

### 💰 PRICING DE CUSTOM VISION

#### Free Tier (F0):

```
✅ INCLUYE:
- 2 proyectos
- 5,000 imágenes de entrenamiento/proyecto
- 10,000 predicciones/mes
- 1 hora de entrenamiento/mes

⚠️ LÍMITE: Solo para desarrollo/pruebas
```

#### Standard Tier (S0):

```
💵 COSTOS (aproximados):
- Entrenamiento: $20/hora de entrenamiento
- Almacenamiento de imágenes: $0.70/1,000 imgs/mes
- Predicciones: $2/1,000 transacciones

✅ PARA PRODUCCIÓN:
- Proyectos ilimitados
- Imágenes ilimitadas
- Predicciones ilimitadas (pagando)
```

---

## 📖 PARTE 3: COMPARACIÓN FINAL Y DECISIONES (20 min)

### 🎯 Árbol de decisión:

```
¿Necesitas analizar ROSTROS?
├── SÍ → FACE API
│   ├── ¿Solo detectar y atributos? → Face Detection
│   ├── ¿Verificar identidad 1:1? → Face Verification
│   └── ¿Identificar quién es (1:N)? → Face Identification
│
└── NO → ¿Qué necesitas detectar?
    │
    ├── Objetos COMUNES (personas, coches, animales)
    │   └── AZURE AI VISION
    │
    ├── TEXTO en imágenes/documentos
    │   └── READ API (Azure AI Vision)
    │
    ├── Objetos ESPECÍFICOS de tu negocio
    │   └── CUSTOM VISION
    │       ├── Clasificar imagen completa → Image Classification
    │       └── Detectar y localizar múltiples objetos → Object Detection
    │
    └── Video en tiempo real (contar personas)
        └── SPATIAL ANALYSIS
```

---

### 📊 TABLA COMPARATIVA COMPLETA

| Servicio             | Pre-entrenado | Personalizable | Mejor para           | Requiere datos | Dificultad |
| -------------------- | ------------- | -------------- | -------------------- | -------------- | ---------- |
| **Azure AI Vision**  | ✅            | ❌             | Objetos comunes, OCR | ❌             | ⭐⚪⚪⚪⚪ |
| **Face API**         | ✅            | ❌             | Rostros, emociones   | ❌             | ⭐⭐⚪⚪⚪ |
| **Custom Vision**    | ❌            | ✅             | Objetos específicos  | ✅ 15-50+ imgs | ⭐⭐⭐⚪⚪ |
| **Spatial Analysis** | ✅            | ❌             | Video tiempo real    | ❌             | ⭐⭐⭐⭐⚪ |

---

## 🎯 CONCEPTOS CLAVE PARA EL EXAMEN

### ⚡ Memoriza esto:

1. **Face Detection** = Detectar rostros + atributos (edad, emoción, gafas)
2. **Face Verification** = Comparar 2 rostros (1:1): ¿Son la misma persona?
3. **Face Identification** = Identificar quién es (1:N) buscando en Person Group
4. **Person Group** = Colección de personas conocidas (hasta 10,000)
5. **faceId** = Identificador temporal del rostro (expira en 24 horas)
6. **Custom Vision** = Entrenar modelos personalizados con tus imágenes
7. **Image Classification** = Una imagen → una etiqueta
8. **Object Detection** = Una imagen → múltiples objetos con ubicaciones
9. **Mínimo imágenes** = 15 por categoría (recomendado: 50+)
10. **Precision** = De las predicciones positivas, cuántas son correctas
11. **Recall** = De los casos reales, cuántos detectamos

---

## 🎴 FLASHCARDS (15 tarjetas)

### Tarjeta 1

**P:** ¿Cuál es la diferencia entre Face Verification y Face Identification?  
**R:**

- **Verification (1:1):** Compara 2 rostros para ver si son la misma persona
- **Identification (1:N):** Identifica quién es una persona buscando en un grupo de rostros conocidos (Person Group)

---

### Tarjeta 2

**P:** ¿Qué es un Person Group en Face API?  
**R:** Una colección de personas conocidas donde cada persona puede tener múltiples fotos de su rostro. Se usa para Face Identification (máximo 10,000 personas en Standard tier).

---

### Tarjeta 3

**P:** ¿Cuánto tiempo dura un faceId en Face API?  
**R:** 24 horas. Después de ese tiempo expira y se debe volver a detectar el rostro.

---

### Tarjeta 4

**P:** Nombra 3 atributos que Face Detection puede proporcionar  
**R:**

1. Edad aproximada
2. Emoción dominante (felicidad, tristeza, etc.)
3. Accesorios (gafas, maquillaje, vello facial)

---

### Tarjeta 5

**P:** ¿Cuándo debes usar Custom Vision en lugar de Azure AI Vision?  
**R:** Cuando necesitas detectar objetos ESPECÍFICOS de tu negocio que Azure AI Vision no reconoce (ej: tipos específicos de productos, defectos personalizados, especies particulares).

---

### Tarjeta 6

**P:** ¿Cuál es el mínimo de imágenes requerido por categoría en Custom Vision?  
**R:** Mínimo 15 imágenes por categoría, pero se recomienda 50+ para mejores resultados.

---

### Tarjeta 7

**P:** ¿Cuáles son los 2 tipos de proyectos en Custom Vision?  
**R:**

1. **Image Classification:** Asignar una etiqueta a toda la imagen
2. **Object Detection:** Detectar y localizar múltiples objetos con bounding boxes

---

### Tarjeta 8

**P:** ¿Qué mide la métrica "Precision" en Custom Vision?  
**R:** De todas las predicciones positivas que el modelo hace, ¿cuántas son correctas? (Mide falsos positivos)

---

### Tarjeta 9

**P:** ¿Qué mide la métrica "Recall" en Custom Vision?  
**R:** De todos los casos reales positivos, ¿cuántos detectó el modelo? (Mide falsos negativos)

---

### Tarjeta 10

**P:** ¿Qué es un "dominio" en Custom Vision?  
**R:** Una especialización del modelo pre-entrenado optimizado para ciertos tipos de imágenes (General, Food, Retail, Landmarks, Logo).

---

### Tarjeta 11

**P:** ¿Por qué Face API tiene restricciones de acceso?  
**R:** Por consideraciones de uso responsable de IA. Microsoft requiere aprobación para evitar usos no éticos como vigilancia masiva, discriminación, o violación de privacidad.

---

### Tarjeta 12

**P:** ¿Qué es data augmentation en Custom Vision?  
**R:** Técnica de generar múltiples variaciones de una imagen (rotar, cambiar brillo, flip) para aumentar el dataset de entrenamiento sin tomar más fotos.

---

### Tarjeta 13

**P:** ¿Cuál es el tamaño máximo de proyecto en Custom Vision Free tier?  
**R:** 2 proyectos, 5,000 imágenes por proyecto, 10,000 predicciones/mes, 1 hora de entrenamiento/mes.

---

### Tarjeta 14

**P:** ¿Qué son "negative images" en Custom Vision?  
**R:** Imágenes que NO pertenecen a ninguna categoría conocida, usadas para enseñar al modelo a reconocer cuando algo no es de las categorías entrenadas.

---

### Tarjeta 15

**P:** En Face API, ¿qué significan los valores de "emotion"?  
**R:** Valores entre 0 y 1 para cada emoción (happiness, sadness, anger, etc.) que indican la intensidad detectada de esa emoción. La suma puede ser mayor a 1.

---

## ❓ PREGUNTAS DE AUTOEVALUACIÓN

### Pregunta 1 (Media)

**Un aeropuerto quiere verificar que la persona que presenta un pasaporte es la misma persona de la foto del pasaporte. ¿Qué capacidad de Face API deben usar?**

A) Face Detection  
B) Face Verification  
C) Face Identification  
D) Face Recognition

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Face Verification**

**Explicación:** Face Verification (1:1) compara dos rostros para determinar si pertenecen a la misma persona. En este caso: foto en vivo vs foto del pasaporte. No necesitan identificar QUIÉN es (Identification), solo verificar que coincidan.

</details>

---

### Pregunta 2 (Difícil)

**Una empresa de seguridad tiene 500 empleados y quiere implementar un sistema donde al llegar a la oficina, una cámara identifique automáticamente al empleado y abra la puerta. ¿Qué configuración de Face API necesitan?**

A) Face Detection para cada empleado  
B) Face Verification comparando con foto de ID  
C) Person Group con los 500 empleados + Face Identification  
D) Custom Vision entrenado con fotos de empleados

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Person Group con los 500 empleados + Face Identification**

**Explicación:**

- Necesitan **Face Identification** porque deben identificar QUIÉN es cada persona (1:N)
- Deben crear un **Person Group** con los 500 empleados
- Cada empleado debe tener varias fotos de su rostro registradas
- Cuando la cámara captura un rostro, Face Identification busca en el Person Group y devuelve la identidad

Face Verification solo funciona 1:1 (demasiado lento comparar contra 500 personas una por una). Custom Vision no está diseñado para rostros.

</details>

---

### Pregunta 3 (Media)

**Una fábrica automotriz necesita detectar 12 tipos diferentes de defectos en piezas metálicas. Los defectos son específicos de su proceso de manufactura. Azure AI Vision no reconoce estos defectos. ¿Qué deben hacer?**

A) Usar Azure AI Vision y esperar a que se actualice  
B) Usar Custom Vision con Object Detection  
C) Usar Face API modificado para objetos  
D) Contratar a un científico de datos para entrenar desde cero

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Usar Custom Vision con Object Detection**

**Explicación:**

- Los defectos son **específicos** de su negocio → Custom Vision
- Necesitan **detectar y localizar** múltiples defectos en una pieza → Object Detection
- Proceso:
  1. Tomar fotos de piezas con defectos
  2. Dibujar bounding boxes alrededor de cada defecto
  3. Etiquetar cada defecto con su tipo (12 categorías)
  4. Entrenar modelo
  5. Usar en línea de producción

Face API es solo para rostros. Custom Vision es mucho más rápido y fácil que entrenar desde cero.

</details>

---

### Pregunta 4 (Fácil)

**¿Cuál es el mínimo de imágenes de entrenamiento recomendado por categoría en Custom Vision?**

A) 5 imágenes  
B) 15 imágenes (mínimo absoluto)  
C) 50+ imágenes (recomendado)  
D) 1000 imágenes

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) 50+ imágenes (recomendado)**

**Explicación:**

- **Mínimo absoluto:** 15 imágenes (el modelo entrenará, pero con baja precisión)
- **Recomendado:** 50+ imágenes para buenos resultados
- **Ideal:** 100+ imágenes con buena variedad

Con solo 5 imágenes el modelo tendrá overfitting. Con 1000 es excesivo para la mayoría de casos (aunque no está mal si las tienes).

</details>

---

### Pregunta 5 (Difícil - Estilo Microsoft)

**Scenario:** Una app de nutrición quiere dos funcionalidades:

1. Identificar el tipo de comida en una foto (pizza, ensalada, hamburguesa, etc.)
2. Analizar la emoción del usuario cuando ve la comida (para estudios de comportamiento)

¿Qué servicios necesitan?

A) Solo Custom Vision para ambas tareas  
B) Azure AI Vision + Face API  
C) Solo Face API (puede detectar comida y emociones)  
D) Custom Vision (comida) + Face API (emoción)

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Azure AI Vision + Face API**

**Explicación:**

- **Funcionalidad 1 (identificar comida):** Azure AI Vision puede reconocer tipos comunes de comida. Si las categorías son muy específicas, podrían considerar Custom Vision, pero generalmente Azure AI Vision funciona bien para comida común.
- **Funcionalidad 2 (emoción del usuario):** Face API con Face Detection para detectar emociones faciales.

No necesitan Custom Vision porque pizza, ensalada, hamburguesa son categorías comunes que Azure AI Vision ya reconoce. Face API no detecta comida, solo rostros.

**Nota:** Si las categorías de comida fueran MUY específicas (ej: "Taco al pastor estilo Guadalajara" vs "Taco de carnitas estilo Michoacán"), entonces sí usarían Custom Vision + Face API (opción D).

</details>

---

### Pregunta 6 (Media)

**Un modelo de Custom Vision para detectar defectos tiene estas métricas: Precision: 95%, Recall: 55%. ¿Qué significa esto y cómo mejorarlo?**

A) Excelente modelo, no necesita mejoras  
B) Modelo conservador: detecta pocos defectos pero cuando lo hace, es correcto. Agregar más imágenes de defectos.  
C) Modelo agresivo: detecta muchos defectos falsos. Agregar negative images.  
D) Modelo con overfitting, reducir número de imágenes

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Modelo conservador: detecta pocos defectos pero cuando lo hace, es correcto. Agregar más imágenes de defectos.**

**Explicación:**

- **Precision alta (95%):** Cuando dice "es un defecto", es correcto el 95% del tiempo → Pocos falsos positivos ✅
- **Recall bajo (55%):** Solo detecta el 55% de los defectos reales → Muchos falsos negativos ❌

**Problema:** El modelo está siendo muy conservador/cauteloso. Se está perdiendo el 45% de defectos reales.

**Solución:**

1. Agregar más imágenes de entrenamiento, especialmente de defectos
2. Agregar más variedad (diferentes ángulos, iluminaciones)
3. Revisar que el etiquetado sea correcto
4. Re-entrenar

</details>

---

### Pregunta 7 (Media)

**¿Cuál de las siguientes afirmaciones sobre Face API es INCORRECTA?**

A) faceId expira después de 24 horas  
B) Face Identification puede buscar en un Person Group de hasta 10,000 personas  
C) Face API puede identificar la raza de una persona con alta precisión  
D) Face API puede detectar si una persona usa gafas

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Face API puede identificar la raza de una persona con alta precisión**

**Explicación:** Face API **NO** proporciona información sobre raza o etnia. Microsoft eliminó esta funcionalidad por consideraciones éticas y de uso responsable de IA. Inferir raza puede llevar a discriminación y sesgos.

Las otras afirmaciones son correctas:

- A) faceId sí expira en 24h
- B) Person Group sí soporta hasta 10,000 personas en Standard tier
- D) Face API sí detecta gafas (NoGlasses, ReadingGlasses, Sunglasses, SwimmingGoggles)

</details>

---

### Pregunta 8 (Difícil)

\*\*Una startup quiere crear una app que:

1. Permita a usuarios hacer login con su rostro
2. Detecte si el usuario está feliz o triste cuando usa la app
3. Identifique celebridades en fotos que suben los usuarios

¿Qué implementación es técnicamente posible Y éticamente apropiada?\*\*

A) Todas las funcionalidades son posibles y apropiadas con Face API  
B) Solo 1 y 2 son apropiadas; 3 viola privacidad de celebridades  
C) Solo 1 es apropiada; 2 y 3 tienen problemas éticos  
D) Ninguna es apropiada sin consentimiento explícito

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Solo 1 y 2 son apropiadas; 3 viola privacidad de celebridades**

**Explicación:**

**Funcionalidad 1 (Login facial):** ✅ Apropiado

- Face Verification es un caso de uso legítimo
- Usuario da consentimiento al registrarse
- Técnicamente: Guardar faceId del usuario y verificar cada vez

**Funcionalidad 2 (Detectar emoción):** ⚠️ Técnicamente posible pero con cuidados

- Face Detection puede detectar emociones
- PERO Microsoft desaconseja inferir estados mentales o emociones en ciertos contextos
- OK si es solo para UX y el usuario lo sabe
- NO OK para decisiones de empleo, crédito, etc.

**Funcionalidad 3 (Identificar celebridades):** ❌ Problemático

- Requeriría crear un Person Group con fotos de celebridades sin su consentimiento
- Violación de privacidad y posiblemente derechos de imagen
- Microsoft probablemente rechazaría la solicitud de acceso

**Respuesta más precisa:** Solo la 1 es claramente apropiada. La 2 es cuestionable. La 3 es inapropiada.

</details>

---

## ✅ CHECKLIST DEL DÍA

Marca cada item al completarlo:

- [ ] Entiendo las 3 capacidades de Face API (Detection, Verification, Identification)
- [ ] Sé la diferencia entre 1:1 (Verification) y 1:N (Identification)
- [ ] Comprendo qué es un Person Group
- [ ] Conozco las consideraciones éticas de Face API
- [ ] Entiendo cuándo usar Custom Vision vs Azure AI Vision
- [ ] Sé los 2 tipos de proyectos en Custom Vision
- [ ] Comprendo el proceso completo: subir, etiquetar, entrenar, probar
- [ ] Entiendo qué son Precision y Recall
- [ ] Sé el mínimo de imágenes por categoría (15 mínimo, 50+ recomendado)
- [ ] Revisé las 15 flashcards
- [ ] Intenté las 8 preguntas de autoevaluación

---

## 🎯 PREPARACIÓN PARA MAÑANA

**Jueves 21 Nov: LAB 1 - Azure AI Vision (Hands-on)**

Mañana harás tu primer laboratorio práctico con Azure AI Vision. Asegúrate de tener claro:

- Diferencias entre los servicios (Vision, Face, Custom)
- Cuándo usar cada uno
- Qué capacidades tiene cada servicio

**Prepara:**

- Acceso a Azure Portal (cuenta gratuita si no tienes)
- 5-10 imágenes propias para probar

---

## 📚 RECURSOS DE MICROSOFT LEARN

### 🔗 Módulos recomendados para HOY:

1. **"Detect, analyze, and recognize faces"**
   - URL: https://learn.microsoft.com/training/modules/detect-analyze-faces/
   - Duración: 30 min
   - Nivel: Beginner

2. **"Classify images with Custom Vision"**
   - URL: https://learn.microsoft.com/training/modules/classify-images-custom-vision/
   - Duración: 42 min
   - Nivel: Beginner

3. **"Detect objects in images with Custom Vision"**
   - URL: https://learn.microsoft.com/training/modules/detect-objects-images-custom-vision/
   - Duración: 45 min
   - Nivel: Beginner

### 📖 Documentación adicional:

- [Face API concepts](https://learn.microsoft.com/azure/ai-services/computer-vision/concept-face-detection)
- [Custom Vision best practices](https://learn.microsoft.com/azure/ai-services/custom-vision-service/getting-started-improving-your-classifier)
- [Responsible AI for Face](https://learn.microsoft.com/azure/ai-services/computer-vision/responsible-use-of-ai-overview)

---

## 📌 NOTAS IMPORTANTES

### 💡 Para el examen AI-900:

1. **Face API tiene 3 capacidades principales:**
   - Detection (detectar + atributos)
   - Verification (1:1)
   - Identification (1:N con Person Group)

2. **Custom Vision requiere:**
   - Mínimo 15 imgs/categoría
   - Proceso: subir → etiquetar → entrenar → probar → iterar

3. **Métricas clave:**
   - Precision = ¿De lo que detecta, cuánto es correcto?
   - Recall = ¿De lo que existe, cuánto detecta?

4. **Uso responsable:**
   - Face API tiene restricciones de acceso
   - Requerir consentimiento
   - No discriminar

### 🎓 Conexión con días anteriores:

**Lunes:** Conceptos de Computer Vision  
**Martes:** Servicios de Azure (Vision, Face, Custom)  
**Miércoles:** Profundización en Face y Custom Vision  
**Mañana:** ¡Práctica hands-on! 🚀

---

**🎉 ¡Excelente trabajo! Ya entiendes los servicios avanzados de Computer Vision en Azure.**

**Siguiente sesión:** Jueves 21 Nov - LAB 1: Azure AI Vision (Práctica)

---

_Documento creado: Miércoles 20 de Noviembre, 2025_  
_Roadmap: Semana 3 de 6 | AI-900 Certification Prep_
