# 📚 MIÉRCOLES 12 NOV - SEMANA 2: Clasificación y Métricas

**Fecha:** Miércoles 12 de noviembre 2025  
**Semana:** 2 de 6  
**Tema:** Clasificación y métricas de evaluación  
**Duración:** 1 hora 30 minutos

---

## 🎯 Objetivos del día

Al finalizar hoy deberás:

- ✅ Entender qué es clasificación y en qué se diferencia de regresión
- ✅ Dominar la matriz de confusión (TP, TN, FP, FN)
- ✅ Comprender las 4 métricas principales: Accuracy, Precision, Recall, F1-Score
- ✅ **Entender ROC Curve y AUC**
- ✅ Saber cuándo priorizar Precision vs Recall
- ✅ Interpretar métricas en contexto real

---

## 📖 PARTE 1: ¿Qué es Clasificación? (15 minutos)

### Definición

**Clasificación:** Tipo de Machine Learning supervisado donde predices una **categoría** o **clase**.

**Diferencia con Regresión:**

- **Regresión:** Predice **números** (precio, temperatura, edad)
- **Clasificación:** Predice **categorías** (spam/no spam, perro/gato, sano/enfermo)

---

### Tipos de clasificación

**1. Clasificación Binaria (2 clases)**

- Spam o No spam
- Fraude o Legítimo
- Positivo o Negativo (enfermedad)
- Aprobar o Reprobar

**2. Clasificación Multiclase (3+ clases)**

- Tipo de flor (setosa, versicolor, virginica)
- Categoría de producto (electrónica, ropa, hogar)
- Nivel de riesgo (bajo, medio, alto)
- Reconocimiento de dígitos (0-9)

**3. Clasificación Multilabel**

- Un ítem puede pertenecer a múltiples clases
- Ejemplo: Una película puede ser "Acción" Y "Comedia" Y "Sci-Fi"

---

### Ejemplos del mundo real

**Medicina:**

- Diagnóstico: ¿Tiene cáncer? (sí/no)
- Tipo de tumor: benigno, maligno, metastásico

**Finanzas:**

- Aprobación de crédito: aprobar/rechazar
- Nivel de riesgo: bajo, medio, alto

**Marketing:**

- Probabilidad de compra: comprará/no comprará
- Segmentación de clientes: premium, regular, básico

**Tecnología:**

- Filtro de spam: spam/legítimo
- Reconocimiento de voz: 10 dígitos (0-9)
- Moderación de contenido: apropiado/inapropiado

---

## 📖 PARTE 2: Matriz de Confusión (20 minutos)

### ¿Qué es?

**La matriz de confusión** muestra cómo se desempeña tu modelo comparando predicciones vs realidad.

**Para clasificación binaria:**

```
                    PREDICCIÓN
                 Negativo  Positivo
                 ─────────────────
REALIDAD  Neg |     TN        FP
          Pos |     FN        TP
```

---

### Los 4 elementos clave

**1. True Positive (TP) - Verdadero Positivo**

- **Realidad:** Positivo
- **Predicción:** Positivo
- **Resultado:** ✅ CORRECTO
- **Ejemplo:** Email es spam y el modelo lo detecta como spam

**2. True Negative (TN) - Verdadero Negativo**

- **Realidad:** Negativo
- **Predicción:** Negativo
- **Resultado:** ✅ CORRECTO
- **Ejemplo:** Email es legítimo y el modelo lo clasifica como legítimo

**3. False Positive (FP) - Falso Positivo**

- **Realidad:** Negativo
- **Predicción:** Positivo
- **Resultado:** ❌ ERROR (Falsa alarma)
- **Ejemplo:** Email es legítimo pero el modelo lo marca como spam
- **También llamado:** Error Tipo I

**4. False Negative (FN) - Falso Negativo**

- **Realidad:** Positivo
- **Predicción:** Negativo
- **Resultado:** ❌ ERROR (Se me escapó)
- **Ejemplo:** Email es spam pero pasa como legítimo
- **También llamado:** Error Tipo II

---

### Ejemplo completo: Detector de spam

**Datos:**

```
100 emails en total:
- 60 son legítimos (reales)
- 40 son spam (reales)
```

**Matriz de confusión:**

