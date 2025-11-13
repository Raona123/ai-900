# 📚 SEMANA 2 - MACHINE LEARNING EN PROFUNDIDAD

---

## 📖 JUEVES 13 NOV (1.5 horas) - Azure Machine Learning Workspace

### 🎯 Objetivo del día

Entender qué es Azure Machine Learning, sus componentes principales y cuándo usarlo

---

## 🔄 REPASO RÁPIDO: Lo que has aprendido esta semana

**Lunes:** Tipos de ML (Supervisado, No supervisado, Refuerzo)
**Martes:** Regresión y métricas (MAE, RMSE, R²)
**Miércoles:** Clasificación y métricas (Accuracy, Precision, Recall, F1)

**HOY:** Conectamos toda esa teoría con Azure ML

---

## 🤔 PREGUNTA CLAVE: ¿Qué es Azure Machine Learning?

### 💡 Definición simple:

**Azure Machine Learning (Azure ML) es una plataforma completa en la nube para:**

- Entrenar modelos de ML personalizados
- Gestionar todo el ciclo de vida del ML
- Desplegar modelos en producción
- Monitorear y mantener modelos

**Analogía:**
Azure ML es como un "taller completo de ML" donde tienes todas las herramientas para construir, probar y desplegar modelos desde cero.

---

## 🎯 Azure ML vs Azure AI Services: La diferencia CLAVE

### 📊 Comparación:

| Aspecto             | Azure AI Services                         | Azure Machine Learning                         |
| ------------------- | ----------------------------------------- | ---------------------------------------------- |
| **Qué es**          | Servicios pre-entrenados listos para usar | Plataforma para entrenar TUS propios modelos   |
| **Cuándo usar**     | Problemas genéricos                       | Problemas específicos de TU negocio            |
| **Ejemplos**        | Detectar spam genérico, OCR estándar      | Predecir TUS ventas, clasificar TUS productos  |
| **Código**          | Poco o nada (APIs)                        | Más código (Python, R) o herramientas visuales |
| **Tiempo setup**    | Minutos                                   | Horas/días                                     |
| **Personalización** | Limitada                                  | Total                                          |
| **Datos**           | No necesitas tus datos                    | Necesitas TUS datos históricos                 |

---

### 💡 Ejemplos concretos:

**USA Azure AI Services (pre-entrenado) CUANDO:**

- ✅ Quieres detectar spam en emails (problema genérico)
- ✅ Necesitas traducir textos (problema común)
- ✅ Quieres analizar sentimiento de reseñas (estándar)
- ✅ Necesitas OCR para documentos (funcionalidad general)

**USA Azure ML (entrena tu modelo) CUANDO:**

- 🎯 Quieres predecir ventas de TU empresa (datos específicos)
- 🎯 Necesitas clasificar defectos en TUS productos (imágenes únicas)
- 🎯 Quieres recomendar productos de TU catálogo (datos propios)
- 🎯 Necesitas detectar fraude específico en TU sistema (patrones únicos)

---

### 🔍 Ejemplo visual:

**Problema: Clasificar frutas**

```
OPCIÓN 1: Azure AI Vision (pre-entrenado)
├─ Ventaja: Ya sabe qué es una manzana, naranja, plátano
├─ Desventaja: Solo frutas comunes
└─ Uso: Fotos genéricas de frutas

OPCIÓN 2: Azure ML (entrenas tu modelo)
├─ Ventaja: Puedes entrenar con TUS frutas exóticas específicas
├─ Necesitas: 1000+ fotos de tus frutas etiquetadas
└─ Uso: Clasificar variedades específicas de tu finca
```

---

## 🏢 ¿QUÉ ES UN WORKSPACE?

### 💡 Concepto:

**Workspace = Tu "oficina de ML" en Azure**

Es el lugar central donde:

- 📊 Guardas tus datos
- 🧪 Haces experimentos
- 🤖 Entrenas modelos
- 🚀 Despliegas modelos
- 📈 Monitorizas resultados

**Analogía:**
Como tu escritorio de trabajo donde tienes todo organizado: documentos (datos), proyectos en curso (experimentos), herramientas (compute), productos finales (modelos).

---

### 🏗️ Arquitectura de Workspace:

```
AZURE ML WORKSPACE
│
├── 📊 DATASETS (Datos)
│   └── Tus datos de entrenamiento y prueba
│
├── 🧪 EXPERIMENTS (Experimentos)
│   └── Registros de todos tus entrenamientos
│
├── 🤖 MODELS (Modelos)
│   └── Modelos entrenados guardados
│
├── 🚀 ENDPOINTS (Puntos de acceso)
│   └── Modelos desplegados y accesibles
│
├── 💻 COMPUTE (Recursos de cómputo)
│   └── Máquinas virtuales para entrenar
│
└── 🛠️ ENVIRONMENTS (Entornos)
    └── Configuraciones de software
```

---

## 📊 1. DATASETS (Conjuntos de Datos)

### ¿Qué son?

**Tus datos de entrenamiento y prueba registrados y versionados.**

### Tipos de datos:

**Tabular (Estructurados):**

```
| Cliente_ID | Edad | Compras | Ciudad    | Comprará |
|-----------|------|---------|-----------|----------|
| 001       | 25   | 10      | Madrid    | Sí       |
| 002       | 45   | 2       | Barcelona | No       |
| 003       | 32   | 15      | Valencia  | Sí       |
```

- Archivos: CSV, Excel, SQL databases
- Uso: Regresión, clasificación con datos tabulares

**Files (No estructurados):**

