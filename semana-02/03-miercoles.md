# 📚 SEMANA 2 - MACHINE LEARNING EN PROFUNDIDAD

---

## 📖 MIÉRCOLES 12 NOV (1.5 horas) - Clasificación y sus métricas

### 🎯 Objetivo del día

Entender clasificación en profundidad y cómo evaluar si un modelo de clasificación es bueno

---

## 🔄 REPASO RÁPIDO: Regresión vs Clasificación

**AYER (Martes) - REGRESIÓN:**

- Predice: NÚMEROS continuos
- Ejemplos: precio (150,000€), temperatura (25°C)
- Métricas: MAE, RMSE, R²

**HOY (Miércoles) - CLASIFICACIÓN:**

- Predice: CATEGORÍAS discretas
- Ejemplos: spam/no spam, gato/perro, sí/no
- Métricas: Accuracy, Precision, Recall, F1-Score

---

## 🏷️ ¿QUÉ ES CLASIFICACIÓN?

### 💡 Concepto fundamental:

**Clasificación = asignar una etiqueta/categoría a cada dato**

**Pregunta que responde:** "¿A qué GRUPO pertenece esto?"

---

### 📊 TIPOS DE CLASIFICACIÓN:

#### 1️⃣ CLASIFICACIÓN BINARIA (2 categorías)

**Las más comunes:**

- ✅ / ❌ → Sí / No
- 📧 / 🗑️ → Legítimo / Spam
- 😊 / 😢 → Positivo / Negativo
- ✓ / ✗ → Aprueba / No aprueba
- 💳 / 🚫 → Pago legítimo / Fraude

**Ejemplos:**

1. Email spam detector
2. Detector de fraude en transacciones
3. Diagnóstico médico: enfermo / sano
4. Aprobar o rechazar préstamo
5. Cliente comprará / no comprará

---

#### 2️⃣ CLASIFICACIÓN MULTICLASE (3+ categorías)

**Ejemplos:**

- 🐕 🐱 🐦 → Perro / Gato / Pájaro
- 🔴 🟢 🔵 → Roja / Verde / Azul
- ⭐⭐⭐⭐⭐ → 1 estrella / 2 / 3 / 4 / 5
- 🌍 → Europa / Asia / América / África / Oceanía

**Ejemplos reales:**

1. Clasificar tipos de flores (iris dataset)
2. Reconocer dígitos escritos a mano (0-9)
3. Clasificar noticias por categoría
4. Identificar idioma de un texto
5. Diagnóstico médico con múltiples enfermedades

---

### 🎯 ¿Cómo funciona un clasificador?

**Proceso:**

```
INPUT (datos)
    ↓
[MODELO CLASIFICADOR]
    ↓
OUTPUT (categoría predicha)
```

**Ejemplo concreto - Detector de spam:**

```
INPUT: Email
- Contiene: "¡Gana dinero rápido!"
- Remitente: desconocido@spam.com
- 10 signos de exclamación
- 5 enlaces sospechosos
    ↓
[MODELO]
    ↓
OUTPUT: SPAM ✅ (Confianza: 98%)
```

---

## 🎭 LA MATRIZ DE CONFUSIÓN

### 📊 ¿Qué es?

**La herramienta CLAVE para evaluar clasificadores.**

Una tabla que muestra:

- ¿Qué predijo el modelo?
- ¿Qué era realmente?

---

### 💡 EXPLICACIÓN CON EJEMPLO: Detector de Spam

**Imagina que evaluaste 100 emails:**

```
MATRIZ DE CONFUSIÓN

                    LO QUE REALMENTE ERA
                  ┌─────────────┬─────────────┐
                  │  Legítimo   │    Spam     │
    ┌─────────────┼─────────────┼─────────────┤
    │  Legítimo   │     50      │      5      │
LO  │             │   (TN)      │    (FN)     │
QUE ├─────────────┼─────────────┼─────────────┤
PRE │    Spam     │     10      │     35      │
DIJE│             │   (FP)      │    (TP)     │
    └─────────────┴─────────────┴─────────────┘
```

**Desglose:**

- **50 Legítimos correctos (TN):** Predije "legítimo" y ERA legítimo ✅
- **35 Spam correctos (TP):** Predije "spam" y ERA spam ✅
- **10 Falsos positivos (FP):** Predije "spam" pero era legítimo ❌
- **5 Falsos negativos (FN):** Predije "legítimo" pero era spam ❌

---

### 🔑 LOS 4 TÉRMINOS CLAVE:

#### 1️⃣ TRUE POSITIVE (TP) - Verdadero Positivo ✅✅

**"Dije que SÍ, y tenía razón"**

**Ejemplo spam:**

- Predije: "Esto ES spam"
- Realidad: "Sí, ERA spam"
- ✅ ¡Acierto!

**Otros ejemplos:**

- Diagnóstico: "Tienes la enfermedad" → y sí la tiene
- Fraude: "Es fraude" → y sí es fraude
- Calidad: "Producto defectuoso" → y sí está defectuoso

---

#### 2️⃣ TRUE NEGATIVE (TN) - Verdadero Negativo ✅✅

**"Dije que NO, y tenía razón"**

**Ejemplo spam:**

- Predije: "Esto NO es spam"
- Realidad: "Correcto, NO era spam"
- ✅ ¡Acierto!

**Otros ejemplos:**

