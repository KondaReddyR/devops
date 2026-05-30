# Skill: Security Scan

## Trigger

`Run the security scan skill`

## Purpose

Find vulnerabilities before code or containers are promoted.

## Steps

1. Scan source:

   ```bash
   ruff check .
   bandit -r app
   ```

2. Scan dependencies:

   ```bash
   pip-audit
   ```

3. Scan filesystem and image:

   ```bash
   trivy fs .
   trivy image <image>
   ```

4. Generate SBOM:

   ```bash
   syft <image> -o spdx-json
   ```

5. Record findings and fixes.

## Done When

- High and critical findings are understood.
- Accepted risks are documented.
- Fixed findings are verified by a repeat scan.

