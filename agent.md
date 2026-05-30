# Agent Operating Brief

This repository is a DevOps enablement curriculum for an experienced Python data engineer.

## Mission

Help the learner move from data engineering application development to independent DevOps support for data and application teams.

The learning path covers:

- Modern Python delivery with `uv`
- Dependency and virtual environment management
- FastAPI services for data APIs
- Batch and pipeline-adjacent service patterns
- Containers with Docker or Podman
- Vulnerability scanning
- Container publishing
- CI/CD design
- OpenShift deployment
- ArgoCD GitOps
- HashiCorp Vault for sensitive data
- Configuration and secrets
- Logging, metrics, tracing, OpenTelemetry, OpenMetrics
- Prometheus, Grafana, Datadog, and distributed tracing
- CNCF ecosystem and platform engineering
- Version control from basic Git usage to release governance
- AI-assisted development and operations

## Local Cluster Facts

- API: `https://api.okd.rhels.com:6443`
- Console: `https://console-openshift-console.apps.okd.rhels.com`
- ArgoCD route: `https://argocd-server-argocd.apps.okd.rhels.com`
- OKD version: `4.21.0-okd-scos.7`
- Kubernetes version: `v1.34.2`
- Single-node cluster
- ArgoCD, OpenShift monitoring, Datadog, and Kyverno are installed
- Internal OpenShift image registry is removed
- No storage class is currently configured
- Machine Config Operator is degraded
- Kyverno pods have high restart counts

## Agent Behavior

When continuing this curriculum:

1. Preserve the book structure: one chapter per topic.
2. Keep each chapter focused on one major concept.
3. Add hands-on work that fits a data engineer: APIs, data pipelines, batch jobs, schedules, object storage, databases, lineage, and observability for data workloads.
4. Update `progress/status.md` whenever a topic is started, completed, or changed.
5. Add or update a Reveal.js deck for every chapter.
6. Add reusable repeated activities under `skills/`.
7. Prefer Mermaid diagrams for lifecycle, architecture, GitOps, CI/CD, and observability flows.
8. Avoid storing secrets in Git.
9. Use Vault for sensitive values in examples.
10. Treat the OpenShift cluster as a learning platform, not production.

## Definition of Done for a Chapter

A chapter is complete when it has:

- Learning objectives
- Data-engineering context
- Core concepts
- Hands-on lab
- Commands or manifests where useful
- Mermaid diagram
- Knowledge check
- Confidence checklist
- Related slide deck

