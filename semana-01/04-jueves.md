# 📚 SEMANA 1 - JUEVES

---

## 📖 JUEVES 6 NOV (1.5 horas) - AI Workloads y Azure AI Services

### 🎯 Objetivo del día

Entender los tipos de WORKLOADS (cargas de trabajo) de IA y qué SERVICIOS de Azure usar para cada uno

---

## 🗺️ CONCEPTO CLAVE: Workloads vs Services

### 💡 ¿Cuál es la diferencia?

**WORKLOAD (Carga de trabajo) = EL PROBLEMA**

- ¿Qué tipo de tarea de IA necesito resolver?
- Ejemplo: "Necesito analizar imágenes"

**SERVICE (Servicio) = LA SOLUCIÓN**

- ¿Qué herramienta de Azure uso?
- Ejemplo: "Uso Azure AI Vision"

---

### 📊 Analogía simple:

```
WORKLOAD = Tipo de enfermedad
SERVICE = Medicamento específico

Tienes dolor de cabeza (workload)
   ↓
Tomas ibuprofeno (service)

Necesitas analizar imágenes (workload)
   ↓
Usas Azure AI Vision (service)
```

---

## 🎯 LOS 6 COMMON AI WORKLOADS (según Microsoft)

Estos son los tipos de problemas que la IA puede resolver:

```
COMMON AI WORKLOADS
│
├── 1. 👁️ Computer Vision workloads
├── 2. 💬 Natural Language Processing (NLP) workloads
├── 3. 🔊 Speech workloads
├── 4. 📄 Document Intelligence workloads
├── 5. 🎯 Decision workloads
├── 6. 🎨 Generative AI workloads
└── 7. 🧠 Machine Learning (crear modelos custom)
```

**IMPORTANTE para el examen:**

- El examen pregunta primero por WORKLOADS
- Luego te pregunta qué SERVICE usar
- Debes conocer ambos

---

## 👁️ 1. COMPUTER VISION WORKLOADS

### 🎯 ¿Qué es?

Workloads relacionados con **analizar y entender contenido visual** (imágenes, videos).

### 📋 Tipos de tareas (sub-workloads):

#### 1.1 Image Classification

**Qué hace:** Clasificar una imagen completa en categorías
**Pregunta:** "¿QUÉ es esto?"
**Ejemplo:**

- Esta imagen es de un "gato" 🐱
- Esta imagen es de "comida" 🍕

#### 1.2 Object Detection

**Qué hace:** Detectar y localizar objetos específicos en una imagen
**Pregunta:** "¿DÓNDE están las cosas?"
**Ejemplo:**

- En esta imagen hay 3 personas, 2 coches y 1 perro
- Ubicación: persona en coordenadas (x, y)

#### 1.3 Optical Character Recognition (OCR)

**Qué hace:** Extraer texto de imágenes o documentos
**Pregunta:** "¿Qué texto hay aquí?"
**Ejemplo:**

- Leer texto de una foto de un recibo
- Digitalizar documentos escaneados

#### 1.4 Facial Detection and Analysis

**Qué hace:** Detectar caras y analizar atributos
**Pregunta:** "¿Hay caras? ¿Qué características tienen?"
**Ejemplo:**

- Detectar 5 caras en una foto grupal
- Estimar edad, emoción, accesorios

#### 1.5 Video Analysis

**Qué hace:** Analizar contenido de videos
**Ejemplo:**

- Detectar escenas en un video
- Identificar personas famosas
- Extraer texto de subtítulos

---

### 🛠️ SERVICIOS de Azure para Computer Vision workloads:

| Servicio de Azure                  | Para qué workload                                             | Cuándo usarlo                                       |
| ---------------------------------- | ------------------------------------------------------------- | --------------------------------------------------- |
| **Azure AI Vision**                | Image classification, Object detection, OCR, análisis general | Tareas genéricas de visión                          |
| **Azure AI Custom Vision**         | Image classification y Object detection PERSONALIZADOS        | Necesitas clasificar TUS objetos específicos        |
| **Azure AI Face API**              | Facial detection y analysis                                   | Reconocimiento facial, análisis de emociones        |
| **Azure AI Video Indexer**         | Video analysis                                                | Analizar contenido de videos                        |
| **Azure AI Document Intelligence** | OCR avanzado + Document processing                            | Extraer datos estructurados de formularios/facturas |

---

### 💡 Casos de uso reales:

**Retail (tienda):**

- Workload: Object detection
- Service: Azure AI Vision o Custom Vision
- Ejemplo: Detectar productos en estantes

**Seguridad:**

- Workload: Facial detection
- Service: Azure AI Face
- Ejemplo: Control de acceso con reconocimiento facial

**Contabilidad:**

- Workload: OCR + Document processing
- Service: Azure AI Document Intelligence
- Ejemplo: Procesar facturas automáticamente

**Manufactura:**

- Workload: Image classification (personalizado)
- Service: Custom Vision
- Ejemplo: Detectar productos defectuosos vs buenos

---

## 💬 2. NATURAL LANGUAGE PROCESSING (NLP) WORKLOADS

### 🎯 ¿Qué es?

Workloads relacionados con **entender y procesar lenguaje humano** (texto escrito).

### 📋 Tipos de tareas (sub-workloads):

#### 2.1 Sentiment Analysis

**Qué hace:** Determinar si un texto es positivo, negativo o neutral
**Ejemplo:**

- "¡Me encantó!" → Positivo (score: 0.95)
- "Horrible producto" → Negativo (score: 0.10)