```
                    Predicción
                 Legítimo    Spam
                 ──────────────────
Real  Legítimo      50        10    ← TN=50, FP=10
      Spam           5        35    ← FN=5,  TP=35
```

**Interpretación:**

- **TP = 35:** Detectó correctamente 35 emails spam
- **TN = 50:** Identificó correctamente 50 emails legítimos
- **FP = 10:** Marcó incorrectamente 10 emails legítimos como spam (¡problema!)
- **FN = 5:** Dejó pasar 5 emails spam al inbox

---

### Consejos para recordar

**Trucos nemotécnicos:**

**True/False** = ¿La predicción fue correcta?

- **True** → Acerté ✅
- **False** → Me equivoqué ❌

**Positive/Negative** = ¿Qué predije?

- **Positive** → Dije "SÍ"
- **Negative** → Dije "NO"

**Combinaciones:**

- **True Positive:** Dije SÍ y acerté ✅
- **True Negative:** Dije NO y acerté ✅
- **False Positive:** Dije SÍ pero me equivoqué ❌ (falsa alarma)
- **False Negative:** Dije NO pero me equivoqué ❌ (se me escapó)

---

## 📖 PARTE 3: Las 4 Métricas Principales (25 minutos)

### 1️⃣ ACCURACY (Exactitud)

**¿Qué mide?**
"¿Qué porcentaje de predicciones fueron correctas?"

**Fórmula:**

```
Accuracy = (TP + TN) / (TP + TN + FP + FN)
Accuracy = Aciertos totales / Total de predicciones
```

**Ejemplo del detector de spam:**

```
Accuracy = (35 + 50) / 100 = 85 / 100 = 0.85 = 85%
```

**Interpretación:**
"El modelo acierta el 85% de las veces"

**✅ Ventajas:**

- Súper fácil de entender
- Intuitivo para explicar
- Métrica más común

**⚠️ PROBLEMA GRAVE: Clases desbalanceadas**

**Ejemplo:**

```
1000 transacciones bancarias:
- 950 son legítimas (95%)
- 50 son fraude (5%)

Modelo TONTO que siempre predice "legítimo":
Accuracy = 95% ← ¡Parece bueno!

Pero NUNCA detecta fraude ← ¡Es inútil!
```

**Por eso necesitamos Precision y Recall.**

---

### 2️⃣ PRECISION (Precisión)

**¿Qué mide?**
"De todo lo que dije que era POSITIVO, ¿cuánto realmente lo era?"

**Pregunta clave:** "¿Qué tan confiable soy cuando digo SÍ?"

**Fórmula:**

```
Precision = TP / (TP + FP)
Precision = Verdaderos positivos / Todos los que dije positivos
```

**Ejemplo del detector de spam:**

```
Predije "SPAM" para 45 emails (TP=35, FP=10)
Precision = 35 / (35 + 10) = 35 / 45 = 0.78 = 78%
```

**Interpretación:**
"Cuando digo que es spam, tengo razón el 78% de las veces"
"22% de las veces bloqueo emails legítimos" ← ¡problema!

**🎯 ¿Cuándo es importante ALTA Precision?**

Cuando los **Falsos Positivos son MUY costosos:**

**Ejemplos:**

- **Filtro de spam:** Bloquear email importante como spam (pierdes info crítica)
- **Condena judicial:** Encarcelar a inocente (injusticia grave)
- **Diagnóstico médico:** Decir que tiene cáncer cuando no lo tiene (estrés innecesario, tratamientos invasivos)
- **Recomendaciones:** Recomendar producto irrelevante (molesta al usuario)

**Estrategia:** "Prefiero ser conservador y solo decir SÍ cuando estoy muy seguro"

---

### 3️⃣ RECALL (Exhaustividad/Sensibilidad)

**¿Qué mide?**
"De todos los casos POSITIVOS reales, ¿cuántos detecté?"

**Pregunta clave:** "¿Qué tan completo soy en encontrar todos los casos positivos?"

**Fórmula:**

```
Recall = TP / (TP + FN)
Recall = Verdaderos positivos / Todos los positivos reales
```

**Ejemplo del detector de spam:**

```
Había 40 emails spam reales (TP=35, FN=5)
Recall = 35 / (35 + 5) = 35 / 40 = 0.875 = 87.5%
```

**Interpretación:**
"Detecto el 87.5% de todos los emails spam"
"Se me escapan el 12.5% de los spam" ← algunos llegan al inbox