- Diagnóstico: "NO tienes la enfermedad" → y no la tiene
- Fraude: "NO es fraude" → y no es fraude
- Calidad: "Producto bueno" → y sí está bueno

---

#### 3️⃣ FALSE POSITIVE (FP) - Falso Positivo ❌ (Error Tipo I)

**"Dije que SÍ, pero me equivoqué"**

**Ejemplo spam:**

- Predije: "Esto ES spam"
- Realidad: "No, era un email importante"
- ❌ ¡Error grave! Perdiste un email importante

**Otros ejemplos:**

- Diagnóstico: "Tienes cáncer" → pero NO lo tiene (alarma innecesaria)
- Fraude: "Es fraude" → pero era una compra legítima (bloqueas al cliente)
- Alarma incendios: Suena → pero NO hay fuego

**Consecuencia:** Falsa alarma, pánico innecesario, molestias

---

#### 4️⃣ FALSE NEGATIVE (FN) - Falso Negativo ❌ (Error Tipo II)

**"Dije que NO, pero me equivoqué"**

**Ejemplo spam:**

- Predije: "Esto NO es spam"
- Realidad: "Sí era spam" → llega a tu bandeja
- ❌ Error molesto, pero menos grave

**Otros ejemplos:**

- Diagnóstico: "NO tienes cáncer" → pero SÍ lo tiene (peligrosísimo)
- Fraude: "NO es fraude" → pero SÍ es fraude (pierdes dinero)
- Seguridad aeropuerto: "NO hay amenaza" → pero SÍ la hay (desastre)

**Consecuencia:** Peligro no detectado, problema pasa desapercibido

---

### 🎯 RESUMEN VISUAL:

```
┌─────────────────────────────────────────────────────┐
│                  REALIDAD                           │
│              Positivo      Negativo                 │
├─────────────────────────────────────────────────────┤
│ PREDICCIÓN                                          │
│              ┌──────────┬──────────┐                │
│  Positivo    │    TP    │    FP    │                │
│              │    ✅✅  │    ❌    │                │
│              │ ¡Acierto!│ Falsa    │                │
│              │          │ alarma   │                │
│              ├──────────┼──────────┤                │
│  Negativo    │    FN    │    TN    │                │
│              │    ❌    │    ✅✅  │                │
│              │ ¡Perdí   │ ¡Acierto!│                │
│              │  algo!   │          │                │
│              └──────────┴──────────┘                │
└─────────────────────────────────────────────────────┘
```

---

## 📏 MÉTRICAS DE CLASIFICACIÓN

### 🎯 Las 4 métricas principales:

```
MÉTRICAS DE CLASIFICACIÓN
│
├── 1. Accuracy (Exactitud)
├── 2. Precision (Precisión)
├── 3. Recall (Exhaustividad/Sensibilidad)
└── 4. F1-Score (Balance entre Precision y Recall)
```

---

## 1️⃣ ACCURACY (Exactitud)

### 📊 ¿Qué mide?

**"¿Qué porcentaje de predicciones fueron correctas?"**

**Fórmula en palabras:**

```
Accuracy = (Aciertos totales) / (Total de predicciones)

Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

---

### 💡 Ejemplo con números:

**Matriz de confusión del detector de spam:**

```
                Legítimo    Spam
Legítimo           50        5
Spam               10       35

Total emails: 100
```

**Cálculo:**

```
TP = 35 (spam detectado correctamente)
TN = 50 (legítimo detectado correctamente)
FP = 10 (falsa alarma)
FN = 5 (spam no detectado)

Accuracy = (TP + TN) / Total
Accuracy = (35 + 50) / 100
Accuracy = 85 / 100
Accuracy = 0.85 = 85%
```

**Interpretación:**
"El modelo acierta el 85% de las veces"

---

### ✅ Ventajas de Accuracy:

✅ **Súper fácil de entender:** "Acierto X% de las veces"
✅ **Intuitivo para explicar a no técnicos**
✅ **Métrica más común y popular**

---

### ⚠️ PROBLEMA GRAVE con Accuracy: Clases desbalanceadas

**Ejemplo: Detector de fraude**

```
Tienes 1000 transacciones:
- 950 son legítimas (95%)
- 50 son fraude (5%)
```

**Modelo TONTO que siempre predice "legítimo":**

```
                Legítimo    Fraude
Legítimo          950        50
Fraude             0         0

Accuracy = (950 + 0) / 1000 = 95%
```

**¡95% de accuracy! ¿Es bueno?**
❌ **NO!** El modelo NUNCA detecta fraude
❌ Es inútil, pero tiene alta accuracy

**Por eso necesitamos Precision y Recall.**

---

## 2️⃣ PRECISION (Precisión)

### 📊 ¿Qué mide?

**"De todo lo que dije que era POSITIVO, ¿cuánto realmente lo era?"**

**Pregunta:** "¿Qué tan confiable soy cuando digo SÍ?"

**Fórmula en palabras:**

```
Precision = TP / (TP + FP)
Precision = Verdaderos positivos / Todos los que dije positivos
```

---

### 💡 Ejemplo con spam:

```
Predije "SPAM" para 45 emails:
- 35 SÍ eran spam (TP)
- 10 NO eran spam (FP) ← falsa alarma

Precision = 35 / (35 + 10)
Precision = 35 / 45
Precision = 0.78 = 78%
```

**Interpretación:**
"Cuando digo que es spam, tengo razón el 78% de las veces"
"22% de las veces bloqueo emails legítimos" ← ¡problema!

---

### 🎯 ¿Cuándo es importante ALTA Precision?

**Cuando los FALSOS POSITIVOS son MUY costosos:**

**Ejemplo 1: Email spam**

- FP = Email importante va a spam
- Consecuencia: Pierdes información crítica
- Solución: Precision alta (mejor dejar pasar spam que bloquear importante)

**Ejemplo 2: Recomendación de películas**

- FP = Recomendar película que no le gustará
- Consecuencia: Usuario molesto, pierde confianza
- Solución: Precision alta (solo recomendar si estás seguro)

**Ejemplo 3: Publicidad**

- FP = Mostrar anuncio a persona no interesada
- Consecuencia: Gastas dinero sin retorno
- Solución: Precision alta (solo mostrar a interesados)

---

## 3️⃣ RECALL (Exhaustividad / Sensibilidad)

### 📊 ¿Qué mide?

**"De todo lo que ERA positivo, ¿cuánto logré detectar?"**

**Pregunta:** "¿Qué tan bueno soy para NO dejar escapar cosas?"

**Fórmula en palabras:**

```
Recall = TP / (TP + FN)
Recall = Verdaderos positivos / Todos los positivos reales
```

---

### 💡 Ejemplo con spam:

```
Había 40 emails de spam en total:
- 35 los detecté como spam (TP)
- 5 pasaron como legítimos (FN) ← se me escaparon

Recall = 35 / (35 + 5)
Recall = 35 / 40
Recall = 0.875 = 87.5%
```

**Interpretación:**
"Detecto el 87.5% del spam que existe"
"El 12.5% del spam se me escapa a la bandeja principal" ← problema

---

### 🎯 ¿Cuándo es importante ALTO Recall?

**Cuando los FALSOS NEGATIVOS son MUY peligrosos:**

**Ejemplo 1: Detector de cáncer**

- FN = Decir "está sano" cuando tiene cáncer
- Consecuencia: Paciente muere
- Solución: Recall altísimo (mejor 10 falsas alarmas que perder 1 caso real)

**Ejemplo 2: Detector de fraude bancario**

- FN = No detectar fraude real
- Consecuencia: Pierdes millones de euros
- Solución: Recall alto (mejor bloquear transacciones legítimas que dejar pasar fraude)

**Ejemplo 3: Seguridad aeropuerto**

- FN = No detectar arma/bomba
- Consecuencia: Desastre
- Solución: Recall 99.99% (mejor molestar pasajeros que dejar pasar amenaza)

---

### 🔥 PRECISION vs RECALL: El trade-off

**El dilema:**

- ↑ Precision → ↓ Recall
- ↑ Recall → ↓ Precision

**No puedes tener ambos perfectos simultáneamente**

---

### 📊 Visualización del trade-off:

```
MODO ESTRICTO (Alta Precision):
"Solo digo SÍ si estoy 99% seguro"
→ Alta Precision (cuando digo SÍ, casi siempre acierto)
→ Baja Recall (me pierdo muchos casos porque soy muy conservador)

Ejemplo: Email spam
Bloqueo solo spam OBVIO → Pocos falsos positivos (FP bajo)
Pero mucho spam pasa → Muchos falsos negativos (FN alto)
```

```
MODO AGRESIVO (Alto Recall):
"Digo SÍ ante la mínima sospecha"
→ Alta Recall (atrapo casi todos los positivos)
→ Baja Precision (muchos falsos positivos)

Ejemplo: Detector de cáncer
Ante mínima duda → "posible cáncer" (no quiero perderme ninguno)
Detecto todos los casos → Muchas falsas alarmas (FP alto)
```

---

### 🎯 ¿Cuál priorizar?

| Situación                 | Prioriza      | Por qué                                                        |
| ------------------------- | ------------- | -------------------------------------------------------------- |
| Email spam                | **Precision** | Peor perder email importante que recibir spam                  |
| Detector de cáncer        | **Recall**    | Peor no detectar cáncer que falsa alarma                       |
| Detector de fraude        | **Recall**    | Peor perder dinero que bloquear transacción legítima           |
| Recomendador de productos | **Precision** | Peor recomendar mal que no recomendar                          |
| Seguridad aeropuerto      | **Recall**    | Peor dejar pasar amenaza que revisar demás                     |
| Búsqueda en Google        | **Balance**   | Quieres resultados relevantes (precision) y completos (recall) |

---

## 4️⃣ F1-SCORE

### 📊 ¿Qué mide?

**"El balance perfecto entre Precision y Recall"**

**Es la media armónica de Precision y Recall**

**Fórmula en palabras:**

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

---

### 💡 ¿Por qué F1-Score?

**Problema:**

- Modelo A: Precision = 90%, Recall = 50%
- Modelo B: Precision = 60%, Recall = 95%
- ¿Cuál es mejor?

**Promedio simple:**

- Modelo A: (90 + 50) / 2 = 70%
- Modelo B: (60 + 95) / 2 = 77.5%

❌ Pero promedio simple no captura el balance

**F1-Score (media armónica):**

- Modelo A: F1 = 2×(90×50)/(90+50) = 64.3%
- Modelo B: F1 = 2×(60×95)/(60+95) = 73.5%

✅ F1 penaliza desequilibrios entre precision y recall

---

### 🎯 ¿Cuándo usar F1-Score?

✅ **Cuando necesitas balance entre Precision y Recall**
✅ **Cuando clases están desbalanceadas**
✅ **Como métrica única para comparar modelos**
✅ **Cuando no puedes decidir si priorizar precision o recall**

---

### 📊 Interpretación de F1:

| F1-Score      | Interpretación               |
| ------------- | ---------------------------- |
| **0.9 - 1.0** | Excelente balance ⭐⭐⭐⭐⭐ |
| **0.7 - 0.9** | Buen balance ⭐⭐⭐⭐        |
| **0.5 - 0.7** | Balance moderado ⭐⭐⭐      |
| **< 0.5**     | Balance pobre ⭐⭐           |

---

## 📊 TABLA COMPARATIVA: Las 4 métricas

| Métrica       | ¿Qué mide?                 | Fórmula       | Cuándo usarla      | Rango |
| ------------- | -------------------------- | ------------- | ------------------ | ----- |
| **Accuracy**  | % de aciertos totales      | (TP+TN)/Total | Clases balanceadas | 0 a 1 |
| **Precision** | ¿Confiable cuando digo SÍ? | TP/(TP+FP)    | FP son costosos    | 0 a 1 |
| **Recall**    | ¿Detecto todos los SÍ?     | TP/(TP+FN)    | FN son peligrosos  | 0 a 1 |
| **F1-Score**  | Balance P y R              | 2(P×R)/(P+R)  | Necesitas balance  | 0 a 1 |

**Para todas: Más cerca de 1 = mejor**

---

## 🎓 EJEMPLO COMPLETO: Detector de fraude

### Caso: Evaluar detector de fraude bancario

**Evaluaste 1000 transacciones:**

```
MATRIZ DE CONFUSIÓN

                  Legítimo    Fraude
