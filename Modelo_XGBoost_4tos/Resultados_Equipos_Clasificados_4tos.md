## RESULTADOS EQUIPOS CLASIFICADOS A CUARTOS - MUNDIAL 2026
```text
rive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).

🏆 PREDICCIÓN DE CLASIFICADOS A CUARTOS DE FINAL (MODELO OPTIMIZADO)
================================================================================

✅ Archivos cargados correctamente.
✅ Nombres normalizados.
⚠️ Equipos sin estadísticas: ['EE. UU.']. Se añadirán con valores por defecto.
📊 Estadísticas de equipos listas con características mejoradas.
🔄 Cargando modelo y scaler guardados...
✅ Modelo y scaler cargados correctamente.
✅ Modelo XGBoost listo.

================================================================================
📊 PREDICCIONES - OCTAVOS DE FINAL (basadas en probabilidades)
================================================================================

📋 TABLA DE PREDICCIONES - OCTAVOS
    Local  Visitante  Prob_Local  Prob_Empate  Prob_Visitante  xG_Local  xG_Visitante    Ganador
   Canadá  Marruecos       0.089        0.137           0.775      1.24          2.73  Marruecos
 Paraguay    Francia       0.239        0.203           0.558      0.56          2.16    Francia
   Brasil    Noruega       0.809        0.150           0.040      1.94          1.82     Brasil
   México Inglaterra       0.266        0.381           0.353      1.18          2.24 Inglaterra
  EE. UU.    Bélgica       0.066        0.053           0.881      0.00          2.60    Bélgica
 Portugal     España       0.128        0.453           0.419      2.02          2.21     España
Argentina     Egipto       0.797        0.127           0.076      1.90          1.34  Argentina
    Suiza   Colombia       0.291        0.482           0.226      1.54          1.29      Suiza


🎯 CLASIFICADOS A CUARTOS DE FINAL (según el modelo)
 1. Marruecos
 2. Francia
 3. Brasil
 4. Inglaterra
 5. Bélgica
 6. España
 7. Argentina
 8. Suiza

🔄 Calculando porcentajes de clasificación a cuartos (1000 iteraciones Monte Carlo)...

📊 PORCENTAJES DE CLASIFICACIÓN A CUARTOS (Monte Carlo)
    Equipo  Prob_Clasificacion_Cuartos
   Bélgica                    0.123875
   Francia                    0.105625
 Marruecos                    0.101250
 Argentina                    0.092375
Inglaterra                    0.092000
    Brasil                    0.080875
    España                    0.073500
     Suiza                    0.069000
  Colombia                    0.056000
  Portugal                    0.051500
   Noruega                    0.044125
    México                    0.033000
    Egipto                    0.032625
    Canadá                    0.023750
  Paraguay                    0.019375
   EE. UU.                    0.001125

================================================================================
RESULTADOS FINALES - CLASIFICADOS A CUARTOS DE FINAL
================================================================================

📌 CLASIFICADOS (por probabilidades)
 Posición     Equipo
        1  Marruecos
        2    Francia
        3     Brasil
        4 Inglaterra
        5    Bélgica
        6     España
        7  Argentina
        8      Suiza

📌 TABLA DE PARTIDOS CON PROBABILIDADES Y xG
    Local  Visitante  Prob_Local  Prob_Empate  Prob_Visitante  xG_Local  xG_Visitante    Ganador
   Canadá  Marruecos       0.089        0.137           0.775      1.24          2.73  Marruecos
 Paraguay    Francia       0.239        0.203           0.558      0.56          2.16    Francia
   Brasil    Noruega       0.809        0.150           0.040      1.94          1.82     Brasil
   México Inglaterra       0.266        0.381           0.353      1.18          2.24 Inglaterra
  EE. UU.    Bélgica       0.066        0.053           0.881      0.00          2.60    Bélgica
 Portugal     España       0.128        0.453           0.419      2.02          2.21     España
Argentina     Egipto       0.797        0.127           0.076      1.90          1.34  Argentina
    Suiza   Colombia       0.291        0.482           0.226      1.54          1.29      Suiza

📌 PROBABILIDADES DE CLASIFICACIÓN A CUARTOS (Monte Carlo)
    Equipo  Prob_Clasificacion_Cuartos
   Bélgica                    0.123875
   Francia                    0.105625
 Marruecos                    0.101250
 Argentina                    0.092375
Inglaterra                    0.092000
    Brasil                    0.080875
    España                    0.073500
     Suiza                    0.069000
  Colombia                    0.056000
  Portugal                    0.051500
   Noruega                    0.044125
    México                    0.033000
    Egipto                    0.032625
    Canadá                    0.023750
  Paraguay                    0.019375
   EE. UU.                    0.001125

✅ Análisis completado.
   - Modelo: XGBoost con ajuste de hiperparámetros (RandomizedSearchCV)
   - Características mejoradas con variables derivadas
   - Decisión basada en la probabilidad más alta
   - Validación cruzada para estimar precisión realista
   - Simulación Monte Carlo: 1000 iteraciones para robustez (ajustable)
   - Modelo guardado para reutilización en futuras ejecuciones

⚠️ Nota: La precisión máxima realista en fútbol es ~66-70%. El modelo está optimizado para ese rango.
```
