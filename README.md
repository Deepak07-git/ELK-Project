# ELK Project

This repository contains Docker Compose files and configuration for a small ELK stack (Elasticsearch, Logstash, Kibana) plus Filebeat example configuration.

## Contents
- docker-compose.yml — services: Elasticsearch, Kibana, Logstash
- ilebeat.yml — sample Filebeat settings
- logstash.conf — example Logstash pipeline

## Run locally with Docker Compose (recommended)
1. Ensure Docker Desktop is installed and running.
2. From the repository root:

`powershell
# Start the stack
docker compose up -d

# Check container status
docker compose ps

# View logs
docker compose logs -f
`

## Notes
- Elasticsearch needs to finish bootstrapping before creating enrollment tokens.
- For production use, add persistent volumes and secure credentials.