#### 2.2 Key Phrase Extraction

**Qué hace:** Extraer las ideas principales de un texto
**Ejemplo:**

- Texto: [artículo largo sobre cambio climático]
- Frases clave: "cambio climático", "emisiones CO2", "energías renovables"

#### 2.3 Named Entity Recognition (NER)

**Qué hace:** Identificar y categorizar entidades en texto
**Ejemplo:**

- Texto: "María viajó a París el 15 de octubre"
- Entidades: María (Persona), París (Lugar), 15 de octubre (Fecha)

#### 2.4 Language Detection

**Qué hace:** Identificar en qué idioma está escrito un texto
**Ejemplo:**

- "Hello world" → Inglés
- "Hola mundo" → Español

#### 2.5 Language Translation

**Qué hace:** Traducir texto entre idiomas
**Ejemplo:**

- "Hello" → "Hola" (Inglés → Español)

#### 2.6 Question Answering

**Qué hace:** Responder preguntas basándose en conocimiento
**Ejemplo:**

- Base de datos: "Horario: Lunes a Viernes 9-18h"
- Pregunta: "¿A qué hora abren?"
- Respuesta: "9:00"

#### 2.7 Language Understanding

**Qué hace:** Entender intención y entidades en comandos
**Ejemplo:**

- Usuario dice: "Reserva una mesa para 4 personas mañana a las 8pm"
- Intención: ReservarMesa
- Entidades: Personas=4, Fecha=mañana, Hora=20:00

---

### 🛠️ SERVICIOS de Azure para NLP workloads:

| Servicio de Azure                               | Para qué workload                                        | Cuándo usarlo                         |
| ----------------------------------------------- | -------------------------------------------------------- | ------------------------------------- |
| **Azure AI Language**                           | Sentiment analysis, Key phrases, NER, Language detection | Análisis general de texto             |
| **Azure AI Translator**                         | Language translation                                     | Traducir textos o documentos          |
| **Question Answering**                          | Question answering                                       | Crear bots de FAQ                     |
| **Conversational Language Understanding (CLU)** | Language understanding                                   | Bots conversacionales con intenciones |

---

### 💡 Casos de uso reales:

**E-commerce:**

- Workload: Sentiment analysis
- Service: Azure AI Language
- Ejemplo: Analizar opiniones de clientes sobre productos

**Recursos Humanos:**

- Workload: Named Entity Recognition
- Service: Azure AI Language
- Ejemplo: Procesar CVs automáticamente (extraer nombres, fechas, empresas)

**Sitio web internacional:**

- Workload: Language translation
- Service: Azure AI Translator
- Ejemplo: Traducir contenido a 20 idiomas

**Atención al cliente:**

- Workload: Question answering
- Service: Question Answering + Bot Service
- Ejemplo: Bot que responde preguntas frecuentes 24/7

---

## 🔊 3. SPEECH WORKLOADS

### 🎯 ¿Qué es?

Workloads relacionados con **procesar voz/audio** (hablar y escuchar).

### 📋 Tipos de tareas (sub-workloads):

#### 3.1 Speech Recognition (Speech-to-Text)

**Qué hace:** Convertir audio hablado en texto escrito
**Ejemplo:**

- Usuario habla: "Hola, ¿cómo estás?"
- Sistema transcribe: "Hola, ¿cómo estás?"

#### 3.2 Speech Synthesis (Text-to-Speech)

**Qué hace:** Convertir texto escrito en audio hablado
**Ejemplo:**

- Texto: "Bienvenido a nuestra aplicación"
- Sistema lo dice en voz alta (audio)

#### 3.3 Speech Translation

**Qué hace:** Traducir voz de un idioma a otro en tiempo real
**Ejemplo:**

- Usuario habla en español
- Sistema responde en inglés (audio)

#### 3.4 Speaker Recognition

**Qué hace:** Identificar quién está hablando
**Ejemplo:**

- Sistema identifica: "Esta es la voz de Juan" (verificación de identidad)

---

### 🛠️ SERVICIOS de Azure para Speech workloads:

| Servicio de Azure   | Para qué workload                                                | Cuándo usarlo              |
| ------------------- | ---------------------------------------------------------------- | -------------------------- |
| **Azure AI Speech** | Speech-to-Text, Text-to-Speech, Translation, Speaker Recognition | TODOS los workloads de voz |

**Nota:** Azure AI Speech es UN servicio que hace TODOS los workloads de voz.

---

### 💡 Casos de uso reales:

**Reuniones:**

- Workload: Speech recognition
- Service: Azure AI Speech (Speech-to-Text)
- Ejemplo: Transcribir reuniones automáticamente

**Asistente virtual:**

- Workload: Speech synthesis
- Service: Azure AI Speech (Text-to-Speech)
- Ejemplo: Alexa, Siri responden con voz

**App de viajes:**

- Workload: Speech translation
- Service: Azure AI Speech (Translation)
- Ejemplo: Traducir conversaciones en tiempo real

**Banca:**

- Workload: Speaker recognition
- Service: Azure AI Speech (Speaker Recognition)
- Ejemplo: Verificar identidad por voz en llamadas

---

## 📄 4. DOCUMENT INTELLIGENCE WORKLOADS

### 🎯 ¿Qué es?

Workloads relacionados con **extraer información estructurada de documentos**.

### 📋 Tipos de tareas:

#### 4.1 Form Processing

**Qué hace:** Extraer datos de formularios estructurados
**Ejemplo:**

