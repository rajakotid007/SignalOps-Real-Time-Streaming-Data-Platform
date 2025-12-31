[![LinkedIn][linkedin-shield]][linkedin-url]

<!-- PROJECT LOGO -->
<br />

<p align="center">
  <img src="./images/2.PNG" alt="Logo" width="500" height="300">
  <h2 align="center"><i>SignalOps — Real-Time Streaming Data Pipeline on Docker</i></h2>
</p>

> Apache Hadoop, Apache Spark, Apache ZooKeeper, Kafka, Scala, Python, PySpark, PostgreSQL, Docker, Django, Flexmonster, Real-Time Streaming, Data Pipeline, Monitoring Dashboard

<!-- ABOUT THE PROJECT -->

## About The Project

SignalOps is a **real-time streaming data engineering platform** designed to ingest, process, store, and visualize high-volume event data using a distributed, containerized architecture. The project demonstrates how production-style streaming systems are built using Apache Kafka, Spark Structured Streaming, and Hadoop.

---

### Project Description

* In large-scale data centers, servers continuously generate operational events such as health status, metrics, and system signals in real time.

* These events must be processed immediately to detect anomalies, monitor performance, and support operational decision-making by infrastructure and monitoring teams.

* Due to the volume and velocity of the data, scalable and fault-tolerant technologies are required for ingestion, processing, and storage.

* This project implements a **real-time data pipeline** using Apache Kafka, Apache Spark, Hadoop, PostgreSQL, Django, and Flexmonster — all running on Docker — to generate actionable insights from streaming data.

* The streaming pipeline is built using Apache Spark Structured Streaming with both **Scala and PySpark**, running on a Hadoop cluster deployed via Docker.

* Data visualization and monitoring are implemented using the Django web framework and Flexmonster to provide live dashboards.

---

### Use Case Diagram

![database](./images/3.png)

---

### Proposed Pipeline Architecture

![database](./images/2.PNG)

---

### Built With

* Apache Hadoop
* Apache Spark
* Apache ZooKeeper
* Docker
* Kafka
* Django (IDE used: VS Code)
* Flexmonster
* Scala (IDE used: IntelliJ IDEA)
* Python (IDE used: PyCharm)
* PySpark (IDE used: PyCharm)

---

### Environment Setup

#### (a) Docker Setup

Docker is used to containerize and run all components of the pipeline locally.  
For Windows 10 Home Edition, Docker Toolbox was installed.

During setup, virtualization must be enabled in the BIOS. In some cases, the hypervisor setting must be explicitly disabled if set to "Auto". The following issue and resolution may be encountered:

![database](./images/5.png)



---

#### (b) Create Single Node Kafka Cluster in Local Machine

Run the following commands in the Docker terminal to create a local Kafka and ZooKeeper setup:

| Steps | Commands |
| :---: | :--- |
| Create Docker Network | docker network create --subnet=172.20.0.0/16 datamakingnet |
| Pull ZooKeeper Image | docker pull zookeeper:3.4 |
| Run ZooKeeper | docker run -d --hostname zookeepernode --net datamakingnet --ip 172.20.1.3 --name datamaking_zookeeper --publish 2181:2181 zookeeper:3.4 |
| Pull Kafka Image | docker pull ches/kafka |
| Run Kafka | docker run -d --hostname kafkanode --net datamakingnet --ip 172.20.1.4 --name datamaking_kafka --publish 9092:9092 --publish 7203:7203 --env KAFKA_ADVERTISED_HOST_NAME=192.168.99.100 --env ZOOKEEPER_IP=192.168.99.100 ches/kafka |
| Verify Containers | docker images / docker ps / docker ps -a |


---

#### (c) Create Single Node Apache Hadoop and Spark Cluster on Docker

Run the following steps in the Docker terminal:

| Steps | Commands |
| :---: | :--- |
| Extract Cluster Image | Unzip datamaking_hadoop_spark_cluster_image.zip |
| Navigate Directory | cd datamaking_hadoop_spark_cluster_image |
| Build Images | ./1_create_hadoop_spark_image.sh |
| Create Containers | ./2_create_hadoop_spark_cluster.sh createa |
| Stop Containers | docker stop $(docker ps -a -q) |
| Remove Containers | docker rm $(docker ps -a -q) |
| Remove Images | docker rmi $(docker images -a -q) |

---

### Development Setup

#### (a) Event Simulator Using Python

Run the Python script `data_center_server_status_simulator.py` to simulate continuous server status events in real time.

---

#### (b) Streaming Data Pipeline using Spark Structured Streaming (Scala)

Load `datamaking_streaming_data_pipeline (Scala)` as a Scala project in IntelliJ IDEA and execute the streaming job.

#### OR

#### (b) Streaming Data Pipeline using Spark Structured Streaming (PySpark)

Open `datamaking_streaming_data_pipeline (PySpark)` and run the script `real_time_streaming_data_pipeline.py`.

---

#### (c) PostgreSQL Database Setup (Events Database)

Access the PostgreSQL CLI inside the Docker container and run the following commands:

| Steps |
| :--- |
| psql -U postgres |
| CREATE USER demouser WITH PASSWORD 'demouser'; |
| ALTER USER demouser WITH SUPERUSER; |
| CREATE DATABASE event_message_db; |
| GRANT ALL PRIVILEGES ON DATABASE event_message_db TO demouser; |
| \c event_message_db; |

---

#### (d) Real-Time Dashboard using Django and Flexmonster

Open the `Server Status Monitoring` folder in VS Code and run the Django application to visualize streaming data in real time.

---

### Final Result

The dashboard updates live as new events are generated and processed through the streaming pipeline.

Sample screenshots:

![database](./images/6.PNG)
![database](./images/7.PNG)

---

## Contact

Rajakoti Dasari
Portfolio Website(https://github.com/rajakotid007)

---

<!-- MARKDOWN LINKS & IMAGES -->
[linkedin-url]: www.linkedin.com/in/rajakoti-dasari-a926b0237