**🎯 ¿Cuándo es importante ALTO Recall?**

Cuando los **Falsos Negativos son MUY peligrosos:**

**Ejemplos:**

- **Detector de cáncer:** NO detectar cáncer cuando sí existe (paciente no recibe tratamiento → fatal)
- **Detector de fraude:** NO detectar fraude real (pierdes dinero)
- **Sistema antivirus:** NO detectar malware (computadora infectada)
- **Detección de fallas:** NO detectar falla en motor de avión (catastrófico)

**Estrategia:** "Prefiero revisar más casos (incluso falsos positivos) con tal de NO perderme ningún caso real"

---

### 4️⃣ F1-SCORE

**¿Qué mide?**
"Balance entre Precision y Recall"

**Fórmula:**

```
F1-Score = 2 × (Precision × Recall) / (Precision + Recall)
```

Es la **media armónica** de Precision y Recall.

**Ejemplo:**

```
Precision = 0.78 (78%)
Recall = 0.875 (87.5%)

F1 = 2 × (0.78 × 0.875) / (0.78 + 0.875)
F1 = 2 × 0.6825 / 1.655
F1 = 1.365 / 1.655
F1 = 0.825 = 82.5%
```

**Interpretación:**

- F1 penaliza extremos (solo alta Precision O solo alto Recall)
- Recompensa balance entre ambos
- Útil cuando necesitas equilibrio

**🎯 ¿Cuándo usar F1-Score?**

- Cuando tanto FP como FN son problemáticos
- Clases desbalanceadas
- Necesitas una métrica única que combine Precision y Recall
- No tienes preferencia clara entre Precision vs Recall

**Nota:** F1 siempre está entre Precision y Recall (nunca es mayor que ambos).

---

### 📊 Tabla comparativa de métricas

| Métrica       | Fórmula       | Pregunta que responde      | Cuándo priorizar     |
| ------------- | ------------- | -------------------------- | -------------------- |
| **Accuracy**  | (TP+TN)/Total | ¿% de aciertos totales?    | Clases balanceadas   |
| **Precision** | TP/(TP+FP)    | ¿Confiable cuando digo SÍ? | FP muy costosos      |
| **Recall**    | TP/(TP+FN)    | ¿Detecto todos los SÍ?     | FN muy peligrosos    |
| **F1-Score**  | 2×(P×R)/(P+R) | ¿Balance P y R?            | Necesitas equilibrio |

---

## 📖 PARTE 4: ROC Curve y AUC (20 minutos)

### ¿Qué es ROC?

**ROC (Receiver Operating Characteristic) Curve:**

Es una **gráfica** que muestra el rendimiento de un clasificador binario en **todos los umbrales posibles**.

**Ejes de la gráfica:**

```
True Positive Rate (TPR)
        ↑
   1.0  |     ●────●
        |   ●──●        ← Curva ROC
   0.8  | ●─●            (mejor modelo)
        |●
   0.6  |      ╱  ← Línea diagonal
        |    ╱     (modelo aleatorio)
   0.4  |  ╱      AUC = 0.5
        |╱
   0.2  |
        |
   0.0  └─────────────────→
        0.0  0.2  0.4  0.6  0.8  1.0
              False Positive Rate (FPR)
```

**Eje Y - True Positive Rate (TPR):**

- También llamado: **Recall** o **Sensibilidad**
- Fórmula: TPR = TP / (TP + FN)
- Pregunta: "¿Qué % de positivos reales detecto?"

**Eje X - False Positive Rate (FPR):**

- Opuesto a: **Especificidad** (FPR = 1 - Especificidad)
- Fórmula: FPR = FP / (FP + TN)
- Pregunta: "¿Qué % de negativos reales marco incorrectamente como positivos?"

---

### ¿Cómo se crea la curva ROC?

**Concepto de umbral:**

La mayoría de clasificadores no dan respuesta binaria directa, sino una **probabilidad** o **score**:

**Ejemplo detector de spam:**

```
Email 1: score = 0.95 → Muy probable spam
Email 2: score = 0.78 → Probable spam
Email 3: score = 0.45 → Incierto
Email 4: score = 0.23 → Probable legítimo
Email 5: score = 0.05 → Muy probable legítimo
```

**Puedes elegir diferentes umbrales:**

**Umbral = 0.5** (estándar):

```
score > 0.5 → SPAM
score ≤ 0.5 → LEGÍTIMO
```

**Umbral = 0.8** (conservador):

```
score > 0.8 → SPAM (más estricto)
score ≤ 0.8 → LEGÍTIMO
```

- Menos FP (más Precision)
- Más FN (menos Recall)

**Umbral = 0.3** (agresivo):

```
score > 0.3 → SPAM (más permisivo)
score ≤ 0.3 → LEGÍTIMO
```

- Más FP (menos Precision)
- Menos FN (más Recall)

**La curva ROC** representa todos estos puntos para TODOS los umbrales posibles.

---

### ¿Qué es AUC?

**AUC (Area Under the Curve):**

Es el **área bajo la curva ROC**.

**Rango:** 0 a 1

**Interpretación:**

| AUC         | Calidad del modelo             |
| ----------- | ------------------------------ |
| **1.0**     | Perfecto (100% separación)     |
| **0.9-1.0** | Excelente                      |
| **0.8-0.9** | Muy bueno                      |
| **0.7-0.8** | Bueno                          |
| **0.6-0.7** | Pobre                          |
| **0.5**     | Aleatorio (como lanzar moneda) |
| **<0.5**    | Peor que aleatorio             |

---

### ¿Qué significa AUC en términos prácticos?

**AUC = 0.85 significa:**

"Si tomas un caso positivo aleatorio y un caso negativo aleatorio, el modelo tiene **85% de probabilidad** de darle mayor score al positivo que al negativo"

**Ejemplo visual:**

```
Caso positivo real:  score = 0.8
Caso negativo real:  score = 0.3

Model correcto: 0.8 > 0.3 ✅

Con AUC = 0.85, esto pasa el 85% de las veces
```

---

### Ventajas de AUC

**✅ Ventajas:**

1. **Métrica única** que resume el rendimiento general
2. **No depende del umbral** de clasificación
3. **Funciona bien con clases desbalanceadas**
4. **Fácil de comparar** diferentes modelos
5. **Robusta** a distribución de clases

**Comparación de modelos:**

```
Modelo A: AUC = 0.92 → Mejor
Modelo B: AUC = 0.87 → Bueno
Modelo C: AUC = 0.73 → Moderado
```

---

### Curva ROC perfecta vs aleatoria

**Modelo perfecto (AUC = 1.0):**

```
TPR
 ↑
1.0|●────────────
   |│
   |│
   |│
   |●
0.0└───────────→ FPR
   0.0        1.0
```

- Va directo a TPR=1.0 con FPR=0
- Separa perfectamente positivos de negativos

**Modelo aleatorio (AUC = 0.5):**

```
TPR
 ↑
1.0|        ●
   |      ╱
   |    ╱
   |  ╱   ← Línea diagonal
   |╱
0.0●───────────→ FPR
   0.0        1.0
```

- Línea diagonal de 45 grados
- No mejor que adivinar al azar

---

### ROC y AUC en Azure AutoML

**En Azure AutoML:**

Puedes elegir **"AUC weighted"** como **primary metric** para clasificación:

```python
automl_config = AutoMLConfig(
    task='classification',
    primary_metric='AUC_weighted',  ← Para optimizar AUC
    training_data=dataset,
    label_column_name='target'
)
```

**"AUC weighted":**

- Para clasificación multiclase
- Calcula AUC para cada clase
- Promedio ponderado por tamaño de clase

---

### Cuándo usar AUC vs otras métricas

**Usa AUC cuando:**

- ✅ Clases desbalanceadas
- ✅ Costo de FP y FN es similar
- ✅ Quieres métrica independiente del umbral
- ✅ Comparar múltiples modelos

**Usa Precision cuando:**

- ✅ FP muy costosos
- ✅ Necesitas alta confianza en positivos

**Usa Recall cuando:**

- ✅ FN muy peligrosos
- ✅ No puedes perderte casos positivos

**Usa F1 cuando:**

- ✅ Necesitas balance
- ✅ Clases desbalanceadas

---

### Ejemplo completo: Detector médico

**Escenario:** Detectar cáncer de mama

**Matriz de confusión:**

```
                No cáncer    Cáncer
No cáncer         850          50
Cáncer             30          70
```

