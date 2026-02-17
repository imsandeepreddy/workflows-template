# Workflows Templates Repository

This repository contains centralized, reusable GitHub Actions workflows
used across all application repositories in the organization.

It enforces:
- Standardized CI/CD
- Shift-left security
- Artifact immutability
- Controlled promotions across environments
- Governance & auditability

---

## 🎯 Purpose

Instead of duplicating YAML pipelines in every repo,
we use reusable workflows (`workflow_call`) to maintain:

- Consistency
- Version control
- Secure change management
- Enterprise-grade governance

---

## 📂 Repository Structure

.github/workflows/
│
├── feature-dev.yml
├── develop.yml
├── release.yml
└── prod.yml

Each workflow is designed to be reusable by application repositories.

---

## 🔁 Workflow Model

| Branch Type | Purpose | Security Level |
|-------------|---------|---------------|
| feature/*   | Fast developer CI | Informational |
| develop     | Integration + Security Gate | Enforced |
| release     | Artifact Promotion | No rebuild |
| master      | Production Deploy | Trusted artifact only |

---

## 🏗 Architecture Overview

Feature → Develop → Release → Master

Security gates are completed before stage.
Production deploys pre-approved artifacts only.

---

## 🔐 Secrets Handling

Reusable workflows require secrets to be passed explicitly.

Example definition:

```yaml
on:
  workflow_call:
    secrets:
      SONAR_TOKEN:
        required: true
