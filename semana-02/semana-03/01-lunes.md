# 📚 AI-900 | SEMANA 3 - LUNES 18 NOV

## 👁️ Fundamentos de Computer Vision

---

## 🎯 OBJETIVOS DEL DÍA

Al finalizar hoy, serás capaz de:

- ✅ Explicar qué es Computer Vision y cómo funciona
- ✅ Diferenciar entre clasificación, detección de objetos y segmentación
- ✅ Identificar aplicaciones reales de Computer Vision
- ✅ Entender el concepto de feature extraction (extracción de características)
- ✅ Conocer los desafíos técnicos de Computer Vision

**Tiempo estimado:** 1.5 horas  
**Nivel de dificultad:** ⭐⭐⚪⚪⚪ (Media-Baja)

---

## 📖 PARTE 1: ¿QUÉ ES COMPUTER VISION? (20 min)

### 🤔 Definición simple

**Computer Vision** es la capacidad de las computadoras para **"ver" y entender imágenes y videos** de la misma manera que los humanos lo hacen.

```
HUMANO ve una foto de un gato:
   👀 → 🧠 "Es un gato naranja en un sofá"

COMPUTER VISION ve la misma foto:
   📷 → 🤖 "Detectado: gato (95% confianza), sofá (88% confianza), color dominante: naranja"
```

### 🎯 ¿Para qué sirve?

Computer Vision permite a las máquinas:

- **Reconocer** objetos, personas, lugares
- **Detectar** movimiento, anomalías, cambios
- **Clasificar** imágenes en categorías
- **Extraer** texto de imágenes (OCR)
- **Analizar** escenas complejas
- **Generar** descripciones de lo que "ven"

### 🌍 Aplicaciones del mundo real

| Industria         | Aplicación            | Ejemplo concreto                          |
| ----------------- | --------------------- | ----------------------------------------- |
| 🏥 Salud          | Diagnóstico médico    | Detectar tumores en radiografías          |
| 🚗 Automotriz     | Vehículos autónomos   | Reconocer señales de tránsito             |
| 🏭 Manufactura    | Control de calidad    | Identificar productos defectuosos         |
| 🛒 Retail         | Análisis de clientes  | Contar personas en tienda, heatmaps       |
| 🔒 Seguridad      | Vigilancia            | Reconocimiento facial en aeropuertos      |
| 📱 Redes sociales | Filtros y efectos     | Snapchat lenses, Instagram filters        |
| 🌾 Agricultura    | Monitoreo de cultivos | Detectar plagas o enfermedades en plantas |
| 📦 Logística      | Automatización        | Lectura automática de códigos de barras   |

### 💡 Ejemplo práctico:

**Caso: Sistema de seguridad en aeropuerto**

```
📷 Cámara captura imagen de pasajero
   ↓
🤖 Computer Vision analiza:
   ├── Detecta rostro
   ├── Compara con base de datos
   ├── Verifica equipaje sospechoso
   └── Identifica comportamiento anómalo
   ↓
✅ Decisión: Permitir paso / Revisión adicional
```

---

## 📖 PARTE 2: TIPOS DE TAREAS EN COMPUTER VISION (30 min)

### 1️⃣ IMAGE CLASSIFICATION (Clasificación de imágenes)

**¿Qué es?**
Asignar una **etiqueta única** a toda la imagen.

```
Pregunta: "¿QUÉ es esta imagen?"
Respuesta: "Es un gato" (una sola etiqueta)
```

**Características:**

- Una imagen → Una etiqueta
- Clasifica la imagen completa
- No indica DÓNDE está el objeto

**Ejemplos:**

- ¿Es un perro o un gato?
- ¿Esta radiografía muestra cáncer o es normal?
- ¿Esta foto es de día o de noche?
- ¿Este correo es spam o legítimo? (con imagen adjunta)

**Diagrama:**

```
   📷 Imagen de entrada
       ↓
   🤖 Modelo de clasificación
       ↓
   🏷️ ETIQUETA: "Gato"
```

### 2️⃣ OBJECT DETECTION (Detección de objetos)

**¿Qué es?**
Identificar **múltiples objetos** en una imagen y **ubicar dónde están** con bounding boxes (cajas delimitadoras).

```
Pregunta: "¿QUÉ hay en esta imagen y DÓNDE está?"
Respuesta:
   - Gato (coordenadas: x=120, y=200, w=80, h=60)
   - Sofá (coordenadas: x=0, y=100, w=300, h=150)
```