Legítimo             940        10
Fraude                30        20

Total: 1000 transacciones
- 970 legítimas
- 30 fraude
```

**Identificar los valores:**

- TP = 20 (fraude detectado correctamente)
- TN = 940 (legítimo detectado correctamente)
- FP = 30 (bloqueé transacción legítima - molestia cliente)
- FN = 10 (fraude no detectado - perdí dinero)

---

### 📊 Calcular todas las métricas:

**1. Accuracy:**

```
Accuracy = (TP + TN) / Total
Accuracy = (20 + 940) / 1000
Accuracy = 960 / 1000 = 0.96 = 96%
```

✅ "Acierto el 96% de las veces"

---

**2. Precision:**

```
Precision = TP / (TP + FP)
Precision = 20 / (20 + 30)
Precision = 20 / 50 = 0.40 = 40%
```

⚠️ "Cuando digo que es fraude, solo acierto el 40% de las veces"
⚠️ "Bloqueo muchas transacciones legítimas (60%)"

---

**3. Recall:**

```
Recall = TP / (TP + FN)
Recall = 20 / (20 + 10)
Recall = 20 / 30 = 0.67 = 67%
```

⚠️ "Detecto solo el 67% del fraude real"
⚠️ "El 33% del fraude se me escapa (pierdo dinero)"

---

**4. F1-Score:**

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
F1 = 2 × (0.40 × 0.67) / (0.40 + 0.67)
F1 = 2 × 0.268 / 1.07
F1 = 0.50 = 50%
```

❌ "El balance es pobre"

---

### 📋 Evaluación completa:

| Métrica   | Valor | Interpretación                 |
| --------- | ----- | ------------------------------ |
| Accuracy  | 96%   | ✅ Parece bueno, pero engañoso |
| Precision | 40%   | ❌ Molesto muchos clientes     |
| Recall    | 67%   | ⚠️ Pierdo 1 de cada 3 fraudes  |
| F1-Score  | 50%   | ❌ Modelo pobre en general     |

**Conclusión:**

- Alta accuracy engaña (porque 97% son legítimos)
- El modelo es MALO para detectar fraude
- Necesita mejorar tanto precision como recall

---

## 🎓 PREGUNTAS TIPO EXAMEN

### Pregunta 1:

\*\*Un modelo de clasificación tiene estos resultados:

- TP = 80
- TN = 800
- FP = 20
- FN = 100

¿Cuál es la Accuracy del modelo?\*\*

A) 80%
B) 88% ✅
C) 44%
D) 50%

**Cálculo:**

```
Accuracy = (TP + TN) / Total
Accuracy = (80 + 800) / (80 + 800 + 20 + 100)
Accuracy = 880 / 1000 = 0.88 = 88%
```

---

### Pregunta 2:

**En un detector de enfermedades raras, ¿qué métrica es MÁS importante priorizar?**

A) Accuracy
B) Precision
C) Recall ✅
D) F1-Score

**Por qué C:** En enfermedades, los falsos negativos (no detectar enfermedad real) son peligrosos. Recall mide qué tan bien detectas TODOS los casos positivos.

---

### Pregunta 3:

**¿Qué representa un Falso Positivo (FP) en un detector de spam?**

A) Email spam correctamente identificado como spam
B) Email legítimo correctamente identificado como legítimo
C) Email legítimo incorrectamente identificado como spam ✅
D) Email spam incorrectamente identificado como legítimo

**Por qué C:** Falso Positivo = dijiste "positivo (spam)" pero era falso (legítimo).

---

### Pregunta 4:

**Tienes un modelo con Precision = 0.90 y Recall = 0.50. ¿Qué significa?**

A) El modelo es excelente
B) El modelo es muy confiable cuando predice positivo, pero se pierde muchos casos positivos ✅
C) El modelo detecta todos los positivos pero tiene muchos falsos positivos
D) El modelo tiene bajo rendimiento en general

**Por qué B:** Alta precision = confiable cuando dice SÍ. Bajo recall = se pierde muchos casos (muchos FN).

---

### Pregunta 5:

**¿Cuál es la principal limitación de usar solo Accuracy para evaluar un clasificador?**

A) Es difícil de calcular
B) No funciona bien con clases desbalanceadas ✅
C) No está disponible en Azure ML
D) Solo funciona para clasificación binaria

**Por qué B:** Con clases desbalanceadas (ej: 95% clase A, 5% clase B), un modelo que siempre predice clase A tendrá 95% accuracy pero es inútil.

---

## ✅ TAREAS DE HOY (Miércoles)

### 1. Microsoft Learn (45 min)

**Módulos a completar:**

- **"Creación de modelos de clasificación"**
- **"Entrenamiento y evaluación de modelos de clasificación"**

Link: https://learn.microsoft.com/es-es/training/modules/train-evaluate-classification-models/

---

### 2. Ejercicio: Calcular métricas (20 min)

**Para cada matriz de confusión, calcula las 4 métricas:**

**Escenario 1: Detector de productos defectuosos**

```
                Bueno    Defectuoso
Bueno            850         50
Defectuoso        20         80

Total: 1000 productos
```

Calcula:

- TP = \_\_\_
- TN = \_\_\_
- FP = \_\_\_
- FN = \_\_\_
- Accuracy = \_\_\_
- Precision = \_\_\_
- Recall = \_\_\_
- ¿Es un buen modelo? \_\_\_

---

**Escenario 2: Clasificador de emociones (positivo/negativo)**

```
               Negativo   Positivo
Negativo          300        50
Positivo          100       550

Total: 1000 reseñas
```

Calcula:

- TP = \_\_\_
- TN = \_\_\_
- FP = \_\_\_
- FN = \_\_\_
- Accuracy = \_\_\_
- Precision = \_\_\_
- Recall = \_\_\_

---

**Escenario 3: Detector médico de diabetes**

```
               Sano    Diabético
Sano           920        10
Diabético       40        30

Total: 1000 pacientes
```

Calcula todas las métricas y responde:

- ¿Qué métrica es más preocupante? \_\_\_
- ¿Por qué? \_\_\_
- ¿Qué debería mejorar este modelo? \_\_\_

---

### 3. Crea Flashcards (15 min)

**Crea estas 15 tarjetas:**

**Tarjeta 1:**

- Frente: "¿Qué mide Accuracy?"
- Atrás: "Porcentaje de predicciones correctas. (TP+TN)/Total"

**Tarjeta 2:**

- Frente: "¿Qué mide Precision?"
- Atrás: "De lo que dije positivo, ¿cuánto era realmente positivo? TP/(TP+FP)"

**Tarjeta 3:**

- Frente: "¿Qué mide Recall?"
- Atrás: "De todo lo que ERA positivo, ¿cuánto detecté? TP/(TP+FN)"

**Tarjeta 4:**

- Frente: "¿Qué es True Positive (TP)?"
- Atrás: "Predije positivo Y era positivo. ✅ ¡Acierto!"

**Tarjeta 5:**

- Frente: "¿Qué es False Positive (FP)?"
- Atrás: "Predije positivo pero era negativo. ❌ Falsa alarma"

**Tarjeta 6:**

- Frente: "¿Qué es False Negative (FN)?"
- Atrás: "Predije negativo pero era positivo. ❌ Se me escapó"

**Tarjeta 7:**

- Frente: "¿Qué es True Negative (TN)?"
- Atrás: "Predije negativo Y era negativo. ✅ ¡Acierto!"

**Tarjeta 8:**

- Frente: "¿Cuándo priorizar Precision?"
- Atrás: "Cuando los FALSOS POSITIVOS son muy costosos. Ej: email spam, recomendaciones"

**Tarjeta 9:**

- Frente: "¿Cuándo priorizar Recall?"
- Atrás: "Cuando los FALSOS NEGATIVOS son peligrosos. Ej: detector de cáncer, fraude"

**Tarjeta 10:**

- Frente: "¿Qué mide F1-Score?"
- Atrás: "Balance entre Precision y Recall. Media armónica de ambas."

**Tarjeta 11:**

- Frente: "Problema con Accuracy en clases desbalanceadas"
- Atrás: "Un modelo tonto que predice siempre la clase mayoritaria tendrá alta accuracy pero es inútil"

**Tarjeta 12:**

- Frente: "Trade-off Precision vs Recall"
- Atrás: "Al aumentar Precision, baja Recall y viceversa. No puedes maximizar ambas simultáneamente"

**Tarjeta 13:**

- Frente: "Ejemplo de Falso Positivo peligroso"
- Atrás: "Detector de spam marca email importante como spam → pierdes info crítica"

**Tarjeta 14:**

- Frente: "Ejemplo de Falso Negativo peligroso"
- Atrás: "Detector médico dice 'no hay cáncer' pero sí lo hay → paciente no recibe tratamiento"

**Tarjeta 15:**

