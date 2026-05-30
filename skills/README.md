# Reusable Cloud Skills

These files are lightweight operational playbooks. They are designed to be triggered repeatedly by an engineer or AI agent.

They are not installed Codex skills. They are repository-local skill equivalents for common DevOps activities.

## Trigger Convention

Use phrases like:

- `Run the OpenShift deploy skill`
- `Run the Vault integration skill`
- `Run the CI/CD design skill`
- `Run the observability skill`
- `Run the Git hygiene skill`

## Available Skills

| Skill | File | Purpose |
| --- | --- | --- |
| Git hygiene | `git-hygiene.md` | Version control workflow and review discipline |
| OpenShift app deploy | `openshift-app-deploy.md` | Deploy a data service to OpenShift |
| Vault integration | `vault-integration.md` | Manage sensitive data with HashiCorp Vault |
| CI/CD design | `cicd-design.md` | Build repeatable pipelines |
| Observability | `observability.md` | Add logs, metrics, traces, and dashboards |
| Security scan | `security-scan.md` | Scan code, dependencies, and images |