**Características:**

- Una imagen → Múltiples etiquetas + ubicaciones
- Dibuja cajas (bounding boxes) alrededor de objetos
- Indica posición con coordenadas

**Ejemplos:**

- Contar cuántos coches hay en un estacionamiento
- Detectar personas en una multitud
- Sistemas de conducción autónoma (detectar peatones, señales, otros vehículos)
- Seguridad: detectar armas en equipaje de aeropuerto

**Diagrama:**

```
   📷 Imagen con varios objetos
       ↓
   🤖 Modelo de detección
       ↓
   📦 CAJAS con etiquetas:
      [Persona] [Coche] [Semáforo]
```

### 3️⃣ SEMANTIC SEGMENTATION (Segmentación semántica)

**¿Qué es?**
Clasificar **cada píxel** de la imagen según la categoría a la que pertenece.

```
Pregunta: "¿Qué representa CADA PÍXEL de esta imagen?"
Respuesta:
   - Píxeles 1-1000: Cielo
   - Píxeles 1001-5000: Edificio
   - Píxeles 5001-8000: Calle
```

**Características:**

- Precisión a nivel de píxel
- Contornos exactos de objetos
- Separa objetos superpuestos

**Ejemplos:**

- Conducción autónoma: identificar carretera vs acera vs vehículos
- Medicina: delimitar exactamente un tumor en una imagen
- Edición de fotos: cambiar fondo (separar persona del fondo)
- Agricultura: separar plantas de maleza

**Diagrama:**

```
   📷 Imagen original
       ↓
   🤖 Modelo de segmentación
       ↓
   🎨 Imagen coloreada por categoría:
      (Cada color = una clase de objeto)
```

### 📊 TABLA COMPARATIVA

| Característica  | Classification | Object Detection            | Segmentation            |
| --------------- | -------------- | --------------------------- | ----------------------- |
| **Output**      | 1 etiqueta     | Múltiples cajas + etiquetas | Máscara de píxeles      |
| **Precisión**   | Baja (general) | Media (cajas)               | Alta (píxeles)          |
| **Ubicación**   | ❌ No          | ✅ Aproximada               | ✅ Exacta               |
| **Velocidad**   | ⚡ Rápida      | 🏃 Media                    | 🐌 Lenta                |
| **Complejidad** | Baja           | Media                       | Alta                    |
| **Uso común**   | Categorizar    | Contar/Localizar            | Delimitar con precisión |

### 🎯 ¿Cuál usar?

**Usa CLASSIFICATION cuando:**

- Solo necesitas saber QUÉ es (no dónde está)
- Ejemplo: "¿Esta foto muestra un producto defectuoso?"

**Usa OBJECT DETECTION cuando:**

- Necesitas saber QUÉ es y DÓNDE está
- Necesitas contar múltiples objetos
- Ejemplo: "¿Cuántas personas hay en esta sala y dónde están?"

**Usa SEGMENTATION cuando:**

- Necesitas precisión exacta a nivel de píxel
- Necesitas separar objetos superpuestos
- Ejemplo: "Extrae este objeto del fondo con precisión"

---

## 📖 PARTE 3: ¿CÓMO FUNCIONA? FEATURE EXTRACTION (25 min)

### 🧠 Conceptos fundamentales

Las computadoras NO "ven" como nosotros. Para ellas, una imagen es una **matriz de números** (píxeles).

```
HUMANO ve:        COMPUTADORA ve (RGB):
    🐱            Píxel (0,0): [255, 128, 64]  ← Naranja
                  Píxel (0,1): [250, 130, 68]  ← Naranja
                  Píxel (0,2): [245, 125, 62]  ← Naranja
                  ...
                  Píxel (500,600): [50, 120, 200] ← Azul
```

Cada píxel = 3 números (Rojo, Verde, Azul)
Rango: 0-255 por canal

### 🔍 Feature Extraction (Extracción de características)

**¿Qué son features?**
Son **patrones y características visuales** que el modelo aprende a identificar.

**Niveles de features:**

