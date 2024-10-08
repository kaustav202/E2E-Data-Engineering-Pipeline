An end-to-end data engineering pipeline that orchestrates data ingestion, processing, and storage using Apache Airflow, Python, Apache Kafka, Apache Zookeeper, Apache Spark, and Cassandra. All components are containerized with Docker for easy deployment and scalability.


![architecture](Data%20engineering%20architecture%20(1).png)



This project serves as a step-by-step guide to building a complete data engineering pipeline, covering everything from data ingestion to processing and storage. Here’s a detailed breakdown:

1. **Data Ingestion with Apache Airflow**:
   - **Task Orchestration**: Apache Airflow is used to manage and schedule tasks in the pipeline. It fetches random user data from the `randomuser.me` API and stores it in a PostgreSQL database.
   - **Ease of Use**: Airflow makes it easy to set up and monitor complex workflows, ensuring data is ingested reliably.

2. **Real-Time Data Streaming with Apache Kafka**:
   - **High-Throughput Streaming**: Apache Kafka streams the data from PostgreSQL to the data processing engine. It handles large volumes of data efficiently and ensures that the data flows smoothly through the pipeline.
   - **Coordination with Zookeeper**: Apache Zookeeper manages Kafka brokers, providing distributed synchronization and ensuring the system is fault-tolerant.

3. **Data Processing with Apache Spark**:
   - **Scalable Processing**: Apache Spark processes the streamed data, performing transformations and aggregations as needed. Spark's distributed computing capabilities allow it to handle large datasets and complex computations efficiently.
   - **Master and Worker Nodes**: Spark's architecture, with master and worker nodes, ensures that the processing tasks are distributed and managed effectively.

4. **Data Storage with Cassandra**:
   - **High Availability Storage**: The processed data is stored in a Cassandra database. Cassandra is chosen for its high availability and scalability, making it suitable for storing large volumes of processed data.
   - **Fast Data Retrieval**: Cassandra provides fast read and write capabilities, ensuring that the stored data can be accessed quickly for analysis and reporting.


### Getting Started

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/kaustav202/E2E-Data-Engineering-Pipeline.git
   ```

2. **Navigate to the Project Directory**:
   ```bash
   cd E2E-Data-Engineering-Pipeline
   ```

3. **Install Docker**: Ensure you have Docker installed on your machine. You can download and install Docker from [here](https://www.docker.com/products/docker-desktop).


4. **Build and Run Containers**: Use Docker Compose to build and run the containers.
   ```bash
   docker-compose up --build
   ```

5. **Access Components**:
   - **Airflow Web Interface**: `http://localhost:8080`
   - **Kafka Control Center**: `http://localhost:9021`


## Running the Application
After completing the setup steps, it's ready to start streaming.

1. Open the Airflow webserver UI and run the DAG.
  ```
  http://localhost:8080/login/
  ```
  -user: airflow
  -password: airflow

2. Alternatively, use the command line to run the application.
  - Run the Producer:
  ```
  cd app
  python ./dags/kafka_stream.py
  ```
  - use spark-submit to run the spark Job
  ```
  docker exec -it spark-master bash
  spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.0,com.datastax.spark:spark-cassandra-connector_2.12:3.4.0 spark_stream.py
  ```

### Using "cqlsh" Cassandra Query Language Shell
Using cqlsh to execute SQL batch scripts on the data loaded into Cassandra.

- Enter the Cassandra container:
   ```
   docker exec -it cassandra bash
   ```
 - then use cassandra query lang shell
   ```
   cqlsh
   ```
 - start writing your queries, for example show the data
   ```
    SELECT * FROM created_users ; 
   ```