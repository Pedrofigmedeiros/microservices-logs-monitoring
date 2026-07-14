# Microservices Logs Monitoring

A hands-on observability platform built to study and experiment with **Java**, **Spring Boot**, and the **Elastic Stack** by simulating a real-world microservices environment.

The project demonstrates how modern backend applications generate, collect, process, store, search, and visualize logs using an end-to-end pipeline composed of:

- Java 21
- Spring Boot 3
- Elasticsearch
- Logstash
- Filebeat
- Kibana
- Docker & Docker Compose

The long-term goal is to build a production-inspired observability platform capable of ingesting and analyzing structured logs from multiple microservices while following modern software engineering and search infrastructure best practices.

---

# Architecture

```text
                Spring Boot Services
                       │
                 Structured JSON Logs
                       │
                  Filebeat
                       │
                   Logstash
                       │
               Elasticsearch Cluster
                       │
                    Kibana
```

The first service developed in this repository is an **Order Service**, responsible for generating realistic application logs that will later be processed by the Elastic Stack.

Future services may include:

- Order Service
- Payment Service
- Inventory Service
- Notification Service
- API Gateway

---

# Technologies

## Java 21 (LTS)

The application is written in **Java 21 LTS**, the current long-term support release of the Java platform.

Java provides:

- Platform independence through the JVM
- Strong typing
- Excellent performance with the Just-In-Time (JIT) compiler
- Mature ecosystem for enterprise backend development

---

## Spring Boot

The backend services are built with **Spring Boot 3**.

Spring Boot simplifies Java application development by providing:

- Embedded Tomcat
- Dependency Injection
- Auto Configuration
- REST API development
- Production-ready monitoring through Spring Boot Actuator
- Convention over configuration

---

## Elastic Stack

The observability platform is built around the Elastic Stack.

### Elasticsearch

- Full-text search
- Distributed indexing
- Aggregations
- Near real-time search
- Clustered architecture

### Logstash

Responsible for:

- Parsing logs
- Data transformation
- Enrichment
- Routing events
- Pipeline processing

### Filebeat

Responsible for collecting application logs and forwarding them to Logstash.

### Kibana

Provides:

- Dashboards
- Discover
- Visualizations
- Monitoring
- Log exploration

---

# Repository Structure

```text
microservices-logs-monitoring/

├── services/
│   └── order-service/
│
├── elasticsearch/
│
├── logstash/
│
├── filebeat/
│
├── kibana/
│
├── docker/
│
├── scripts/
│
├── docker-compose.yml
│
└── README.md
```

---

# Current Progress

- [x] Java 21 environment
- [x] Spring Boot project
- [x] Maven Wrapper
- [x] Docker environment
- [ ] Structured JSON logging
- [ ] Filebeat integration
- [ ] Logstash pipeline
- [ ] Elasticsearch cluster
- [ ] Kibana dashboards
- [ ] Distributed tracing
- [ ] Alerts
- [ ] Multi-service environment

---

# Running the Spring Boot Application

Requirements

- Java 21
- Docker
- Docker Compose

Start the application:

```bash
cd services/order-service
./mvnw spring-boot:run
```

The application will start on:

```
http://localhost:8080
```

Health endpoint:

```
http://localhost:8080/actuator/health
```

---

# Learning Goals

This project is intended to provide practical experience with:

- Java
- Spring Boot
- Docker
- Elasticsearch
- Logstash
- Filebeat
- Kibana
- Distributed Systems
- Structured Logging
- Observability
- Search Infrastructure
- Production-ready backend architecture
