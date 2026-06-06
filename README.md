# Actividad 2 - Procesamiento de Datos en Databricks con Apache Spark

## Descripción

Este proyecto corresponde al desarrollo de la Actividad 2, cuyo objetivo fue diseñar una infraestructura básica de procesamiento de datos utilizando Databricks Free Edition, cargar un conjunto de datos obtenido desde Kaggle y realizar validaciones mediante Apache Spark y Spark SQL.

Para la actividad se utilizó el dataset **FIDE World Chess Ratings (201K Players)**, que contiene información de más de 200.000 jugadores registrados por la Federación Internacional de Ajedrez (FIDE).

---

## Objetivos

* Diseñar el esquema de almacenamiento para el dataset seleccionado.
* Configurar y documentar la infraestructura en Databricks.
* Cargar datos desde Kaggle utilizando Apache Spark.
* Crear una tabla administrada mediante Spark SQL.
* Realizar validaciones utilizando PySpark y SQL.
* Comparar las ventajas y desventajas de SQL frente a Spark.

---

## Dataset utilizado

**Nombre:** FIDE World Chess Ratings (201K Players)

**Fuente:** Kaggle

https://www.kaggle.com/datasets/ibrahimqasimi/fide-world-chess-ratings-201k-players

### Variables principales

| Campo  |
| ------ |
| id     |
| name   |
| fed    |
| sex    |
| title  |
| wtitle |
| otitle |
| foa    |
| rating |
| games  |
| k      |
| bday   |

---

## Tecnologías utilizadas

* Databricks Free Edition
* Apache Spark
* Spark SQL
* Python
* Delta Lake
* Kaggle Dataset


---

## Proceso realizado

### 1. Diseño del esquema

Se diseñó un esquema para representar la información de los jugadores FIDE, definiendo tipos de datos, restricciones y estructura de almacenamiento.

### 2. Configuración de Databricks

Se configuró un entorno Databricks Free Edition utilizando cómputo Serverless y almacenamiento mediante Volumes.

### 3. Ingesta de datos

El archivo CSV fue descargado desde Kaggle y cargado manualmente a Databricks mediante un Volume.

Ruta utilizada:

```text
dbfs:/Volumes/workspace/default/fideworldchessratings201kplayers/03_FIDE_Chess_Ratings.csv
```

### 4. Creación de la tabla

Los datos fueron cargados mediante Spark DataFrame y almacenados en una tabla administrada llamada:

```sql
fide_players
```

### 5. Validaciones

Se realizaron validaciones utilizando:

* DESCRIBE TABLE
* SHOW CREATE TABLE
* COUNT(*)
* SELECT con filtros
* GROUP BY
* Estadísticas descriptivas con PySpark

### 6. Comparación SQL vs Spark

Se analizaron las ventajas y desventajas de ambos enfoques para el procesamiento y análisis de datos.

---

## Instrucciones de ejecución

### 1. Abrir Databricks

Acceder a Databricks Free Edition y crear un nuevo Notebook con lenguaje Python.

### 2. Cargar el dataset

Subir el archivo CSV a un Volume o al almacenamiento disponible en Databricks.

### 3. Leer el archivo

```python
df = spark.read.csv(
    "dbfs:/Volumes/workspace/default/fideworldchessratings201kplayers/03_FIDE_Chess_Ratings.csv",
    header=True,
    inferSchema=True
)
```

### 4. Verificar la carga

```python
df.printSchema()
print(df.count())
```

### 5. Crear la tabla

```python
df.write.mode("overwrite").saveAsTable("fide_players")
```

### 6. Ejecutar consultas SQL

```sql
SELECT *
FROM fide_players
LIMIT 10;
```

```sql
SELECT
    fed,
    COUNT(*) AS total_jugadores
FROM fide_players
GROUP BY fed
ORDER BY total_jugadores DESC;
```

---

## Resultados obtenidos

* Carga exitosa de más de 200.000 registros.
* Creación de una tabla administrada en Spark SQL.
* Validación del esquema y metadatos.
* Análisis descriptivo de ratings y federaciones.
* Comparación práctica entre consultas SQL y PySpark.

---

## Autores

Padron Yeison_
Gonzalez JuanPablo
Castaño Simon
Gomez Luisa

Actividad académica desarrollada utilizando Apache Spark y Databricks Free Edition.
