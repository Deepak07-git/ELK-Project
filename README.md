 
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

## Testing with provided sample logs

This repo now includes `sample_logs.log` (mixed web, syslog, app, and security/audit lines) and a `filebeat` service in `docker-compose.yml` that mounts both `filebeat.yml` and `sample_logs.log`.

To test ingestion:

1. Start the stack:

```powershell
docker compose up -d
```

2. Filebeat (running as a container) will read `sample_logs.log` and forward events to Logstash which indexes them into `college-logs-*`.

3. Open Kibana → Discover and create an index pattern (e.g. `college-logs-*`) to explore the ingested documents.

4. Use sample queries or visualizations to surface HTTP 500s, failed logins, DB errors etc.

Parsing notes: Logstash is configured to try JSON parsing first and then fall back to grok + kv parsing for mixed logs (Apache/Nginx combined access logs, syslog/auth entries, application logs with levels, and key=value audit lines). Parsed fields are written using nested fields (e.g. `kv_parsed` / `app_kv`) to avoid mapping conflicts with ECS top-level fields.

If Filebeat logs show `permission` errors, the service runs as root in the container to allow reading the mounted file in the development setup.

Append new test lines to `logs/sample_logs.log` to exercise parsing and trigger indexing. Example (PowerShell):

```powershell
Add-Content -Path .\logs\sample_logs.log -Value '203.0.113.99 - - [29/Nov/2025:11:00:01 +0000] "GET /metrics HTTP/1.1" 200 1234 "-" "curl/7.68.0"'
```
