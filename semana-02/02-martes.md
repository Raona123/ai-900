# 📚 SEMANA 2 - MACHINE LEARNING EN PROFUNDIDAD

---

## 📖 MARTES 11 NOV (1.5 horas) - Regresión y sus métricas

### 🎯 Objetivo del día

Entender qué es regresión en profundidad y cómo evaluar si un modelo de regresión es bueno

---

## 🔄 REPASO RÁPIDO: ¿Qué es Regresión?

**Del Lunes aprendiste:**

- ✅ Regresión = predecir NÚMEROS continuos
- ✅ Responde "¿Cuánto?" o "¿Qué valor?"
- ✅ Ejemplos: precio, temperatura, ventas, edad, tiempo

**Hoy profundizaremos en:**

- Cómo funciona realmente la regresión
- Cómo saber si tu modelo es bueno
- Métricas para evaluar modelos de regresión

---

## 📈 ¿CÓMO FUNCIONA LA REGRESIÓN?

### 💡 Concepto fundamental: Encontrar la relación

**La regresión busca la RELACIÓN entre:**

- **Variables de entrada (features/características):** Los datos que tienes
- **Variable de salida (target/objetivo):** El número que quieres predecir

**Analogía:**
Como encontrar la fórmula que conecta causa → efecto

- Tamaño de casa (causa) → Precio (efecto)
- Horas de estudio (causa) → Nota del examen (efecto)

---

### 📊 REGRESIÓN LINEAL (el tipo más simple)

**Concepto:** Encontrar una **línea recta** que mejor representa los datos

#### Ejemplo visual (imagina este gráfico):

```
Precio ($)
↑
|                                    •
|                              •
|                        •
|                  •
|            •
|      •
|•
└──────────────────────────────────→ Tamaño (m²)
     Línea de regresión: y = mx + b
```

**La línea representa:**

- `y` = precio (lo que queremos predecir)
- `x` = tamaño (lo que sabemos)
- `m` = pendiente (cuánto sube el precio por cada m² adicional)
- `b` = intersección (precio base)

**Ejemplo concreto:**

```
Precio = 1,000€ * Tamaño + 50,000€
         ↑                 ↑
      Por cada m²    Precio base

Si casa tiene 100m²:
Precio = 1,000 * 100 + 50,000 = 150,000€
```

---

### 🎯 El objetivo: Minimizar el ERROR

**¿Qué es el error?**
La diferencia entre:

- Lo que el modelo PREDIJO
- Lo que REALMENTE era

**Ejemplo:**

- Precio real de casa: 152,000€
- Precio predicho: 150,000€
- Error: 2,000€

**El modelo busca:** Ajustar la línea para que los errores sean lo más pequeños posible

---

## 📏 MÉTRICAS DE REGRESIÓN: ¿Es bueno mi modelo?

**Pregunta clave:** "Entrené un modelo de regresión. ¿Cómo sé si funciona bien?"

**Respuesta:** Usas MÉTRICAS de evaluación

### 🎯 Las 3 métricas principales:

```
MÉTRICAS DE REGRESIÓN
│
├── MAE (Mean Absolute Error) - Error Absoluto Medio
├── RMSE (Root Mean Square Error) - Raíz del Error Cuadrático Medio
└── R² (R-squared) - Coeficiente de Determinación
```

---

## 1️⃣ MAE (Mean Absolute Error)

### 📊 ¿Qué mide?

**El error promedio en las mismas unidades que tu predicción.**

**Fórmula en palabras:**

```
MAE = Promedio del valor absoluto
VALOR ABSOLUTO = Valor real - Valor Predicho
```

## NOTA: El valor absoluto ignora si es positivo o negativo

### 💡 Ejemplo práctico:

**Predijiste precios de 5 casas:**

| Casa | Precio Real | Precio Predicho | Error   | Error Absoluto |
| ---- | ----------- | --------------- | ------- | -------------- |
| 1    | 150,000€    | 148,000€        | +2,000€ | 2,000€         |
| 2    | 200,000€    | 205,000€        | -5,000€ | 5,000€         |
| 3    | 180,000€    | 178,000€        | +2,000€ | 2,000€         |
| 4    | 220,000€    | 215,000€        | +5,000€ | 5,000€         |
| 5    | 190,000€    | 192,000€        | -2,000€ | 2,000€         |

**Cálculo del MAE:**

```
MAE = (2,000 + 5,000 + 2,000 + 5,000 + 2,000) / 5
MAE = 16,000 / 5
MAE = 3,200€
```

**Interpretación:**
"En promedio, mis predicciones se equivocan por 3,200€"

---

### ✅ Ventajas del MAE:

✅ **Fácil de entender:** Está en las mismas unidades (euros, metros, días)
✅ **Interpretable:** "Me equivoco en promedio por X"
✅ **No se afecta tanto por valores extremos (outliers)**

### ⚠️ Limitaciones del MAE:

⚠️ Trata todos los errores igual (un error de 10€ = diez errores de 1€)
⚠️ No "castiga" errores grandes más que errores pequeños

---

## 2️⃣ RMSE (Root Mean Square Error)

### 📊 ¿Qué mide?

**Similar al MAE, pero "castiga" más los errores grandes.**

**Fórmula en palabras:**