- Procesar formularios médicos
- Extraer: Nombre, Fecha de nacimiento, Diagnóstico

#### 4.2 Invoice Processing

**Qué hace:** Extraer datos de facturas
**Ejemplo:**

- De una factura extraer: Vendedor, Total, Fecha, Items

#### 4.3 Receipt Processing

**Qué hace:** Extraer datos de recibos
**Ejemplo:**

- De un ticket extraer: Tienda, Total, Fecha, Productos

#### 4.4 ID Document Processing

**Qué hace:** Extraer datos de documentos de identidad
**Ejemplo:**

- De un pasaporte extraer: Nombre, Número, Fecha de expiración

---

### 🛠️ SERVICIOS de Azure para Document Intelligence:

| Servicio de Azure                  | Para qué workload                               | Cuándo usarlo                             |
| ---------------------------------- | ----------------------------------------------- | ----------------------------------------- |
| **Azure AI Document Intelligence** | Form processing, Invoice, Receipt, ID documents | Extraer datos estructurados de documentos |
| **Azure AI Vision (Read API)**     | OCR simple                                      | Solo leer texto, sin estructura           |

**Diferencia clave:**

- **Read API (Vision):** Solo lee texto "plano"
- **Document Intelligence:** Lee texto Y entiende la estructura (campos, tablas, etc.)

---

### 💡 Casos de uso reales:

**Contabilidad:**

- Workload: Invoice processing
- Service: Azure AI Document Intelligence
- Ejemplo: Procesar miles de facturas automáticamente

**Finanzas:**

- Workload: Receipt processing
- Service: Azure AI Document Intelligence
- Ejemplo: App de gastos que procesa recibos con foto

**Verificación de identidad:**

- Workload: ID document processing
- Service: Azure AI Document Intelligence
- Ejemplo: Verificar pasaportes en aeropuertos

---

## 🎯 5. DECISION WORKLOADS

### 🎯 ¿Qué es?

Workloads relacionados con **tomar decisiones automatizadas basadas en datos**.

### 📋 Tipos de tareas:

#### 5.1 Anomaly Detection

**Qué hace:** Detectar patrones inusuales en datos
**Ejemplo:**

- Detectar picos sospechosos en transacciones financieras
- Identificar fallas en sensores industriales

#### 5.2 Content Moderation

**Qué hace:** Moderar contenido inapropiado
**Ejemplo:**

- Detectar contenido ofensivo en comentarios
- Filtrar imágenes inapropiadas

#### 5.3 Personalization

**Qué hace:** Personalizar experiencias de usuario
**Ejemplo:**

- Recomendar productos basándose en historial
- Personalizar contenido de app

---

### 🛠️ SERVICIOS de Azure para Decision workloads:

| Servicio de Azure             | Para qué workload  | Cuándo usarlo                                    |
| ----------------------------- | ------------------ | ------------------------------------------------ |
| **Azure AI Anomaly Detector** | Anomaly detection  | Detectar patrones inusuales en series temporales |
| **Azure AI Content Safety**   | Content moderation | Moderar contenido generado por usuarios          |
| **Azure Personalizer**        | Personalization    | ⚠️ DEPRECATED - No usar en nuevos proyectos      |

---

### ⚠️ IMPORTANTE sobre Decision workloads:

**En el examen AI-900 (Mayo 2025):**

- Decision workloads tienen **POCO peso** (~5% o menos)
- Se mencionan brevemente
- NO son el foco principal
- Conoce que existen, pero no profundices mucho

**Enfócate más en:** Vision, NLP, Speech, GenAI, ML

---

### 💡 Casos de uso reales:

**Finanzas:**

- Workload: Anomaly detection
- Service: Azure AI Anomaly Detector
- Ejemplo: Detectar fraude en transacciones

**Redes sociales:**

- Workload: Content moderation
- Service: Azure AI Content Safety
- Ejemplo: Filtrar comentarios ofensivos automáticamente

---

## 🎨 6. GENERATIVE AI WORKLOADS

### 🎯 ¿Qué es?

Workloads relacionados con **crear contenido nuevo** (no solo analizar existente).

### 📋 Tipos de tareas:

#### 6.1 Text Generation

**Qué hace:** Generar texto nuevo
**Ejemplo:**

- Escribir artículos, emails, historias
- Responder preguntas complejas
- Completar código

#### 6.2 Image Generation

**Qué hace:** Crear imágenes desde descripciones de texto
**Ejemplo:**

- "Un astronauta montando un caballo en Marte" → genera imagen

#### 6.3 Code Generation

**Qué hace:** Generar código de programación
**Ejemplo:**

- "Crea una función que ordene una lista" → genera el código

#### 6.4 Conversational AI

**Qué hace:** Mantener conversaciones naturales
**Ejemplo:**

- Chatbots avanzados que entienden contexto
- Asistentes virtuales inteligentes

---

### 🛠️ SERVICIOS de Azure para Generative AI workloads:

| Servicio de Azure        | Para qué workload                                  | Cuándo usarlo                  |
| ------------------------ | -------------------------------------------------- | ------------------------------ |
| **Azure OpenAI Service** | Text generation, Image generation, Code generation | Acceso a GPT-4, DALL-E, Codex  |
| **Azure AI Foundry**     | Crear y desplegar soluciones de GenAI              | Plataforma completa para GenAI |

---

### 💡 Conceptos clave de GenAI:

#### Prompts

**Qué son:** Instrucciones que le das a la IA generativa
**Ejemplo bueno:**