```
NIVEL 1 - Features simples (bordes, líneas, colores):
   ├── Bordes horizontales: ━━━
   ├── Bordes verticales: ┃┃┃
   ├── Esquinas: └ ┘ ┌ ┐
   └── Colores: 🔴 🟢 🔵

NIVEL 2 - Features intermedias (texturas, formas):
   ├── Círculos 🔵
   ├── Rectángulos ▭
   ├── Texturas (rayas, puntos)
   └── Patrones repetitivos

NIVEL 3 - Features complejas (partes de objetos):
   ├── Ojos 👁️
   ├── Ruedas 🛞
   ├── Puertas 🚪
   └── Ventanas 🪟

NIVEL 4 - Features de alto nivel (objetos completos):
   ├── Rostro 😊
   ├── Coche 🚗
   ├── Casa 🏠
   └── Gato 🐱
```

### 🧪 Proceso completo de Computer Vision:

```
1️⃣ INPUT (Entrada)
   📷 Imagen cruda (píxeles)
      ↓
2️⃣ PREPROCESSING (Preprocesamiento)
   🔧 Ajustar tamaño, normalizar colores
      ↓
3️⃣ FEATURE EXTRACTION (Extracción de características)
   🔍 CNN extrae features en múltiples niveles
      ↓
4️⃣ CLASSIFICATION/DETECTION (Clasificación/Detección)
   🤖 Modelo decide qué es basándose en features
      ↓
5️⃣ OUTPUT (Salida)
   🏷️ Etiquetas, cajas, o segmentación
```

### 🏗️ Convolutional Neural Networks (CNN)

**¿Qué son?**
Son redes neuronales especializadas en procesar imágenes.

**Componentes clave:**

1. **Convolutional Layers (Capas convolucionales)**
   - Aplican filtros para detectar features
   - Ejemplo: filtro de bordes, filtro de colores

2. **Pooling Layers (Capas de pooling)**
   - Reducen el tamaño de la imagen
   - Mantienen lo más importante

3. **Fully Connected Layers (Capas completamente conectadas)**
   - Toman decisiones finales
   - Clasifican o detectan objetos

**Diagrama simplificado:**

```
   📷 Imagen (224x224 píxeles)
       ↓
   [Convolutional Layer 1] → detecta bordes
       ↓
   [Pooling Layer] → reduce tamaño
       ↓
   [Convolutional Layer 2] → detecta formas
       ↓
   [Pooling Layer] → reduce más
       ↓
   [Convolutional Layer 3] → detecta objetos
       ↓
   [Fully Connected] → decide: "Es un gato"
       ↓
   🏷️ OUTPUT: "Gato (95% confianza)"
```

---

## 📖 PARTE 4: DESAFÍOS EN COMPUTER VISION (15 min)

### 🚧 Problemas comunes

#### 1. **VARIACIONES DE ILUMINACIÓN** 💡

```
Misma imagen con diferente luz:
☀️ Día soleado    → Fácil de reconocer
🌙 Noche oscura   → Difícil de reconocer
💡 Contraluz      → Puede fallar
```

#### 2. **OCLUSIONES (objetos tapados)** 🫣

```
🐱 Gato completo     → ✅ Fácil
🪑🐱 Gato detrás sofá → ❌ Difícil
```

#### 3. **ÁNGULOS Y PERSPECTIVAS** 📐

```
🚗 Vista frontal     → Fácil
🚗 Vista desde arriba → Puede confundir
🚗 Vista lateral      → Diferente apariencia
```

#### 4. **VARIABILIDAD DENTRO DE CLASE** 🐕

```
Todos son "perros" pero muy diferentes:
🐕 Chihuahua
🦮 Pastor Alemán
🐩 Poodle
→ El modelo debe reconocer todos como "perro"
```

#### 5. **SIMILITUD ENTRE CLASES** 😼

```
Difícil distinguir:
🐱 Gato vs 🦁 León (ambos felinos)
🥐 Croissant vs 🥖 Pan (ambos productos de panadería)
```

#### 6. **ESCALA (tamaño del objeto)** 🔍

```
🏠 Casa vista de lejos   → píxeles pequeños
🏠 Casa vista de cerca   → píxeles grandes
→ Mismo objeto, diferente escala
```

### ✅ Soluciones modernas

| Desafío      | Solución                                                       |
| ------------ | -------------------------------------------------------------- |
| Iluminación  | Data augmentation (aumentar brillo/oscuridad en entrenamiento) |
| Oclusiones   | Entrenar con imágenes parcialmente tapadas                     |
| Ángulos      | Rotar imágenes durante entrenamiento                           |
| Variabilidad | Datasets grandes y diversos                                    |
| Similitud    | More training data, better features                            |
| Escala       | Multi-scale detection, image pyramids                          |

