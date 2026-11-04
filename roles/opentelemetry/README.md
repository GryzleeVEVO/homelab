# OTEL role

Role for installing and configuring OTEL components on bare metal.

- **Alloy** is a service that centralizes the collection and processing of
    telemetry data (metrics, traces, logs, etc...).
- **`node_exporter`** is a Prometheus-compatible system metrics exporter.

## Requirements

No requirements.

## Tags

- `alloy`: Install Alloy
- `node_exporter`: Install `node_exporter`

## Role Variables

- `alloy_monitor_services`: Select which services to include in the pipeline.
- `alloy_loki_endpoint`: Path to the destination Loki API endpoint.

## Dependencies

Some tasks depend on the `grafana.grafana` collection.

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - otel
```