```
"Escribe un email profesional para pedir una reunión con mi jefe
sobre un aumento de sueldo. Tono formal pero amigable.
Máximo 150 palabras."
```

#### Tokens

**Qué son:** Unidades de medida del texto (palabras o partes de palabras)
**Por qué importan:**

- El costo se calcula por tokens
- Los modelos tienen límites de tokens
- Aproximadamente: 1 token ≈ 0.75 palabras en inglés

#### Content Filters

**Qué son:** Sistemas que previenen contenido dañino
**Categorías bloqueadas:**

- Hate speech (discurso de odio)
- Violence (violencia)
- Sexual content (contenido sexual)
- Self-harm (autolesiones)

---

### 💡 Casos de uso reales:

**Marketing:**

- Workload: Text generation
- Service: Azure OpenAI (GPT-4)
- Ejemplo: Generar descripciones de productos automáticamente

**Diseño:**

- Workload: Image generation
- Service: Azure OpenAI (DALL-E)
- Ejemplo: Crear ilustraciones para blog posts

**Desarrollo:**

- Workload: Code generation
- Service: Azure OpenAI (Codex)
- Ejemplo: GitHub Copilot

**Atención al cliente:**

- Workload: Conversational AI
- Service: Azure OpenAI + Azure AI Foundry
- Ejemplo: Chatbot que responde preguntas complejas

---

## 🧠 7. MACHINE LEARNING

### 🎯 ¿Qué es?

Crear y entrenar **modelos de ML personalizados** para problemas específicos.

**Nota:** ML no es un "workload" como los anteriores, es la **base** de muchos workloads.

### 📋 Tipos de ML:

#### 7.1 Supervised Learning

- Regresión (predecir números)
- Clasificación (predecir categorías)

#### 7.2 Unsupervised Learning

- Clustering (agrupar similares)

#### 7.3 Reinforcement Learning

- Aprender por prueba y error

---

### 🛠️ SERVICIOS de Azure para Machine Learning:

| Servicio de Azure          | Para qué                                                  | Cuándo usarlo                                   |
| -------------------------- | --------------------------------------------------------- | ----------------------------------------------- |
| **Azure Machine Learning** | Entrenar, desplegar y gestionar modelos ML personalizados | Necesitas un modelo específico para TU problema |
| **Automated ML (AutoML)**  | Entrenar modelos automáticamente                          | Quieres ML sin ser experto                      |
| **Azure ML Designer**      | Crear ML visualmente (drag & drop)                        | Prefieres herramienta visual sin código         |

---

### 💡 Casos de uso reales:

**Retail:**

- ML Type: Regresión supervisada
- Service: Azure ML + AutoML
- Ejemplo: Predecir ventas futuras

**Banca:**

- ML Type: Clasificación supervisada
- Service: Azure ML
- Ejemplo: Detectar fraude en transacciones

**Marketing:**

- ML Type: Clustering no supervisado
- Service: Azure ML
- Ejemplo: Segmentar clientes en grupos

---

## 📊 TABLA MAESTRA: WORKLOADS → SERVICES

### Para el examen, memoriza esta tabla:

| WORKLOAD                  | Pregunta típica                                | SERVICIO de Azure                    | Ejemplo real                    |
| ------------------------- | ---------------------------------------------- | ------------------------------------ | ------------------------------- |
| **Computer Vision**       | "Necesito analizar imágenes..."                | Azure AI Vision, Custom Vision, Face | Detectar productos defectuosos  |
| **NLP**                   | "Necesito analizar/entender texto..."          | Azure AI Language, Translator        | Analizar sentimiento de reviews |
| **Speech**                | "Necesito procesar voz..."                     | Azure AI Speech                      | Transcribir reuniones           |
| **Document Intelligence** | "Necesito extraer datos de documentos..."      | Azure AI Document Intelligence       | Procesar facturas               |
| **Decision**              | "Necesito detectar anomalías..."               | Anomaly Detector, Content Safety     | Detectar fraude                 |
| **Generative AI**         | "Necesito generar contenido nuevo..."          | Azure OpenAI, Azure AI Foundry       | Chatbot inteligente             |
| **Machine Learning**      | "Necesito entrenar un modelo personalizado..." | Azure Machine Learning, AutoML       | Predecir ventas                 |

---

## ✅ TAREAS DE HOY (Jueves)

### 1. Microsoft Learn (60 min)

**Módulos a completar:**

- **"Introducción a los servicios de IA de Azure"**
- **"Identify features of common AI workloads"**
- **"Uso de Computer Vision"**
- **"Análisis de texto con Language Services"**

Link principal: https://learn.microsoft.com/es-es/training/paths/get-started-with-artificial-intelligence-on-azure/

---

### 2. Ejercicio: Identificar WORKLOAD y SERVICE (20 min)

**Para cada situación, identifica:**
a) ¿Qué WORKLOAD de IA es?
b) ¿Qué SERVICE de Azure usarías?

---

**Situación 1:**
Una tienda online quiere analizar automáticamente si las reseñas de clientes son positivas, negativas o neutrales para identificar productos con problemas.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 2:**
Un hospital necesita digitalizar miles de documentos médicos escaneados para poder buscar información por texto y extraer datos estructurados de formularios.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 3:**
Una empresa de seguridad quiere un sistema de reconocimiento facial para control de acceso en sus oficinas, que identifique empleados automáticamente.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 4:**
Una app de idiomas necesita convertir la voz del usuario a texto para evaluar su pronunciación y darle feedback.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 5:**
Una fábrica de frutas quiere clasificar automáticamente manzanas en "buenas", "regulares" o "malas" según fotos tomadas en la línea de producción. Tienen 5,000 fotos etiquetadas.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 6:**
Un sitio web internacional necesita traducir automáticamente su contenido (artículos, productos, descripciones) a 20 idiomas diferentes.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 7:**
Una empresa quiere un chatbot que responda preguntas frecuentes de clientes 24/7 basándose en su base de conocimientos de 200 preguntas y respuestas.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