```
📁 imagenes_productos/
  ├── 🖼️ producto_001.jpg
  ├── 🖼️ producto_002.jpg
  └── 🖼️ producto_003.jpg
```

- Archivos: Imágenes, audio, video, texto
- Uso: Computer Vision, NLP, audio processing

---

### 💡 Ventajas de registrar datasets:

✅ **Versionado:** Sabes qué datos usaste en cada modelo
✅ **Reproducibilidad:** Puedes volver a entrenar con los mismos datos
✅ **Compartir:** Tu equipo puede usar los mismos datos
✅ **Trazabilidad:** Auditoría completa

**Ejemplo:**

```
Dataset: ventas_2024_v1.csv
├─ Versión 1: Enero-Marzo (10,000 filas)
├─ Versión 2: Enero-Junio (20,000 filas)
└─ Versión 3: Enero-Diciembre (40,000 filas)

Modelo A entrenado con v1 → R² = 0.75
Modelo B entrenado con v3 → R² = 0.88 (mejor con más datos)
```

---

## 🧪 2. EXPERIMENTS (Experimentos)

### ¿Qué son?

**Un registro de cada vez que entrenas un modelo.**

Cada experimento guarda:

- 📊 Qué datos usaste
- ⚙️ Qué hiperparámetros configuraste
- 📈 Qué métricas obtuviste (accuracy, RMSE, etc.)
- ⏱️ Cuánto tiempo tardó
- 💻 Qué compute usaste

---

### 💡 ¿Por qué son útiles?

**Imagina que entrenas 20 modelos diferentes:**

```
Experimento 1: Decision Tree → Accuracy = 0.75
Experimento 2: Random Forest → Accuracy = 0.82
Experimento 3: Neural Network → Accuracy = 0.88 ✅ (el mejor)
...
Experimento 20: SVM → Accuracy = 0.79
```

**Con Experiments puedes:**

- ✅ Comparar todos los modelos fácilmente
- ✅ Ver cuál fue el mejor y por qué
- ✅ Reproducir el mejor modelo después
- ✅ Compartir resultados con tu equipo

---

### 📊 Información que guarda cada Experiment:

**Ejemplo de un experimento:**

```
EXPERIMENT: prediccion-ventas-exp-15
├─ Fecha: 2024-11-13 10:30
├─ Dataset: ventas_2024_v3.csv
├─ Algoritmo: Random Forest
├─ Hiperparámetros:
│  ├─ n_trees: 100
│  ├─ max_depth: 10
│  └─ min_samples: 5
├─ Métricas obtenidas:
│  ├─ R²: 0.88
│  ├─ RMSE: 1,250€
│  └─ MAE: 980€
├─ Tiempo entrenamiento: 12 minutos
└─ Compute usado: Standard_DS3_v2
```

---

## 🤖 3. MODELS (Modelos)

### ¿Qué son?

**Modelos entrenados y guardados, listos para usar.**

**Analogía:**
Como un producto final en tu taller. Ya está listo, solo necesitas "empaquetarlo" y enviarlo a producción.

---

### 🎯 Registro de modelos:

**Cuando entrenas un modelo bueno, lo REGISTRAS:**

```
MODEL: predictor-ventas
├─ Versión 1: R² = 0.75 (Marzo 2024)
├─ Versión 2: R² = 0.82 (Junio 2024)
└─ Versión 3: R² = 0.88 (Noviembre 2024) ⭐ EN PRODUCCIÓN
```

**Beneficios:**

- ✅ Versionado (puedes volver a v2 si v3 falla)
- ✅ Metadata (sabes con qué se entrenó)
- ✅ Trazabilidad completa
- ✅ Facilita el despliegue

---

### 📦 ¿Qué incluye un modelo registrado?

```
MODELO REGISTRADO: fraud-detector-v3
│
├── 📄 Archivo del modelo (.pkl, .h5)
├── 📊 Métricas de evaluación
│   ├─ Accuracy: 0.95
│   ├─ Precision: 0.92
│   └─ Recall: 0.89
├── 📋 Metadata
│   ├─ Fecha entrenamiento
│   ├─ Dataset usado
│   ├─ Experiment ID
│   └─ Autor
├── 📦 Dependencias
│   └─ Librerías necesarias (scikit-learn 1.2, pandas 2.0)
└── 📝 Descripción y notas
```

---

## 🚀 4. ENDPOINTS (Puntos de Acceso)

### ¿Qué son?

**URLs donde tu modelo está DESPLEGADO y accesible para hacer predicciones.**

**Analogía:**
Como poner tu producto en una tienda online. Está disponible 24/7 para que cualquiera lo use.

---

### 💡 Flujo de despliegue:

```
1. ENTRENAR modelo en Azure ML
   ↓
2. REGISTRAR modelo (si es bueno)
   ↓
3. DESPLEGAR a endpoint
   ↓
4. USAR desde aplicaciones

Aplicación → [HTTP Request] → Endpoint → Modelo → [Predicción] → Aplicación
```

---

### 🔍 Ejemplo práctico:

**Tienes un modelo que predice precios de casas:**

```
ENDPOINT: https://predictor-casas.azureml.net/score

Tu aplicación web envía:
{
  "tamaño": 120,
  "habitaciones": 3,
  "ubicacion": "Madrid"
}

Endpoint responde:
{
  "precio_predicho": 285000,
  "confianza": 0.92
}
```

---

### 🎯 Tipos de despliegue:

**1. Real-time (Tiempo real):**