---

## 🎯 CONCEPTOS CLAVE PARA EL EXAMEN

### ⚡ Memoriza esto:

1. **Computer Vision** = Máquinas que "ven" y entienden imágenes
2. **Classification** = 1 imagen → 1 etiqueta
3. **Object Detection** = 1 imagen → múltiples objetos + ubicaciones
4. **Segmentation** = 1 imagen → clasificación por píxel
5. **Feature Extraction** = Proceso de identificar patrones en imágenes
6. **CNN** = Tipo de red neuronal especializada en imágenes
7. **Convolutional Layers** = Detectan features (bordes, formas, etc.)
8. **Pooling** = Reduce tamaño manteniendo información importante

### 📝 Preguntas típicas del examen:

**Pregunta:** "Una empresa quiere clasificar productos en su línea de producción como 'defectuoso' o 'no defectuoso'. ¿Qué tipo de modelo necesitan?"
**Respuesta:** Image Classification (solo necesitan una etiqueta por imagen)

**Pregunta:** "Un sistema de conducción autónoma necesita identificar peatones, coches y señales de tráfico en tiempo real. ¿Qué técnica es más apropiada?"
**Respuesta:** Object Detection (necesita detectar múltiples objetos y sus ubicaciones)

**Pregunta:** "¿Qué componente de una CNN es responsable de reducir el tamaño espacial de la representación?"
**Respuesta:** Pooling Layer

---

## 📚 RECURSOS DE MICROSOFT LEARN

### 🔗 Módulos recomendados para HOY:

1. **"Analyze images with the Computer Vision service"**
   - URL: https://learn.microsoft.com/training/modules/analyze-images-computer-vision/
   - Duración: 45 min
   - Nivel: Beginner

2. **"Computer Vision Concepts"**
   - URL: https://learn.microsoft.com/training/modules/get-started-ai-fundamentals/4-understand-computer-vision
   - Duración: 10 min
   - Nivel: Beginner

### 📖 Documentación adicional:

- [Azure AI Vision overview](https://learn.microsoft.com/azure/ai-services/computer-vision/overview)
- [Computer Vision for beginners](https://learn.microsoft.com/shows/ai-show/computer-vision-for-beginners)

---

## 🎴 FLASHCARDS (12 tarjetas)

### Tarjeta 1

**P:** ¿Qué es Computer Vision?  
**R:** La capacidad de las computadoras para "ver" y entender imágenes y videos, identificando objetos, escenas y actividades.

---

### Tarjeta 2

**P:** ¿Cuál es la diferencia entre Classification y Object Detection?  
**R:**

- **Classification:** 1 imagen → 1 etiqueta (¿QUÉ es?)
- **Object Detection:** 1 imagen → múltiples objetos + ubicaciones (¿QUÉ es y DÓNDE está?)

---

### Tarjeta 3

**P:** ¿Qué hace Semantic Segmentation?  
**R:** Clasifica CADA PÍXEL de la imagen según la categoría a la que pertenece, creando contornos precisos de objetos.

---

### Tarjeta 4

**P:** ¿Qué es Feature Extraction en Computer Vision?  
**R:** El proceso mediante el cual un modelo identifica patrones y características visuales en una imagen (bordes, formas, texturas, objetos).

---

### Tarjeta 5

**P:** ¿Qué es una CNN (Convolutional Neural Network)?  
**R:** Una red neuronal especializada en procesar imágenes, que usa capas convolucionales para detectar features a diferentes niveles de abstracción.

---

### Tarjeta 6

**P:** ¿Qué hace una Convolutional Layer?  
**R:** Aplica filtros a la imagen para detectar features específicas como bordes, líneas, texturas y patrones.

---

### Tarjeta 7

**P:** ¿Qué hace una Pooling Layer?  
**R:** Reduce el tamaño espacial de la imagen manteniendo la información más importante, lo que hace el procesamiento más eficiente.

---

### Tarjeta 8

**P:** Nombra 3 aplicaciones reales de Computer Vision  
**R:**

1. Diagnóstico médico (detectar tumores)
2. Vehículos autónomos (reconocer señales)
3. Seguridad (reconocimiento facial)

---

### Tarjeta 9

**P:** ¿Cuándo usarías Object Detection en lugar de Classification?  
**R:** Cuando necesitas detectar y localizar MÚLTIPLES objetos en una imagen, no solo clasificar la imagen completa.

---

### Tarjeta 10

**P:** ¿Qué es un bounding box en Object Detection?  
**R:** Una caja rectangular que rodea un objeto detectado en una imagen, definida por coordenadas (x, y, ancho, alto).

---

### Tarjeta 11

**P:** Nombra 3 desafíos comunes en Computer Vision  
**R:**

1. Variaciones de iluminación
2. Oclusiones (objetos tapados)
3. Diferentes ángulos y perspectivas

---

### Tarjeta 12

**P:** ¿Cómo ve una computadora una imagen?  
**R:** Como una matriz de números (píxeles), donde cada número representa la intensidad de color en ese punto.

---

## ❓ PREGUNTAS DE AUTOEVALUACIÓN

### Pregunta 1 (Fácil)

**Una empresa de ecommerce quiere clasificar automáticamente fotos de productos en categorías como "ropa", "electrónica", "hogar". ¿Qué tipo de modelo de Computer Vision necesitan?**

A) Object Detection  
B) Image Classification  
C) Semantic Segmentation  
D) Instance Segmentation

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Image Classification**

