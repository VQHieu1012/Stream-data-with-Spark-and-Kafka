## Streaming data with Kafka and Spark Streaming
In this project, we apply techstack to create a Streaming data pipeline.
This document outlines the architecture and technology stack used for a real-time user data analysis pipeline.
The pipeline is designed to ingest, process, and store user data from API to generate actionable insights.

### 1. Architecture Overview

![Architecture](https://github.com/VQHieu1012/Stream-data-with-Spark-and-Kafka/blob/main/asset/pipeline.png)

* **Data Ingestion**: User data from API is collected and streamed into the pipeline.
* **Data Processing**: The ingested data is processed in real-time using distributed stream processing frameworks.
* **Data Storage**: Processed data is stored in a suitable database for further analysis and reporting.

### 2. Technology Stack

* **Apache Airflow**: orchestrating the data pipeline. It schedules and manages the streaming tasks from API and Kafka.
* **Kafka**: Kafka is a distributed streaming platform used as a message broker in the pipeline. It receives the incoming stream of user data from Airflow and reliably delivers it to the downstream processing components. Kafka's high throughput and fault tolerance make it suitable for handling large volumes of real-time data.
* **Spark**: Apache Spark is a powerful distributed computing framework used for real-time data processing. It consumes the data stream from Kafka, performs transformations and aggregations, and prepares the data for storage.
* **Control Center**: A tool to manage and monitor Kafka Clusters.
* **Schema Registry**: A central repository to store and manage schemas used by Kafka. It ensures data consistency and compatibility across different applications consuming the data.
* **Cassandra**: A NoSQL database was chosen for its ability to handle high-volume, high-velocity data with low latency. It provides a distributed and scalable solution for storing the processed user data. Cassandra's fault tolerance and tunable consistency levels make it a reliable choice for real-time data storage.
* **Docker**: Dockerize the components of the pipeline.

### 3. Why these technologies are used

* **Scalability**: Each component is designed to scale horizontally, handling increasing data volumes and user traffic.
* **Fault Tolerance**: The distributed nature of the technologies ensures resilience to failures, minimizing downtime and data loss.
* **Real-time Processing**: Kafka and Spark enable real-time data ingestion and processing, providing immediate insights.
* **Data Consistency**: The schema registry ensures data integrity and compatibility throughout the pipeline.
* **Flexibility**: The modular design allows for easy integrating new data sources and processing tasks.
### 4. How to run
1 - Clone the repository:
```
git clone https://github.com/ntd284/streaming_realtime_data.git
```
2 - Navigate to the project directory
3 - Set up a Virtual Environment 
```
pip3 install virtualenv
python3 -m venv venv
source venv/bin/activate
```
4 - Install packages and libraries
```
pip3 install -r ./requirements.txt
```
5 - Start docker-compose
```
docker compose up -d
```
6 - Run streaming task
```
python3 spark-streaming.py
```
7 - Access to airflow UI to monitor streaming process: `localhost:8080` with account: `admin`, password: `admin`

8 - Access to control center UI monitor Topic health, Procuder and consumer performance, Offset, Cluster health: `localhost:9021`

9 - Check Cassandra database
```
docker exec -it cassandra cqlsh -u cassandra -p cassandra localhost 9042
```
### Reference
[1]. [Streaming data pipeline](https://www.youtube.com/watch?v=GqAcTrqKcrY)

[2]. [Cassandra and Pyspark](https://medium.com/@yoke_techworks/cassandra-and-pyspark-5d7830512f19)