- Frente: "Diferencia clave: Regresión vs Clasificación métricas"
- Atrás: "Regresión: MAE, RMSE, R² (para números). Clasificación: Accuracy, Precision, Recall, F1 (para categorías)"

---

## 📝 CONCEPTOS CLAVE DEL MIÉRCOLES

**Memoriza:**

- Clasificación predice categorías (no números)
- Matriz de confusión: TP, TN, FP, FN
- Accuracy = aciertos totales / total
- Precision = confiable cuando digo SÍ
- Recall = detecto todos los SÍ reales
- F1 = balance entre Precision y Recall
- FP = falsa alarma, FN = se me escapó
- Prioriza Precision cuando FP sean costosos
- Prioriza Recall cuando FN sean peligrosos

---

## ✅ CHECKLIST MIÉRCOLES

- [ ] Entiendo qué es clasificación vs regresión
- [ ] Domino la matriz de confusión (TP, TN, FP, FN)
- [ ] Sé qué miden Accuracy, Precision, Recall, F1
- [ ] Puedo calcular métricas de una matriz de confusión
- [ ] Entiendo cuándo priorizar Precision vs Recall
- [ ] Sé el problema de Accuracy con clases desbalanceadas
- [ ] Completé los 3 ejercicios de cálculo
- [ ] Creé 15 flashcards nuevas
- [ ] Repasé flashcards de Lunes y Martes (10 min)
- [ ] Puedo explicar las métricas en voz alta

---

## 📚 RESPUESTAS A LOS EJERCICIOS

### Escenario 1: Detector de productos defectuosos

```
                Bueno    Defectuoso
Bueno            850         50
Defectuoso        20         80
```

**Identificar valores:**

- **TP = 80** (defectuosos detectados correctamente)
- **TN = 850** (buenos detectados correctamente)
- **FP = 20** (buenos marcados como defectuosos - desperdicio)
- **FN = 50** (defectuosos que pasaron como buenos - PELIGROSO)

**Cálculos:**

```
Accuracy = (80 + 850) / 1000 = 930 / 1000 = 0.93 = 93%

Precision = 80 / (80 + 20) = 80 / 100 = 0.80 = 80%

Recall = 80 / (80 + 50) = 80 / 130 = 0.615 = 61.5%

F1 = 2 × (0.80 × 0.615) / (0.80 + 0.615) = 0.695 = 69.5%
```

**Evaluación:**

- ✅ Accuracy alta (93%) - pero puede engañar
- ✅ Precision aceptable (80%) - cuando marca defectuoso, suele acertar
- ⚠️ Recall bajo (61.5%) - se pierde muchos defectuosos (FN = 50)
- **Problema:** 50 productos defectuosos llegan a clientes → quejas, devoluciones
- **Necesita mejorar:** RECALL (detectar más defectuosos)

---

### Escenario 2: Clasificador de emociones

```
               Negativo   Positivo
Negativo          300        50
Positivo          100       550
```

**Identificar valores:**

- **TP = 550** (positivos detectados correctamente)
- **TN = 300** (negativos detectados correctamente)
- **FP = 100** (negativos marcados como positivos)
- **FN = 50** (positivos marcados como negativos)

**Cálculos:**

```
Accuracy = (550 + 300) / 1000 = 850 / 1000 = 0.85 = 85%

Precision = 550 / (550 + 100) = 550 / 650 = 0.846 = 84.6%

Recall = 550 / (550 + 50) = 550 / 600 = 0.917 = 91.7%

F1 = 2 × (0.846 × 0.917) / (0.846 + 0.917) = 0.880 = 88%
```

**Evaluación:**

- ✅ Accuracy buena (85%)
- ✅ Precision buena (84.6%)
- ✅✅ Recall excelente (91.7%)
- ✅ F1 muy bueno (88%)
- **Conclusión:** Modelo BUENO en general, buen balance

---

### Escenario 3: Detector médico de diabetes

```
               Sano    Diabético
Sano           920        10
Diabético       40        30
```

**Identificar valores:**

- **TP = 30** (diabéticos detectados)
- **TN = 920** (sanos detectados)
- **FP = 40** (sanos marcados como diabéticos - falsa alarma)
- **FN = 10** (diabéticos marcados como sanos - PELIGROSÍSIMO)

**Cálculos:**

```
Accuracy = (30 + 920) / 1000 = 950 / 1000 = 0.95 = 95%

Precision = 30 / (30 + 40) = 30 / 70 = 0.429 = 42.9%

Recall = 30 / (30 + 10) = 30 / 40 = 0.75 = 75%

F1 = 2 × (0.429 × 0.75) / (0.429 + 0.75) = 0.545 = 54.5%
```

**Evaluación y análisis:**

- ✅ Accuracy muy alta (95%) - PERO ES ENGAÑOSA
- ❌ Precision baja (42.9%) - muchas falsas alarmas (40 sanos diagnosticados)
- ⚠️ Recall moderado (75%) - pero 10 diabéticos no detectados
- ❌ F1 bajo (54.5%) - modelo pobre en general

**¿Qué métrica es más preocupante?**
**RECALL (75%)**

**¿Por qué?**

- FN = 10 significa que 10 personas con diabetes NO fueron detectadas
- Estas personas NO recibirán tratamiento
- Consecuencia: Complicaciones graves, posible muerte
- En medicina, los FN son CRÍTICOS

**¿Qué debería mejorar?**