- ⚡ Respuesta instantánea (milisegundos)
- 🎯 Uso: Apps web, móviles que necesitan respuesta inmediata
- 💰 Costo: Más alto (servidor siempre activo)
- Ejemplo: Detector de fraude en transacciones

**2. Batch (Por lotes):**

- 📦 Procesa muchas predicciones a la vez
- ⏱️ No necesita ser instantáneo
- 💰 Costo: Más bajo (se activa cuando hay trabajo)
- Ejemplo: Analizar todas las transacciones del día por la noche

---

## 💻 5. COMPUTE (Recursos de Cómputo)

### ¿Qué son?

**Las máquinas virtuales que ejecutan tu entrenamiento.**

**Concepto clave:** Entrenar modelos ML consume MUCHA potencia de cómputo.

---

### 🎯 Tipos de Compute:

**1. Compute Instances (Instancias):**

- 💻 Máquina virtual personal
- 🎯 Uso: Desarrollo, experimentación, notebooks
- Ejemplo: Tu "escritorio virtual" para trabajar

**2. Compute Clusters (Clústeres):**

- 🚀 Múltiples máquinas trabajando juntas
- 🎯 Uso: Entrenar modelos grandes, AutoML, muchos experimentos
- ⚙️ Auto-scaling: Se ajusta según necesidad (0-10 nodos)
- Ejemplo: Entrenar 100 variaciones de modelo en paralelo

**3. Inference Clusters:**

- 🌐 Para desplegar modelos (endpoints)
- 🎯 Uso: Servir predicciones en producción
- Ejemplo: Endpoint que recibe 1000 requests/segundo

---

### 💡 ¿Por qué usar Compute Clusters?

**Sin cluster (1 máquina):**

```
Entrenar 10 modelos diferentes:
Modelo 1: 30 min
Modelo 2: 30 min
...
Modelo 10: 30 min
Total: 5 horas ⏱️
```

**Con cluster (10 máquinas):**

```
Entrenar 10 modelos EN PARALELO:
Todos al mismo tiempo: 30 min
Total: 30 minutos ⚡
```

---

### 🎯 Elegir el compute correcto:

| Tarea                      | Compute recomendado          | Ejemplo                |
| -------------------------- | ---------------------------- | ---------------------- |
| Experimentar con notebooks | Compute Instance             | Desarrollo interactivo |
| Entrenar 1 modelo pequeño  | Compute Instance             | Dataset 1000 filas     |
| Entrenar 1 modelo grande   | Compute Cluster (1-2 nodos)  | Dataset 1M filas       |
| AutoML (muchos modelos)    | Compute Cluster (5-10 nodos) | Probar 50 algoritmos   |
| Desplegar modelo           | Inference Cluster / AKS      | Producción             |

---

## 🛠️ AZURE ML DESIGNER (Herramienta Visual)

### ¿Qué es?

**Una herramienta de ARRASTRAR Y SOLTAR (drag & drop) para crear modelos ML SIN CÓDIGO.**

**Analogía:**
Como usar PowerPoint en vez de escribir HTML para hacer una presentación.

---

### 💡 Concepto: Pipelines visuales

**Creas un "pipeline" (tubería) de pasos:**

```
[📊 Dataset]
    ↓
[🧹 Limpiar datos]
    ↓
[✂️ Dividir Train/Test]
    ↓
[🤖 Entrenar modelo]
    ↓
[📊 Evaluar modelo]
    ↓
[💾 Guardar modelo]
```

**Cada paso es un "módulo" que arrastras y conectas.**

---

### 🎯 Componentes del Designer:

**1. Módulos de datos:**

- 📥 Import Data (importar)
- 🧹 Clean Missing Data (limpiar)
- ✂️ Split Data (dividir)
- 🔄 Transform Data (transformar)

**2. Módulos de ML:**

- 🌳 Train Model (entrenar)
- 🎯 Score Model (predecir)
- 📊 Evaluate Model (evaluar)
- 🔧 Tune Hyperparameters (ajustar)

**3. Algoritmos:**

- 📈 Linear Regression
- 🌲 Decision Tree
- 🎲 Random Forest
- 🧠 Neural Network
- Y muchos más...

---

### 💡 Ejemplo visual de pipeline:

```
┌─────────────┐
│   Dataset   │ ventas.csv
│  (CSV file) │
└──────┬──────┘
       │
       ↓
┌─────────────┐
│   Select    │ Elegir columnas: precio, tamaño, ubicación
│   Columns   │
└──────┬──────┘
       │
       ↓
┌─────────────┐
│    Split    │ 80% Train, 20% Test
│    Data     │
└──────┬──────┘
       │
       ├───────────────┐
       ↓               ↓
┌─────────────┐  ┌─────────────┐
│   Train     │  │    Test     │
│   (80%)     │  │    (20%)    │
└──────┬──────┘  └──────┬──────┘
       │                │
       ↓                │
┌─────────────┐         │
│   Train     │         │
│   Model     │ Linear  │
│             │Regression│
└──────┬──────┘         │
       │                │
       ├────────────────┘
       ↓
┌─────────────┐
│   Score     │ Hacer predicciones
│   Model     │
└──────┬──────┘
       │
       ↓
┌─────────────┐
│  Evaluate   │ RMSE, R², MAE
│   Model     │
└─────────────┘
```

---

### ✅ Ventajas del Designer:

✅ **Sin código:** No necesitas programar
✅ **Visual:** Ves todo el flujo claramente
✅ **Rápido:** Arrastrar módulos es más rápido que escribir código
✅ **Educativo:** Entiendes el proceso paso a paso
✅ **Reproducible:** Guardas el pipeline completo

