## Kibana saved objects

This folder contains saved objects (NDJSON format) you can import in Kibana → Stack Management → Saved Objects → Import.

- `index-pattern.ndjson` — saved object that creates a `college-logs-*` data view (index pattern). Import this first so visualizations and dashboards can reference it.

How to import:

1. Open Kibana (http://localhost:5601)
2. Go to Stack Management → Saved Objects → Import
3. Choose `kibana_saved_objects/index-pattern.ndjson` and import

After importing you can create visualizations + dashboards in the UI or import additional saved objects.