```
1. Calcula el error para cada predicción
2. Eleva cada error al cuadrado (esto amplifica errores grandes)
3. Saca el promedio de esos cuadrados
4. Saca la raíz cuadrada del promedio
```

**¿Por qué elevar al cuadrado?**

- Un error de 10 al cuadrado = 100
- Dos errores de 5 al cuadrado = 25 + 25 = 50
- ¡Prefiere muchos errores pequeños que un error grande!

---

### 💡 Ejemplo práctico (mismos datos):

| Casa | Precio Real | Precio Predicho | Error  | Error²     |
| ---- | ----------- | --------------- | ------ | ---------- |
| 1    | 150,000€    | 148,000€        | 2,000€ | 4,000,000  |
| 2    | 200,000€    | 205,000€        | 5,000€ | 25,000,000 |
| 3    | 180,000€    | 178,000€        | 2,000€ | 4,000,000  |
| 4    | 220,000€    | 215,000€        | 5,000€ | 25,000,000 |
| 5    | 190,000€    | 192,000€        | 2,000€ | 4,000,000  |

**Cálculo del RMSE:**

```
Suma de errores² = 4M + 25M + 4M + 25M + 4M = 62,000,000
Promedio = 62,000,000 / 5 = 12,400,000
RMSE = √12,400,000 ≈ 3,521€
```

**Interpretación:**
"En promedio (penalizando errores grandes), me equivoco por 3,521€"

---

### ✅ Ventajas del RMSE:

✅ **Penaliza errores grandes:** Útil cuando errores grandes son MUY malos
✅ **Mismas unidades** que el objetivo (euros, metros, etc.)
✅ **Más usado en competencias de ML**

### ⚠️ Limitaciones del RMSE:

⚠️ Más difícil de interpretar que MAE
⚠️ Muy sensible a outliers (valores extremos)
⚠️ Siempre será ≥ MAE (por diseño)

---

### 🔍 MAE vs RMSE: ¿Cuál usar?

| Situación                         | Usa  | Por qué                           |
| --------------------------------- | ---- | --------------------------------- |
| Errores grandes son CRÍTICOS      | RMSE | Penaliza más los errores grandes  |
| Quieres métrica fácil de explicar | MAE  | Más interpretable                 |
| Tienes muchos outliers en datos   | MAE  | Menos sensible a valores extremos |
| Estándar de la industria          | RMSE | Más común en competencias         |

**Para el examen AI-900:**

- ✅ Conocer QUÉ miden ambas
- ✅ Saber que ambas miden el error promedio
- ✅ RMSE penaliza errores grandes más
- ❌ NO necesitas calcularlas manualmente

---

## 3️⃣ R² (R-squared) - Coeficiente de Determinación

### 📊 ¿Qué mide?

**"¿Qué tan bien el modelo explica la variabilidad de los datos?"**

**Rango de valores: 0 a 1 (a veces puede ser negativo si el modelo es muy malo)**

- **R² = 1.0** (100%) → Modelo PERFECTO, predice TODO correctamente
- **R² = 0.8** (80%) → Modelo explica 80% de la variabilidad
- **R² = 0.5** (50%) → Modelo explica solo 50%
- **R² = 0.0** (0%) → Modelo no explica nada (tan malo como predecir el promedio)
- **R² < 0** → Modelo PEOR que predecir el promedio

```
R² responde: "De TODO lo que varían mis datos,
             ¿qué PORCENTAJE puedo explicar con mi modelo?"

R² = 0.85 significa:
"Mi modelo explica 85% de POR QUÉ los datos son diferentes.
El otro 15% se debe a factores que no incluí."
```

---

### 💡 Interpretación intuitiva:

**Imagina que:**

- Tienes datos de precios de casas: 100k, 150k, 200k, 250k
- La variabilidad (cuánto varían) es grande

**Tres escenarios:**

**1. Sin modelo (solo promedio):**

```
Predigo 175k para TODAS las casas
R² = 0 (no explico la variabilidad)
```

**2. Modelo malo:**

```
Mis predicciones varían un poco: 160k, 170k, 180k, 190k
R² = 0.3 (explico 30% de la variabilidad)
```

**3. Modelo bueno:**

```
Mis predicciones: 105k, 152k, 198k, 247k
R² = 0.95 (explico 95% de la variabilidad)
```

---

### 📊 ¿Qué es un buen R²?

**Depende del dominio, pero en general:**

| R²            | Interpretación   | Calidad    |
| ------------- | ---------------- | ---------- |
| **0.9 - 1.0** | Excelente modelo | ⭐⭐⭐⭐⭐ |
| **0.7 - 0.9** | Buen modelo      | ⭐⭐⭐⭐   |
| **0.5 - 0.7** | Modelo moderado  | ⭐⭐⭐     |
| **0.3 - 0.5** | Modelo débil     | ⭐⭐       |
| **< 0.3**     | Modelo muy débil | ⭐         |
| **< 0**       | Modelo horrible  | 💀         |

**IMPORTANTE:**

- En ciencias sociales: R² = 0.5 puede ser bueno
- En física/ingeniería: R² = 0.9 es el mínimo esperado
- En finanzas: R² = 0.3 puede ser útil

---

### ✅ Ventajas del R²:

✅ **Sin unidades:** Siempre entre 0 y 1, fácil de comparar
✅ **Intuitivo:** Porcentaje de variabilidad explicada
✅ **Estándar de la industria**

### ⚠️ Limitaciones del R²:

⚠️ Puede ser engañoso con datos pequeños
⚠️ No indica el tamaño del error (solo "fit")
⚠️ Puede mejorar artificialmente añadiendo más features

---

## 📊 TABLA COMPARATIVA: Las 3 métricas

| Métrica  | ¿Qué mide?                        | Rango  | Mejor valor  | Unidades            | Interpretación                  |
| -------- | --------------------------------- | ------ | ------------ | ------------------- | ------------------------------- |
| **MAE**  | Error promedio                    | 0 a ∞  | 0 (perfecto) | Mismas que objetivo | "Me equivoco en promedio por X" |
| **RMSE** | Error promedio (penaliza grandes) | 0 a ∞  | 0 (perfecto) | Mismas que objetivo | "Error típico es X"             |
| **R²**   | Variabilidad explicada            | -∞ a 1 | 1 (perfecto) | Sin unidades        | "Explico X% de los datos"       |

**Regla general:**

- MAE y RMSE: **Más bajo = mejor**
- R²: **Más alto = mejor** (cercano a 1)

---

## 🎯 EJEMPLO COMPLETO: Evaluar un modelo

### Caso: Predecir precio de casas

**Datos reales de 10 casas:**

| Casa | Precio Real | Precio Predicho | Error   |
| ---- | ----------- | --------------- | ------- |
| 1    | 150,000€    | 148,000€        | 2,000€  |
| 2    | 200,000€    | 205,000€        | -5,000€ |
| 3    | 180,000€    | 178,000€        | 2,000€  |
| 4    | 220,000€    | 215,000€        | 5,000€  |
| 5    | 190,000€    | 192,000€        | -2,000€ |
| 6    | 160,000€    | 158,000€        | 2,000€  |
| 7    | 210,000€    | 208,000€        | 2,000€  |
| 8    | 175,000€    | 180,000€        | -5,000€ |
| 9    | 195,000€    | 193,000€        | 2,000€  |
| 10   | 230,000€    | 225,000€        | 5,000€  |

**Resultados del modelo:**

- **MAE = 3,200€**
- **RMSE = 3,521€**
- **R² = 0.92**

---

### 📋 Interpretación:

**MAE = 3,200€**

- "En promedio, mis predicciones se desvían 3,200€ del precio real"
- En un mercado de casas de ~190,000€, un error de 3,200€ es apenas ~1.7%
- ✅ Bastante bueno

**RMSE = 3,521€**

- Un poco más alto que MAE (normal)
- Indica que hay algunos errores más grandes (las casas 2, 4, 8, 10)
- Pero no demasiado diferente del MAE → no hay outliers extremos

**R² = 0.92**

- El modelo explica 92% de la variabilidad en precios
- ⭐⭐⭐⭐⭐ Excelente modelo
- Solo 8% de la variabilidad no se explica

**Conclusión:** Este es un modelo MUY BUENO para predecir precios de casas.

---

## 🔍 CONCEPTOS ADICIONALES IMPORTANTES

### 1️⃣ Overfitting (Sobreajuste)

**¿Qué es?**
Cuando el modelo "memoriza" los datos de entrenamiento en lugar de aprender patrones generales.

**Analogía:**
Como estudiar SOLO los exámenes anteriores con sus respuestas exactas, pero no entender los conceptos. Cuando viene un examen con preguntas diferentes, fallas.

**Síntomas:**

```
Datos de entrenamiento: R² = 0.99 ⭐⭐⭐⭐⭐
Datos de prueba:        R² = 0.45 ⭐⭐

¡OVERFITTING! El modelo no generaliza bien.
```

**Solución:**

- Más datos de entrenamiento
- Modelo más simple
- Regularización (técnicas avanzadas)
- Validación cruzada

---

### 2️⃣ Underfitting (Subajuste)

**¿Qué es?**
Cuando el modelo es DEMASIADO simple y no captura los patrones de los datos.

**Analogía:**
Como intentar dibujar un círculo con solo una línea recta. No importa cómo la dibujes, nunca capturarás la forma.

**Síntomas:**

```
Datos de entrenamiento: R² = 0.40 ⭐⭐
Datos de prueba:        R² = 0.38 ⭐⭐

Mal en ambos → UNDERFITTING
```

**Solución:**

- Modelo más complejo
- Más features (características)
- Mejor ingeniería de features

---

### 3️⃣ El modelo ideal: Balance perfecto

**Lo que queremos:**

```
Datos de entrenamiento: R² = 0.88 ⭐⭐⭐⭐
Datos de prueba:        R² = 0.85 ⭐⭐⭐⭐

¡PERFECTO! Generaliza bien.
```

**Visual:**

```
     │
 R²  │     Underfitting │  Sweet Spot  │ Overfitting
     │                  │              │
1.0  │                  │     ⭐       │    •
     │                  │              │   /
0.8  │        •         │              │  •
     │       /          │     Train    │
0.6  │      •           │     Test     │
     │                  │              │
0.4  │                  │              │  Test
     │    Test=Train    │              │
     │                  │              │
     └──────────────────┴──────────────┴─────────→
          Muy simple   Complejidad   Muy complejo
```