### ⚠️ Limitaciones del Designer:

⚠️ Menos flexible que código
⚠️ No todo se puede hacer visualmente
⚠️ Para modelos muy personalizados, necesitas código

---

## 🎯 FLUJO COMPLETO EN AZURE ML

### 📋 Proceso típico de ML project:

```
1️⃣ PREPARAR DATOS
├─ Subir datos a Azure ML
├─ Crear Dataset registrado
└─ Explorar y limpiar datos

2️⃣ ENTRENAR MODELO
├─ Crear Compute (cluster o instance)
├─ Elegir algoritmo
├─ Configurar hiperparámetros
├─ Entrenar (esto crea un Experiment)
└─ Evaluar métricas (R², Accuracy, etc.)

3️⃣ COMPARAR Y SELECCIONAR
├─ Ver todos los Experiments
├─ Comparar métricas
└─ Elegir el mejor modelo

4️⃣ REGISTRAR MODELO
├─ Guardar el mejor modelo
├─ Versionar
└─ Añadir metadata

5️⃣ DESPLEGAR
├─ Crear Endpoint
├─ Configurar compute para inference
└─ Publicar modelo

6️⃣ USAR EN PRODUCCIÓN
├─ Aplicación hace requests al endpoint
├─ Modelo devuelve predicciones
└─ Monitorizar performance
```

---

## 🎓 PREGUNTAS TIPO EXAMEN

### Pregunta 1:

**¿Cuál es la principal diferencia entre Azure AI Services y Azure Machine Learning?**

A) Azure ML es más barato que AI Services
B) Azure AI Services son modelos pre-entrenados, Azure ML entrena modelos personalizados ✅
C) Azure ML solo funciona con imágenes
D) No hay diferencia, son lo mismo

**Por qué B:** AI Services = pre-entrenado (genérico). Azure ML = entrenas TU modelo (personalizado con TUS datos).

---

### Pregunta 2:

**En Azure Machine Learning, ¿qué es un Workspace?**

A) Una máquina virtual para entrenar modelos
B) Un dataset de entrenamiento
C) El contenedor central que agrupa datasets, experiments, models y compute ✅
D) Un modelo desplegado

**Por qué C:** Workspace es el "contenedor" o "proyecto" que agrupa todos los recursos de ML.

---

### Pregunta 3:

**¿Para qué sirve un Endpoint en Azure ML?**

A) Para almacenar datasets
B) Para desplegar modelos y hacerlos accesibles vía HTTP para predicciones ✅
C) Para entrenar modelos más rápido
D) Para visualizar métricas

**Por qué B:** Endpoint = modelo desplegado accesible vía URL para hacer predicciones en producción.

---

### Pregunta 4:

**¿Qué ventaja tiene usar Compute Clusters en lugar de Compute Instances para AutoML?**

A) Es más barato
B) Permite entrenar múltiples modelos en paralelo ✅
C) Usa menos memoria
D) No hay diferencia

**Por qué B:** Clusters tienen múltiples nodos que pueden entrenar varios modelos simultáneamente (paralelización).

---

### Pregunta 5:

**¿Cuándo usarías Azure ML Designer?**

A) Cuando necesitas entrenar modelos complejos con código personalizado
B) Cuando quieres crear pipelines de ML visualmente sin escribir código ✅
C) Solo para Computer Vision
D) Para desplegar modelos únicamente

**Por qué B:** Designer es la herramienta visual (drag & drop) para crear ML sin código.

---

## ✅ TAREAS DE HOY (Jueves)

### 1. Microsoft Learn (45 min)

**Módulos a completar:**

- **"Introducción a Azure Machine Learning"**
- **"Exploración de Azure Machine Learning workspace"**
- **"Uso de herramientas automatizadas de ML"**

Link: https://learn.microsoft.com/es-es/training/paths/get-started-with-artificial-intelligence-on-azure/

---

### 2. Ejercicio: Identificar componentes (15 min)

**Para cada escenario, identifica qué componentes de Azure ML usarías:**

**Escenario 1:**
Tienes 50,000 registros de clientes con datos históricos de compras. Quieres predecir qué clientes comprarán en el próximo mes.

- ¿Qué crearías primero? **\*\***\_\_\_**\*\***
- ¿Dónde entrenas? **\*\***\_\_\_**\*\***
- ¿Dónde guardas el modelo final? **\*\***\_\_\_**\*\***
- ¿Cómo lo haces accesible para tu app? **\*\***\_\_\_**\*\***

---

**Escenario 2:**
Eres nuevo en ML y quieres crear un modelo de regresión para predecir precios. No sabes programar.

- ¿Qué herramienta de Azure ML usarías? **\*\***\_\_\_**\*\***
- ¿Por qué? **\*\***\_\_\_**\*\***

---

**Escenario 3:**
Necesitas entrenar 50 variaciones de un modelo para encontrar el mejor. Cada modelo tarda 30 minutos.

- ¿Qué tipo de compute usarías? **\*\***\_\_\_**\*\***
- ¿Por qué? **\*\***\_\_\_**\*\***
- ¿Cuánto tiempo ahorrarías vs usar 1 sola máquina? **\*\***\_\_\_**\*\***

---

**Escenario 4:**
Tu modelo está listo y funciona bien. Tu aplicación web necesita hacer predicciones en tiempo real cuando los usuarios interactúan.

- ¿Qué necesitas crear en Azure ML? **\*\***\_\_\_**\*\***
- ¿Qué tipo de despliegue? **\*\***\_\_\_**\*\***

