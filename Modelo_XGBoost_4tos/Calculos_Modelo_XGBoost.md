# 🧠 Predicción de Clasificación a Cuartos de Final mediante Machine Learning

## 📌 Introducción

Este proyecto desarrolla un sistema predictivo para estimar qué equipos clasificarán a cuartos de final en una competición de fútbol, utilizando técnicas de **aprendizaje supervisado** mediante **XGBoost (eXtreme Gradient Boosting)** y una **simulación Monte Carlo** para modelar la incertidumbre inherente al deporte.

El sistema combina datos estadísticos, ingeniería de características y modelos probabilísticos para estimar resultados de partidos y probabilidades de clasificación.

---

## 🎯 Planteamiento del Problema

Sea un partido entre un equipo local ( i ) y un equipo visitante ( j ). Se define la variable objetivo:

$$
Y \in {0, 1, 2}
$$

donde:

* ( Y = 0 ): gana el visitante
* ( Y = 1 ): empate
* ( Y = 2 ): gana el local

El modelo estima la probabilidad condicional:

$$
P(Y = k \mid \mathbf{x}_{ij}), \quad k \in {0,1,2}
$$

donde ( \mathbf{x}_{ij} \in \mathbb{R}^d ) es el vector de características del partido.

---

## 📊 Representación Matemática de las Características

Cada partido se representa como la diferencia entre características del equipo local y visitante:

$$
\mathbf{x}_{ij} = \mathbf{x}_i - \mathbf{x}_j
$$

o componente a componente:

$$
x_m = f_{local,m} - f_{visitante,m}
$$

donde las variables incluyen:

* ranking FIFA
* valor de mercado
* goles promedio
* posesión
* remates a puerta
* córneres
* tarjetas
* faltas
* pases completados

---

## ⚙️ Ingeniería de Características

Se generan variables derivadas para capturar relaciones no lineales:

$$
\text{ratio}_{gp} = \frac{g}{\text{pos} + \epsilon}
$$

$$
\text{ratio}*{tarj} = \frac{t*{amarillas}}{faltas + \epsilon}
$$

$$
\text{eficiencia}_{gol} = \frac{g}{remates_puerta + \epsilon}
$$

$$
\text{ratio}_{corners} = \frac{corners}{\text{pos} + \epsilon}
$$

donde ( \epsilon = 0.01 ) evita divisiones por cero.

---

## 📏 Normalización de Variables

Se aplica estandarización tipo Z-score:

$$
z = \frac{x - \mu}{\sigma}
$$

donde:

* ( \mu ): media
* ( \sigma ): desviación estándar

Esto garantiza que todas las variables tengan media 0 y varianza 1.

---

## 🌳 Modelo XGBoost (Clasificación Multiclase)

El modelo predice probabilidades mediante la función softmax:

$$
P(Y = k \mid \mathbf{x}) = \frac{e^{s_k(\mathbf{x})}}{\sum_{k'=0}^{2} e^{s_{k'}(\mathbf{x})}}
$$

La predicción final es:

$$
\hat{y} = \arg\max_k P(Y = k \mid \mathbf{x})
$$

---

## ⚡ Función Objetivo

El modelo minimiza:

$$
\mathcal{L} = \sum_{i=1}^{N} \ell(y_i, \hat{y}*i) + \sum*{t=1}^{T} \Omega(f_t)
$$

donde la pérdida logarítmica es:

$$
\ell(y_i, \hat{y}_i) = -\log P(Y = y_i \mid \mathbf{x}_i)
$$

y la regularización:

$$
\Omega(f) = \gamma T + \frac{1}{2} \lambda \sum_{j=1}^{J} w_j^2
$$

---

## 🔁 Construcción del Modelo (Boosting)

El modelo se construye como:

$$
\hat{y}*i^{(t)} = \sum*{k=1}^{t} f_k(\mathbf{x}_i)
$$

En cada iteración se minimiza:

$$
\mathcal{L}^{(t)} \approx \sum_{i=1}^{N} \left[ g_i f_t(\mathbf{x}_i) + \frac{1}{2} h_i f_t(\mathbf{x}_i)^2 \right] + \Omega(f_t)
$$

donde:

* ( g_i ): gradiente
* ( h_i ): hessiano

---

## 📈 Evaluación del Modelo

### Accuracy

$$
\text{Accuracy} = \frac{1}{N} \sum_{i=1}^{N} \mathbb{I}(\hat{y}_i = y_i)
$$

### Log Loss

$$
\text{LogLoss} = -\frac{1}{N} \sum_{i=1}^{N} \log P(Y = y_i \mid \mathbf{x}_i)
$$

---

## 🎲 Simulación Monte Carlo (Clasificación a Cuartos)

Para estimar qué equipos avanzan a cuartos de final, se realizan ( N_{sim} = 1000 ) simulaciones.

### Modelado de goles (Poisson)

$$
G_h \sim \text{Poisson}(\lambda_h), \quad G_a \sim \text{Poisson}(\lambda_a)
$$

donde:

$$
\lambda_h = \max(0.1, \bar{g}_h + \alpha \cdot P(Y=2 \mid \mathbf{x}))
$$

$$
\lambda_a = \max(0.1, \bar{g}_a + \alpha \cdot P(Y=0 \mid \mathbf{x}))
$$

con ( \alpha = 1.5 ).

---

## ⚽ Resolución de Empates (Penales)

Si ( G_h = G_a ), el ganador se decide con:

$$
P_{penal} = \text{clip} \left( 0.5 + \frac{R_h - R_a}{2000}, , 0.2, , 0.8 \right)
$$

---

## 🏆 Probabilidad de Clasificación

La probabilidad de avanzar a cuartos se calcula como:

$$
P(\text{clasificación}) = \frac{1}{N_{sim}} \sum_{s=1}^{N_{sim}} \mathbb{I}(\text{equipo clasifica en simulación } s)
$$

---

## 🔄 Flujo del Sistema

1. Preprocesamiento de datos
2. Construcción del dataset
3. Ingeniería de características
4. Normalización
5. Entrenamiento con XGBoost
6. Predicción de partidos
7. Simulación Monte Carlo
8. Estimación de clasificados

---

## 📌 Conclusión

El sistema combina modelos de aprendizaje supervisado con simulaciones probabilísticas para estimar resultados de partidos y clasificaciones. Matemáticamente, integra:

* Modelos de probabilidad condicional
* Optimización basada en gradientes
* Distribuciones de Poisson
* Simulación Monte Carlo

Esto permite obtener estimaciones robustas en un entorno altamente incierto como el fútbol.

---

## 📚 Referencias

* Chen, T., & Guestrin, C. (2016). *XGBoost: A Scalable Tree Boosting System*.
* Friedman, J. (2001). *Gradient Boosting Machine*.
* Kuhn, M., & Johnson, K. (2013). *Applied Predictive Modeling*.