---

### 4️⃣ Train/Test Split

**Concepto crucial:**
NO evalúes tu modelo con los MISMOS datos con los que entrenaste.

**Proceso correcto:**

```
Datos totales: 1000 ejemplos
    ↓
Split (división)
    ↓
├─ Train (80%): 800 ejemplos → Entrena el modelo
└─ Test (20%):  200 ejemplos → Evalúa el modelo
```

**¿Por qué?**

- Train: El modelo aprende de estos
- Test: Simula datos "nuevos" que el modelo nunca vio
- Evalúas cómo generaliza a datos nuevos

**Split típico:**

- 80/20 (80% train, 20% test)
- 70/30
- 60/20/20 (train/validation/test)

---

## ✅ TAREAS DE HOY (Martes)

### 1. Microsoft Learn (45 min)

**Módulos a completar:**

- **"Creación de modelos de regresión"**
- **"Entrenamiento y evaluación de modelos de regresión"**

Link: https://learn.microsoft.com/es-es/training/modules/train-evaluate-regression-models/

---

### 2. Ejercicio: Interpretar métricas (20 min)

**Para cada escenario, evalúa el modelo:**

**Escenario 1:**
Predecir temperatura diaria (rango: -5°C a 35°C)

- MAE = 0.8°C
- RMSE = 1.1°C
- R² = 0.94

¿Es un buen modelo? **\*\***\_\_\_**\*\***
¿Por qué? **\*\***\_\_\_**\*\***

---

**Escenario 2:**
Predecir precio de acciones (rango: $50 - $500)

- MAE = $45
- RMSE = $80
- R² = 0.35

¿Es un buen modelo? **\*\***\_\_\_**\*\***
¿Por qué? **\*\***\_\_\_**\*\***

---

**Escenario 3:**
Predecir días de hospitalización (rango: 1-30 días)

- MAE = 1.5 días
- RMSE = 2.8 días
- R² = 0.75

¿Es un buen modelo? **\*\***\_\_\_**\*\***
¿RMSE mucho mayor que MAE indica qué? **\*\***\_\_\_**\*\***

---

**Escenario 4:**
Modelo A vs Modelo B para predecir ventas:

Modelo A:

- MAE = 1,000 unidades
- RMSE = 1,200 unidades
- R² = 0.82

Modelo B:

- MAE = 1,200 unidades
- RMSE = 1,250 unidades
- R² = 0.85

¿Cuál elegirías y por qué? **\*\***\_\_\_**\*\***

---

**Escenario 5:**
Entrenaste un modelo para predecir ingresos anuales:

- Train R² = 0.98
- Test R² = 0.52

¿Qué problema tiene el modelo? **\*\***\_\_\_**\*\***
¿Cómo lo solucionarías? **\*\***\_\_\_**\*\***

---

### 3. Crea Flashcards (15 min)

**Crea estas 12 tarjetas:**

**Tarjeta 1:**

- Frente: "¿Qué mide MAE?"
- Atrás: "Error promedio en las mismas unidades que el objetivo. Fácil de interpretar."

**Tarjeta 2:**

- Frente: "¿Qué mide RMSE?"
- Atrás: "Error promedio pero penalizando errores grandes más. Siempre ≥ MAE."

**Tarjeta 3:**

- Frente: "¿Qué mide R²?"
- Atrás: "Qué porcentaje de la variabilidad de los datos explica el modelo. Rango: 0 a 1."

**Tarjeta 4:**

- Frente: "¿Cuál es mejor: MAE alto o bajo?"
- Atrás: "BAJO. MAE mide error, menor error = mejor modelo."

**Tarjeta 5:**

- Frente: "¿Cuál es mejor: R² alto o bajo?"
- Atrás: "ALTO. R² cerca de 1 = modelo explica casi toda la variabilidad."

**Tarjeta 6:**

- Frente: "¿Qué significa R² = 0.85?"
- Atrás: "El modelo explica 85% de la variabilidad en los datos. Modelo bueno/excelente."

**Tarjeta 7:**

- Frente: "¿Qué significa R² negativo?"
- Atrás: "El modelo es PEOR que simplemente predecir el promedio. Modelo muy malo."

**Tarjeta 8:**

- Frente: "¿Por qué RMSE > MAE?"
- Atrás: "RMSE penaliza errores grandes más al elevar al cuadrado. Si RMSE >> MAE, hay outliers."

**Tarjeta 9:**

- Frente: "¿Qué es overfitting?"
- Atrás: "Cuando el modelo memoriza datos de entrenamiento pero no generaliza bien a datos nuevos."

**Tarjeta 10:**

- Frente: "Síntoma de overfitting"
- Atrás: "Train R² muy alto (0.99) pero Test R² bajo (0.50). Gran diferencia entre train y test."

**Tarjeta 11:**

- Frente: "¿Qué es el train/test split?"
- Atrás: "Dividir datos en 2 grupos: uno para entrenar (80%) y otro para evaluar (20%) el modelo."

**Tarjeta 12:**

- Frente: "¿Por qué necesitamos test set?"
- Atrás: "Para evaluar cómo el modelo generaliza a datos que NUNCA vio durante entrenamiento."

---

## 📝 CONCEPTOS CLAVE DEL MARTES

**Memoriza:**