**Situación 8:**
Un banco necesita predecir qué clientes tienen más probabilidad de no pagar su préstamo, basándose en datos históricos de 50,000 clientes.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de ML: **\*\***\_\_\_**\*\***

---

**Situación 9:**
Una startup quiere crear contenido automático para redes sociales: generar textos publicitarios y imágenes atractivas desde descripciones simples de productos.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipos de generación: **\*\***\_\_\_**\*\***

---

**Situación 10:**
Un departamento de contabilidad procesa miles de facturas mensualmente y quiere automatizar la extracción de: vendedor, total, fecha, items, IVA.

a) Workload: **\*\***\_\_\_**\*\***
b) Service: **\*\***\_\_\_**\*\***
c) Tipo específico de tarea: **\*\***\_\_\_**\*\***

---

### 3. Crea Flashcards enfocadas en WORKLOADS (10 min)

**Crea estas 12 tarjetas:**

**Tarjeta 1:**

- Frente: "¿Qué workload uso para analizar contenido visual (imágenes/videos)?"
- Atrás: "Computer Vision workloads"

**Tarjeta 2:**

- Frente: "¿Qué workload uso para analizar y entender texto?"
- Atrás: "Natural Language Processing (NLP) workloads"

**Tarjeta 3:**

- Frente: "¿Qué workload uso para procesar voz/audio?"
- Atrás: "Speech workloads"

**Tarjeta 4:**

- Frente: "¿Qué workload uso para extraer datos estructurados de documentos?"
- Atrás: "Document Intelligence workloads"

**Tarjeta 5:**

- Frente: "¿Qué workload uso para generar contenido nuevo?"
- Atrás: "Generative AI workloads"

**Tarjeta 6:**

- Frente: "Para Computer Vision workloads, ¿qué servicio de Azure uso?"
- Atrás: "Azure AI Vision (genérico) o Custom Vision (personalizado)"

**Tarjeta 7:**

- Frente: "Para NLP workloads de análisis de texto, ¿qué servicio uso?"
- Atrás: "Azure AI Language"

**Tarjeta 8:**

- Frente: "Para Speech workloads, ¿qué servicio uso?"
- Atrás: "Azure AI Speech (hace todo: STT, TTS, translation)"

**Tarjeta 9:**

- Frente: "Para Document Intelligence workloads, ¿qué servicio uso?"
- Atrás: "Azure AI Document Intelligence"

**Tarjeta 10:**

- Frente: "Para Generative AI workloads, ¿qué servicio uso?"
- Atrás: "Azure OpenAI Service o Azure AI Foundry"

**Tarjeta 11:**

- Frente: "Nombra 3 tipos de Computer Vision workloads"
- Atrás: "1) Image classification, 2) Object detection, 3) OCR"

**Tarjeta 12:**

- Frente: "Nombra 3 tipos de NLP workloads"
- Atrás: "1) Sentiment analysis, 2) Named Entity Recognition, 3) Key phrase extraction"

---

## 📝 CONCEPTOS CLAVE DEL JUEVES

**Memoriza:**

- **WORKLOAD = Tipo de problema de IA**
- **SERVICE = Herramienta de Azure para resolver ese problema**
- **Los 6 main workloads:** Vision, NLP, Speech, Document Intelligence, Decision, GenAI
- **Qué servicio usar para cada workload**
- **Decision workloads tienen poco peso en el examen**

---

## ✅ CHECKLIST JUEVES

- [ ] Entiendo la diferencia entre WORKLOAD y SERVICE
- [ ] Conozco los 6 tipos principales de AI workloads
- [ ] Sé qué servicio de Azure usar para cada workload
- [ ] Resolví el ejercicio de identificar workloads y services
- [ ] Creé 12 flashcards nuevas
- [ ] Repasé flashcards de lunes, martes y miércoles (10 min)
- [ ] Puedo explicar qué workload usar para situaciones comunes

---

## 📚 RESPUESTAS AL EJERCICIO (no mires antes de intentarlo)

**Situación 1 (reseñas positivas/negativas):**

- a) Workload: NLP workload
- b) Service: Azure AI Language
- c) Tipo: Sentiment Analysis

**Situación 2 (digitalizar documentos):**

- a) Workload: Document Intelligence workload
- b) Service: Azure AI Document Intelligence
- c) Tipo: Form processing + OCR

**Situación 3 (reconocimiento facial):**

- a) Workload: Computer Vision workload
- b) Service: Azure AI Face
- c) Tipo: Facial detection and recognition

**Situación 4 (voz a texto):**

- a) Workload: Speech workload
- b) Service: Azure AI Speech
- c) Tipo: Speech-to-Text (Speech recognition)

**Situación 5 (clasificar manzanas):**

- a) Workload: Computer Vision workload
- b) Service: Azure AI Custom Vision
- c) Tipo: Image classification (personalizado con sus propias fotos)

**Situación 6 (traducir web):**

