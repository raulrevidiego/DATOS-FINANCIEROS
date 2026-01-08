Proyecto de Predicción de Incumplimiento de Pagos de Tarjetas de Crédito
Descripción General del Proyecto
Este proyecto se centra en el análisis y modelado de un conjunto de datos de clientes de tarjetas de crédito para predecir el incumplimiento de pagos el próximo mes. El objetivo es construir un modelo de Machine Learning que pueda identificar a los clientes con mayor probabilidad de incumplir, ayudando a las instituciones financieras a tomar decisiones informadas.

Dataset
El conjunto de datos utilizado es default_credit_card_clients.xls, que contiene información detallada sobre clientes de tarjetas de crédito, incluyendo su límite de crédito, demografía, historial de pagos, montos de facturación y montos de pagos previos.

Columnas Clave:
ID: Identificador único de la cuenta.
LIMIT_BAL: Cantidad del crédito dado.
SEX: Género (1=hombre, 2=mujer).
EDUCATION: Nivel educativo (1=posgrado, 2=universidad, 3=secundaria, 4=otros).
MARRIAGE: Estado marital (1=casado, 2=soltero, 3=otro).
AGE: Edad.
PAY_1 - PAY_6: Historial de pagos pasados (desde septiembre hasta abril).
-2: Comienzo del mes con saldo cero.
-1: Pago realizado debidamente.
0: Pago mínimo realizado.
1 a 9: Retraso de 1 a 9 meses.
BILL_AMT1 - BILL_AMT6: Monto de la factura (desde septiembre hasta abril).
PAY_AMT1 - PAY_AMT6: Monto del pago previo (desde septiembre hasta abril).
default payment next month: Variable objetivo (1=sí, 0=no).
Limpieza y Preparación de Datos
Se realizaron los siguientes pasos de limpieza y preprocesamiento:

Manejo de IDs Duplicados: Se identificaron y eliminaron filas duplicadas de ID que presentaban valores de cero en todas las demás columnas, indicando posibles registros incorrectos o incompletos.
Valores 'Not available' en PAY_1: Se eliminaron las filas donde la columna PAY_1 contenía el valor 'Not available', ya que no era posible imputar un valor numérico significativo.
Conversión de Tipo de Dato: La columna PAY_1 fue convertida de tipo object a int64 para permitir su uso en el modelado numérico.
Exploración de Datos (EDA)
Se realizó un análisis exploratorio para comprender las características del conjunto de datos:

Distribución del Historial de Pagos (PAY_x): La mayoría de los clientes mantienen sus pagos al día (-1 o 0). Sin embargo, se observaron discrepancias en las columnas PAY_2 a PAY_6 que sugieren que el historial de pagos puede no estar reflejando correctamente la progresión de los retrasos (e.g., un cliente con PAY_2=2 no debería tener PAY_3=2 si el retraso es acumulativo).
Montos de Facturación (BILL_AMT_x) y Pagos (PAY_AMT_x): Se observó que la mayoría de los montos de facturación y pagos eran relativamente bajos. Se realizaron transformaciones logarítmicas en los montos de pago para visualizar mejor su distribución, revelando una alta frecuencia de pagos mínimos o cero.
Límite de Crédito (LIMIT_BAL): Se visualizó la distribución de los límites de crédito.
Modelo de Machine Learning
Objetivo
Predecir si un cliente incurrirá en el incumplimiento de pago el próximo mes (default payment next month).

Enfoque
Se utilizó un modelo de Random Forest Classifier.

División de Datos
El conjunto de datos se dividió en conjuntos de entrenamiento y prueba utilizando train_test_split con un test_size del 20% y random_state=42.

Características (Features) Utilizadas
Inicialmente, el modelo se entrenó con las siguientes características:

EDUCATION
PAY_1
LIMIT_BAL
Posteriormente, se experimentó añadiendo MARRIAGE.

Evaluación del Modelo
Métrica Principal: accuracy_score (precisión).
Resultados: La precisión obtenida para el modelo inicial fue aproximadamente del 81.6%. La adición de la característica MARRIAGE no mejoró significativamente el rendimiento.
Nota sobre r2_score: Aunque se intentó aplicar r2_score, esta métrica no es apropiada para problemas de clasificación como este, ya que está diseñada para modelos de regresión. La precisión (accuracy) es la métrica correcta para evaluar el rendimiento de un clasificador binario.

Librerías Utilizadas
pandas
numpy
matplotlib
sklearn (para train_test_split, RandomForestClassifier, accuracy_score, r2_score)
Cómo Ejecutar el Proyecto
Asegúrate de tener instaladas todas las librerías mencionadas.
Carga el archivo default_credit_card_clients.xls en tu entorno.
Ejecuta las celdas en el orden presentado en el notebook para realizar la limpieza de datos, exploración y entrenamiento del modelo.
