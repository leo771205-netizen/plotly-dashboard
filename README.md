# README del Proyecto de Análisis de Ventas y Marketing

## 📊 Visión General del Proyecto

Este proyecto se enfoca en un análisis exhaustivo de datos de ventas, clientes y marketing para identificar patrones, evaluar el rendimiento de campañas de Redes Sociales (RRSS) y comprender las tendencias de ventas por producto y categoría. El objetivo es proporcionar insights que puedan guiar decisiones estratégicas en marketing y gestión de productos.

## 📂 Datos Utilizados

Se utilizaron tres conjuntos de datos principales, cada uno cargado desde Google Drive y preprocesado para asegurar su calidad:

1.  **`df_cli` (Clientes):** Contiene información sobre los clientes, incluyendo `id_cliente`, `nombre`, `edad`, `ciudad` e `ingresos`. Tras el EDA, se confirmó que este DataFrame no contenía valores nulos ni duplicados y tenía tipos de datos correctos.
2.  **`df_ven` (Ventas):** Incluye detalles de transacciones como `id_venta`, `producto`, `precio`, `cantidad`, `fecha_venta` y `categoria`. Se realizó una limpieza significativa, convirtiendo `precio` a numérico (eliminando '$'), `fecha_venta` a formato `datetime`, `cantidad` a `int`, eliminando duplicados y filas con valores nulos.
3.  **`df_mar` (Marketing):** Registra campañas con `id_campanha`, `producto`, `canal`, `costo`, `fecha_inicio` y `fecha_fin`. Se convirtieron las columnas de fecha a tipo `datetime`. No se encontraron nulos ni duplicados.

## 🛠️ Metodología

El análisis se llevó a cabo en varias etapas clave:

### 1. Recopilación y Preparación de Datos

*   **Carga de Datos:** Se implementó una función para cargar archivos CSV desde Google Drive.
*   **Análisis Exploratorio Inicial (EDA):** Una función `resumen_eda` personalizada se aplicó a cada DataFrame para examinar dimensiones, tipos de datos, estadísticas descriptivas, valores nulos y duplicados.

### 2. Preprocesamiento y Limpieza de Datos

*   **`df_cli_pp`:** Copia de `df_cli` sin cambios debido a su limpieza inicial.
*   **`df_ven_pp`:** Transformación de tipos de datos (`precio` a `float`, `fecha_venta` a `datetime`, `cantidad` a `int`), eliminación de 35 registros duplicados y 2 filas con valores nulos.
*   **`df_mar_pp`:** Conversión de `fecha_inicio` y `fecha_fin` a `datetime`.

### 3. Creación de Tablas Agregadas y Feature Engineering

*   **Productos de Alto Rendimiento:** Se identificaron productos con alto rendimiento de ventas utilizando el promedio y el percentil 90 de `venta_total`.
*   **Ciudades con Altos Ingresos:** Se agregaron ingresos por ciudad para identificar aquellas con mayor contribución.
*   **Productos con Alto Costo de Marketing:** Se agruparon productos por costo de campaña para detectar inversiones significativas.
*   **Integración de Ventas y Marketing:** Se realizó un `merge` entre `df_ven_pp` y un `df_mar_rrss` (marketing filtrado por el canal RRSS). Se creó la columna `en_campanha` para indicar si una venta ocurrió durante una campaña activa.

### 4. Análisis de Datos

*   **Estadística Descriptiva:** Se calcularon medidas de tendencia central y dispersión para variables clave, segmentadas por `en_campanha`.
*   **Análisis Exploratorio de Datos (EDA Visual):**
    *   **Histogramas:** Comparación de la distribución de `venta_total` dentro y fuera de campaña.
    *   **Boxplots:** Visualización de la distribución de `venta_total` y `cantidad` por estado de campaña (`en_campanha`). También se utilizó un boxplot para analizar la distribución de `venta_total` por `producto` para identificar la variabilidad de precios.
    *   **Pairplot:** Análisis de dispersión entre `precio`, `cantidad`, `venta_total` y `costo`.
*   **Correlación:** Se generó una matriz de correlación y un mapa de calor para las variables numéricas cuando una campaña estaba activa.
*   **Consolidación y Series Temporales:** Se analizaron ventas mensuales totales, desglosadas por `en_campanha`.

### 5. Visualización de Datos

Se generaron gráficos utilizando Matplotlib, Seaborn y Plotly para ilustrar los hallazgos:

*   **Serie Temporal (Lineplot Plotly):** Evolución mensual de la venta promedio (`venta_total_avg`) dentro y fuera de campaña.
*   **Barplot 1 (Seaborn):** Ventas promedio por producto, comparando rendimiento dentro y fuera de campañas RRSS.
*   **Barplot 2 (Matplotlib):** Ventas promedio y costos de marketing por producto en campañas activas.
*   **Boxplot (Seaborn):** Distribución de ventas totales comparando ventas dentro y fuera de campaña, embebido como imagen base64 en el dashboard final.

## 📈 Hallazgos Clave

*   **Impacto de RRSS:** El análisis mostró un ROI de 96.35, lo que sugiere que por cada $1 invertido en campañas de RRSS, se generaron aproximadamente $96.35 en ventas. Sin embargo, las ventas fuera de campaña son significativamente mayores en volumen, lo que indica la importancia de comparar el rendimiento a nivel de producto.
*   **Distribución de Ventas:** Los boxplots revelaron que, aunque las medianas de `venta_total` son similares dentro y fuera de campaña, puede haber diferencias en la dispersión y la presencia de valores atípicos que merecen un análisis más profundo.
*   **Productos de Alto Rendimiento/Costo:** Se identificaron productos específicos que contribuyen más a las ventas o que requieren una mayor inversión en marketing.
*   **Tendencias Temporales:** El lineplot de ventas mensuales proporciona una visión clara de las fluctuaciones estacionales y cómo las campañas impactan el promedio de ventas a lo largo del año.

## 🌐 Visualización del Dashboard

Se ha generado un archivo `plotly_dashboard.html` que contiene una Se ha generado un archivo plotly_dashboard.html que contiene una presentación final con un boxplot de Matplotlib y un gráfico de líneas de Plotly, junto con las explicaciones correspondientes
