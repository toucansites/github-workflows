Reusable GitHub Actions workflows for working with [Toucan](https://github.com/toucansites/toucan).

---

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
```

> Ensure GitHub Pages is enabled and set to deploy from GitHub Actions.

#### Cache directory

A `cache` directory is set up during the build so that [transformers](https://toucansites.com/docs/rendering/transformers/) can make use of it.

---

## License

MIT — see the [Toucan source repository](https://github.com/toucansites/toucan) for license details.
