# analysis-connectatel

Este proyecto consiste en un análisis de datos para ConnectaTel, una empresa de telecomunicaciones en Latinoamérica, con el fin de evaluar el comportamiento de sus clientes a partir de información registrada hasta el año 2024.

## Objetivo del proyecto

Como analista de datos, el objetivo fue explorar, limpiar y analizar los datos de clientes y uso del servicio para:
- Construir un perfil estadístico de los clientes.
- Detectar comportamientos atípicos (outliers) en el uso del servicio.
- Crear segmentos de clientes basados en edad y nivel de uso.
- Identificar patrones de consumo que permitan diseñar estrategias de retención y sugerir mejoras en los planes ofrecidos.

## Datasets utilizados

- plans.csv: Información de los planes actuales (precio, minutos y GB incluidos, costo por extra).
- users_latam.csv: Información de los clientes (edad, ciudad, fecha de registro, plan, fecha de baja).
- usage.csv: Detalle del uso real del servicio (llamadas y mensajes).

## Etapas del analisis 

- Exploración inicial: revisión de estructura, dimensiones y tipos de dato de los tres datasets.
- Detección de problemas de calidad de datos: valores nulos, sentinels (-999 en age, '?' en city) y fechas inconsistentes (registros de 2026 con uso previo en 2024).
- Limpieza de datos: corrección de sentinels y fechas, y verificación de que los nulos en duration/length dependen del tipo de evento (MAR).
- Métricas de uso por usuario: agregación de usage por cliente (cant_mensajes, cant_llamadas, cant_minutos_llamada).
- Análisis de distribuciones y outliers: histogramas, boxplots y cálculo de límites con IQR.
- Segmentación de clientes: por edad (grupo_edad) y nivel de uso (grupo_uso).
- Insight ejecutivo: traducción de hallazgos en recomendaciones de negocio.

## Cómo ejecutar el Notebook

- Descarga o clona este repositorio.
- Abre el notebook S7_Version-Estudiante-Project-ConnectaTel.ipynb en Google Colab:
Ve a colab.research.google.com.
-Selecciona Archivo → Abrir notebook → GitHub, pega la URL de este repositorio y selecciona el archivo .ipynb.

## Guía de reproducción

- Asegúrate de tener instaladas las siguientes librerías:
pip install pandas seaborn matplotlib
- Coloca los archivos plans.csv, users_latam.csv y usage.csv en la ruta /datasets/ (o ajusta la ruta de carga en las celdas correspondientes si los guardas en otra ubicación).
- Ejecuta las celdas del notebook en orden, de principio a fin, ya que cada sección depende de las transformaciones realizadas en la anterior (limpieza → agregación → visualización → segmentación).
- Los resultados (gráficos, tablas y el análisis ejecutivo final) se generarán automáticamente al ejecutar el notebook completo.