**Métricas calculadas:**

```
Accuracy = (850+70)/1000 = 92%
Precision = 70/(70+50) = 58.3%
Recall = 70/(70+30) = 70%
F1 = 2×(0.583×0.70)/(0.583+0.70) = 63.6%

TPR = 70/100 = 0.70
FPR = 50/900 = 0.056

AUC = 0.89 (calculado considerando todos los umbrales)
```

**Interpretación:**

- **Alta Accuracy (92%)** pero engañosa (clases desbalanceadas)
- **Recall moderado (70%)** - detecta 70% de cánceres ⚠️
- **Precision baja (58.3%)** - muchos falsos positivos
- **AUC bueno (0.89)** - modelo tiene buena capacidad de discriminación

**Decisión:**
Para cáncer, **priorizar Recall** (no podemos perdernos casos reales). Ajustar umbral para aumentar Recall, aunque aumente FP.

---

## 📖 PARTE 5: Trade-off Precision vs Recall (10 minutos)

### El dilema fundamental

**NO puedes maximizar ambos simultáneamente** ⚠️

```
          Alta Precision
               ↑
               │
   Conservador │
   (digo SÍ solo│
    si estoy    │
    muy seguro) │
               │
               │
───────────────┼───────────────→ Alto Recall
               │
               │ Agresivo
               │ (digo SÍ con
               │  poca evidencia)
               │
               ↓
         Baja Precision
```

---

### ¿Por qué existe este trade-off?

**Ejemplo detector de spam:**

**Modelo conservador (alta Precision):**

```
Umbral alto = 0.9
Solo marca spam si score > 0.9

Resultado:
✅ Precision alta (pocos FP)
❌ Recall bajo (muchos FN - spam no detectado)
```

**Modelo agresivo (alto Recall):**

```
Umbral bajo = 0.3
Marca spam si score > 0.3

Resultado:
✅ Recall alto (pocos FN)
❌ Precision baja (muchos FP - emails legítimos bloqueados)
```

---

### ¿Cómo decidir?

**Pregúntate:** "¿Qué error es MÁS costoso?"

**Tabla de decisión:**

| Escenario              | FP más costoso                    | FN más costoso        | Priorizar     |
| ---------------------- | --------------------------------- | --------------------- | ------------- |
| Spam email             | Email importante bloqueado        | Spam en inbox         | **Precision** |
| Detector cáncer        | Estrés por falso positivo         | No tratar cáncer real | **Recall**    |
| Fraude bancario        | Bloquear transacción legítima     | Perder dinero         | **Recall**    |
| Recomendación producto | Molestar con producto irrelevante | Perder venta          | **Precision** |
| Antivirus              | Bloquear programa legítimo        | Infectar computadora  | **Recall**    |

---

## ✅ EJERCICIOS PRÁCTICOS (20 minutos)

### Ejercicio 1: Calcular métricas

**Detector de productos defectuosos en fábrica:**

```
Matriz de confusión:
                Bueno    Defectuoso
Bueno            850         50
Defectuoso        20         80
```

**Calcula:**

1. Accuracy
2. Precision
3. Recall
4. F1-Score

<details>
<summary>Ver solución</summary>

**Identificar valores:**

- TP = 80 (defectuoso detectado correctamente)
- TN = 850 (bueno detectado correctamente)
- FP = 50 (falsa alarma - bueno marcado como defectuoso)
- FN = 20 (error - defectuoso no detectado)
- Total = 1000

**Cálculos:**

1. **Accuracy:**

```
Accuracy = (TP + TN) / Total
Accuracy = (80 + 850) / 1000
Accuracy = 930 / 1000 = 0.93 = 93%
```

2. **Precision:**

```
Precision = TP / (TP + FP)
Precision = 80 / (80 + 50)
Precision = 80 / 130 = 0.615 = 61.5%
```

3. **Recall:**

```
Recall = TP / (TP + FN)
Recall = 80 / (80 + 20)
Recall = 80 / 100 = 0.80 = 80%
```

