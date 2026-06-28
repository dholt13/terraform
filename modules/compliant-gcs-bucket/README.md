# Lab 2.4: Terraform Modules for Compliance (GCP)

In this lab I deployed a module that deploys buckets, and the security floor sits inside the module where consumers can't reach it.

## Learning objectives

- Compose a Terraform module with a clear interface: inputs, outputs, hardcoded compliance defaults.
- Encode the following NIST Family controls so they cannot be turned off by a consumer.:
    - SC-12: States how you generate, protect, distribute, and destroy cryptographic keys used to secure data.
    - SC-13: Requires cryptographic protection for sensitive data both in transit and at rest.
    - SC-28: protects sensitive data at rest. 
    - AU-11: defines how long you have to store audit and event logs.
    - CM-6: Enforces a strict security configuration baselines for all hardware and software.
- Emit a compliance attestation as a module output that downstream labs consume as evidence.

### Concept: Design the interface

Three rules:

1. `main.tf` hardcodes anything compliance-relevant: encryption, uniform access, versioning, retention behavior, required labels.
2. `variables.tf` exposes only what business actually changes: project, environment, retention duration, names.
3. `outputs.tf` returns evidence: identifiers, plus a computed `compliance_attestation` map.

## Testing

For testing, I created separate dev (30-day retention) and prod (365-day retention) environments. Then I created a compliance check that fails a deployment if a consumer attempts to alter the strict 365-day retention policy in production.