**Explicación:** Solo necesitan asignar UNA categoría por imagen (clasificar toda la foto). No necesitan detectar múltiples objetos ni delimitar contornos precisos.

</details>

---

### Pregunta 2 (Media)

**Un sistema de seguridad en un aeropuerto necesita contar cuántas personas hay en una sala de espera y marcar su ubicación en tiempo real. ¿Qué técnica es más apropiada?**

A) Image Classification  
B) Semantic Segmentation  
C) Object Detection  
D) Facial Recognition

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Object Detection**

**Explicación:** Necesitan detectar MÚLTIPLES personas (objetos) y conocer su UBICACIÓN exacta. Object Detection proporciona cajas delimitadoras para cada persona detectada.

</details>

---

### Pregunta 3 (Media)

**¿Cuál de las siguientes NO es una función típica de una Pooling Layer en una CNN?**

A) Reducir el tamaño espacial de la representación  
B) Disminuir la cantidad de parámetros del modelo  
C) Detectar bordes y líneas en la imagen  
D) Hacer el modelo más eficiente computacionalmente

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Detectar bordes y líneas en la imagen**

**Explicación:** Detectar bordes es función de las **Convolutional Layers**, no de las Pooling Layers. Las Pooling Layers solo reducen tamaño.

</details>

---

### Pregunta 4 (Difícil)

**Una empresa agrícola quiere crear una app que identifique enfermedades en plantas. Necesitan delimitar EXACTAMENTE las áreas afectadas de cada hoja para calcular el porcentaje de daño. ¿Qué técnica deben usar?**

A) Image Classification  
B) Object Detection  
C) Semantic Segmentation  
D) Optical Character Recognition

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Semantic Segmentation**

**Explicación:** Necesitan precisión a nivel de PÍXEL para delimitar exactamente las áreas enfermas. Ni Classification (solo etiqueta) ni Object Detection (solo cajas) ofrecen esa precisión.

</details>

---

### Pregunta 5 (Media)

**¿Qué afirmación sobre Feature Extraction es CORRECTA?**

A) Es un proceso manual donde el programador define qué características buscar  
B) Solo funciona con imágenes en blanco y negro  
C) Las CNNs aprenden automáticamente qué features son importantes  
D) Todas las CNNs extraen exactamente las mismas features

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Las CNNs aprenden automáticamente qué features son importantes**

**Explicación:** Una de las grandes ventajas de las CNNs es que aprenden automáticamente durante el entrenamiento qué features (patrones, formas, texturas) son relevantes para la tarea, sin intervención manual.

</details>

---

### Pregunta 6 (Fácil)

**¿Cuál de estos es un desafío común en Computer Vision?**

A) Las imágenes ocupan muy poco espacio en memoria  
B) Los modelos siempre funcionan perfectamente en cualquier condición  
C) Variaciones en iluminación pueden afectar el rendimiento  
D) Las computadoras ven exactamente igual que los humanos

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: C) Variaciones en iluminación pueden afectar el rendimiento**

**Explicación:** Cambios en la iluminación (día/noche, sombras, contraluz) son uno de los desafíos más comunes que afectan la precisión de los modelos de Computer Vision.