4. **F1-Score:**

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
F1 = 2 × (0.615 × 0.80) / (0.615 + 0.80)
F1 = 2 × 0.492 / 1.415
F1 = 0.984 / 1.415 = 0.695 = 69.5%
```

**Interpretación:**

- Alta Accuracy (93%) - parece bueno
- Precision moderada (61.5%) - muchos falsos positivos (descartar productos buenos)
- Recall bueno (80%) - detecta la mayoría de defectos
- F1 moderado (69.5%) - balance entre P y R

**Problema:** Estamos descartando muchos productos buenos (FP=50). Esto tiene costo económico.

</details>

---

### Ejercicio 2: Interpretar escenarios

**Escenario A: Sistema de seguridad aeropuerto**

```
Detector de armas:
Precision = 85%
Recall = 60%
```

**Pregunta:** ¿Es aceptable? ¿Qué métrica mejorarías?

<details>
<summary>Ver solución</summary>

**❌ NO es aceptable**

**Problema:** Recall de 60% significa que el 40% de las armas reales NO se detectan. ¡Inaceptable en seguridad!

**Solución:** **Priorizar Recall** - debemos detectar TODAS las armas, aunque tengamos más falsas alarmas (revisiones manuales extra).

**Trade-off:** Aceptar baja Precision (más revisiones manuales) para maximizar Recall (seguridad).

</details>

---

**Escenario B: Sistema de recomendación de películas**

```
Precision = 70%
Recall = 40%
```

**Pregunta:** ¿Qué métrica es más importante aquí?

<details>
<summary>Ver solución</summary>

**Priorizar: Precision**

**Razón:**

- **FP:** Recomendar película mala → usuario molesto, pierde confianza
- **FN:** No recomendar película buena → hay muchas otras películas

Es mejor recomendar pocas películas pero muy relevantes (alta Precision) que recomendar muchas incluyendo malas (bajo Precision).

El usuario no puede ver todas las películas buenas de todas formas (FN es menos grave).

</details>

---

### Ejercicio 3: Matriz de confusión multiclase

**Clasificador de flores (3 clases):**

```
              Setosa  Versicolor  Virginica
