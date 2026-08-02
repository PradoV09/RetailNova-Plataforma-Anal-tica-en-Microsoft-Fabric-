# RetailNova — Plataforma Analítica en Microsoft Fabric

**Data Lab · Proyecto Final — Caso #1**
Microsoft Fabric · ML · SQL · Agentes de IA

**Autores:**
- Luisa Fernanda Gonzales Delgado
- Jose Luis Prado Valencia

**Fechas del reto:**
- Socialización: 10 de junio 2026
- Entrega: 14 de junio 2026
- Presentación: 16 de junio 2026

---

## 1. Objetivo General

Construcción de un proceso completo de integración, transformación y análisis de datos en Microsoft Fabric para **RetailNova**, cadena retail con presencia nacional que comercializa productos tecnológicos y accesorios. El proyecto cubre tres componentes: ETL/ELT con arquitectura Medallón, Machine Learning con MLflow y un Modelo Dimensional en SQL.

**Dataset:** [Retail Sales Dataset (Kaggle)](https://www.kaggle.com/datasets/mohammadtalib786/retail-sales-dataset)

## 2. Caso de Negocio

RetailNova no posee visibilidad consolidada sobre ventas, clientes, productos e inventario. La solución debe permitir:

- Consolidar datos de ventas de múltiples fuentes
- Identificar productos y categorías con mayor desempeño
- Analizar el comportamiento de clientes
- Monitorear inventario y rotación de productos
- Generar indicadores ejecutivos para toma de decisiones

### Preguntas de negocio respondidas

| # | Pregunta | Componente que la resuelve |
|---|----------|----------------------------|
| 1 | ¿Cuáles son las categorías con mayor venta? | _completar (SQL / Gold)_ |
| 2 | ¿Qué clientes generan más ingresos? | _completar_ |
| 3 | ¿Qué productos tienen baja rotación? | _completar_ |
| 4 | ¿Cómo evolucionan las ventas en el tiempo? | _completar_ |
| 5 | ¿Qué regiones presentan mejor desempeño? | _completar_ |

## 3. Arquitectura del Proyecto

```
WorkSpace/
├── 01_EXT/                        # Extracción (Bronze)
├── 02_TRANS/                      # Transformación (Silver)
│   └── MODELO_DIMENSIONAL_SQL/    # Componente SQL
│       ├── limpieza.sql
│       ├── modelado.sql
│       ├── analisis.sql
│       ├── vistas.sql
│       └── README.md
├── 03_SILVER/
├── 04_GOLD/
├── 05_VISUALIZACION/
│   ├── 06_modelo_semantico/
│   └── 07_dashboard/
└── ML/
    ├── 01_feature_engineering.ipynb
    ├── 02_entrenamiento_experimentos.ipynb
    ├── 03_evaluacion.ipynb
    ├── 04_registro_deployment.ipynb
    └── README.md
```

### 3.1 Arquitectura Medallón

| Capa | Descripción | Criterio clave |
|------|-------------|-----------------|
| **Bronze** | Extracción e ingestión del dataset original, conservando el dato fuente sin transformaciones críticas. Registro de origen y fecha de carga. | Dato fuente intacto con metadata de carga |
| **Silver** | Limpieza y estandarización: tratamiento de nulos y duplicados, conversión de tipos, reglas de calidad y enriquecimiento. | 0 nulos sin tratar, 0 duplicados en PK |
| **Gold** | Modelo analítico listo para negocio: tablas agregadas/dimensionales preparadas para el modelo semántico. | Responde las preguntas de negocio definidas |

_Completar: decisiones técnicas tomadas en cada capa, reglas de calidad aplicadas, particiones, etc._

## 4. Componente SQL — Modelo Dimensional

Construido íntegramente en SQL/SparkSQL sobre el dataset del caso de negocio, siguiendo un esquema en estrella (mínimo 3 tablas dimensionales + 1 tabla de hechos en 3NF), disponible en la zona Gold para consumo de visualización.

| Script | Contenido | Estado |
|--------|-----------|--------|
| `limpieza.sql` | Diagnóstico y limpieza de datos (nulos, duplicados, tipos) | _completar_ |
| `modelado.sql` | DDL del esquema estrella (dimensiones + hechos) | _completar_ |
| `analisis.sql` | Mínimo 5 consultas analíticas con CTEs y Window Functions | _completar_ |
| `vistas.sql` | Mínimo 3 vistas finales documentadas | _completar_ |

### Modelo estrella

_Completar: diagrama ER o listado de tablas dimensionales (`dim_producto`, `dim_cliente`, `dim_fecha`, etc.) y la tabla de hechos (`fact_ventas`), con sus llaves y relaciones._

## 5. Componente ML — Machine Learning con MLflow

Pipeline de ML construido a partir de la capa Gold, con tracking y versionamiento en MLflow.

### 5.1 Definición de problemas (prerequisito)

Dos tipos seleccionados de los tres disponibles (Clasificación / Regresión / Clustering) → **2 modelos entregados**.

| Campo | Problema 1 | Problema 2 |
|-------|-----------|-----------|
| Tipo de problema | _completar_ | _completar_ |
| Variable objetivo (target) | _completar_ | _completar_ |
| Algoritmo seleccionado | _completar_ | _completar_ |
| Justificación del algoritmo | _completar_ | _completar_ |
| Justificación de negocio | _completar_ | _completar_ |
| Viabilidad técnica | _completar_ | _completar_ |
| Criterios de éxito | _completar_ | _completar_ |

### 5.2 Resultados

_Completar: métricas obtenidas por modelo (Accuracy/F1/ROC-AUC o MAE/RMSE/R² o Silhouette/Davies-Bouldin según corresponda), visualizaciones generadas, interpretación de negocio._

### 5.3 MLflow

_Completar: nombres de experimentos, runs relevantes, modelo(s) registrados en el Model Registry._

## 6. Modelo Semántico y Dashboard

_Completar: KPIs definidos, medidas DAX/Spark relevantes, capturas o enlace al dashboard, relaciones del modelo semántico._

## 7. Reglas de Gobernanza Aplicadas

- Convención de nombres `snake_case` en todos los objetos (tablas, columnas, vistas, variables, experimentos MLflow)
- Scripts SQL re-ejecutables (`DROP IF EXISTS` previo a la creación de objetos)
- Sin uso de `SELECT *` en consultas de entrega final
- Sin transformación de datos fuera de Fabric (Excel, Python externo, etc.)
- Notebooks de ML idempotentes, ejecutados en orden lógico sin errores
- `requirements.txt` con dependencias y versiones exactas

## 8. Cómo ejecutar el proyecto

_Completar: pasos para reproducir el pipeline ETL en Fabric, orden de ejecución de los scripts SQL y los notebooks de ML, requisitos previos (workspace de Fabric, permisos, etc.)._

## 9. Estructura de Entregables

| Capa/Componente | Entregable | Criterio de aceptación |
|------------------|-----------|--------------------------|
| Bronze | Ingestión y persistencia del dato fuente | Datos cargados con metadata de origen |
| Silver | Limpieza y calidad de datos | Nulos y duplicados tratados, tipos correctos |
| Gold | Modelo analítico final | Responde las preguntas de negocio definidas |
| Modelo Semántico | Semantic Model + dashboard | Navegación funcional y métricas correctas |
| SQL | Modelo dimensional en estrella | Mínimo 3 dimensiones + 1 hechos en 3NF |
| ML | 2 modelos entrenados y registrados en MLflow | Tracking, evaluación y registro completos |
| Documentación | Este README + READMEs de subcomponentes | Claridad y reproducibilidad |

## 10. Conclusiones

_Completar: hallazgos principales, recomendaciones de negocio para RetailNova, limitaciones del proyecto y posibles trabajos futuros._
