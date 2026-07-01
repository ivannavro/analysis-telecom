# ConnectaTel Customer Analysis
Este repositorio contiene el análisis de comportamiento de clientes realizado para **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica. El objetivo es evaluar patrones de uso, calidad de datos y segmentación de clientes con base en información registrada hasta el año 2024.

## 🧠 Objetivo del análisis

- Explorar, limpiar y validar la calidad de los datos de planes, clientes y uso de servicios.
- Construir un perfil estadístico consolidado por usuario (`user_profile`) a partir de múltiples fuentes.
- Analizar distribuciones de uso (llamadas, mensajes, duración) y edad, identificando diferencias por tipo de plan.
- Detectar y evaluar valores atípicos (outliers) mediante el método IQR.
- Segmentar a los clientes por **nivel de uso** y por **edad** para identificar patrones de comportamiento.
- Generar un insight ejecutivo con recomendaciones accionables para la oferta de planes de ConnectaTel.

## 📊 Datasets utilizados

| Archivo | Filas | Descripción |
|---|---|---|
| `plans.csv` | 2 | Información de los planes actuales (Básico y Premium): precio mensual, minutos y mensajes incluidos, GB incluidos y costos por excedente. |
| `users_latam.csv` | 4,000 | Información de los clientes: edad, ciudad, fecha de registro, plan contratado y fecha de cancelación (churn). |
| `usage.csv` | 40,000 | Detalle del uso real de los servicios por cliente: tipo de evento (llamada o mensaje), fecha, duración de llamada y longitud de mensaje. |

## 📂 Contenido del repositorio

- `Project-ConnectaTel.ipynb`
  → Notebook principal con limpieza de datos, EDA, visualización de distribuciones, detección de outliers, segmentación de clientes e insight ejecutivo.
- `README.md`
  → Este documento.

## 🧩 Etapas del análisis realizadas

1. **Carga y exploración inicial** — lectura de los tres datasets y revisión de estructura, dimensiones y tipos de datos (`.shape`, `.info()`).
2. **Identificación de problemas de calidad de datos**
   - Conteo y proporción de valores nulos por columna.
   - Detección de valores *sentinel* inválidos (ej. `age = -999`, `city = "?"`).
   - Revisión y estandarización de fechas, identificando registros con años imposibles (ej. 2026).
3. **Limpieza básica de datos**
   - Corrección de sentinels (imputación con mediana en `age`, conversión a nulo en `city`).
   - Marcado de fechas fuera de rango como valores nulos.
   - Validación de nulos estructurales (MAR) en `duration` y `length`, dependientes del tipo de evento (`call`/`text`).
4. **Construcción de `user_profile`** — agregación de `usage` por usuario (total de mensajes, llamadas y minutos) y combinación con los datos de `users`.
5. **Visualización de distribuciones y outliers**
   - Histogramas de edad, mensajes, llamadas y duración de llamada, segmentados por tipo de plan (`hue='plan'`).
   - Boxplots para identificar outliers y cálculo de límites mediante el método IQR.
6. **Segmentación de clientes**
   - Clasificación por nivel de uso (`grupo_uso`: Bajo, Medio, Alto).
   - Clasificación por edad (`grupo_edad`: Joven, Adulto, Senior).
   - Visualización de ambas segmentaciones mediante gráficos de conteo.
7. **Insight ejecutivo para stakeholders** — conclusiones sobre calidad de datos, segmentos de valor, patrones de uso extremo y recomendaciones de negocio para la oferta de planes.

## ▶ Cómo abrir el notebook en Google Colab

Haz clic en el siguiente botón:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ivannavro/analysis-telecom/blob/main/Project-ConnectaTel.ipynb)

O manualmente:
1. Abre el archivo `.ipynb` en GitHub.
2. Haz clic en **Open in Colab**.

## 📘 Cómo reproducir el análisis

1. Abre `Project-ConnectaTel.ipynb` en Google Colab o Jupyter.
2. Asegúrate de tener disponibles los tres archivos fuente (`plans.csv`, `users_latam.csv`, `usage.csv`) en la ruta `/datasets/`, o ajusta las rutas de carga en el notebook si los ubicas en otro lugar (por ejemplo, subiéndolos manualmente en Colab).
3. Ejecuta las celdas **en orden**, de principio a fin — el notebook depende de que cada etapa (limpieza → agregación → segmentación) se ejecute secuencialmente.
4. Las librerías requeridas son `pandas`, `numpy`, `seaborn` y `matplotlib`. Si trabajas fuera de Colab, instálalas con:
   ```bash
   pip install pandas numpy seaborn matplotlib
   ```
5. Al finalizar, la sección **Paso 7: Insight Ejecutivo** contiene las conclusiones y recomendaciones finales del análisis.

---

📎 Link al repositorio público del proyecto: [github.com/ivannavro/analysis-telecom](https://github.com/ivannavro/analysis-telecom)
