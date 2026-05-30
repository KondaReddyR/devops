# Chapter 08: CI/CD Pipeline Design

## Learning Objectives

- Design CI/CD pipelines for Python data services.
- Separate validation, build, publish, and deployment concerns.
- Promote artifacts safely across environments.

## Pipeline Architecture

```mermaid
flowchart LR
    A["Pull Request"] --> B["CI Validation"]
    B --> C["Merge"]
    C --> D["Build Image"]
    D --> E["Scan"]
    E --> F["Publish"]
    F --> G["Update GitOps"]
    G --> H["ArgoCD Sync"]
```

## Pipeline Stages

- Install dependencies with `uv`
- Lint
- Unit test
- Type check
- Security scan
- Build image
- Image scan
- Publish image
- Update GitOps manifests

## Data Engineering Additions

- contract tests for API schemas
- data quality tests
- migration checks
- pipeline dry runs
- sample file validation

## Knowledge Check

- What belongs in CI?
- What belongs in CD?
- Why should deployments use immutable image tags?
- How does artifact promotion reduce risk?

## Confidence Checklist

- I can design a pipeline from commit to deployment.
- I can explain quality gates.
- I can connect CI output to GitOps input.
- I can add data-specific validation.