- a) Workload: NLP workload
- b) Service: Azure AI Translator
- c) Tipo: Language translation

**Situación 7 (chatbot FAQ):**

- a) Workload: NLP workload
- b) Service: Question Answering + Azure Bot Service
- c) Tipo: Question answering

**Situación 8 (predecir impago préstamos):**

- a) Workload: Machine Learning
- b) Service: Azure Machine Learning (con AutoML)
- c) Tipo: Clasificación supervisada (pagará / no pagará)

**Situación 9 (generar contenido redes sociales):**

- a) Workload: Generative AI workload
- b) Service: Azure OpenAI Service
- c) Tipos: Text generation (GPT) + Image generation (DALL-E)

**Situación 10 (procesar facturas):**

- a) Workload: Document Intelligence workload
- b) Service: Azure AI Document Intelligence
- c) Tipo: Invoice processing

---

## 🎯 AUTOEVALUACIÓN (10 min)

**Responde en voz alta (sí, en voz alta):**

### Pregunta 1:

"¿Cuál es la diferencia entre un workload y un service?"

**Respuesta esperada:**

- Workload = tipo de problema de IA que necesito resolver
- Service = herramienta específica de Azure que uso para resolver ese problema

---

### Pregunta 2:

"Nombra los 6 tipos principales de AI workloads"

**Respuesta esperada:**

1. Computer Vision workloads
2. Natural Language Processing (NLP) workloads
3. Speech workloads
4. Document Intelligence workloads
5. Decision workloads
6. Generative AI workloads

---

### Pregunta 3:

"Si necesito detectar objetos en imágenes de seguridad, ¿qué workload es y qué service uso?"

**Respuesta esperada:**

- Workload: Computer Vision workload
- Tipo específico: Object detection
- Service: Azure AI Vision (si es genérico) o Custom Vision (si necesito detectar objetos específicos míos)

---

### Pregunta 4:

"¿Por qué usaría Custom Vision en vez de Azure AI Vision?"

**Respuesta esperada:**

- Azure AI Vision = análisis genérico de cualquier imagen
- Custom Vision = cuando necesito clasificar/detectar objetos ESPECÍFICOS de mi negocio con mis propias fotos
- Ejemplo: Detectar defectos específicos en productos de mi fábrica

---

### Pregunta 5:

"Nombra 3 tipos de tareas de NLP workloads y para qué sirven"

**Respuesta esperada:**

1. Sentiment Analysis = detectar si texto es positivo/negativo/neutral
2. Named Entity Recognition = extraer personas, lugares, fechas de textos
3. Key phrase extraction = extraer ideas principales de un texto

---

### Pregunta 6:

"¿Cuál es la diferencia entre Azure AI Vision (Read API) y Azure AI Document Intelligence?"

**Respuesta esperada:**

- Read API = solo lee texto "plano" de imágenes (OCR simple)
- Document Intelligence = lee texto Y entiende estructura (campos, tablas, formularios)
- Ejemplo: Document Intelligence puede extraer "Total: $500" de una factura y sabe que es el total

---

### Pregunta 7:

"¿Qué workload y service usaría para un chatbot que genera respuestas inteligentes y personalizadas?"

**Respuesta esperada:**

- Workload: Generative AI workload (Conversational AI)
- Service: Azure OpenAI Service (con GPT-4)
- Por qué: Necesita generar contenido nuevo, no solo respuestas pre-programadas

---

## 📊 COMPARACIÓN: WORKLOADS SIMILARES

### 🔍 Confusiones comunes que debes aclarar:

#### 1. Computer Vision vs Document Intelligence

| Aspecto         | Computer Vision               | Document Intelligence                   |
| --------------- | ----------------------------- | --------------------------------------- |
| **Qué analiza** | Imágenes generales            | Documentos estructurados                |
| **Objetivo**    | Entender contenido visual     | Extraer datos específicos               |
| **OCR**         | Lee texto plano               | Lee texto + estructura                  |
| **Ejemplo**     | "Esta es una foto de un gato" | "Factura: Total=$500, Fecha=15/03/2024" |

---

#### 2. Azure AI Vision vs Custom Vision

| Aspecto         | Azure AI Vision             | Custom Vision                                            |
| --------------- | --------------------------- | -------------------------------------------------------- |
| **Tipo**        | Pre-entrenado genérico      | Entrenar con TUS datos                                   |
| **Cuándo usar** | Objetos comunes             | Objetos específicos tuyos                                |
| **Ejemplo**     | Detectar "persona", "coche" | Detectar "grieta tipo A", "grieta tipo B" en tu producto |
| **Setup**       | Usar inmediatamente         | Subir fotos, etiquetar, entrenar                         |

---

#### 3. NLP vs Speech

| Aspecto     | NLP                    | Speech                         |
| ----------- | ---------------------- | ------------------------------ |
| **Input**   | Texto escrito          | Audio/voz                      |
| **Procesa** | Palabras escritas      | Sonido de voz                  |
| **Ejemplo** | Analizar email escrito | Transcribir llamada telefónica |
| **Service** | Azure AI Language      | Azure AI Speech                |

**Nota:** A veces Speech se considera parte de NLP porque al final procesa lenguaje, pero en Azure son servicios separados.

---

#### 4. Question Answering vs Generative AI (GPT)

