Reusable GitHub Actions workflows for working with [Toucan](https://github.com/toucansites/toucan).

## Workflows

### `deploy.yml`

Builds a static site using Toucan in Docker and deploys it to GitHub Pages.

#### Usage

Example github action:

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
      version : "1.0.0-beta.4"
```

> Ensure GitHub Pages is enabled and set to deploy from GitHub Actions.

#### Inputs

| Name     | Description                                                | Required | Default  |
|----------|------------------------------------------------------------|----------|----------|
| `version` | Docker image tag to use | No       | `latest` |

If no `version` is specified, the workflow will default to using the `latest` tag of the Docker image.

#### Cache directory

A `cache` directory is set up during the build so that [transformers](https://toucansites.com/docs/rendering/transformers/) can make use of it.

---

## License

MIT — see the [Toucan source repository](https://github.com/toucansites/toucan) for license details.
