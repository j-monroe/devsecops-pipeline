# devsecops-pipeline

A reference **DevSecOps CI pipeline** that shifts security left by running automated checks (code quality + security scanning) on every change. Use this repo as a starting point/template for adding security gates to your CI.

## What this repo does

On push / pull request, the pipeline can run:

- **SCA (dependency vulnerability scanning)** (e.g., OWASP Dependency-Check)
- **Secrets scanning** (to prevent committing credentials)
- **SAST** (static analysis on application code)
- Optional: **IaC scanning** (Terraform/Kubernetes manifests), **container image scanning**, **DAST**
- Report generation and artifacts upload for review/auditing

> Note: The repository currently includes Dependency-Check report artifacts (JSON) in the root (e.g. `dependency-check-report-*.json`), which are useful as sample outputs.

## CI/CD Platform

- **GitHub Actions** (recommended/default for this repo)

If you’re using another CI system (GitLab CI, Jenkins), you can still reuse the tooling and scripts, but the workflow definitions will differ.

## Tooling (typical choices)

You can mix and match; common options:

- **SCA**: OWASP Dependency-Check, Dependabot, Snyk
- **Secrets**: Gitleaks, TruffleHog
- **SAST**: CodeQL, Semgrep, SonarQube
- **IaC**: Checkov, tfsec, Terrascan
- **Containers**: Trivy, Grype
- **SBOM**: Syft (CycloneDX/SPDX)
- **Signing/Attestation**: Cosign + OIDC (keyless), SLSA provenance

## Repository structure

Typical layout (adjust to match your repo):

- `.github/workflows/` – GitHub Actions workflows (CI security pipeline)
- `scripts/` – helper scripts to run scanners locally (optional)
- `reports/` – generated scanner outputs (optional; often kept as CI artifacts)

## Getting started

### Prerequisites

- Git
- (Optional) Docker, if you run scanners in containers
- Language toolchain(s) for your project (Node/Java/Python/etc.) if applicable

### Run scans locally (example)

If you add scripts, keep the interface consistent, e.g.:

```bash
# examples (create scripts to match your tooling)
./scripts/scan-secrets.sh
./scripts/scan-deps.sh
./