- MAE = error promedio (unidades originales)
- RMSE = error promedio penalizando grandes
- R² = porcentaje de variabilidad explicada (0 a 1)
- Menor MAE/RMSE = mejor
- Mayor R² = mejor (cerca de 1)
- Overfitting = memoriza, no generaliza
- Train/Test split es esencial

---

## ✅ CHECKLIST MARTES

- [ ] Entiendo qué es regresión en profundidad
- [ ] Sé qué miden MAE, RMSE y R²
- [ ] Puedo interpretar valores de métricas
- [ ] Entiendo overfitting vs underfitting
- [ ] Sé por qué necesitamos train/test split
- [ ] Completé el ejercicio de interpretar métricas
- [ ] Creé 12 flashcards nuevas
- [ ] Repasé flashcards del Lunes (5-10 min)
- [ ] Puedo explicar las métricas en voz alta

---

## 📚 RESPUESTAS AL EJERCICIO

**Escenario 1 (temperatura):**

- ¿Es bueno? **SÍ, excelente**
- Por qué: MAE de 0.8°C es muy preciso, R² de 0.94 es excelente. RMSE cercano a MAE = sin outliers.

**Escenario 2 (acciones):**

- ¿Es bueno? **NO, débil**
- Por qué: R² de 0.35 es bajo, explica solo 35% de variabilidad. MAE de $45 en rango $50-500 es alto. RMSE >> MAE indica errores grandes variables.

**Escenario 3 (hospitalización):**

- ¿Es bueno? **SÍ, moderado/bueno**
- Por qué: R² de 0.75 es bueno. MAE de 1.5 días es razonable.
- RMSE >> MAE indica: Hay algunos pacientes con errores de predicción grandes (outliers), quizás casos complicados.

**Escenario 4 (comparar modelos):**

- **Elegir: Modelo B**
- Por qué: Aunque tiene MAE ligeramente mayor, tiene R² mejor (0.85 vs 0.82) y RMSE mucho más cercano a MAE (errores más consistentes, menos outliers). Modelo B es más estable.

**Escenario 5 (overfitting):**

- Problema: **OVERFITTING**
- Train R² = 0.98 pero Test R² = 0.52 → Memoriza datos de entrenamiento
- Soluciones: Más datos, modelo más simple, regularización, menos features

---

## 🎊 ¡EXCELENTE TRABAJO EN EL MARTES!

**Lo que has logrado hoy:**

✅ **Dominas qué es regresión en profundidad**

- Cómo funciona la regresión lineal
- Objetivo: minimizar el error

✅ **Entiendes las 3 métricas clave**

- MAE: error promedio simple
- RMSE: error promedio penalizando grandes
- R²: variabilidad explicada

✅ **Sabes interpretar métricas**

- Qué valores son buenos/malos
- Cómo comparar modelos
- Qué significan los números

✅ **Conceptos avanzados**

- Overfitting y underfitting
- Train/test split
- Por qué necesitamos evaluación separada

---

## 📅 MAÑANA (Miércoles):

**Tema:** Clasificación y sus métricas

- Accuracy, Precision, Recall, F1-Score
- Matriz de confusión
- Cuándo usar cada métrica
- Diferencias con regresión

**Prepárate para:** Conceptos similares pero para categorías en vez de números

---

## 💡 DIFERENCIA CLAVE: Regresión vs Clasificación (preview)

**Regresión (HOY):**

- Predice: Números
- Métricas: MAE, RMSE, R²
- Pregunta: "¿Cuánto?"

**Clasificación (MAÑANA):**

- Predice: Categorías
- Métricas: Accuracy, Precision, Recall
- Pregunta: "¿Cuál?"

---

## 🎯 MINI QUIZ FINAL (5 min)

**Responde mentalmente (sin mirar):**

1. ¿Qué métrica te dice "en promedio me equivoco por X euros"?
2. ¿Qué métrica está entre 0 y 1 y sin unidades?
3. Si R² = 0.9, ¿es un modelo bueno o malo?
4. Si Train R² = 0.99 y Test R² = 0.45, ¿qué problema hay?
5. ¿Para qué sirve el test set?

**Respuestas:**

1. MAE
2. R²
3. Bueno/Excelente (explica 90%)
4. Overfitting
5. Para evaluar cómo generaliza el modelo a datos nuevos

**Si acertaste 4-5:** ¡Perfecto! Listo para mañana
**Si acertaste 2-3:** Repasa 10 min más
**Si acertaste 0-1:** Repasa la sección de métricas completa

---

## 📊 TABLA RESUMEN PARA IMPRIMIR

