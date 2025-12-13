# GitHub Actions – Shared Workflow Library

This repository contains **reusable GitHub Actions workflows** (shared YAML files) that can be consumed by multiple repositories.  
Instead of duplicating CI logic in every project, teams can reference these workflows directly from their main CI files.

---

## Purpose

- Centralize CI/CD logic in one place
- Enforce consistent Terraform standards across repositories
- Reduce duplication and maintenance effort
- Enable easy updates to CI behavior without changing every repo

---

## How It Works

- This repository hosts **shared workflows** under:

.github/workflows/

- Other repositories **do not copy** these YAML files
- Instead, they **reference them using `uses:`** in their own CI pipeline

---

## Repository Structure
github-actions-library/
├── .github/
│ └── workflows/
│ ├── terraform-fmt.yml
│ └── terraform-validate.yml
├── .....
└── README.md


---

## Using a Shared Workflow in Another Repo

In your application or infrastructure repository, create a CI file  
(e.g., `.github/workflows/ci.yml`) and reference the shared workflow.

### Example

```yaml
name: CI

on:
  push:
    branches: [ main ]

jobs:
  format:
    uses: YOUR-USERNAME/github-actions-library/.github/workflows/terraform-fmt.yml@main
    with:
      path: modules/compute

  validate:
    uses: YOUR-USERNAME/github-actions-library/.github/workflows/terraform-validate.yml@main
    with:
      path: modules/compute
