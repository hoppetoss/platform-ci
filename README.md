# 🧰 Platform CI Library

Reusable **GitHub Actions workflows** for Docker image builds and Terraform automation.  
This repository is meant to serve as the **central CI/CD toolkit** for all other platform and service repos.

---

## 📦 Workflows Included

### 1️⃣ Docker Build & Push

Reusable workflow to build and push Docker images.

**File:** `.github/workflows/docker-build.yml`

**Usage:**
```yaml
jobs:
  build:
    uses: hoppetoss/platform-ci/.github/workflows/docker-build.yml@main
    with:
      image_name: "demo-api"
      registry: "ghcr.io"        # optional, defaults to ghcr.io
      context: "."               # optional build context
      dockerfile: "Dockerfile"   # optional Dockerfile path
    secrets:
      DOCKER_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**What it does**
	•	Builds a Docker image using Buildx.
	•	Pushes it to GitHub Container Registry (ghcr.io).
	•	Supports caching, multiple tags, and optional build args.


### 2️⃣ Terraform Validate, Plan & Apply

Reusable workflow for validating and applying Terraform modules.

**File:** `.github/workflows/terraform-deploy.yml`

**Usage:**
```yaml
jobs:
  infra:
    uses: hoppetoss/platform-ci/.github/workflows/terraform-deploy.yml@main
    with:
      tf_directory: "./infra"
      auto_apply: false           # change to true to auto-apply
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

**What it does**
	•	Runs terraform fmt, init, validate, and plan.
	•	Optionally applies changes if auto_apply is true.
	•	Posts plan results to pull requests automatically.

### How to Use in Other Repositories

In any repository (for example, demo-platform-infra or demo-apps), create a `.github/workflows/main.yml` file:

```yaml
name: Build and Deploy
on:
  push:
    branches: [main]

jobs:
  build:
    uses: hoppetoss/platform-ci/.github/workflows/docker-build.yml@main
    with:
      image_name: "demo-api"
    secrets:
      DOCKER_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

This allows all repositories to reuse the same standardized CI/CD workflows.

### 💡 Why This Exists
	•	Promotes DRY (Don’t Repeat Yourself) principles for CI/CD.
	•	Ensures consistency across all service and infrastructure repos.
	•	Makes automation versioned and discoverable in one place.
	•	Helps developers focus on code, not pipelines.


### 👩‍💻 Maintainers

Owner: @hoppetoss￼
Contributions: Welcome via pull requests or issues.

```yaml
👩‍💻 Maintainers

Owner: @hoppetoss￼
Contributions: Welcome via pull requests or issues.
```