- **PRIORIDAD 1:** Aumentar RECALL (detectar más diabéticos)
- Mejor tener 100 falsas alarmas que perder 1 caso real
- Después de mejorar recall, trabajar en precision para reducir falsas alarmas

---

## 🎯 COMPARACIÓN FINAL: Regresión vs Clasificación

### 📊 Tabla resumen completa:

| Aspecto                       | REGRESIÓN                               | CLASIFICACIÓN                     |
| ----------------------------- | --------------------------------------- | --------------------------------- |
| **Predice**                   | Números continuos                       | Categorías discretas              |
| **Ejemplo output**            | 150,000€, 25.5°C                        | "Spam", "Gato", "Sí"              |
| **Pregunta**                  | "¿Cuánto?"                              | "¿Cuál?"                          |
| **Métricas principales**      | MAE, RMSE, R²                           | Accuracy, Precision, Recall, F1   |
| **Mejor valor métricas**      | MAE/RMSE: 0 (bajo), R²: 1 (alto)        | Todas: 1 (alto)                   |
| **Concepto clave evaluación** | Error numérico y variabilidad explicada | Matriz de confusión               |
| **Problema común**            | Overfitting                             | Clases desbalanceadas             |
| **Ejemplos**                  | Precio casas, temperatura, ventas       | Spam/no spam, fraude, diagnóstico |

---

## 🎓 EJERCICIO MENTAL: Identifica el tipo

**Para cada problema, ¿es Regresión o Clasificación?**

1. Predecir si un cliente comprará o no
   - **Clasificación** (Sí/No)

2. Estimar cuánto gastará un cliente en su próxima compra
   - **Regresión** (cantidad en €)

3. Identificar si una imagen muestra un perro, gato o pájaro
   - **Clasificación** (3 categorías)

4. Predecir cuántos días de hospitalización necesitará un paciente
   - **Regresión** (número de días)

5. Determinar el nivel de satisfacción: bajo, medio, alto
   - **Clasificación** (3 categorías)

6. Estimar el precio de un coche usado
   - **Regresión** (precio en €)

7. Clasificar emails en trabajo, personal, promociones, spam
   - **Clasificación** (4 categorías)

8. Predecir la temperatura máxima de mañana
   - **Regresión** (temperatura en °C)

---

## 📋 CHEAT SHEET PARA IMPRIMIR

```
╔══════════════════════════════════════════════════════════╗
║        MÉTRICAS DE CLASIFICACIÓN - CHEAT SHEET          ║
╠══════════════════════════════════════════════════════════╣
║ MATRIZ DE CONFUSIÓN                                     ║
║                      REALIDAD                            ║
║               Positivo      Negativo                     ║
║  PREDICCIÓN  ┌──────────┬──────────┐                    ║
║  Positivo    │    TP    │    FP    │                    ║
║              │  ✅✅    │  ❌      │                    ║
║              ├──────────┼──────────┤                    ║
║  Negativo    │    FN    │    TN    │                    ║
║              │  ❌      │  ✅✅    │                    ║
║              └──────────┴──────────┘                    ║
╠══════════════════════════════════════════════════════════╣
║ ACCURACY (Exactitud)                                     ║
║ • Fórmula: (TP + TN) / Total                            ║
║ • Qué mide: % de aciertos totales                       ║
║ • Cuándo: Clases balanceadas                            ║
║ • ⚠️ Engañosa con clases desbalanceadas                 ║
╠══════════════════════════════════════════════════════════╣
║ PRECISION (Precisión)                                    ║
║ • Fórmula: TP / (TP + FP)                               ║
║ • Qué mide: Confiable cuando digo SÍ                    ║
║ • Pregunta: "De lo que dije positivo, ¿cuánto lo era?" ║
║ • Prioriza: Cuando FP son costosos                      ║
║ • Ejemplo: Email spam, recomendaciones                  ║
╠══════════════════════════════════════════════════════════╣
║ RECALL (Exhaustividad/Sensibilidad)                     ║
║ • Fórmula: TP / (TP + FN)                               ║
║ • Qué mide: Detecto todos los positivos                 ║
║ • Pregunta: "De todo lo positivo, ¿cuánto detecté?"    ║
║ • Prioriza: Cuando FN son peligrosos                    ║
║ • Ejemplo: Cáncer, fraude, seguridad                    ║
╠══════════════════════════════════════════════════════════╣
║ F1-SCORE (Balance)                                       ║
║ • Fórmula: 2×(P×R)/(P+R)                                ║
║ • Qué mide: Balance entre Precision y Recall            ║
║ • Cuándo: Necesitas balance, clases desbalanceadas     ║
║ • Media armónica (penaliza desequilibrios)              ║
╠══════════════════════════════════════════════════════════╣
║ REGLAS RÁPIDAS                                           ║
║ • TP = Acierto positivo ✅✅                             ║
║ • TN = Acierto negativo ✅✅                             ║
║ • FP = Falsa alarma ❌ (dije SÍ, era NO)                ║
║ • FN = Se me escapó ❌ (dije NO, era SÍ)                ║
║                                                          ║
║ • ↑ Precision → ↓ Recall (trade-off)                    ║
║ • Accuracy engaña en clases desbalanceadas              ║
║ • FN peligrosos → prioriza Recall                       ║
║ • FP costosos → prioriza Precision                      ║
╚══════════════════════════════════════════════════════════╝
```

---

