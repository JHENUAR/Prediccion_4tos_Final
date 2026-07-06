# ⚽ Predicción de Clasificados a Cuartos de Final – Mundial de Fútbol

---

## 📖 Descripción del Proyecto

Este proyecto desarrolla un sistema de predicción para determinar qué equipos avanzarán a los **cuartos de final** de un torneo mundial de fútbol a partir de los partidos de octavos de final. Para ello, se emplean técnicas de **aprendizaje supervisado**, combinando:

* **XGBoost** (eXtreme Gradient Boosting) como modelo de clasificación multiclase.
* **Simulación Monte Carlo** para estimar probabilidades robustas de clasificación.

El modelo se entrena con datos históricos de partidos internacionales (desde 2021 hasta 2026) y se complementa con estadísticas actualizadas de equipos (ranking FIFA, valor de mercado, rendimiento reciente, etc.). El resultado es una predicción de cada enfrentamiento de octavos, junto con la probabilidad de que cada equipo alcance los cuartos de final.

---

## 🗂️ Datos Utilizados

Todos los datos necesarios se encuentran en la carpeta `Data/` dentro de este repositorio. Los archivos son los siguientes:

| Archivo                | Descripción                                                                                                                       |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `Cruces_4tos.csv`      | Enfrentamientos de octavos de final (equipo local, visitante, fecha, estadio).                                                    |
| `datos_historicos.csv` | Historial de más de 1000 partidos internacionales (2021–2026) con variables como goles, posesión, remates, tarjetas, faltas, etc. |
| `datos_mundial.csv`    | Estadísticas de rendimiento de cada equipo en el torneo actual (promedios por partido).                                           |
| `ranking_fifa.csv`     | Puntuaciones FIFA de cada selección en distintas fechas (se usa la más reciente).                                                 |
| `transfermarkt.csv`    | Valor de mercado de la plantilla de cada equipo en millones de euros.                                                             |
| `partidos_mundial.csv` | Calendario completo de la fase de grupos (contexto).                                                                              |
| `Grupos_Mundial.csv`   | Composición de los grupos.                                                                                                        |

> **Nota:** Los datos provienen de fuentes públicas (Football-Data.org, Transfermarkt, FIFA). Si deseas usar tus propios datos, mantén la misma estructura.

---

## ⚙️ Instalación y Configuración

### Requisitos previos

* Python 3.8 o superior
* `pip`

### 1. Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/mundial-prediccion-cuartos.git
cd mundial-prediccion-cuartos
```

### 2. Crear entorno virtual (opcional)

```bash
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

O manualmente:

```bash
pip install pandas numpy xgboost scikit-learn joblib
```

### 📄 requirements.txt

```text
pandas>=1.3.0
numpy>=1.21.0
xgboost>=1.5.0
scikit-learn>=1.0.0
joblib>=1.1.0
```

---

## 🚀 Ejecución del Modelo

```bash
python prediccion_cuartos.py
```

### ¿Qué ocurre al ejecutarlo?

* **Carga de datos:** lectura de archivos CSV
* **Preprocesamiento:** limpieza y normalización
* **Feature engineering:** diferencias y ratios
* **Entrenamiento XGBoost:** con o sin modelo previo
* **Predicción:** probabilidades y xG
* **Monte Carlo:** 1000 simulaciones
* **Salida:** resultados en consola

---

## 📊 Ejemplo de Resultados

### Predicción de octavos

| Local  | Visitante  | Prob Local | Prob Empate | Prob Visitante | xG Local | xG Visitante | Ganador |
| ------ | ---------- | ---------- | ----------- | -------------- | -------- | ------------ | ------- |
| España | Cabo Verde | 0.78       | 0.15        | 0.07           | 2.45     | 0.62         | España  |
| Brasil | Marruecos  | 0.55       | 0.28        | 0.17           | 1.83     | 1.21         | Brasil  |

---

### Probabilidades de clasificación

| Equipo       | Prob. Clasificación |
| ------------ | ------------------- |
| España       | 0.92                |
| Países Bajos | 0.85                |
| Brasil       | 0.78                |

---

## 🔬 Metodología (resumen)

El modelo utiliza **XGBoost** para clasificación multiclase (local, empate, visitante). Se emplean variables diferenciales y ratios de eficiencia.

La función de pérdida es **entropía cruzada con regularización L2**.

Para estimar probabilidades robustas, se aplica una **simulación Monte Carlo** con 1000 iteraciones, modelando los goles mediante una distribución de Poisson dependiente del modelo y del promedio histórico.

---

## 📈 Evaluación del Modelo

* Accuracy: ~68%
* Log-Loss: 0.85

Resultados consistentes con modelos de predicción futbolística.

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Puedes abrir un issue o pull request.

---

## 📚 Referencias

* Chen, T., & Guestrin, C. (2016). *XGBoost: A Scalable Tree Boosting System*.
* Friedman, J. H. (2001). *Gradient Boosting Machine*.
* Football-Data.org
* Transfermarkt
