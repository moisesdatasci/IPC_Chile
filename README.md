# 📈 Análisis de la Inflación en Chile: Una Radiografía de 100 Años (1928-2025)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg?logo=python&style=for-the-badge)
![Pandas](https://img.shields.io/badge/Pandas-Utilizado-orange.svg?logo=pandas&style=for-the-badge)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Usado-green.svg?logo=matplotlib&style=for-the-badge)
![Seaborn](https://img.shields.io/badge/Seaborn-Usado-purple.svg?logo=seaborn&style=for-the-badge)

Este repositorio contiene la **Fase 1 (Análisis y Visualización)** de un proyecto de ciencia de datos sobre la evolución histórica de la inflación en Chile. El análisis cubre casi un siglo de historia económica, desde 1928 hasta 2025.

El objetivo de esta fase es realizar un **Análisis Exploratorio de Datos (EDA)** profundo y una **descomposición de la serie temporal** para entender los patrones, tendencias y componentes estructurales del Índice de Precios al Consumidor (IPC) antes de proceder a cualquier modelado predictivo.

---

## 📊 Fuente de Datos

Los datos utilizados provienen de los indicadores diarios del **Banco Central de Chile**.
* **Archivo:** `Indicador.xls - Export.csv`
* **Indicador:** IPC General (Variación mensual c/r al período anterior)
* **Período:** 1928 al 2025

---

## ⚙️ Metodología de Análisis

El notebook sigue un proceso estructurado en 5 pasos clave para asegurar la calidad e interpretabilidad de los hallazgos.

### 1. Comprensión del Negocio y Objetivos
Definir el alcance del proyecto: "Comprender la evolución del IPC en Chile y sus características estadísticas".

### 2. Limpieza y Preparación de Datos
Esta fue una etapa crucial que incluyó:
* **Manejo de Encabezados:** Omitir las filas iniciales de metadatos del archivo `.csv`.
* **Renombrar Columnas:** De `Mes` y `Valor` a `Fecha_Excel` y `Variacion_IPC` para mayor claridad.
* **Conversión de Fechas:** Transformar el formato numérico de fecha serie de Excel a un objeto `datetime` estándar de Python.
* **Manejo de Nulos:** Asegurar la integridad de la serie temporal antes del análisis.

### 3. Análisis Exploratorio de Datos (EDA)
Una primera "conversación" con los datos para descubrir patrones visuales.
* Cálculo de estadísticas descriptivas (media, mediana, std, min, max).
* Visualización de la serie temporal completa para identificar anomalías.
* Análisis de la distribución con histogramas y boxplots.

### 4. Creación de Características (Feature Engineering)
Enriquecimiento de los datos para permitir análisis más profundos:
* Extracción de las columnas `Año` y `Mes` desde la `Fecha`.
* Cálculo de la **Inflación Anual Compuesta**, multiplicando los factores de crecimiento mensuales (`1 + IPC/100`) para obtener el valor real acumulado cada año.

### 5. Descomposición de Series Temporales
Se utilizó `statsmodels.tsa.seasonal_decompose` para diseccionar la serie en sus componentes fundamentales, usando un **modelo multiplicativo** (debido a que la volatilidad varía con la tendencia) y un **período de 12 meses** (para capturar el ciclo anual).

---

## 💡 Hallazgos y Visualizaciones Clave

Esta es la historia que nos cuentan los datos:

### Hallazgo 1: Las Tres Eras de la Inflación en Chile

El gráfico de la evolución histórica (`Observed`) muestra con claridad tres períodos económicos distintos. La volatilidad no es constante; la historia económica de Chile cambió radicalmente.

1.  **Estabilidad (1928-1970):** Variaciones mensuales bajas y controladas.
2.  **Hiperinflación (1970-1990):** Un período de volatilidad extrema, con variaciones **mensuales** que llegaron a superar el **+2000%**.
3.  **Estabilidad Moderna (1990-Hoy):** Una clara tendencia a la baja y un control de la inflación, que se estabiliza en niveles bajos.

> **¡Puedes insertar tu gráfico de descomposición aquí!**
> 
> `![Gráfico de Descomposición de la Serie Temporal](ruta/a/tu/graficos.PNG)`

### Hallazgo 2: La Anatomía Oculta de la Inflación

La descomposición de la serie nos permite ver sus "ingredientes" invisibles:

* **`Trend` (Tendencia):** Esta línea suavizada confirma la historia de las "Tres Eras". Muestra claramente el éxito de las políticas de control de inflación post-1990.
* **`Seasonal` (Estacionalidad):** ¡La inflación tiene un ritmo! Se confirma un patrón anual claro y repetitivo. Se observan picos recurrentes en ciertos meses (ej. marzo y septiembre), demostrando que la inflación tiene un ciclo estacional predecible.
* **`Residuals` (Residuos):** Muestra el "ruido" o caos. Es casi plano en los períodos de estabilidad, pero explota en los años 70-80. Esto nos dice que esos años no solo tuvieron una *tendencia* alta, sino que fueron *impredecibles* mes a mes.

### Hallazgo 3: Los Años Más Extremos

Mediante *Feature Engineering*, se calculó la inflación anual compuesta para identificar los años clave:

*(Aquí puedes añadir tus tablas o hallazgos sobre los 5 años de mayor/menor inflación)*

---

## 🛠️ Herramientas Utilizadas

* **Python 3.x**
* **Pandas:** Para la carga, limpieza y manipulación de datos (`DataFrame`).
* **Matplotlib:** Para la creación de los gráficos base.
* **Seaborn:** Para visualizaciones estadísticas más atractivas (histogramas, boxplots).
* **Statsmodels:** Para el análisis estadístico de series temporales (`seasonal_decompose`).

---

## 🚀 Próximos Pasos (Fase 2)

Este análisis exploratorio es la base fundamental. La siguiente fase de este proyecto (que no se incluye en este repositorio) se centrará en el **Modelado Predictivo**:

* **Pruebas de Estacionariedad** (Test de Dickey-Fuller) para preparar la serie.
* **Modelado ARIMA:** Construcción de un primer modelo para capturar la tendencia (`p, d, q`).
* **Modelado SARIMA:** Mejora del modelo para incluir la **Estacionalidad** que descubrimos en este análisis (`P, D, Q, s`).