---

### 3. Crea Flashcards (15 min)

**Crea estas 12 tarjetas:**

**Tarjeta 1:**

- Frente: "¿Qué es Azure Machine Learning?"
- Atrás: "Plataforma completa para entrenar, desplegar y gestionar modelos ML personalizados"

**Tarjeta 2:**

- Frente: "Diferencia: Azure AI Services vs Azure ML"
- Atrás: "AI Services = pre-entrenados (genéricos). Azure ML = entrenas TUS modelos (personalizados)"

**Tarjeta 3:**

- Frente: "¿Qué es un Workspace en Azure ML?"
- Atrás: "Contenedor central que agrupa datasets, experiments, models, compute y endpoints"

**Tarjeta 4:**

- Frente: "¿Qué es un Dataset en Azure ML?"
- Atrás: "Tus datos de entrenamiento registrados y versionados (tabular o files)"

**Tarjeta 5:**

- Frente: "¿Qué es un Experiment?"
- Atrás: "Registro de cada entrenamiento: datos, hiperparámetros, métricas, tiempo"

**Tarjeta 6:**

- Frente: "¿Qué es un Model registrado?"
- Atrás: "Modelo entrenado guardado con versionado, metadata y métricas"

**Tarjeta 7:**

- Frente: "¿Qué es un Endpoint?"
- Atrás: "URL donde el modelo está desplegado y accesible para hacer predicciones"

**Tarjeta 8:**

- Frente: "Tipos de Compute en Azure ML"
- Atrás: "Compute Instance (desarrollo), Compute Cluster (entrenamiento paralelo), Inference Cluster (producción)"

**Tarjeta 9:**

- Frente: "¿Qué es Azure ML Designer?"
- Atrás: "Herramienta visual (drag & drop) para crear pipelines de ML sin código"

**Tarjeta 10:**

- Frente: "¿Cuándo usar Compute Cluster?"
- Atrás: "Entrenar modelos grandes, AutoML (muchos modelos), paralelizar entrenamientos"

**Tarjeta 11:**

- Frente: "Diferencia: Real-time vs Batch deployment"
- Atrás: "Real-time = respuesta instantánea (ms). Batch = procesa lotes, no instantáneo"

**Tarjeta 12:**

- Frente: "Flujo básico Azure ML (5 pasos)"
- Atrás: "1) Preparar datos, 2) Entrenar modelo, 3) Comparar experiments, 4) Registrar modelo, 5) Desplegar endpoint"

---

## 📝 CONCEPTOS CLAVE DEL JUEVES

**Memoriza:**

- Azure ML = plataforma para modelos personalizados
- Workspace = contenedor central de todo
- Dataset → Experiment → Model → Endpoint (flujo)
- Designer = herramienta visual sin código
- Compute Cluster = paralelizar entrenamientos
- Endpoint = modelo desplegado accesible
- Azure AI Services (pre-entrenado) vs Azure ML (personalizado)

---

## ✅ CHECKLIST JUEVES

- [ ] Entiendo qué es Azure Machine Learning
- [ ] Sé la diferencia entre Azure AI Services y Azure ML
- [ ] Conozco los 5 componentes del Workspace
- [ ] Entiendo el flujo completo de un proyecto ML
- [ ] Sé qué es Designer y cuándo usarlo
- [ ] Entiendo tipos de Compute y cuándo usar cada uno
- [ ] Completé el ejercicio de identificar componentes
- [ ] Creé 12 flashcards nuevas
- [ ] Repasé flashcards de Lunes-Miércoles (10 min)
- [ ] Puedo explicar el flujo de Azure ML en voz alta

---

## 📚 RESPUESTAS AL EJERCICIO

### Escenario 1 (Predecir clientes que comprarán):

- **¿Qué crearías primero?** Dataset con los 50,000 registros de clientes
- **¿Dónde entrenas?** Compute Instance o Compute Cluster (esto crea un Experiment)
- **¿Dónde guardas el modelo final?** Lo registras como Model en el Workspace
- **¿Cómo lo haces accesible?** Crear un Endpoint (real-time o batch según necesidad)

---

### Escenario 2 (Nuevo en ML, sin programar):

- **¿Qué herramienta usarías?** Azure ML Designer
- **¿Por qué?** Es visual (drag & drop), no requiere código, perfecto para principiantes

---

### Escenario 3 (50 modelos, 30 min cada uno):

- **¿Qué tipo de compute?** Compute Cluster con múltiples nodos
- **¿Por qué?** Permite entrenar múltiples modelos EN PARALELO
- **¿Cuánto ahorras?**
  - 1 máquina: 50 × 30 min = 25 horas
  - Cluster 10 nodos: 5 × 30 min = 2.5 horas
  - Ahorro: 22.5 horas (10x más rápido)

---

### Escenario 4 (Predicciones en tiempo real):

- **¿Qué crear?** Endpoint (punto de acceso)
- **¿Qué tipo?** Real-time deployment (respuesta instantánea para usuarios)

---

## 🎯 DIAGRAMA RESUMEN: Azure ML Ecosystem

