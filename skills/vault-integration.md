# Skill: Vault Integration

## Trigger

`Run the Vault integration skill`

## Purpose

Manage sensitive data with HashiCorp Vault instead of storing secrets in Git.

## Pattern

```mermaid
flowchart LR
    A["OpenShift Workload"] --> B["Service Account"]
    B --> C["Vault Kubernetes Auth"]
    C --> D["Vault Policy"]
    D --> E["KV Secret"]
    E --> F["Runtime Secret Injection"]
```

## Steps

1. Identify the sensitive values.
2. Create a Vault path for the app, for example:

   ```text
   kv/data/data-devops/dev/fastapi-demo
   ```

3. Define least-privilege Vault policy.
4. Configure Kubernetes auth for the OpenShift service account.
5. Choose injection approach:

   - Vault Agent Injector
   - External Secrets Operator
   - CSI Secrets Store
   - App-level Vault client

6. Validate that no secret value is committed to Git.
7. Rotate the secret and confirm the application still works.

## Done When

- Secret is stored in Vault.
- Workload can read it.
- Git contains references, not values.
- Rotation procedure is documented.

