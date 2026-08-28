# ELK Stack Centralized Logging & Monitoring

A centralized logging and monitoring solution built using the **ELK Stack (Elasticsearch, Logstash, and Kibana)** along with **Filebeat** and **Docker Compose**.

This project demonstrates how logs from different sources can be collected, processed, indexed, and visualized in a centralized platform.

---

## 📌 Project Overview

Modern applications generate logs from multiple sources such as web servers, applications, databases, and security systems. Managing these logs manually can be difficult.

This project implements a centralized logging pipeline where:

1. **Filebeat** collects log data.
2. **Logstash** processes and parses the logs.
3. **Elasticsearch** stores and indexes the processed data.
4. **Kibana** provides visualization and log exploration.

The entire setup runs locally using **Docker Compose**.

---

## 🏗️ Architecture

```text
                 ┌─────────────────┐
                 │   Sample Logs   │
                 │ Web / App / Sys │
                 └────────┬────────┘
                          │
                          ▼
                    ┌───────────┐
                    │ Filebeat  │
                    │ Log Agent │
                    └─────┬─────┘
                          │
                          ▼
                    ┌───────────┐
                    │ Logstash  │
                    │ Processing│
                    │ & Parsing │
                    └─────┬─────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │ Elasticsearch   │
                 │ Storage & Index │
                 └────────┬────────┘
                          │
                          ▼
                    ┌───────────┐
                    │  Kibana   │
                    │ Dashboard │
                    │ & Explore │
                    └───────────┘
```

---

## 🛠️ Technologies Used

- **Elasticsearch** – Log storage and indexing
- **Logstash** – Log processing and parsing
- **Kibana** – Log visualization and analysis
- **Filebeat** – Log collection and forwarding
- **Docker** – Containerization
- **Docker Compose** – Multi-container orchestration
- **Azure Pipelines** – CI configuration

---

## 📂 Project Structure

```text
ELK-Project/
│
├── docker-compose.yml
├── filebeat.yml
├── logstash.conf
├── azure-pipelines.yml
├── .gitignore
│
├── logs/
│   └── sample_logs.log
│
└── kibana_saved_objects/
    └── dashboard configuration files
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

- Docker Desktop
- Docker Compose

Verify the installation:

```bash
docker --version
docker compose version
```

---

## ▶️ Run the ELK Stack

Clone the repository:

```bash
git clone <your-repository-url>
cd ELK-Project
```

Start all services:

```bash
docker compose up -d
```

Check container status:

```bash
docker compose ps
```

View logs:

```bash
docker compose logs -f
```

To stop the stack:

```bash
docker compose down
```

---

## 📊 Log Ingestion Flow

The project includes a sample log file containing different types of logs, including:

- Web server logs
- System logs
- Application logs
- Security and authentication logs
- Audit logs

Filebeat reads the logs and forwards them to Logstash.

Logstash attempts to parse the logs using:

1. JSON parsing
2. Grok patterns
3. Key-value parsing

The processed logs are then indexed into Elasticsearch.

Example index:

```text
college-logs-*
```

---

## 🔍 Exploring Logs in Kibana

After starting the ELK stack:

1. Open Kibana in your browser.
2. Navigate to **Discover**.
3. Create a data view using:

```text
college-logs-*
```

4. Explore the ingested logs.
5. Create visualizations and dashboards.

You can analyze events such as:

- HTTP 500 errors
- Failed login attempts
- Application errors
- Database errors
- Security events

---

## 🧪 Testing with Sample Logs

The repository includes:

```text
logs/sample_logs.log
```

Filebeat continuously reads this file and forwards new events through the pipeline.

You can append a new test log entry using PowerShell:

```powershell
Add-Content -Path .\logs\sample_logs.log -Value '203.0.113.99 - - [29/Nov/2025:11:00:01 +0000] "GET /metrics HTTP/1.1" 200 1234 "-" "curl/7.68.0"'
```

After adding the log, check Kibana to verify that the event has been indexed successfully.

---

## ⚙️ Log Parsing

The Logstash pipeline supports multiple log formats.

The processing flow attempts:

```text
JSON
   ↓
Grok Parsing
   ↓
Key-Value Parsing
```

Parsed fields are stored using nested fields such as:

```text
kv_parsed
app_kv
```

This helps avoid mapping conflicts with Elasticsearch Common Schema (ECS) fields.

---

## ⚠️ Notes

- Elasticsearch may take some time to finish bootstrapping.
- Filebeat runs with root permissions in the development container to allow access to mounted log files.
- This project is intended for learning and local development.

For a production environment, additional configuration would be required, including:

- Persistent volumes
- Secure credentials
- Authentication and authorization
- TLS/SSL encryption
- Resource limits
- Monitoring and alerting

---

## 🎯 Key Learnings

Through this project, I gained hands-on experience with:

- Centralized logging architecture
- Docker and Docker Compose
- Elasticsearch indexing
- Logstash pipelines
- Grok pattern parsing
- Filebeat configuration
- Kibana log exploration
- Processing multiple log formats
- Basic CI configuration using Azure Pipelines

---

## 👨‍💻 Author

**Deepak S**

Aspiring Engineer interested in:

☁️ Cloud & DevOps | 🤖 AI/ML | 📊 Data Analytics

---

⭐ Feel free to explore the repository and project files!