```
╔════════════════════════════════════════════════════════════╗
║           AZURE MACHINE LEARNING WORKSPACE                 ║
╠════════════════════════════════════════════════════════════╣
║                                                            ║
║  📊 DATASETS                                               ║
║  ├─ ventas_2024.csv (v1, v2, v3)                          ║
║  ├─ imagenes_productos/ (15,000 fotos)                    ║
║  └─ clientes_historico.parquet                            ║
║                                                            ║
║  ──────────────────────────────────────────               ║
║                                                            ║
║  🧪 EXPERIMENTS                                            ║
║  ├─ exp-01: RandomForest → R²=0.75                        ║
║  ├─ exp-02: XGBoost → R²=0.82                             ║
║  ├─ exp-03: Neural Net → R²=0.88 ⭐ MEJOR                 ║
║  └─ exp-04: Linear Reg → R²=0.70                          ║
║                                                            ║
║  ──────────────────────────────────────────               ║
║                                                            ║
║  🤖 MODELS                                                 ║
║  ├─ predictor-ventas                                       ║
║  │  ├─ v1 (Marzo): R²=0.75                                ║
║  │  ├─ v2 (Junio): R²=0.82                                ║
║  │  └─ v3 (Nov): R²=0.88 🚀 EN PRODUCCIÓN                 ║
║  │                                                         ║
║  └─ clasificador-fraude                                    ║
║     ├─ v1: F1=0.82                                        ║
║     └─ v2: F1=0.91 🚀 EN PRODUCCIÓN                       ║
║                                                            ║
║  ──────────────────────────────────────────               ║
║                                                            ║
║  🚀 ENDPOINTS                                              ║
║  ├─ https://predictor-ventas.azureml.net/score            ║
║  │  └─ Real-time | predictor-ventas-v3                    ║
║  │                                                         ║
║  └─ https://detector-fraude.azureml.net/score             ║
║     └─ Real-time | clasificador-fraude-v2                 ║
║                                                            ║
║  ──────────────────────────────────────────               ║
║                                                            ║
║  💻 COMPUTE                                                ║
║  ├─ Instance: mi-vm-dev (Standard_DS3_v2)                 ║
║  ├─ Cluster: training-cluster (0-10 nodos)                ║
║  └─ AKS: prod-cluster (inference)                         ║
║                                                            ║
╚════════════════════════════════════════════════════════════╝
```

---

## 🔄 CONEXIÓN CON LO APRENDIDO ESTA SEMANA

### 📊 Todo se conecta:

**LUNES: Aprendiste los tipos de ML**

- Supervisado (Regresión, Clasificación)
- No supervisado (Clustering)
- → En Azure ML, eliges el tipo cuando entrenas

**MARTES: Aprendiste métricas de Regresión**

- MAE, RMSE, R²
- → En Azure ML Experiments, ves estas métricas automáticamente

**MIÉRCOLES: Aprendiste métricas de Clasificación**

- Accuracy, Precision, Recall, F1
- → En Azure ML Experiments, ves estas métricas automáticamente

**HOY: Aprendiste dónde y cómo entrenar**

- Azure ML Workspace
- → Es donde HACES todo lo que aprendiste esta semana

**MAÑANA: Aprenderás AutoML**

- → Herramienta que prueba muchos algoritmos automáticamente

**SÁBADO: Practicarás todo**

- → Lab real creando un modelo en Azure ML

---

## 🎯 EJEMPLO COMPLETO: De inicio a fin

### Caso: Predecir cancelaciones de suscripciones

**1. SETUP INICIAL**

```
Crear Workspace: "empresa-ml-prod"
├─ Región: West Europe
├─ Subscription: Mi suscripción
└─ Resource Group: rg-ml-production
```

---

**2. PREPARAR DATOS**

```
Dataset: clientes_suscripciones.csv
├─ 100,000 filas
├─ Columnas:
│  ├─ cliente_id
│  ├─ meses_suscrito (feature)
│  ├─ soporte_contactos (feature)
│  ├─ facturas_pagadas (feature)
│  ├─ precio_plan (feature)
│  └─ canceló (target: Sí/No) ← LO QUE QUEREMOS PREDECIR
│
└─ Registro en Azure ML:
   ├─ Nombre: suscripciones-2024
   ├─ Versión: v1
   └─ Tipo: Tabular
```

---

**3. ENTRENAR MODELO**

**Opción A: Con Designer (visual)**

```
Pipeline creado:
[Dataset] → [Select Columns] → [Split Data 80/20] →
[Train Model: Logistic Regression] → [Score Model] →
[Evaluate Model]

Resultado: Accuracy = 0.85, Precision = 0.82, Recall = 0.79
```

**Opción B: Con código (Python notebook)**

```python
# Cargar dataset
dataset = workspace.datasets['suscripciones-2024']
df = dataset.to_pandas_dataframe()

# Train/Test split
X = df[['meses_suscrito', 'soporte_contactos', 'facturas_pagadas', 'precio_plan']]
y = df['canceló']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Entrenar modelo
from sklearn.ensemble import RandomForest
model = RandomForest(n_estimators=100)
model.fit(X_train, y_train)

# Evaluar
predictions = model.predict(X_test)
accuracy = accuracy_score(y_test, predictions)
print(f"Accuracy: {accuracy}")
```

---

**4. EXPERIMENT CREADO AUTOMÁTICAMENTE**

```
Experiment: "prediccion-cancelaciones-exp-01"
├─ Fecha: 2024-11-13 14:30
├─ Dataset: suscripciones-2024-v1
├─ Algoritmo: Random Forest
├─ Métricas:
│  ├─ Accuracy: 0.87
│  ├─ Precision: 0.84
│  ├─ Recall: 0.82
│  └─ F1-Score: 0.83
├─ Tiempo: 8 minutos
└─ Compute: training-cluster (2 nodos)
```

---

**5. REGISTRAR MODELO**

```
Model: "cancelacion-predictor"
├─ Versión: v1
├─ Framework: scikit-learn 1.3
├─ Métricas guardadas: Accuracy=0.87, F1=0.83
├─ Descripción: "Predice cancelaciones de suscripciones"
└─ Tags: ["producción", "clasificación", "v1"]
```

---

**6. DESPLEGAR A ENDPOINT**

```
Endpoint: https://cancelacion-api.azureml.net/score
├─ Modelo: cancelacion-predictor-v1
├─ Tipo: Real-time
├─ Compute: AKS cluster (2 nodos)
├─ Autenticación: API Key
└─ Estado: ✅ Activo
```

---

**7. USAR DESDE APLICACIÓN**

**Tu app web hace una petición:**

```javascript
// JavaScript en tu aplicación web
const clienteData = {
  meses_suscrito: 6,
  soporte_contactos: 2,
  facturas_pagadas: 5,
  precio_plan: 29.99,
};

fetch("https://cancelacion-api.azureml.net/score", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer tu-api-key",
  },
  body: JSON.stringify(clienteData),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Predicción:", data.prediccion); // "Sí" o "No"
    console.log("Probabilidad:", data.probabilidad); // 0.78

    // Si alta probabilidad de cancelación:
    if (data.probabilidad > 0.7) {
      // Mostrar oferta especial al cliente
      showRetentionOffer();
    }
  });
```

**Respuesta del endpoint:**

```json
{
  "prediccion": "Sí",
  "probabilidad": 0.78,
  "confianza": "alta"
}
```

---

**8. MONITOREAR**

```
Dashboard en Azure ML:
├─ Requests/día: 15,000
├─ Latencia promedio: 45ms
├─ Errores: 0.01%
├─ Precisión real (feedback): 0.85
└─ Estado: ✅ Saludable
```

---

## 💡 VENTAJAS DE USAR AZURE ML vs Hacerlo Local

### 🏠 Entrenar en tu laptop (local):

❌ Limitado por tu hardware (RAM, CPU)
❌ Si tu laptop se apaga, pierdes el entrenamiento
❌ No puedes entrenar múltiples modelos en paralelo
❌ Difícil compartir con tu equipo
❌ Complicado desplegar a producción
❌ Sin versionado automático
❌ Tú gestionas todo manualmente

### ☁️ Entrenar en Azure ML (cloud):

✅ Escalable (más potencia cuando necesites)
✅ Siempre activo (24/7)
✅ Paralelización (múltiples modelos simultáneamente)
✅ Fácil compartir workspace con equipo
✅ Despliegue sencillo a endpoints
✅ Versionado automático de datasets, models, experiments
✅ Azure gestiona infraestructura
✅ Monitorización y logging automáticos
✅ Integración con otros servicios Azure

---

## 🆚 CUÁNDO USAR QUÉ: Tabla de decisión

| Necesidad                          | Usa esto                       | Por qué                               |
| ---------------------------------- | ------------------------------ | ------------------------------------- |
| Detectar spam genérico             | Azure AI Language              | Pre-entrenado, problema común         |
| Predecir TUS ventas específicas    | Azure ML                       | Datos únicos de tu negocio            |
| Traducir textos                    | Azure Translator               | Pre-entrenado, funcionalidad estándar |
| Clasificar TUS productos           | Azure ML + Custom Vision       | Imágenes específicas tuyas            |
| OCR de documentos estándar         | Azure AI Vision (Read)         | Pre-entrenado para docs generales     |
| Extraer campos de TUS formularios  | Azure AI Document Intelligence | Pre-entrenado pero personalizable     |
| Crear modelo desde cero sin código | Azure ML Designer              | Visual, sin programar                 |
| Crear modelo complejo con código   | Azure ML + Notebooks           | Máxima flexibilidad                   |
| Probar muchos algoritmos rápido    | Azure ML AutoML                | Automatiza búsqueda del mejor         |

---

## 🎓 PREGUNTAS AVANZADAS TIPO EXAMEN

### Pregunta 6:

**Una empresa tiene un dataset de 1 millón de filas y quiere probar 20 algoritmos diferentes de ML para encontrar el mejor. Cada algoritmo tarda 45 minutos en entrenar. ¿Qué debería usar?**

A) Compute Instance con AutoML
B) Compute Cluster con AutoML ✅
C) Azure AI Services
D) Entrenar localmente

**Por qué B:**

- AutoML probará los 20 algoritmos automáticamente
- Compute Cluster permite entrenar varios en paralelo
- Con 10 nodos: 2 algoritmos simultáneamente = ~4.5 horas total vs 15 horas en serie

---

### Pregunta 7:

**Has entrenado 5 versiones de un modelo. La v3 tiene mejor Accuracy (0.92) pero la v2 tiene mejor Recall (0.95). ¿Qué ventaja tiene registrar ambas versiones en Azure ML?**

A) Ocupa menos espacio
B) Es más barato
C) Puedes desplegar la v2 si en producción necesitas priorizar Recall ✅
D) No hay ventaja, solo necesitas la mejor

**Por qué C:** Versionado permite cambiar entre modelos según necesidad del negocio. Si después descubres que Recall es más importante, usas v2.

---

### Pregunta 8:

**¿Qué información NO está incluida automáticamente en un Experiment de Azure ML?**

A) Métricas de evaluación (Accuracy, RMSE)
B) Dataset usado
C) Tiempo de entrenamiento
D) Decisiones de negocio sobre cuándo desplegar el modelo ✅

**Por qué D:** Experiments guardan información técnica del entrenamiento, no decisiones de negocio.

---

## 🎊 ¡EXCELENTE TRABAJO EN EL JUEVES!