```
╔══════════════════════════════════════════════════════════╗
║         MÉTRICAS DE REGRESIÓN - CHEAT SHEET            ║
╠══════════════════════════════════════════════════════════╣
║ MAE (Mean Absolute Error)                               ║
║ • Qué mide: Error promedio                              ║
║ • Rango: 0 a ∞                                          ║
║ • Mejor: 0 (sin error)                                  ║
║ • Unidades: Mismas que objetivo                         ║
║ • Interpretación: "Me equivoco en promedio por X"      ║
╠══════════════════════════════════════════════════════════╣
║ RMSE (Root Mean Square Error)                           ║
║ • Qué mide: Error promedio (penaliza grandes)          ║
║ • Rango: 0 a ∞                                          ║
║ • Mejor: 0 (sin error)                                  ║
║ • Unidades: Mismas que objetivo                         ║
║ • Siempre ≥ MAE                                         ║
║ • Si RMSE >> MAE → hay outliers                         ║
╠══════════════════════════════════════════════════════════╣
║ R² (R-squared / Coeficiente de Determinación)          ║
║ • Qué mide: % de variabilidad explicada                ║
║ • Rango: -∞ a 1                                         ║
║ • Mejor: 1 (perfecto)                                   ║
║ • Sin unidades                                          ║
║ • R² = 0.85 → explica 85% de datos                     ║
║ • R² < 0 → modelo muy malo                              ║
╠══════════════════════════════════════════════════════════╣
║ VALORES DE REFERENCIA                                   ║
║ R² > 0.9    → ⭐⭐⭐⭐⭐ Excelente                       ║
║ R² 0.7-0.9  → ⭐⭐⭐⭐ Bueno                             ║
║ R² 0.5-0.7  → ⭐⭐⭐ Moderado                            ║
║ R² < 0.5    → ⭐⭐ Débil                                 ║
║ R² < 0      → 💀 Horrible                               ║
╠══════════════════════════════════════════════════════════╣
║ PROBLEMAS COMUNES                                       ║
║ Overfitting:  Train R² alto, Test R² bajo              ║
║ Underfitting: Train R² bajo, Test R² bajo              ║
║ Ideal:        Train R² ≈ Test R² (ambos altos)         ║
╠══════════════════════════════════════════════════════════╣
║ TRAIN/TEST SPLIT                                        ║
║ • Train 80% → Entrenar modelo                           ║
║ • Test 20%  → Evaluar modelo                            ║
║ • NUNCA evaluar con datos de entrenamiento             ║
╚══════════════════════════════════════════════════════════╝
```

---

## 🔗 CONEXIÓN CON AZURE MACHINE LEARNING

**En Azure ML, verás estas métricas:**

Cuando entrenas un modelo de regresión en Azure:

- AutoML muestra automáticamente: MAE, RMSE, R²
- Puedes comparar modelos por estas métricas
- Azure ML Designer también muestra estas métricas
- En la Semana 2 Sábado harás un lab y verás esto en práctica

**Preview del lab del sábado:**

```
Azure ML Output:
├── Primary Metric: R² = 0.87
├── Mean Absolute Error: 2,450
├── Root Mean Squared Error: 3,120
└── Explained Variance: 0.88

"Tu modelo explica 87% de la variabilidad
 con un error promedio de 2,450 unidades"
```

---

## 🎯 EJERCICIO BONUS (Opcional - 10 min)

**Si tienes tiempo extra, piensa en estos escenarios:**

**Escenario A:**
Trabajas para una empresa de seguros que predice costos médicos anuales de clientes (rango: $1,000 - $50,000).

Modelo actual:

- MAE = $3,500
- RMSE = $5,200
- R² = 0.72

**Preguntas:**

1. ¿Es aceptable un error promedio de $3,500?
2. ¿Qué te dice que RMSE sea mucho mayor que MAE?
3. ¿Cómo podrías mejorar el modelo?

---

**Escenario B:**
Predices tiempo de entrega de paquetes (rango: 1-10 días).

Modelo A: MAE = 0.5 días, R² = 0.65
Modelo B: MAE = 0.8 días, R² = 0.80

**Preguntas:**

1. ¿Qué modelo tiene predicciones más precisas?
2. ¿Qué modelo explica mejor la variabilidad?
3. ¿Cuál elegirías y por qué?

**Piensa en las respuestas. No hay una respuesta única, depende del contexto del negocio.**

---

## 📖 RECURSOS ADICIONALES (Opcional)

**Si quieres profundizar más:**

**Videos recomendados (YouTube):**

- "What is R-squared?" - StatQuest (inglés con subtítulos)
- "MAE vs RMSE" - explicaciones visuales
- "Regression metrics explained" - tutoriales cortos

**Microsoft Learn:**

- "Train and evaluate regression models"
- "Interpret machine learning models"

**Documentación Azure ML:**

- Cómo Azure ML calcula métricas
- Interpretación de resultados en Azure ML Studio

## 🎓 PARA EL EXAMEN - PREGUNTAS TÍPICAS

## Pregunta 1

**ES:** _Está_s construyendo un modelo para predecir el consumo energético de un edificio. ¿Qué tipo de problema de Machine Learning es este?_

**EN:** **You are building a model to predict the energy consumption of a building. What type of Machine Learning problem is this?**

**Opciones:**
A) Classification (Clasificación)  
B) Regression (Regresión)  
C) Clustering (Agrupamiento)  
D) Anomaly Detection (Detección de anomalías)

**Respuesta correcta:** B

**Explicación:**  
Predecir el consumo energético es un problema de **regresión** porque:

- La variable objetivo es **numérica continua** (kWh, watts)
- Puede tomar cualquier valor en un rango
- No son categorías discretas

Ejemplos similares de regresión:

- Predecir temperatura
- Predecir ventas
- Predecir precio de acciones

---

## Pregunta 2

**ES:** _¿Qué métrica de regresión penaliza más los errores grandes_

**EN:** _Which regression metric penalizes large errors more?_

