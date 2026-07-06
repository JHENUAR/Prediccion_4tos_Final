# ⚽ Predicción de Clasificados a Cuartos de Final – Mundial de Fútbol

---

## 📖 Descripción del Proyecto

Este proyecto desarrolla un sistema de predicción para determinar qué equipos avanzarán a los **cuartos de final** de un torneo mundial de fútbol, a partir de los partidos de **octavos de final**.

Para ello, se emplean técnicas de **aprendizaje supervisado**, combinando:

* **XGBoost (eXtreme Gradient Boosting)** como modelo de clasificación multiclase.
* **Simulación Monte Carlo** para estimar probabilidades robustas de clasificación.

El modelo se entrena con datos históricos de partidos internacionales (2021–2026) y se complementa con estadísticas actualizadas de equipos (ranking FIFA, valor de mercado, rendimiento reciente, entre otros).

Como resultado, se obtiene:

* La predicción de cada enfrentamiento de octavos.
* La probabilidad de que cada equipo alcance los cuartos de final.

---

## 🎯 Objetivo del Proyecto

* Predecir el ganador de cada partido de octavos de final mediante un modelo de clasificación.
* Estimar la probabilidad de clasificación a cuartos de final para cada equipo.
* Validar la robustez de las predicciones mediante simulación estocástica (Monte Carlo).
* Aplicar técnicas de:

  * Ingeniería de características
  * Ajuste de hiperparámetros
  * Evaluación de modelos

---

## 🧠 Metodología

### 1. Fuentes de Datos

* **datos_historicos.csv**: Más de 1000 partidos internacionales (2021–2026).
* **ranking_fifa.csv**: Puntuación histórica de selecciones.
* **transfermarkt.csv**: Valor de mercado de plantillas (millones de euros).
* **datos_mundial.csv**: Estadísticas del torneo actual.
* **Cruces_4tos.csv**: Enfrentamientos de octavos de final.

---

### 2. Construcción de Características

Para cada partido se generan variables diferenciales:

$$
\Delta f = f_{local} - f_{visitante}
$$

---
#### Variables derivadas

| Variable | Fórmula (texto) | Descripción |
|---|---|---|
| Ratio goles/posesión | `ratio_goles_posesion = goles_totales / (posesion + 0.01)` | Mide la efectividad ofensiva por unidad de posesión. |
| Ratio tarjetas/faltas | `ratio_tarjetas = tarjetas_amarillas / (faltas + 0.01)` | Indica la disciplina o agresividad del equipo. |
| Eficiencia de gol | `eficiencia_gol = goles_totales / (remates_a_puerta + 0.01)` | Porcentaje de remates que se convierten en gol. |
| Ratio córners/posesión | `ratio_corners = corners / (posesion + 0.01)` | Capacidad de generar peligro en ataque. |
> **Nota:** Se añade `+0.01` al denominador para evitar divisiones por cero y estabilizar las características.

### 3. Modelo XGBoost (Clasificación)

El modelo predice la variable objetivo:

$$
Y \in {0,1,2}
$$

Donde:

* 0 = victoria visitante
* 1 = empate
* 2 = victoria local

---

#### 3.1 Función de Pérdida

Se minimiza la entropía cruzada con regularización:

$$
L = \sum_{i=1}^{N} -\log \big(P(Y = y_i \mid x_i)\big) + \sum_{t=1}^{T} \Omega(f_t)
$$

Con:

$$
\Omega(f) = \gamma \cdot \text{hojas} + \frac{1}{2} \lambda \sum_{j=1}^{J} w_j^2
$$

---

#### 3.2 Salida del Modelo

Probabilidades mediante **softmax**:

$$
P(Y = k \mid x) = \frac{e^{s_k(x)}}{\sum_{k'=0}^{2} e^{s_{k'}(x)}}
$$

Predicción final:

$$
\hat{y}(x) = \arg\max_k P(Y = k \mid x)
$$

---

#### 3.3 Ajuste de Hiperparámetros

Se emplea **RandomizedSearchCV** con validación cruzada estratificada.

Parámetros optimizados:

* `n_estimators`: 200, 300
* `max_depth`: 6, 8, 10
* `learning_rate`: 0.03, 0.05, 0.07
* `subsample`: 0.7, 0.8, 0.9
* `colsample_bytree`: 0.7, 0.8, 0.9

---

### 4. Simulación Monte Carlo

Se simulan **1000 torneos completos**.

Modelo de goles:

$$
G_{local} \sim \text{Poisson}(\lambda_{local}), \quad
G_{visitante} \sim \text{Poisson}(\lambda_{visitante})
$$

Parámetros:

$$
\lambda_{local} = \max \left(0.1,\ \bar{g}_{local} + 1.5 \cdot P(Y=2) \right)
$$

$$
\lambda_{visitante} = \max \left(0.1,\ \bar{g}_{visitante} + 1.5 \cdot P(Y=0) \right)
$$

---

#### Resolución por penales

$$
P_{penal_local} = \text{clip} \left(0.5 + \frac{FIFA_{local} - FIFA_{visitante}}{2000},\ 0.2,\ 0.8 \right)
$$

La frecuencia de clasificación en las simulaciones define la probabilidad final.

---

## 5. Evaluación del modelo

### Precisión (Accuracy)

$$ \text{Accuracy} = \frac{1}{N} \sum_{i=1}^{N} \mathbf{1}\left(\hat{y}_i = y_i\right) $$

### Pérdida logarítmica (Log‑Loss)

$$ \text{LogLoss} = -\frac{1}{N} \sum_{i=1}^{N} \log\left(P(Y = y_i \mid \mathbf{x}_i)\right) $$

## 📂 Estructura del Repositorio

```
├── 📁 01_Scraping
├── 📁 02_Limpieza_Datos
├── 📁 03_Modelo_Simulacion
├── 📁 04_Web
├── 📁 Data
│    ├── 📄 Cruces_4tos.csv
│    ├── 📄 Grupos_Mundial.csv
│    ├── 📄 partidos_mundial.csv
│    ├── 📄 ranking_fifa.csv
│    ├── 📄 transfermarkt.csv
│    └──  ...
├── 📁 Modelo_XGBoost_4tos/
│   ├── 📄 Resultados_Equipos_Clasificados_4tos
    ├── 📄 Codigo_Modelo_XGBoost.py
    ├── 📄 Calculos_Modelo_XGBoost
│   └── 📄 Descripcion_Modelo_XGBoost
├── 📄 Observaciones_Modelo_XGBoost
└── 📄 README.md
```

---

## ⚙️ Instalación y Uso

### Requisitos

* Python 3.8+
* pandas, numpy, xgboost, scikit-learn, joblib

### Instalación

```bash
git clone https://github.com/JHENUAR/Prediccion_4tos_Final.git
cd Prediccion_4tos_Final
pip install -r requirements.txt
```

### Ejecución

```bash
python Codigo_Modelo_XGBoost.py
```

---

## 📊 Ejemplo de Resultados

### Predicción de octavos

| Local  | Visitante  | Prob Local | Prob Empate | Prob Visitante | xG Local | xG Visitante | Ganador |
| ------ | ---------- | ---------- | ----------- | -------------- | -------- | ------------ | ------- |
| España | Cabo Verde | 0.78       | 0.15        | 0.07           | 2.45     | 0.62         | España  |

---

### Probabilidad de clasificación

| Equipo | Probabilidad |
| ------ | ------------ |
| España | 0.92         |
| Brasil | 0.78         |

---

## 📈 Evaluación del Modelo

* Accuracy: ~68%
* Log-Loss: 0.85

Este rendimiento es consistente con modelos predictivos en fútbol (65%–70%).

---

## 🔬 Conclusiones

* XGBoost captura patrones complejos en datos futbolísticos.
* Monte Carlo aporta robustez frente a la incertidumbre.
* El modelo distingue entre favoritos claros y partidos equilibrados.
* Metodología replicable a otros torneos.

---

## 📚 Referencias

* Chen, T., & Guestrin, C. (2016). *XGBoost: A Scalable Tree Boosting System*.
* Friedman, J. H. (2001). *Gradient Boosting Machine*.
* Kuhn, M., & Johnson, K. (2013). *Applied Predictive Modeling*.
* Datos: Football-Data.org, Transfermarkt.