| Aspecto          | Question Answering                     | GPT (Generative AI)                  |
| ---------------- | -------------------------------------- | ------------------------------------ |
| **Respuestas**   | Pre-definidas en base de conocimientos | Generadas dinámicamente              |
| **Flexibilidad** | Solo responde lo que está en la base   | Puede responder cualquier cosa       |
| **Precisión**    | Muy preciso (solo info verificada)     | Puede "alucinar" (inventar)          |
| **Costo**        | Más económico                          | Más costoso                          |
| **Ejemplo**      | Bot FAQ: "¿Horario?" → "9-18h"         | ChatGPT: responde cualquier pregunta |

---

## 🎓 PREGUNTAS TIPO EXAMEN

### Pregunta 1: Identificar workload

**Una empresa de manufactura necesita inspeccionar automáticamente productos en su línea de producción para identificar defectos visuales. ¿Qué tipo de AI workload es este?**

A) Natural Language Processing workload
B) Computer Vision workload ✅
C) Speech workload
D) Decision workload

**Por qué B:** Analizar imágenes para detectar defectos es Computer Vision.

---

### Pregunta 2: Identificar service

**Una empresa ya identificó que necesita un Computer Vision workload para clasificar productos defectuosos vs buenos. Tienen 10,000 fotos etiquetadas de sus productos específicos. ¿Qué servicio de Azure deberían usar?**

A) Azure AI Vision
B) Azure AI Custom Vision ✅
C) Azure AI Face
D) Azure AI Document Intelligence

**Por qué B:** Tienen fotos específicas de SUS productos → Custom Vision.

---

### Pregunta 3: Workload vs Service

**¿Cuál es la diferencia principal entre un AI workload y un Azure AI service?**

A) Son lo mismo
B) Workload es el tipo de problema, Service es la herramienta de Azure ✅
C) Workload es más caro que Service
D) Service solo funciona en la nube

**Por qué B:** Workload = problema, Service = solución.

---

### Pregunta 4: NLP tasks

**Una empresa quiere analizar miles de tweets sobre su marca para entender si la percepción pública es positiva o negativa. ¿Qué tipo específico de NLP workload necesitan?**

A) Key phrase extraction
B) Named Entity Recognition
C) Sentiment Analysis ✅
D) Language translation

**Por qué C:** Detectar si es positivo/negativo = Sentiment Analysis.

---

### Pregunta 5: Document Intelligence

**¿Cuál es la principal ventaja de Azure AI Document Intelligence sobre Azure AI Vision (Read API) para procesar facturas?**

A) Document Intelligence es más barato
B) Document Intelligence solo lee texto plano
C) Document Intelligence entiende la estructura del documento y puede extraer campos específicos ✅
D) Document Intelligence funciona más rápido

**Por qué C:** Document Intelligence extrae datos estructurados, no solo texto.

---

### Pregunta 6: Generative AI

**Una empresa quiere crear un asistente virtual que pueda responder preguntas complejas de clientes y generar respuestas personalizadas que no están pre-programadas. ¿Qué workload y service necesitan?**

A) NLP workload con Question Answering
B) Generative AI workload con Azure OpenAI Service ✅
C) Speech workload con Azure AI Speech
D) Decision workload con Anomaly Detector

**Por qué B:** Generar respuestas nuevas (no pre-programadas) = Generative AI.

---

### Pregunta 7: Multiple services

**Una aplicación necesita: (1) transcribir voz del usuario, (2) analizar el sentimiento de lo que dijo, (3) traducirlo a otro idioma. ¿Qué servicios de Azure necesita? (Selecciona 3)**

A) Azure AI Speech ✅
B) Azure AI Language ✅
C) Azure AI Translator ✅
D) Azure AI Vision
E) Azure OpenAI Service

**Por qué A, B, C:**

- Speech = transcribir voz (Speech-to-Text)
- Language = analizar sentimiento
- Translator = traducir a otro idioma

---

## 📋 TABLA PARA IMPRIMIR Y PEGAR EN TU ESCRITORIO

```
╔═══════════════════════════════════════════════════════════╗
║           WORKLOADS → SERVICES CHEAT SHEET               ║
╠═══════════════════════════════════════════════════════════╣
║ 🎯 PROBLEMA          → 🛠️ SOLUCIÓN DE AZURE              ║
╠═══════════════════════════════════════════════════════════╣
║ Analizar imágenes     → Azure AI Vision                  ║
║ Clasificar MIS fotos  → Azure AI Custom Vision           ║
║ Reconocer caras       → Azure AI Face                    ║
║ Leer texto (OCR)      → Azure AI Vision (Read)           ║
║ Procesar documentos   → Azure AI Document Intelligence   ║
╠═══════════════════════════════════════════════════════════╣
║ Analizar sentimiento  → Azure AI Language                ║
║ Extraer entidades     → Azure AI Language                ║
║ Traducir textos       → Azure AI Translator              ║
║ Bot FAQ              → Question Answering                ║
╠═══════════════════════════════════════════════════════════╣
║ Voz a texto          → Azure AI Speech (STT)             ║
║ Texto a voz          → Azure AI Speech (TTS)             ║
║ Traducir voz         → Azure AI Speech (Translation)     ║
╠═══════════════════════════════════════════════════════════╣
║ Generar texto        → Azure OpenAI (GPT)                ║
║ Generar imágenes     → Azure OpenAI (DALL-E)             ║
║ Generar código       → Azure OpenAI (Codex)              ║
║ Chatbot inteligente  → Azure OpenAI + AI Foundry         ║
╠═══════════════════════════════════════════════════════════╣
║ Entrenar modelo ML   → Azure Machine Learning            ║
║ ML sin ser experto   → Automated ML (AutoML)             ║
║ ML visual            → Azure ML Designer                 ║
╠═══════════════════════════════════════════════════════════╣
║ Detectar anomalías   → Azure AI Anomaly Detector         ║
║ Moderar contenido    → Azure AI Content Safety           ║
╚═══════════════════════════════════════════════════════════╝
```

