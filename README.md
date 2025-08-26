# Informe Técnico — Prueba DataKnow  
**Proyecto:** Estimación de costos de equipos para proyecto de construcción  

---

## 1. Explicación del caso
Una empresa del sector construcción planifica un proyecto de 36 meses y requiere estimar el costo base de dos equipos clave.  
Los equipos se valoran en función de las materias primas **X, Y, Z**:

- **Equipo 1** = 0.2·X + 0.8·Y  
- **Equipo 2** = (X + Y + Z) / 3  

El objetivo del análisis es calcular los costos históricos y proyectar los siguientes 36 meses para soportar la planificación financiera.

---

## 2. Supuestos
- Se trabaja con series históricas de precios de materias primas: `X_normalized.csv`, `Y_normalized.csv`, `Z_normalized.csv`.  
- Frecuencia de análisis: **mensual (MS)** → se calcula el **promedio mensual** de precios.  
- Faltantes tratados con **forward-fill y backward-fill** para evitar NaN.  
- Forecast a 36 meses usando **Exponential Smoothing (Holt)**, modelo sin estacionalidad.  

---

## 3. Formas para resolver el caso y opción tomada
### Opciones posibles
1. **Promedio histórico simple** 
2. **Modelos ARIMA/Prophet** 
3. **Exponential Smoothing (Holt)**
   
### Opción tomada
**Exponential Smoothing (Holt)**
- Los datos muestran tendencia. 
- Es un método interpretable y rápido de entrenar.  
- Adecuado para un horizonte 36 meses.  

---

## 4. Resultados del análisis de los datos y los modelos
- **Consolidado mensual:** X, Y, Z alineados a frecuencia mensual sin faltantes.  
- **Costos base históricos:** calculados para Equipo 1 y Equipo 2.  
- **Forecast materias primas:** proyección de 36 meses de X, Y, Z.  
- **Forecast equipos:** proyección de 36 meses de Equipo1 y Equipo2.  

### Principales métricas (36 meses)
*(ejemplo, resultados reales de `reports/costos_resumen_36m.csv`)*

| Equipo   | Costo total 36m | Promedio mensual | Máximo mensual | Mínimo mensual |
|----------|-----------------|------------------|----------------|----------------|
| Equipo 1 | 45,200          | 1,255            | 1,410          | 1,120          |
| Equipo 2 | 39,800          | 1,105            | 1,280          | 980            |

---

## 5. Futuros ajustes o mejoras
- Probar modelos adicionales (ARIMA, Prophet) y comparar métricas (MAPE, RMSE).  
- Implementar pipeline automatizado en **Azure/AWS** para actualizaciones periódicas.

---

## 6. Apreciaciones y comentarios del caso (opcional)
- El problema está bien planteado para evaluar manejo de datos, modelado y comunicación de resultados.  
- Documentar supuestos y limitaciones es clave para que el área de negocio confíe en los resultados.

---
