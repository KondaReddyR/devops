# Skill: Observability

## Trigger

`Run the observability skill`

## Purpose

Add useful operational signals to a data service or data workload.

## Signals

- Logs: structured events with request IDs and job IDs
- Metrics: request rate, errors, duration, data records processed, lag
- Traces: request flow and downstream dependency timing

## Steps

1. Add structured JSON logging.
2. Expose Prometheus/OpenMetrics metrics.
3. Add OpenTelemetry instrumentation.
4. Add dashboards for service and data workload signals.
5. Add alerts for user-impacting or data-quality-impacting symptoms.

## Data Engineering Metrics

- Records processed
- Failed records
- Pipeline duration
- Freshness lag
- Source read latency
- Sink write latency
- Duplicate count
- Schema validation failures

## Done When

- A failure can be diagnosed from logs, metrics, and traces.
- The dashboard answers: is it healthy, slow, wrong, or stuck?