---

## 💡 TIPS PARA EL EXAMEN

### 1. Lee la pregunta buscando palabras clave:

**Palabras clave para Computer Vision:**

- "analizar imágenes", "detectar objetos", "clasificar fotos", "reconocer caras", "leer texto en imagen"

**Palabras clave para NLP:**

- "analizar texto", "sentimiento", "entidades", "traducir", "entender lenguaje"

**Palabras clave para Speech:**

- "voz", "audio", "transcribir", "speech", "hablar"

**Palabras clave para Document Intelligence:**

- "facturas", "formularios", "documentos estructurados", "extraer campos"

**Palabras clave para GenAI:**

- "generar", "crear contenido", "chatbot inteligente", "respuestas personalizadas"

**Palabras clave para ML:**

- "entrenar modelo", "predecir", "clasificar" (con datos históricos), "personalizado"

---

### 2. Proceso de 2 pasos:

**Paso 1:** ¿Qué WORKLOAD es?

- Lee el problema
- Identifica: ¿Imágenes? ¿Texto? ¿Voz? ¿Generar? ¿ML?

**Paso 2:** ¿Qué SERVICE usar?

- Si es Computer Vision: ¿Genérico (Vision) o Personalizado (Custom Vision)?
- Si es NLP: ¿Qué tipo? (Sentiment, NER, Translation, etc.)
- Si es GenAI: ¿Qué tipo de contenido? (Texto=GPT, Imagen=DALL-E)

---

### 3. Pistas en las opciones:

Si las opciones son:

- A) Azure AI Vision
- B) Azure AI Custom Vision
- C) Azure AI Language
- D) Azure OpenAI

**Pregúntate:**

- Si menciona "fotos propias/específicas" → Custom Vision
- Si menciona "generar contenido" → OpenAI
- Si menciona "texto/sentimiento" → Language

---

## 🎊 ¡FELICIDADES POR COMPLETAR EL JUEVES!

**Lo que ahora entiendes:**

✅ **Diferencia clara entre WORKLOAD y SERVICE**

- Workload = tipo de problema
- Service = herramienta de Azure

✅ **Los 6 tipos principales de AI workloads**

- Computer Vision
- NLP
- Speech
- Document Intelligence
- Decision
- Generative AI

✅ **Qué servicio usar para cada workload**

- Tabla completa memorizada

✅ **Cómo identificar workloads en situaciones reales**

- Ejercicio de 10 situaciones completado

✅ **Diferencias clave entre servicios similares**

- Vision vs Custom Vision
- Read API vs Document Intelligence
- Question Answering vs GPT

---

## 📅 SIGUIENTE PASO

**Mañana (Viernes):**

- Repasarás TODO lo de la semana
- Consolidarás estos conceptos
- Harás autoevaluación
- Identificarás áreas débiles

**Este nuevo enfoque de WORKLOADS es CLAVE para el examen.**

---

## 🔄 IMPACTO EN EL RESTO DEL ROADMAP

### ¿Necesitamos cambiar las otras semanas?

**Semana 1:** ✅

**Semana 2 (Machine Learning):** ✅

- Ya enfoca ML como "entrenar modelos personalizados"
- Solo pequeños ajustes de terminología

**Semana 3 (Computer Vision):** ⚠️ Necesita ajustes menores

- Cambiar "servicios de visión" → "Computer Vision workloads"
- Mantener estructura pero enfatizar: workload primero, service después

**Semana 4 (NLP):** ⚠️ Necesita ajustes menores

- Cambiar "servicios de lenguaje" → "NLP workloads"
- Misma estructura, diferente enfoque

**Semana 5 (GenAI):** ⚠️ Necesita actualización

- Añadir Azure AI Foundry
- Enfoque en "Generative AI workloads"

**Semana 6 (Examen):** ✅ Ya incluye esta perspectiva en practice tests

---

## 💬 PARA TI

**Este Jueves:**

- ✅ Está alineado con el examen actual (Mayo 2025)
- ✅ Usa la terminología correcta (WORKLOADS)
- ✅ Te prepara mejor para las preguntas reales
- ✅ Es el enfoque que Microsoft usa en la guía oficial

**Cuando llegues a Semanas 3, 4 y 5:**

- Pídeme las versiones con el enfoque de WORKLOADS
- Te las daré con la misma calidad que este Jueves

---

## ✅ CHECKLIST FINAL JUEVES

- [ ] Entiendo WORKLOAD vs SERVICE perfectamente
- [ ] Conozco los 6 main AI workloads
- [ ] Sé qué Azure service usar para cada workload
- [ ] Completé el ejercicio de 10 situaciones
- [ ] Creé 12 flashcards de workloads
- [ ] Puedo explicar en voz alta las diferencias clave
- [ ] Entiendo por qué Custom Vision ≠ AI Vision
- [ ] Entiendo por qué Document Intelligence ≠ Read API
- [ ] Sé cuándo usar GenAI vs Question Answering
- [ ] Repasé todas las flashcards anteriores (5-10 min)

---

**¡Excelente trabajo hoy!** 💪

**Mañana es Viernes: repaso y consolidación de toda la semana.**

**Nos vemos mañana o cuando tengas dudas.** 🚀