Setosa          45        3          2
Versicolor       1       38          6
Virginica        0        4         46
```

**Calcula:**

1. Accuracy total
2. Precision para cada clase
3. Recall para cada clase

<details>
<summary>Ver solución</summary>

**Total de muestras:** 45+3+2+1+38+6+0+4+46 = 145

**1. Accuracy total:**

```
Predicciones correctas = 45 + 38 + 46 = 129
Accuracy = 129 / 145 = 0.890 = 89%
```

**2. Precision por clase:**

**Setosa:**

```
TP = 45
FP = 1 + 0 = 1
Precision = 45 / (45 + 1) = 45/46 = 0.978 = 97.8%
```

**Versicolor:**

```
TP = 38
FP = 3 + 4 = 7
Precision = 38 / (38 + 7) = 38/45 = 0.844 = 84.4%
```

**Virginica:**

```
TP = 46
FP = 2 + 6 = 8
Precision = 46 / (46 + 8) = 46/54 = 0.852 = 85.2%
```

**3. Recall por clase:**

**Setosa:**

```
TP = 45
FN = 3 + 2 = 5
Recall = 45 / (45 + 5) = 45/50 = 0.90 = 90%
```

**Versicolor:**

```
TP = 38
FN = 1 + 4 = 5
Recall = 38 / (38 + 5) = 38/43 = 0.884 = 88.4%
```

**Virginica:**

```
TP = 46
FN = 6 + 0 = 6
Recall = 46 / (46 + 6) = 46/52 = 0.885 = 88.5%
```

**Interpretación:**

- Setosa es la más fácil de identificar (alta Precision)
- Las tres clases tienen Recall similar (~88-90%)
- Versicolor y Virginica se confunden más entre sí
</details>

---

## 📝 FLASHCARDS para crear HOY

### Conceptos básicos

**Tarjeta 1:**

- Frente: "¿Qué predice Clasificación?"
- Atrás: "Categorías o clases (spam/no spam, perro/gato), NO números"

**Tarjeta 2:**

- Frente: "Diferencia Clasificación vs Regresión"
- Atrás: "Clasificación → categorías. Regresión → números continuos"

**Tarjeta 3:**

- Frente: "True Positive (TP)"
- Atrás: "Realidad: Positivo. Predicción: Positivo. ✅ CORRECTO"

**Tarjeta 4:**

- Frente: "False Positive (FP)"
- Atrás: "Realidad: Negativo. Predicción: Positivo. ❌ Falsa alarma"

**Tarjeta 5:**

- Frente: "False Negative (FN)"
- Atrás: "Realidad: Positivo. Predicción: Negativo. ❌ Se me escapó"

### Métricas

**Tarjeta 6:**

- Frente: "Fórmula Accuracy"
- Atrás: "(TP + TN) / Total. % de predicciones correctas"

**Tarjeta 7:**

- Frente: "Fórmula Precision"
- Atrás: "TP / (TP + FP). ¿Confiable cuando digo SÍ?"

**Tarjeta 8:**

- Frente: "Fórmula Recall"
- Atrás: "TP / (TP + FN). ¿Detecto todos los SÍ reales?"

**Tarjeta 9:**

- Frente: "Fórmula F1-Score"
- Atrás: "2 × (Precision × Recall) / (Precision + Recall). Balance entre P y R"

### ROC y AUC

**Tarjeta 10:**

- Frente: "¿Qué es ROC Curve?"
- Atrás: "Gráfica de TPR (Recall) vs FPR en todos los umbrales posibles"

**Tarjeta 11:**

- Frente: "¿Qué es AUC?"
- Atrás: "Área bajo la curva ROC. Rango: 0-1. Mide capacidad de discriminación del modelo"

**Tarjeta 12:**

- Frente: "Interpretación AUC = 0.85"
- Atrás: "85% probabilidad de que el modelo dé mayor score a caso positivo que negativo. Modelo muy bueno"

**Tarjeta 13:**

- Frente: "AUC = 0.5 significa..."
- Atrás: "Modelo aleatorio, no mejor que lanzar una moneda"

**Tarjeta 14:**

- Frente: "Ventaja de AUC sobre Accuracy"
- Atrás: "No depende del umbral, funciona bien con clases desbalanceadas"

### Cuándo usar cada métrica

**Tarjeta 15:**

- Frente: "¿Cuándo priorizar Precision?"
- Atrás: "Cuando Falsos Positivos son muy costosos (ej: spam, condena judicial)"

**Tarjeta 16:**

- Frente: "¿Cuándo priorizar Recall?"
- Atrás: "Cuando Falsos Negativos son muy peligrosos (ej: cáncer, fraude, antivirus)"

**Tarjeta 17:**

- Frente: "Trade-off Precision vs Recall"
- Atrás: "No puedes maximizar ambos simultáneamente. Aumentar uno reduce el otro"

**Tarjeta 18:**

- Frente: "Ejemplo FP peligroso"
- Atrás: "Detector de spam marca email importante como spam → pierdes info crítica"

**Tarjeta 19:**

- Frente: "Ejemplo FN peligroso"
- Atrás: "Detector médico dice 'no hay cáncer' pero sí lo hay → paciente no recibe tratamiento"

**Tarjeta 20:**

- Frente: "¿Cuándo usar AUC?"
- Atrás: "Clases desbalanceadas, comparar modelos, cuando necesitas métrica independiente del umbral"

---

## 🎯 RESUMEN DEL DÍA

### Lo que aprendiste hoy:

✅ **Clasificación vs Regresión**

- Clasificación predice categorías
- Regresión predice números

✅ **Matriz de confusión**

- TP, TN, FP, FN
- Cómo identificar cada uno

✅ **4 métricas principales**

- Accuracy: % aciertos totales
- Precision: confiable cuando digo SÍ
- Recall: detecto todos los SÍ reales
- F1: balance entre P y R

✅ **ROC Curve y AUC**

- ROC: gráfica TPR vs FPR
- AUC: área bajo curva (0-1)
- Interpretación de AUC
- Ventajas sobre otras métricas

✅ **Trade-off Precision vs Recall**

- No puedes maximizar ambos
- Depende del costo de FP vs FN
- Cómo decidir cuál priorizar

✅ **Aplicación práctica**

- Detector spam: priorizar Precision
- Detector cáncer: priorizar Recall
- Productos defectuosos: depende del costo

---

## 📊 Tu progreso en Semana 2

```
Semana 2: Machine Learning en profundidad
├── ✅ Lunes 10: Tipos de ML profundo
├── ✅ Martes 11: Regresión y métricas
├── ✅ Miércoles 12: Clasificación y métricas (HOY - ACTUALIZADO)
├── 📅 Jueves 13: Azure ML workspace
├── 📅 Viernes 14: AutoML
└── 📅 Sábado 15: Lab - Crear primer modelo
```

**¡Ya completaste el 43% de la Semana 2!** 🎉

---

## 📅 MAÑANA (Jueves 13 de noviembre)

**Tema:** Azure Machine Learning Workspace en detalle

**Lo que aprenderás:**

- Qué es Azure ML workspace
- Componentes principales (compute, datastores, datasets)
- Azure ML Designer (herramienta visual)
- Cómo desplegar modelos
- Diferencia entre Azure ML y otros servicios

---

## 💡 CONSEJOS PARA HOY

1. **Practica con los ejercicios** - no solo leas
2. **Crea las flashcards inmediatamente** después de cada sección
3. **Relaciona con el Martes:**
   - Martes: métricas para números (MAE, RMSE, R²)
   - Miércoles: métricas para categorías (Accuracy, Precision, Recall, AUC)
4. **Piensa en ejemplos reales** de tu vida/trabajo
5. **La sección de ROC y AUC** es nueva y importante - repásala bien

---

## 🎓 PARA EL EXAMEN - PREGUNTAS TÍPICAS

**Ejemplo 1:**
_"Un modelo de detección de fraude tiene 95% de Accuracy pero solo detecta el 30% de los fraudes reales. ¿Cuál es el problema?"_

- **Respuesta:** Bajo Recall (solo 30%). El modelo tiene alta Accuracy porque la mayoría son transacciones legítimas, pero se pierde el 70% de los fraudes (Falsos Negativos).

**Ejemplo 2:**
_"¿Qué métrica priorizarías en un sistema que detecta defectos críticos en piezas de avión?"_

- **Respuesta:** Recall - no podemos permitirnos perder ningún defecto crítico (Falsos Negativos son peligrosos).

**Ejemplo 3:**
_"Tu modelo tiene Precision=90% y Recall=50%. ¿Qué significa?"_

- **Respuesta:** El modelo es muy confiable cuando predice positivo (90%), pero se pierde la mitad de los casos positivos reales (50%).

**Ejemplo 4:**
_"¿Qué representa el área bajo la curva ROC (AUC)?"_

- **Respuesta:** La capacidad del modelo para discriminar entre clases. AUC=0.85 significa 85% de probabilidad de que el modelo dé mayor score a un caso positivo que a uno negativo.

**Ejemplo 5:**
_"Un modelo tiene AUC=0.92. ¿Es un buen modelo?"_

- **Respuesta:** Sí, es un modelo excelente (0.9-1.0 es rango excelente). Tiene muy buena capacidad de separar clases positivas y negativas.

**Ejemplo 6:**
_"¿Por qué AUC es mejor que Accuracy para clases desbalanceadas?"_

- **Respuesta:** Accuracy puede ser engañosa con clases desbalanceadas (un modelo que siempre predice la clase mayoritaria puede tener alta Accuracy pero ser inútil). AUC evalúa la capacidad de discriminación independientemente del desbalanceo.

---

## ✅ CHECKLIST DE HOY

Antes de terminar, asegúrate de:

- [-] Entender clasificación vs regresión
- [-] Dominar matriz de confusión (TP, TN, FP, FN)
- [-] Saber calcular las 4 métricas principales
- [-] **Entender qué son ROC y AUC**
- [-] **Saber cuándo usar AUC vs otras métricas**
- [-] Comprender trade-off Precision vs Recall
- [-] Completar los 3 ejercicios
- [-] Crear las 20 flashcards en Anki
- [-] Repasar flashcards de Lunes y Martes

---

## 🚀 MOTIVACIÓN

**¡Excelente progreso!** Clasificación y sus métricas son conceptos **fundamentales** en ML.

**Lo que dominas ahora:**

- ✅ Tipos de ML
- ✅ Regresión completa
- ✅ Clasificación completa
- ✅ **ROC y AUC** (concepto avanzado)

## **Mañana:** Conectarás todo esto con Azure ML - verás estas métricas en acción.

**¡Que tengas un excelente estudio!** 📚💻

**Nos vemos mañana para Azure ML Workspace.** 🚀

---

_Última actualización: Miércoles 12 de noviembre 2025_  
_Semana 2 de 6 - Día 3 de 7_