**Lo que has logrado hoy:**

✅ **Entiendes Azure Machine Learning completo**

- Qué es y para qué sirve
- Diferencia con Azure AI Services

✅ **Dominas los componentes del Workspace**

- Datasets, Experiments, Models, Endpoints, Compute
- Cómo se relacionan entre sí

✅ **Conoces el flujo completo de ML**

- Desde preparar datos hasta desplegar en producción
- Cada paso y su propósito

✅ **Sabes usar Designer**

- Herramienta visual sin código
- Cuándo es útil

✅ **Entiendes tipos de Compute**

- Instance vs Cluster
- Cuándo usar cada uno
- Paralelización

✅ **Puedes decidir qué usar**

- Azure AI Services vs Azure ML
- Cuándo cada herramienta

---

## 📅 MAÑANA (Viernes):

**Tema:** Automated ML (AutoML)

- Qué es AutoML
- Cómo funciona
- Qué hace automáticamente
- Feature engineering automático
- Selección de algoritmos
- Configuración de AutoML
- Interpretar resultados

**Prepárate para:** La herramienta que automatiza MUCHO del trabajo de ML

---

## 💡 PREVIEW DE MAÑANA

**AutoML es como tener un experto en ML trabajando por ti:**

```
TÚ sin AutoML:
├─ Elegir algoritmo 1, entrenar → evaluar
├─ Elegir algoritmo 2, entrenar → evaluar
├─ Elegir algoritmo 3, entrenar → evaluar
├─ ... (20 algoritmos más)
├─ Ajustar hiperparámetros manualmente
├─ Probar feature engineering
└─ Total: 40 horas de trabajo 😰

AutoML por ti:
├─ Le das los datos
├─ Le dices: "Encuentra el mejor modelo"
├─ Prueba 50+ algoritmos automáticamente
├─ Ajusta hiperparámetros automáticamente
├─ Hace feature engineering automáticamente
├─ Te da el mejor modelo
└─ Total: 2 horas (mientras tomas café) ☕

¡MAGIA! 🎩✨
```

---

## 🎯 MINI QUIZ FINAL (5 min)

**Responde mentalmente:**

1. ¿Qué es un Workspace?
2. ¿Cuál es el flujo básico: Dataset → ? → ? → ?
3. ¿Cuándo usarías Compute Cluster vs Instance?
4. ¿Qué es Designer?
5. ¿Diferencia entre Azure AI Services y Azure ML?

**Respuestas:**

1. Contenedor central que agrupa datasets, experiments, models, compute, endpoints
2. Dataset → Experiment → Model → Endpoint
3. Cluster para paralelizar/AutoML. Instance para desarrollo individual
4. Herramienta visual (drag & drop) para ML sin código
5. AI Services = pre-entrenado. Azure ML = entrenas personalizado con tus datos

**Si acertaste 4-5:** ¡Perfecto! Listo para mañana
**Si acertaste 2-3:** Repasa componentes del Workspace
**Si acertaste 0-1:** Repasa todo el material 20 min

---

## 📖 RECURSOS ADICIONALES (Opcional)

**Si quieres explorar más:**

**Videos recomendados (YouTube):**

- "What is Azure Machine Learning" - Microsoft
- "Azure ML Studio walkthrough"
- "Azure ML Designer tutorial"

**Microsoft Learn:**

- "Introduction to Azure Machine Learning"
- "Create a regression model with Designer"
- "Train models with Azure ML"

**Documentación:**

- Azure ML workspace concepts
- Designer module reference
- Compute targets in Azure ML

---

## 💭 REFLEXIÓN FINAL DEL DÍA

**Antes de terminar, reflexiona 2 minutos:**

1. ¿Qué componente de Azure ML te pareció más útil?
2. ¿Puedes pensar en un problema de tu trabajo que resolverías con Azure ML?
3. ¿Usarías Designer o código? ¿Por qué?

**Ejemplo de reflexión:**
"El versionado de modelos me parece súper útil. En mi empresa podríamos usar Azure ML para predecir demanda de productos. Empezaría con Designer para prototipar rápido..."

---

## 🌙 ANTES DE DORMIR (5 min)

**Repaso relámpago:**

- Cierra los ojos
- Visualiza el Workspace con sus 5 componentes
- Recuerda el flujo: Dataset → Experiment → Model → Endpoint
- Piensa en la diferencia: AI Services (pre-entrenado) vs Azure ML (personalizado)

**Repasa tus flashcards nuevas 2 veces**

**Duerme bien.** Mañana AutoML te sorprenderá. 😴

---

## 📊 PROGRESO SEMANA 2

```
Lunes:     ████████████████████ 100% ✅
Martes:    ████████████████████ 100% ✅
Miércoles: ████████████████████ 100% ✅
Jueves:    ████████████████████ 100% ✅
Viernes:   ░░░░░░░░░░░░░░░░░░░░   0%
Sábado:    ░░░░░░░░░░░░░░░░░░░░   0%
```

**Horas Semana 2:** 6/10 horas completadas (60%) ✅
**Progreso Total:** 16/60 horas (26.7%) 📈

---

**¡Nos vemos mañana Viernes para Automated ML!** 🚀

**Mañana aprenderás:**

- Qué hace AutoML por ti automáticamente
- Cómo configurar un experimento de AutoML
- Feature engineering automático
- Selección de algoritmos y hiperparámetros
- Cómo interpretar los resultados
- Cuándo usar AutoML vs entrenar manualmente

**Será fascinante ver cómo Azure hace el trabajo pesado por ti.** 💪
