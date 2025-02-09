---

# Data Lake and Analytics Stack with Docker Compose

This repository sets up a complete **data lake and analytics environment** using Docker Compose. It integrates multiple services like **Kafka**, **Trino**, **Spark**, **MinIO**, **Elasticsearch**, **Kibana**, and **Glue Jupyter Notebooks** for seamless data ingestion, querying, and analytics.

---

## **Latest Update**
- **Removed Zookeeper** and transitioned to **KRaft Mode** for Kafka to simplify the setup and improve performance.
- **Removed Hive Metastore** to streamline the architecture and reduce dependencies.

---

## **Services Overview**

### 1. **Kafka**
- **Description:** Distributed streaming platform for building real-time data pipelines, now using **KRaft mode** (no Zookeeper required).
- **Ports:** 
  - `9092` (Internal Broker)
  - `29092` (External Broker)

### 2. **Kafka UI**
- **Description:** Web interface for managing and monitoring Kafka clusters.
- **URL:** [http://localhost:8083](http://localhost:8083)
- **Port:** `8083`

### 3. **Elasticsearch**
- **Description:** Distributed search and analytics engine.
- **URL:** [http://localhost:9201](http://localhost:9201)
- **Ports:** 
  - `9201` (HTTP API)
  - `9301` (Transport Layer)

### 4. **Kibana**
- **Description:** Visualization tool for Elasticsearch.
- **URL:** [http://localhost:5602](http://localhost:5602)
- **Port:** `5602`

### 5. **MinIO**
- **Description:** High-performance object storage compatible with AWS S3.
- **Console URL:** [http://localhost:9001](http://localhost:9001)
- **Ports:** 
  - `9000` (S3 API)
  - `9001` (MinIO Console)
- **Credentials:**
  - **Access Key:** `minioadmin`
  - **Secret Key:** `minioadmin`

### 6. **Trino**
- **Description:** Distributed SQL query engine for big data.
- **URL:** [http://localhost:8080](http://localhost:8080)
- **Port:** `8080`

### 7. **Glue Jupyter Notebooks**
- **Description:** AWS Glue environment for running data transformation scripts.
- **URL:** [http://localhost:8888](http://localhost:8888)
- **Port:** `8888`

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

#### **Access Glue Jupyter Notebooks**
Visit [http://localhost:8888](http://localhost:8888) to use AWS Glue Jupyter Notebooks for data transformation.

---

## **Volumes and Persistent Data**

- **MinIO Data:** `minio_data`
- **Postgres Data:** `postgres_data`
- **Elastic Data:** `elastic_data`

These volumes ensure your data persists even if containers are restarted.

---

## **Credentials and Configuration**

### **MinIO Credentials:**
- **Access Key:** `minioadmin`
- **Secret Key:** `minioadmin`

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

