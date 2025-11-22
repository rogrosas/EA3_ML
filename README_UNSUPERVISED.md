# README_UNSUPERVISED

## 1. Descripción de la técnica utilizada y justificación

En este análisis se aplicaron dos técnicas de aprendizaje no supervisado:

- **PCA (Análisis de Componentes Principales)**: Se utilizó para reducir la dimensionalidad del conjunto de datos y facilitar la visualización. PCA permite identificar las direcciones de mayor varianza en los datos, eliminando redundancia y ruido.

- **K-Means Clustering**: Se empleó para segmentar clientes en grupos homogéneos según características financieras y demográficas. Esta técnica es adecuada para identificar patrones ocultos y subpoblaciones con diferentes niveles de riesgo crediticio.

La combinación PCA + K-Means es útil porque:
- PCA mejora la eficiencia y la interpretabilidad del clustering.
- K-Means permite crear segmentos que pueden relacionarse con la variable objetivo (`TARGET`), aportando valor al modelo supervisado.

---

## 2. Instrucciones de ejecución del código

1. Instalar dependencias:
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn pyarrow
   ```

2. Ubicar los archivos Parquet en la carpeta definida en el notebook (por defecto: `./datos_examen`).

3. Abrir el notebook:
   - `unsupervised_analysis.ipynb`

4. Ejecutar las celdas en orden:
   - Carga de datos.
   - Generación de variables agregadas.
   - Preparación (manejo de nulos, estandarización).
   - PCA + K-Means.
   - Visualización y análisis.

---

## 3. Análisis e interpretación de resultados

- **Clusters identificados**: Se generaron 5 clusters que agrupan clientes según ingresos, monto de crédito, antigüedad laboral, historial en bureau y comportamiento en créditos previos.

- **Visualización PCA**: El gráfico muestra cómo los clientes se distribuyen en dos componentes principales, con separación clara entre algunos grupos.

- **Relación con riesgo (`TARGET`)**: Al calcular la tasa de morosidad por cluster, se observan diferencias significativas entre grupos. Esto indica que ciertos segmentos presentan mayor riesgo crediticio, lo que puede ser útil para ajustar políticas de scoring.

---

## 4. Discusión sobre aplicabilidad al proyecto final

El método aplicado **sí podría incorporarse** al proyecto de scoring crediticio porque:
- Permite identificar segmentos con riesgo diferenciado.
- Ayuda a detectar sesgos en el modelo supervisado.
- Facilita estrategias personalizadas (por ejemplo, límites de crédito según cluster).

Limitaciones:
- K-Means requiere definir el número de clusters (hiperparámetro sensible).
- PCA reduce interpretabilidad de variables originales.
- No se consideraron todas las variables categóricas (posible mejora futura).
