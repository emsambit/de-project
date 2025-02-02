# Data Lake and Analytics Stack with Docker Compose

This repository sets up a complete **data lake and analytics environment** using Docker Compose. It integrates multiple services like **Kafka**, **Trino**, **Spark**, **MinIO**, **Hive**, **Elasticsearch**, **Kibana**, and **Glue Jupyter Notebooks** for seamless data ingestion, querying, and analytics.

---

## **Services Overview**

### 1. **Zookeeper**
- **Description:** Coordination service for Kafka.
- **URL:** N/A
- **Port:** `2181`

### 2. **Kafka**
- **Description:** Distributed streaming platform for building real-time data pipelines.
- **Ports:** 
  - `9092` (Internal Broker)
  - `29092` (External Broker)

### 3. **Kafka UI**
- **Description:** Web interface for managing and monitoring Kafka clusters.
- **URL:** [http://localhost:8082](http://localhost:8082)
- **Port:** `8082`

### 4. **Elasticsearch**
- **Description:** Distributed search and analytics engine.
- **URL:** [http://localhost:9200](http://localhost:9200)
- **Ports:** 
  - `9200` (HTTP API)
  - `9300` (Transport Layer)

### 5. **Kibana**
- **Description:** Visualization tool for Elasticsearch.
- **URL:** [http://localhost:5601](http://localhost:5601)
- **Port:** `5601`

### 6. **MinIO**
- **Description:** High-performance object storage compatible with AWS S3.
- **Console URL:** [http://localhost:9001](http://localhost:9001)
- **Ports:** 
  - `9000` (S3 API)
  - `9001` (MinIO Console)
- **Credentials:**
  - **Access Key:** `minioadmin`
  - **Secret Key:** `minioadmin`

### 7. **PostgreSQL**
- **Description:** Relational database used as Hive Metastore backend.
- **Port:** `5432`

### 8. **Hive Metastore**
- **Description:** Centralized metadata repository for data lake tables.
- **Port:** `9083`

### 9. **Trino**
- **Description:** Distributed SQL query engine for big data.
- **URL:** [http://localhost:8080](http://localhost:8080)
- **Port:** `8080`

### 10. **Spark with Iceberg**
- **Description:** Unified analytics engine with Apache Iceberg support.
- **Ports:** 
  - `9999`, `9090`, `10000`, `10001`

### 11. **Glue Jupyter Notebooks**
- **Description:** AWS Glue environment for running data transformation scripts.
- **URL:** [http://localhost:8888](http://localhost:8888)
- **Port:** `8888`

### 12. **Iceberg REST Catalog**
- **Description:** REST interface for managing Iceberg table metadata.
- **Port:** `8181`

---

## **How to Use This Repository**

### **1. Prerequisites**
- Install [Docker](https://docs.docker.com/get-docker/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)

---

### **2. Running the Stack**

#### **Start All Services**
```bash
# Navigate to the project directory
cd path/to/your/repository

# Start all services
docker-compose up -d
```

#### **Stop All Services**
```bash
docker-compose down
```

#### **Rebuild Services (if necessary)**
```bash
docker-compose up --build -d
```

---

### **3. Interacting with Services**

#### **Kafka CLI Commands**

**Create a Topic:**
```bash
docker exec -it kafka kafka-topics.sh --create --topic test_topic --bootstrap-server localhost:9092
```

**Produce a Message:**
```bash
docker exec -it kafka kafka-console-producer.sh --broker-list localhost:9092 --topic test_topic
```
Type your message and press **Enter**.

**Consume a Message:**
```bash
docker exec -it kafka kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test_topic --from-beginning
```

---

#### **Trino CLI Commands**

**Access Trino CLI:**
```bash
docker exec -it trino trino
```

**Run a Query in Trino:**
```sql
SHOW CATALOGS;
```

---

#### **Spark Shell**

**Access Spark Shell:**
```bash
docker exec -it spark-iceberg spark-shell
```

---

### **4. Accessing Web Interfaces**

- **Kafka UI:** [http://localhost:8082](http://localhost:8082)
- **Trino:** [http://localhost:8080](http://localhost:8080)
- **MinIO Console:** [http://localhost:9001](http://localhost:9001)
- **Elasticsearch:** [http://localhost:9200](http://localhost:9200)
- **Kibana:** [http://localhost:5601](http://localhost:5601)
- **Glue Jupyter Notebooks:** [http://localhost:8888](http://localhost:8888)

---

## **Volumes and Persistent Data**

- **MinIO Data:** `minio_data`
- **Postgres Data:** `postgres_data`
- **Spark Data:** `spark_data`
- **Elasticsearch Data:** `elastic_data`

These volumes ensure your data persists even if containers are restarted.

---

## **Credentials and Configuration**

### **MinIO Credentials:**
- **Access Key:** `minioadmin`
- **Secret Key:** `minioadmin`

### **Postgres Credentials:**
- **Username:** `hive`
- **Password:** `hive`
- **Database:** `metastore`

### **AWS CLI Credentials (for MinIO):**
- **Access Key:** `minioadmin`
- **Secret Key:** `minioadmin`

---

## **Troubleshooting**

### **Check Service Logs:**
```bash
docker logs kafka  # Replace 'kafka' with any service name to check logs
```

### **Check Network Issues:**
Ensure all services are connected to the `iceberg_net` network:
```bash
docker network inspect iceberg_net
```

---

## **License**

This project is licensed under the MIT License.

---

Enjoy building your data lake and analytics environment! 🚀