## 🎊 ¡EXCELENTE TRABAJO EN EL MIÉRCOLES!

**Lo que has logrado hoy:**

✅ **Dominas clasificación en profundidad**

- Clasificación binaria y multiclase
- Diferencia con regresión

✅ **Entiendes la matriz de confusión**

- TP, TN, FP, FN
- Qué significa cada uno

✅ **Dominas las 4 métricas clave**

- Accuracy, Precision, Recall, F1-Score
- Cuándo usar cada una
- Cómo calcularlas

✅ **Entiendes el trade-off Precision vs Recall**

- Por qué no puedes maximizar ambos
- Cuándo priorizar cada uno

✅ **Puedes evaluar modelos de clasificación**

- Interpretar métricas en contexto
- Identificar problemas
- Sugerir mejoras

---

## 📅 MAÑANA (Jueves):

**Tema:** Azure Machine Learning en detalle

- Qué es Azure ML workspace
- Componentes principales
- Designer (herramienta visual)
- Cómo desplegar modelos
- Azure ML vs otros servicios

**Prepárate para:** Conectar toda la teoría con la práctica en Azure

---

## 💡 CONEXIÓN CON LO QUE VIENE

**Esta semana:**

- ✅ Lunes: Tipos de ML (supervisado, no supervisado, refuerzo)
- ✅ Martes: Regresión y métricas (MAE, RMSE, R²)
- ✅ Miércoles: Clasificación y métricas (HOY)
- 📅 Jueves: Azure ML workspace
- 📅 Viernes: Automated ML (AutoML)
- 📅 Sábado: LAB - Crear tu primer modelo real

**El sábado pondrás en práctica TODO esto:**

- Crearás un modelo de clasificación o regresión
- Verás las métricas en Azure ML
- Interpretarás los resultados
- Entenderás qué significa cada número

---

## 🎯 MINI QUIZ FINAL (5 min)

**Responde mentalmente (sin mirar):**

1. ¿Qué es un Falso Positivo?
2. ¿Qué métrica usarías en un detector de cáncer?
3. Si Precision = 0.90 y Recall = 0.40, ¿qué problema hay?
4. ¿Por qué Accuracy puede engañar?
5. ¿Qué mide F1-Score?

**Respuestas:**

1. Dije "positivo" pero era "negativo" - falsa alarma
2. RECALL (no quiero perderme ningún caso)
3. Modelo muy conservador, se pierde muchos casos (bajo recall)
4. Con clases desbalanceadas, un modelo tonto puede tener alta accuracy
5. Balance entre Precision y Recall

**Si acertaste 4-5:** ¡Perfecto! Listo para mañana
**Si acertaste 2-3:** Repasa matriz de confusión y métricas
**Si acertaste 0-1:** Repasa toda la sección de métricas 15 min

---

## 📖 RECURSOS ADICIONALES (Opcional)

**Si quieres profundizar:**

**Videos recomendados (YouTube):**

- "Confusion Matrix explained" - StatQuest
- "Precision and Recall" - explicaciones visuales
- "F1 Score explained" - tutoriales cortos
- "Classification metrics" - comparaciones

**Microsoft Learn:**

- "Train and evaluate classification models"
- "Understand classification metrics"

**Documentación Azure ML:**

- Cómo interpretar métricas en Azure ML
- Matriz de confusión en Azure ML Studio

---

## 💭 REFLEXIÓN FINAL DEL DÍA

**Antes de terminar, reflexiona 2 minutos:**

1. ¿Qué métrica te pareció más útil? ¿Por qué?
2. ¿Puedes pensar en un problema de clasificación en tu trabajo/vida?
3. ¿Qué priorizarías: Precision o Recall? ¿Por qué?

**Ejemplo de reflexión:**
"Recall me parece la más crítica en medicina. En mi trabajo de atención al cliente, podríamos clasificar tickets por urgencia. Priorizaría Recall para no perder tickets urgentes..."

---

## 🌙 ANTES DE DORMIR (5 min)

**Repaso relámpago:**

- Cierra los ojos
- Visualiza la matriz de confusión: TP, TN, FP, FN
- Recuerda: Accuracy = total aciertos, Precision = confiable, Recall = detecta todos
- Piensa en ejemplos donde FP son peores vs donde FN son peores

**Repasa tus flashcards nuevas 2 veces**

**Duerme bien.** Mañana conectamos todo con Azure ML. 😴

---

## 📊 PROGRESO SEMANA 2

```
Lunes:     ████████████████████ 100% ✅
Martes:    ████████████████████ 100% ✅
Miércoles: ████████████████████ 100% ✅
Jueves:    ░░░░░░░░░░░░░░░░░░░░   0%
Viernes:   ░░░░░░░░░░░░░░░░░░░░   0%
Sábado:    ░░░░░░░░░░░░░░░░░░░░   0%
```

**Horas Semana 2:** 4.5/10 horas completadas (45%) ✅
**Progreso Total:** 14.5/60 horas (24.2%) 📈

---

**¡Nos vemos mañana Jueves para Azure Machine Learning workspace!** 🚀

**Mañana aprenderás:**

- Qué es Azure ML workspace y sus componentes
- Datasets, experiments, models, endpoints
- Azure ML Designer (visual, sin código)
- Diferencia entre Azure ML y Azure AI Services
- Cuándo usar cada uno

**Será el puente entre teoría y práctica.** 💪