**Opciones:**
A) MAE (Mean Absolute Error)  
B) RMSE (Root Mean Squared Error)  
C) R² (R-squared)  
D) MAPE (Mean Absolute Percentage Error)

**Respuesta correcta:** B

**Explicación:**  
**RMSE** (Root Mean Squared Error) penaliza más los errores grandes porque:

1. Eleva cada error al cuadrado (error²)
2. Los errores grandes se magnifican exponencialmente
3. Ejemplo: error de 10 → 100, error de 2 → 4

**MAE** trata todos los errores linealmente (sin elevar al cuadrado).

**Cuándo usar cada una:**

- **RMSE:** Cuando los errores grandes son muy costosos
- **MAE:** Cuando todos los errores tienen peso similar

---

## Pregunta 3

**ES:** T*u modelo de regresión tiene un R² de 0.92. ¿Qué significa esto*

**EN:** _Your regression model has an R² of 0.92. What does this mean?_

**Opciones:**
A) El modelo es 92% preciso  
B) El modelo explica el 92% de la varianza en los datos  
C) El modelo tiene un error del 8%  
D) El modelo está sobreajustado

**Respuesta correcta:** B

**Explicación:**  
**R² (Coeficiente de determinación)** indica qué porcentaje de la variabilidad de la variable objetivo es explicada por el modelo.

**R² = 0.92 significa:**

- ✅ El modelo explica el 92% de la varianza
- ✅ Solo el 8% queda sin explicar
- ✅ Generalmente es un muy buen modelo

**Rango de R²:**

- 1.0 = Perfecto (explica todo)
- 0.7-0.9 = Bueno
- 0.4-0.7 = Moderado
- <0.4 = Pobre
- Negativo = Peor que predecir la media

---

## Pregunta 4

**ES:** _¿Cuál es la diferencia entre MAE y RMSE?_

**EN:** _What is the difference between MAE and RMSE?_

**Opciones:**
A) MAE se usa para clasificación, RMSE para regresión  
B) MAE es la media de errores absolutos, RMSE es la raíz del error cuadrático medio  
C) No hay diferencia, son lo mismo  
D) MAE es siempre mayor que RMSE

**Respuesta correcta:** B

**Explicación:**

**MAE (Mean Absolute Error):**

```
MAE = (|error₁| + |error₂| + ... + |errorₙ|) / n
```

- Promedio de errores absolutos
- Todos los errores pesan igual
- Más intuitivo (mismas unidades que la variable)

**RMSE (Root Mean Squared Error):**

```
RMSE = √[(error₁² + error₂² + ... + errorₙ²) / n]
```

- Raíz del promedio de errores al cuadrado
- Penaliza más los errores grandes
- Más sensible a outliers

**RMSE ≥ MAE siempre** (debido al cuadrado)

---

## Pregunta 4

**ES:** _Estás evaluando un modelo de predicción de precios de casas. Tu RMSE es $50,000. ¿Qué significa esto en términos prácticos?_

**EN:** _You are evaluating a house price prediction model. Your RMSE is $50,000. What does this mean in practical terms?_

**Opciones:**
A) El modelo predice exactamente $50,000 por casa  
B) El modelo tiene un error promedio de aproximadamente $50,000 en sus predicciones  
C) El 50% de las predicciones tienen un error de $50,000  
D) El modelo es 50% preciso

**Respuesta correcta:** B

**Explicación:**  
RMSE representa el **error promedio típico** del modelo en las mismas unidades que la variable objetivo.

**RMSE = $50,000 significa:**

- En promedio, tus predicciones se desvían ~$50,000 del valor real
- Si predices una casa en $300,000, el valor real probablemente está entre $250,000-$350,000

**Para evaluar si es bueno o malo:**

- Depende del contexto (rango de precios)
- Si casas valen $200,000-$500,000 → RMSE aceptable
- Si casas valen $50,000-$100,000 → RMSE muy alto

---

## Pregunta 5

**ES:** _¿Cuál de estas afirmaciones sobre MAPE es correcta?_

**EN:** _Which of these statements about MAPE is correct?_

**Opciones:**
A) MAPE siempre es mejor que RMSE para evaluar modelos  
B) MAPE expresa el error como un porcentaje del valor real  
C) MAPE funciona bien cuando hay valores objetivo de cero  
D) MAPE y MAE son exactamente lo mismo

**Respuesta correcta:** B

**Explicación:**  
**MAPE (Mean Absolute Percentage Error)** expresa el error como porcentaje:

```
MAPE = (|error| / |valor_real|) × 100
```

**Ventajas:**

- ✅ Fácil de interpretar (%, sin unidades)
- ✅ Permite comparar modelos en diferentes escalas

**Desventajas:**

- ❌ NO funciona si hay valores reales = 0 (división por cero)
- ❌ Sesgo hacia subestimaciones
- ❌ Penaliza más errores en valores pequeños

**Ejemplo:**

- Valor real: 100, Predicción: 110 → Error: 10%
- Valor real: 1000, Predicción: 1100 → Error: 10%

---

## Pregunta 6

**ES:** _¿Qué indica un R² negativo en un modelo de regresión?_

**EN:** _What does a negative R² indicate in a regression model?_

