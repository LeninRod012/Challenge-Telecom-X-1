Informe de Análisis de Evasión de Clientes (Churn) — Telecom X

Introducción

El objetivo de este análisis es comprender los factores que influyen en la evasión de clientes (Churn) en Telecom X y proponer acciones que ayuden a reducirla. La evasión impacta directamente los ingresos y el costo de adquisición de clientes; anticiparla permite diseñar estrategias de retención más eficaces y rentables.

Limpieza y Tratamiento de Datos

Fuente de datos: API pública en formato JSON (cargada con pandas.read_json).

Expansión de columnas anidadas: el conjunto original incluía estructuras tipo diccionario (por ejemplo, información de cuenta). Se expandieron para obtener un DataFrame tabular (df_telecomx_expanded).

Valores nulos: verificación realizada; no se identificaron valores nulos tras la expansión y depuración.

Duplicados: verificación realizada; no se identificaron filas duplicadas tras la estandarización.

Inconsistencias en ‘Churn’: valores vacíos en la columna Churn fueron reemplazados por "No" para mantener consistencia binaria (Sí/No).

Nueva característica: se creó Cuentas_Diarias como Charges.Monthly / 30 para aproximar el gasto diario y analizar patrones de facturación a un nivel temporal más granular.

Análisis Exploratorio de Datos (EDA)

Distribución de Churn

Se visualizó la distribución de Churn mediante un gráfico de barras, evidenciando la proporción de clientes que permanecen frente a los que cancelan.

Churn por variables categóricas (ejemplos)

Contrato (Contract): comparación de tasas de churn por tipo de contrato (mensual vs. anual, etc.).

Método de pago (PaymentMethod): inspección de churn por forma de pago (automático/manual, tarjeta/transferencia, etc.).

Género (gender): revisión de diferencias de churn, si las hubiera, entre categorías.

Variables numéricas vs. Churn (ejemplos)

Antigüedad (tenure): distribución por estado de churn; típicamente menor antigüedad puede asociarse a mayor cancelación.

Cargos mensuales y totales (Charges.Monthly, Charges.Total): boxplots por estado de churn para detectar niveles de gasto asociados a mayor probabilidad de baja.

Cuentas_Diarias: inspección de su distribución por estado de churn para identificar umbrales de gasto diario relevantes.

Nota: Las visualizaciones incluyeron gráficos de barras apiladas para variables categóricas y boxplots para variables numéricas, además de tablas de contingencia normalizadas por fila para tasas de churn (%).

Conclusiones e Insights

Tipo de contrato: Los contratos de mayor plazo suelen presentar menor churn que los contratos mes a mes. Reforzar la migración a contratos más largos puede reducir la evasión.

Método de pago: Métodos automáticos tienden a asociarse a menor churn frente a pagos manuales. Incentivos para configurar débito automático pueden ser efectivos.

Antigüedad (tenure): Clientes de baja antigüedad muestran mayor riesgo de churn. Los primeros meses son críticos para acciones proactivas de onboarding y valor percibido.

Nivel de cargos: Segmentos con cargos mensuales/diarios extremos (muy altos o muy bajos según el caso) pueden mostrar mayor propensión a cancelar; conviene revisar adecuación de plan/beneficios.

Recomendaciones

Programas de retención tempranos: campañas específicas durante los primeros meses (bonificaciones, soporte proactivo, encuestas de satisfacción tempranas).

Incentivos a contratos de mayor plazo: descuentos escalonados, beneficios adicionales o puntos de fidelización por migrar desde contratos mensuales.

Fomento del pago automático: ofrecer beneficios por adherirse a débito automático para reducir fricción y atrasos.

Alertas preventivas: monitorear picos en consultas/reclamos y variaciones en cargos diarios para activar contactabilidad proactiva.

Segmentación: diseñar ofertas y comunicaciones diferenciadas por perfil (combinando tenure, método de pago y patrón de cargos).

Notas de Reproducibilidad

Se utilizó pandas para carga/limpieza, expansión de columnas anidadas y creación de Cuentas_Diarias.

La columna Churn fue normalizada para valores binarios consistentes (reemplazo de vacíos por "No").

Las visualizaciones emplearon gráficos de barras y boxplots.

Próximos Pasos (Opcional / Siguiente Módulo ML)

Selección de variables: análisis de correlación y relevancia predictiva (incluyendo Cuentas_Diarias).

Codificación y escalado: one‑hot encoding para categóricas y normalización/estandarización de numéricas donde aplique.

Modelado: entrenamiento de modelos de clasificación (Regresión Logística, Árboles/Random Forest, Gradient Boosting), validación y comparación por AUC‑ROC, F1‑score y recall de la clase positiva (Churn = Sí).

Interpretabilidad: importancia de variables y, si se requiere, técnicas como SHAP para comprensión local/global del modelo.
