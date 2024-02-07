# Realtime Streaming Project

## Overview

This project demonstrates a real-time streaming pipeline using Apache Kafka, Apache Spark, and Apache Airflow. It includes two main scripts:

- `kafka_stream.py`: Fetches user data from a public API, formats it, and streams it to a Kafka topic named 'users_created'.
- `spark_streams.py`: Consumes data from the 'users_created' Kafka topic, processes it, and stores it in a Cassandra database.

## Kafka Stream Script - kafka_stream.py

The `kafka_stream.py` script performs the following tasks:

1. Fetches user data from the [Random User Generator API](https://randomuser.me/api/).
2. Formats the data.
3. Streams the formatted data to the 'users_created' Kafka topic.

The Kafka producer is configured to connect to a Kafka broker running at `broker:29092`.

## Spark Streams Script - spark_streams.py

The `spark_streams.py` script performs the following tasks:

1. Connects to Kafka and consumes data from the 'users_created' topic.
2. Creates a Spark DataFrame from the Kafka stream.
3. Establishes a connection to a Cassandra database.
4. Defines a schema for the data and inserts it into the 'created_users' table in Cassandra.

The script utilizes Apache Spark and Cassandra to process and store the streaming data.

## Docker Compose Configuration - docker_compose.yml

The `docker_compose.yml` file defines a Docker Compose configuration with the following services:

- Zookeeper: Used by Kafka for distributed coordination.
- Kafka Broker: Kafka message broker.
- Schema Registry: Centralized schema management for Kafka.
- Control Center: Web-based interface for managing and monitoring Kafka.
- Apache Airflow: Used for orchestrating and scheduling data streaming tasks.
- Spark Master and Worker: Apache Spark cluster components.
- Cassandra: NoSQL database for storing processed data.

## Entry Point Script - entrypoint.sh

The `entrypoint.sh` script is executed when starting the Airflow webserver container. It handles package installations and initializes the Airflow database if it doesn't exist.

## Getting Started

To run the project locally, make sure you have Docker and Docker Compose installed. Then, execute:

```bash
docker-compose up