**Opciones:**
A) El modelo es perfecto  
B) El modelo es peor que simplemente predecir la media de los datos  
C) Es un error de cálculo, R² no puede ser negativo  
D) El modelo tiene un 0% de precisión

**Respuesta correcta:** B

**Explicación:**  
**R² negativo** es posible (aunque raro) y significa:

- Tu modelo es **peor** que una predicción trivial (la media)
- El modelo está haciendo predicciones muy malas
- Probablemente hay un error fundamental en el modelo o los datos

**Interpretación de R²:**

- 1.0 = Perfecto
- 0.7-0.9 = Excelente
- 0.4-0.7 = Bueno
- 0.0-0.4 = Pobre
- 0.0 = Predecir la media (baseline)
- **Negativo = Peor que predecir la media** 🚨

Cuando ves R² negativo, necesitas revisar:

- Features seleccionadas
- Preprocesamiento de datos
- Tipo de modelo elegido
- Posibles errores en el código

---

## 💭 REFLEXIÓN FINAL DEL DÍA

**Antes de terminar, reflexiona 2 minutos:**

1. ¿Qué métrica te pareció más fácil de entender? ¿Por qué?
2. ¿Qué concepto te costó más? (para repasarlo mañana)
3. ¿Puedes pensar en un problema de tu trabajo/vida donde usarías regresión?

**Ejemplo de reflexión:**
"Entendí bien MAE porque es muy directo. R² me costó un poco pero ahora veo que es como un porcentaje de qué tan bien funciona el modelo. En mi trabajo podríamos usar regresión para predecir ventas mensuales..."

---

## 🎓 PREGUNTAS TIPO EXAMEN

### Pregunta 1:

_**Has entrenado un modelo de regresión para predecir ventas mensuales. El modelo tiene un R² de 0.85. ¿Qué significa esto?**_

A) El modelo se equivoca en promedio por 0.85 unidades
B) El modelo es 85% preciso
C) El modelo explica 85% de la variabilidad en las ventas ✅
D) El modelo tiene 85% de probabilidad de ser correcto

**Por qué C:** R² mide qué porcentaje de la variabilidad de los datos explica el modelo.

---

### Pregunta 2:

_Tienes dos modelos de regresión para predecir precios:_

_- Modelo A: MAE = 5,000€, RMSE = 5,200€_
_- Modelo B: MAE = 5,000€, RMSE = 8,000€_

_¿Qué puedes concluir?_

A) Ambos modelos son idénticos
B) Modelo B tiene errores más grandes y variables ✅
C) Modelo A es peor que Modelo B
D) No se puede determinar cuál es mejor

**Por qué B:** Si RMSE es mucho mayor que MAE, significa que hay errores grandes (outliers) que están siendo penalizados. Modelo B tiene RMSE mucho mayor = errores más variables.

---

### Pregunta 3:

_**¿Cuál de estas métricas de regresión penaliza MÁS los errores grandes?**_

A) MAE
B) RMSE ✅
C) R²
D) Todas por igual

**Por qué B:** RMSE eleva los errores al cuadrado antes de promediarlos, lo que penaliza errores grandes más que MAE.

---

### Pregunta 4:

_**Un modelo de regresión tiene R² = -0.2. ¿Qué significa esto?**_

A) El modelo es excelente
B) El modelo explica 20% de los datos
C) El modelo es peor que simplemente predecir el promedio ✅
D) Hay un error en el cálculo

**Por qué C:** R² negativo significa que el modelo es PEOR que un modelo básico que solo predice el promedio. Es un modelo muy malo.

---

### Pregunta 5:

_**¿Qué métrica de regresión está en las mismas unidades que la variable objetivo?**_

A) Solo MAE
B) Solo RMSE
C) MAE y RMSE ✅
D) R²

**Por qué C:** Tanto MAE como RMSE están en las mismas unidades que lo que predices (euros, metros, días). R² no tiene unidades.

---

## 🌙 ANTES DE DORMIR (5 min)

**Repaso relámpago:**

- Cierra los ojos
- Visualiza las 3 métricas: MAE, RMSE, R²
- Recuerda: MAE simple, RMSE penaliza grandes, R² es porcentaje
- Piensa en el ejemplo de precios de casas

**Repasa tus flashcards nuevas 1 vez**

**Duerme bien.** Tu cerebro consolidará todo esto mientras duermes. 😴

---

## 📊 PROGRESO SEMANA 2

```
Lunes:     ████████████████████ 100% ✅
Martes:    ████████████████████ 100% ✅
Miércoles: ░░░░░░░░░░░░░░░░░░░░   0%
Jueves:    ░░░░░░░░░░░░░░░░░░░░   0%
Viernes:   ░░░░░░░░░░░░░░░░░░░░   0%
Sábado:    ░░░░░░░░░░░░░░░░░░░░   0%
```

**Horas Semana 2:** 3/10 horas completadas (30%) ✅
**Progreso Total:** 13/60 horas (21.7%) 📈

---

**¡Nos vemos mañana Miércoles para Clasificación y sus métricas!** 🚀

**Mañana aprenderás:**

- Accuracy, Precision, Recall, F1-Score
- Matriz de confusión (confusion matrix)
- Verdaderos positivos, falsos negativos...
- Cuándo usar cada métrica de clasificación

**Será similar a hoy, pero para categorías en vez de números.** 💪
