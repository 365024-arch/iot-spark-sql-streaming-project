# IoT Spark SQL and Structured Streaming Project

## Overview

Questo progetto è stato sviluppato per il corso di **Big Data Analytics** dell'Università di Modena e Reggio Emilia (UNIMORE).

L'obiettivo del progetto è sperimentare **Apache Spark SQL** e **Structured Streaming** per l'analisi di dati provenienti da dispositivi IoT (Internet of Things).

È stato generato un dataset simulato contenente 10.000 misurazioni provenienti da sensori virtuali e successivamente analizzato mediante Apache Spark.

---

## Technologies Used

* Python 3
* Apache Spark 4.0.2
* PySpark
* Google Colaboratory
* Spark SQL
* Structured Streaming

---

## Dataset

Il dataset contiene misurazioni simulate provenienti da sensori IoT.

Ogni record include i seguenti attributi:

* timestamp
* sensor_id
* temperature
* humidity

Il dataset contiene 10.000 record generati da 10 sensori virtuali.

---

## Installation

Installare PySpark:

```bash
pip install pyspark
```

Verificare l'installazione:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("IoT Spark SQL and Structured Streaming Project") \
    .getOrCreate()

print("Spark Version:", spark.version)
```

---

## Running the Project

1. Aprire il notebook in Google Colab.
2. Installare PySpark.
3. Creare una Spark Session.
4. Generare o caricare il dataset IoT.
5. Importare il dataset in un DataFrame Spark.
6. Creare la tabella SQL `sensors`.
7. Eseguire le query Spark SQL.
8. Avviare la simulazione di Structured Streaming.

---

## Spark SQL Analyses

Le principali analisi effettuate sono:

### Average Temperature per Sensor

```sql
SELECT sensor_id,
ROUND(AVG(temperature),2) AS avg_temperature
FROM sensors
GROUP BY sensor_id
ORDER BY sensor_id;
```

### Average Humidity per Sensor

```sql
SELECT sensor_id,
ROUND(AVG(humidity),2) AS avg_humidity
FROM sensors
GROUP BY sensor_id
ORDER BY sensor_id;
```

### Anomaly Detection

```sql
SELECT *
FROM sensors
WHERE temperature > 35
ORDER BY temperature DESC;
```

---

## Structured Streaming

Structured Streaming è stato utilizzato per simulare l'elaborazione di dati in tempo reale.

Nuovi file CSV vengono aggiunti progressivamente in una directory monitorata da Spark. Il sistema aggiorna automaticamente le statistiche aggregate all'arrivo di nuovi batch di dati.

Esempio:

```python
query = stream_result.writeStream \
    .outputMode("complete") \
    .format("memory") \
    .queryName("iot_stream_results") \
    .start()
```

---

## Results

La sperimentazione ha dimostrato l'efficacia di Apache Spark nell'analisi di dati IoT.

I principali risultati ottenuti sono:

* Elaborazione corretta di 10.000 misurazioni IoT.
* Calcolo della temperatura media per ciascun sensore.
* Calcolo dell'umidità media per ciascun sensore.
* Individuazione delle anomalie con temperatura superiore a 35°C.
* Elaborazione in tempo reale tramite Structured Streaming.
* Aggiornamento automatico dei risultati dopo l'arrivo di nuovi batch di dati.

---

## Repository Structure

```text
iot-spark-sql-streaming-project/
│
├── IoT Spark SQL and Structured Streaming Project.ipynb
├── README.md
├── sensors.csv

```

---

## Author

Siwar Mhamdi

---

## Course

Big Data Analytics – A.A. 2025/2026

University of Modena e Reggio Emilia (UNIMORE)