</details>

---

### Pregunta 7 (Difícil - Estilo Microsoft)

**Scenario:** Una cadena de supermercados quiere implementar cajas de auto-checkout donde los clientes simplemente colocan los productos y el sistema los identifica automáticamente. Algunos productos son similares (manzanas rojas vs manzanas verdes, diferentes marcas de leche). ¿Qué combinación de técnicas sería más apropiada?

A) Solo Image Classification con un modelo muy grande  
B) Object Detection + Classification refinada  
C) Semantic Segmentation de todos los productos  
D) Solo reconocimiento de códigos de barras

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Object Detection + Classification refinada**

**Explicación:**

1. **Object Detection** para detectar cada producto individual en la cesta (puede haber múltiples productos)
2. **Classification refinada** para distinguir entre productos similares (manzana roja vs verde)

La Segmentation sería excesiva (no necesitan contornos exactos), y solo códigos de barras no funcionaría si los productos no están bien orientados.

</details>

---

### Pregunta 8 (Media)

**En el contexto de CNNs, ¿qué significa que las primeras capas detecten "features de bajo nivel" y las últimas "features de alto nivel"?**

A) Las primeras capas son más lentas que las últimas  
B) Las primeras detectan patrones simples (bordes, colores) y las últimas detectan objetos completos  
C) Las primeras capas procesan imágenes grandes y las últimas imágenes pequeñas  
D) Las primeras capas son opcionales pero las últimas son obligatorias

<details>
<summary>👉 Ver respuesta</summary>

**Respuesta: B) Las primeras detectan patrones simples (bordes, colores) y las últimas detectan objetos completos**

**Explicación:** Las CNNs aprenden jerárquicamente:

- **Capas iniciales:** features simples (líneas, bordes, colores)
- **Capas intermedias:** formas, texturas
- **Capas finales:** objetos completos (rostros, coches, animales)

</details>

---

## ✅ CHECKLIST DEL DÍA

Marca cada item al completarlo:

- [ ] Leí y entendí PARTE 1: ¿Qué es Computer Vision?
- [ ] Leí y entendí PARTE 2: Tipos de tareas (Classification, Detection, Segmentation)
- [ ] Leí y entendí PARTE 3: Feature Extraction y CNNs
- [ ] Leí y entendí PARTE 4: Desafíos en Computer Vision
- [ ] Completé el módulo de Microsoft Learn sugerido
- [ ] Revisé las 12 flashcards y puedo responderlas
- [ ] Intenté las 8 preguntas de autoevaluación
- [ ] Revisé los conceptos que no entendí bien

---

## 🎯 PREPARACIÓN PARA MAÑANA

**Martes 19 Nov: Azure AI Vision Service**

Mañana aprenderás sobre el servicio específico de Azure para Computer Vision y sus capacidades. Asegúrate de tener claro:

- La diferencia entre los 3 tipos de tareas (Classification, Detection, Segmentation)
- Qué son features y cómo las extrae una CNN
- Ejemplos de aplicaciones reales

---

## 📌 NOTAS IMPORTANTES

### 💡 Tips para estudiar:

1. **No memorices todo:** Enfócate en ENTENDER los conceptos
2. **Piensa en ejemplos reales:** Relaciona cada concepto con aplicaciones que conozcas
3. **Usa las flashcards diariamente:** Repaso espaciado = mejor retención
4. **Pregunta si algo no queda claro:** Es mejor aclarar dudas ahora que antes del examen

### 🎓 Para el examen AI-900:

- Computer Vision representa aprox. 15-20% del examen
- Se enfocan en CASOS DE USO más que en detalles técnicos profundos
- Debes poder recomendar qué técnica usar según el escenario
- Conocer las capacidades de Azure AI Vision (lo veremos mañana)

---

## 📞 ¿DUDAS O NECESITAS AYUDA?

Si algo no quedó claro o necesitas más explicación sobre algún concepto, no dudes en preguntar. Estamos aquí para asegurar que domines cada tema antes de seguir adelante.

---

**🎉 ¡Excelente trabajo hoy! Has dado un gran paso en tu preparación para el AI-900.**

**Siguiente sesión:** Martes 19 Nov - Azure AI Vision Service (servicios específicos de Azure)

---

_Documento creado: Lunes 18 de Noviembre, 2025_  
_Roadmap: Semana 3 de 6 | AI-900 Certification Prep_
