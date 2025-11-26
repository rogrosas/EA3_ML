# Integrantes: Rodrigo Andres Santis Erices, Roger Andres Rosas peña

# README_UNSUPERVISED

## 1. Introducción

En este análisis se aplicó un método de aprendizaje no supervisado para complementar el modelo de scoring crediticio.
La técnica seleccionada fue **PCA (Análisis de Componentes Principales) combinado con K-Means Clustering**, por las siguientes razones:

- **PCA** permite reducir la dimensionalidad del dataset, eliminando redundancia y facilitando la visualización.
- **K-Means** segmenta clientes en grupos homogéneos según características financieras y demográficas, lo que ayuda a identificar patrones ocultos y subpoblaciones con riesgo diferenciado.

### Datos utilizados
Se trabajó con el conjunto de entrenamiento del proyecto, específicamente:
- Tabla principal `application_.parquet` (información del solicitante y variable objetivo `TARGET`).
- Tablas relacionadas: `bureau`, `previous_application`, `POS_CASH_balance`, `credit_card_balance`, `installments_payments`.

### Variables seleccionadas
Se incluyeron variables numéricas relevantes:
- Ingresos (`AMT_INCOME_TOTAL`), monto del crédito (`AMT_CREDIT`), antigüedad laboral (`DAYS_EMPLOYED`), edad (`DAYS_BIRTH`).
- Variables agregadas: promedio de créditos en bureau, cantidad de solicitudes previas, número de registros en POS, tarjetas y pagos.
(Necesario tenerlos descargados en una carpeta dentro del proyecto llamada "datos_examen")
---

## 2. Proceso CRISP-DM aplicado

### Comprensión del negocio
El objetivo es identificar segmentos de clientes con diferentes niveles de riesgo crediticio para mejorar la interpretación del modelo supervisado y detectar posibles sesgos.

### Comprensión y preparación de datos
- Se cargaron los archivos Parquet desde la carpeta definida.
- Se generaron variables agregadas por cliente.
- Se manejaron valores faltantes mediante imputación con la media.
- Se estandarizaron las variables numéricas con `StandardScaler`.

### Modelado
- Se aplicó PCA para reducir a 2 componentes principales.
- Se ejecutó K-Means con 5 clusters sobre los datos estandarizados.

### Evaluación
- Se visualizó la distribución de clientes en el espacio PCA.
- Se calculó la tasa de morosidad (`TARGET`) por cluster para evaluar diferencias de riesgo.

---

## 3. Evaluación del desempeño y utilidad

El método se evaluó en función de:
- Separación visual de clusters en el espacio PCA.
- Diferencias en la tasa de morosidad por cluster, lo que indica que los grupos tienen comportamientos crediticios distintos.

---

## 4. Discusión sobre aplicabilidad

El análisis **sí puede incorporarse** al proyecto porque:
- Permite segmentar clientes y ajustar estrategias de scoring.
- Ayuda a detectar sesgos y mejorar la interpretación del modelo supervisado.

Limitaciones:
- PCA reduce interpretabilidad de variables originales.
- K-Means requiere definir el número de clusters.
- No se incluyeron variables categóricas (posible mejora futura).
