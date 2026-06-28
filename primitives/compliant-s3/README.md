# Lab 2.4: Terraform Modules for Compliance (GCP)

In this lab I deployed a single S3 bucket that satisfies five NIST 800-53 controls, SC-28, AU-3, AU-6, CM-6, AC-3, and produce machine-readable evidence of every one. No screenshots.

## Learning objectives

- Express NIST 800-53 controls as Terraform resources, citing each control where it's enforced.
- Capture pre- and post-deploy compliance evidence as JSON instead of screenshots.
- Build a primitive that the rest of the CGE-P labs will reuse and verify automatically.

### Concept: Design the interface

Three rules:

1. `main.tf` hardcodes anything compliance-relevant: encryption, uniform access, versioning, retention behavior, required labels.
2. `variables.tf` exposes only what business actually changes: project, environment.
3. `outputs.tf` returns evidence: identifiers.