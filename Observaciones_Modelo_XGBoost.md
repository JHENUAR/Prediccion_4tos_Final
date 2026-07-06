## 🔍 Observaciones del Modelo y Limitaciones

### 📌 Dependencia de la calidad de los datos

Las predicciones generadas por el modelo dependen directamente de la **calidad, cantidad y actualidad de los datos utilizados**. Si los datos históricos no reflejan el estado actual de los equipos (lesiones, cambios tácticos, rendimiento reciente), la precisión del modelo puede verse afectada.

> **Nota:** Las predicciones deben interpretarse como estimaciones basadas en la información disponible, no como resultados deterministas.

---

### 📌 Naturaleza estocástica del fútbol

El fútbol es un deporte altamente impredecible. Factores como expulsiones, errores arbitrales o eventos fortuitos no pueden ser modelados completamente, lo que limita la capacidad predictiva del sistema.

En la práctica, incluso modelos avanzados suelen alcanzar una precisión máxima aproximada de **65%–70%**.

---

### 📌 Limitaciones del modelo XGBoost

Si bien XGBoost permite capturar relaciones no lineales entre variables, presenta algunas limitaciones:

* No modela explícitamente la **dinámica temporal** (forma reciente vs histórica).
* No captura dependencias secuenciales entre partidos.
* Su interpretabilidad es limitada sin herramientas adicionales.

---

### 📌 Simplificación en la simulación Monte Carlo

La simulación utiliza una distribución de Poisson para modelar los goles:

* Es una aproximación estándar en análisis deportivo.
* Sin embargo, **simplifica la realidad**, ya que no considera correlación entre equipos ni contexto del partido.

---

### 📌 Variables no incluidas

El modelo puede mejorarse incorporando variables adicionales como:

* Forma reciente (últimos partidos)
* Lesiones o ausencias clave
* Ventaja de localía real
* Importancia del partido (fase eliminatoria)
* Métricas avanzadas (expected goals reales, presión, etc.)

---

### 📌 Validación y generalización

El modelo ha sido validado mediante **validación cruzada**, lo cual permite estimar su desempeño de forma robusta. Sin embargo:

* Está entrenado con datos del periodo **2021–2026**.
* Puede requerir reentrenamiento para futuros torneos o contextos diferentes.

---

## 🚀 Trabajo Futuro

Para mejorar el rendimiento y robustez del modelo, se proponen las siguientes líneas de trabajo:

* Incorporación de modelos de series temporales (LSTM, modelos bayesianos).
* Uso de distribuciones más complejas (Poisson bivariante).
* Implementación de técnicas de interpretabilidad (SHAP values).
* Inclusión de nuevas variables contextuales y métricas avanzadas.
* Evaluación con datos reales del torneo para validar predicciones.

---

> ⚠️ **Conclusión:** Este modelo proporciona una aproximación probabilística basada en datos históricos. Sus resultados deben interpretarse como apoyo al análisis y no como predicciones exactas del resultado real.
