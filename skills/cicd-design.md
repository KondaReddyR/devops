# Skill: CI/CD Design

## Trigger

`Run the CI/CD design skill`

## Purpose

Create a pipeline from source code to deployable, scanned container image.

## Pipeline

```mermaid
flowchart LR
    A["Commit"] --> B["Lint"]
    B --> C["Test"]
    C --> D["Security Scan"]
    D --> E["Build Image"]
    E --> F["Image Scan"]
    F --> G["Publish Image"]
    G --> H["Update GitOps Repo"]
```

## Required Stages

- Checkout
- Install with `uv`
- Lint with `ruff`
- Test with `pytest`
- Type check
- Dependency scan
- Build image
- Image scan
- Publish image
- Update deployment metadata

## Done When

- Pipeline is reproducible.
- Failing tests block promotion.
- Critical vulnerabilities block image publishing.
- Build output is traceable to a commit SHA.

