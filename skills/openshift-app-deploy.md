# Skill: OpenShift App Deploy

## Trigger

`Run the OpenShift deploy skill`

## Purpose

Deploy a Python data service to OpenShift using repeatable manifests.

## Inputs

- Namespace
- Image reference
- App name
- Port
- ConfigMap values
- Secret or Vault reference

## Steps

1. Verify login:

   ```bash
   oc whoami
   oc project
   ```

2. Create or select namespace:

   ```bash
   oc new-project data-devops-lab
   ```

3. Apply manifests:

   ```bash
   oc apply -k deploy/overlays/dev
   ```

4. Watch rollout:

   ```bash
   oc rollout status deploy/<app-name>
   oc get pods
   oc get route
   ```

5. Validate endpoint:

   ```bash
   curl https://<route>/health
   ```

## Done When

- Pods are ready.
- Route responds.
- Logs are visible.
- Progress tracker contains deployment evidence.

