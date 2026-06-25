# Enterprise ELK Stack Pipeline for Microservices Log Management

A production-grade, highly available, and fully encrypted **ELK Stack pipeline** designed for centralized log management and real-time observability across **distributed microservices architectures**. 

This platform leverages a resilient **6-Node Elasticsearch Cluster** (partitioned into dedicated Master and Data tiers) to ingest, index, and analyze high-throughput log streams, trace data, and container telemetry.

---

## 1. Core Architecture & Pipeline Flow

The ecosystem is engineered to handle chaotic log streams from decoupled microservices (e.g., API Gateways, Auth Services, Payment Processing units) by isolating master consensus from indexing operations.



* **Ingestion Layer:** Accepts structured JSON logs, exception stack traces, and HTTP request metrics from containerized application runtimes.
* **Storage & Indexing Layer (The 6-Node Core):** Splitting the cluster prevents heavy aggregation queries (e.g., searching for a critical error across millions of logs) from degrading the cluster state or breaking node consensus.
* **Observability Layer (Kibana):** A secure, unified cockpit for engineering teams to build APM dashboards, track error rates, and monitor distributed transaction traces.

---

## 2. Infrastructure Breakdown (Topology Map)

| Service Name | Dedicated Role | Mission-Critical Purpose in Microservices |
| :--- | :--- | :--- |
| `setup` | Cryptographic Engine | Automated $TLS$/$SSL$ factory. Secures the log transit pipelines before any node exposed interface wakes up. |
| `es-master01` | Cluster State Leader | Manages global cluster metadata, dynamic index templates, and master state distribution. |
| `es-master02`, `03` | Master Quorum | Prevents split-brain state scenarios during high-concurrency log traffic spikes. |
| `es-data01`, `02`, `03` | Shard Data Tier | Stores the actual application log shards, handles historical rollups, and executes text search queries. |
| `kibana` | Observability UI | The centralized dashboard interface mapped to port `5601`. |

---

## 3. Distributed Security Architecture (Zero-Trust Network)

Because microservices often handle sensitive user payloads and access tokens, network eavesdropping is prevented through mandatory cryptographic enforcement:

* **Internal Mesh Security (Transport Layer / Port 9300):** Cross-node synchronization and master election traffic are encrypted out-of-the-box. Foreign rogue containers cannot inject data into the cluster.
* **REST API Security (HTTP Layer / Port 9200):** Plaintext HTTP is blocked. Log shippers (like Filebeat, Logstash, or native application appenders) must communicate strictly over **HTTPS** using the generated `ca.crt`.

---

## 4. Quickstart Deployment Guide

### Step 1: Adjust Host Virtual Memory (Linux Host)
Elasticsearch uses `mmapfs` to persist log indices efficiently. Run these commands on your host virtual machine to prevent kernel allocation panics:
```bash
sudo sysctl -w vm.max_map_count=262144
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf