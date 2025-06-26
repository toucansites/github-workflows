# Reusable GitHub Actions Workflows for [Toucan](https://github.com/toucansites/toucan)

## `deploy.yml`

Builds a static site using Toucan in Docker and deploys it to GitHub Pages.

---

## Usage

Example GitHub Actions workflow:

```yaml
name: Build and Deploy with Toucan

on:
  push:
    branches: [main]

jobs:
  build-with-toucan:
    uses: toucansites/github-workflows/.github/workflows/deploy.yml@main
    permissions:
      contents: read
      pages: write
      id-token: write
    with:
      version: "1.0.0-beta.5"
      target: "github-deploy"
```

> **Note:** Ensure GitHub Pages is enabled and set to deploy from GitHub Actions.

---

## Inputs

| Name     | Description                                                | Required | Default         |
|----------|------------------------------------------------------------|----------|-----------------|
| `version` | Toucan Docker image tag to use                             | No       | `latest`        |
| `target`  | Toucan build target (used with `--target`)                 | No       | *(none)*        |

---

## Target Configuration Options

Toucan supports **multiple build targets** (e.g. `dev`, `live`, `preview`, `github-deploy`).  
There are **two ways to use a target** with this workflow:

### Option 1: Specify the target explicitly

Set the `target` name in the GitHub Actions workflow:

```yaml
with:
  target: "github-deploy"
```

This instructs the workflow to run:

```bash
toucan generate . --target github-deploy
```

### Option 2: Define a default target in `toucan.yml`

```yaml
targets:
  - name: github-deploy
    default: true
    output: /tmp/output
    url: "https://binarybirds.com/"
```

[Toucan](https://github.com/toucansites/toucan) will automatically use this default target if no `--target` is provided.

---

### Required: `output: /tmp/output`

> **Important:**  
> The selected target **must** define an explicit output path:
>
> ```yaml
> output: /tmp/output
> ```
>
> The workflow expects the build output at this path inside the container.  
> If it's missing, the deployment will fail because no files will be found to upload.

---

### Version Requirement for `targets`

> **Toucan targets require version `1.0.0-beta.5` or `latest`.**  
> If you're using an older image (e.g., `beta.4`), the `targets` will be ignored and build output will not work as expected.  
> Be sure to set:
>
> ```yaml
> with:
>   version: "1.0.0-beta.5"  # or "latest"
> ```

## Cache Directory

A `cache` directory is created and mounted into the Docker container so [transformers](https://toucansites.com/docs/rendering/transformers/) can use it for optimization.

---

## License

MIT — see the [Toucan source repository](https://github.com/toucansites/toucan) for license details.
