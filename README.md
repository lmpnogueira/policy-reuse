# Reusing Policy-as-Code Across CI/CD and Kubernetes Admission Control

This repository contains the replication package associated with the paper:

> **Reusing Policy-as-Code Across CI/CD and Kubernetes Admission Control: An Empirical Assessment of Governance Consistency**

The repository provides the experimental artefacts used to evaluate the reuse of Policy-as-Code definitions across Continuous Integration (CI) validation and Kubernetes admission control. All policies, test cases, admission-control configurations, automation scripts, and evaluation results required to reproduce the study are included.

## Overview

Policy-as-Code (PaC) has emerged as an important mechanism for automating governance, security, and compliance enforcement within cloud-native software delivery pipelines. However, organisations frequently maintain separate policy implementations across different enforcement stages, increasing maintenance effort and creating opportunities for policy drift.

This study evaluates a reusable multi-stage Policy-as-Code enforcement model in which the same Open Policy Agent (OPA) Rego policies are executed during:

* Continuous Integration (CI) validation using Conftest;
* Kubernetes admission control using OPA Gatekeeper.

The evaluation investigates:

1. Automatic detection of insecure Kubernetes configurations;
2. Governance assurance through multi-stage enforcement;
3. Mitigation of CI bypass scenarios through Kubernetes admission control.

## Repository Structure

```text
.
├── docs/                  # Supporting documentation
├── gatekeeper/            # Gatekeeper ConstraintTemplates and Constraints
├── policies/
│   └── kubernetes/        # Rego policy definitions
├── results/              # Experimental outputs and validation results
├── scripts/              # Automation and execution scripts
├── tests/                # Evaluation manifests and test scenarios
└── README.md
```

### Directory Description

| Directory              | Purpose                                                                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `docs/`                | Supporting documentation describing the evaluation artefacts and execution process.                                                  |
| `gatekeeper/`          | OPA Gatekeeper ConstraintTemplates and Constraints used during admission-control validation.                                         |
| `policies/kubernetes/` | Reusable Rego policies evaluated across both enforcement stages.                                                                     |
| `results/`             | Validation outputs and experimental results generated during the study.                                                              |
| `scripts/`             | Helper scripts used to execute validation workflows and collect results.                                                             |
| `tests/`               | Kubernetes manifests used throughout the evaluation, including compliant configurations, policy violations, and CI bypass scenarios. |

Together, these artefacts provide the materials required to reproduce the experimental evaluation presented in the paper.

## Experimental Dataset

The evaluation dataset comprises:

| Item                      | Value |
| ------------------------- | ----- |
| Kubernetes manifests      | 29    |
| Experimental scenarios    | 37    |
| Kubernetes resource types | 8     |
| Governance policies       | 5     |
| Rego deny rules           | 9     |
| Policy assertions         | 261   |

The dataset includes:

* compliant workloads;
* negative-control resources;
* single-policy violations;
* multi-policy violations;
* CI bypass scenarios.

## Governance Policies

The evaluation considers five representative Kubernetes governance policies:

| Policy ID | Description                           |
| --------- | ------------------------------------- |
| P1        | No Root Execution                     |
| P2        | No Privilege Escalation               |
| P3        | Resource Requests and Limits Required |
| P4        | No Mutable Image Tags (`latest`)      |
| P5        | No Privileged Containers              |

These policies are implemented as reusable Rego definitions and evaluated across multiple enforcement stages.

## Reproducing the Evaluation

### CI Validation

Policy validation can be executed using Conftest and the policies available under `policies/kubernetes/`.

Example:

```bash
conftest test tests/
```

Validation failures generate policy-violation reports suitable for integration into CI/CD pipelines.

### Kubernetes Admission Control

Admission-control validation is performed using OPA Gatekeeper.

Deploy Gatekeeper and apply the ConstraintTemplates and Constraints contained in the `gatekeeper/` directory:

```bash
kubectl apply -f gatekeeper/
```

Evaluation manifests from the `tests/` directory can then be submitted to the cluster to reproduce the admission-control scenarios used in the study.

## Research Questions

The experimental evaluation addresses the following research questions:

**RQ1:** Can Policy-as-Code enforcement detect insecure Kubernetes configurations automatically?

**RQ2:** Does multi-stage enforcement strengthen governance assurance compared with reliance on a single enforcement boundary?

**RQ3:** Can Kubernetes admission control mitigate governance failures caused by CI bypass scenarios?

## Replication Artefacts

This repository includes:

* reusable Rego policies;
* Kubernetes evaluation manifests;
* Gatekeeper admission-control configurations;
* experimental scenarios;
* automation scripts;
* validation outputs;
* supporting documentation.

These artefacts are intended to support transparency, reproducibility, and independent verification of the results reported in the paper.

## Citation

If you use this repository in academic work, please cite the associated paper.

```text
[ Citation details will be added upon publication. ]
```

## License

This repository is released for research and educational purposes. Please refer to the repository license for usage conditions.
