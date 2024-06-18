[![Entur/Artifactory/CI](https://github.com/entur/gha-artifactory/actions/workflows/ci.yml/badge.svg?event=pull_request)](https://github.com/entur/gha-artifactory/actions/workflows/ci.yml)

GitHub Actions for working with Artifactory

## Golden Path

- Using the [Maven Publish Plugin](https://docs.gradle.org/current/userguide/publishing_maven.html)
- `./gradle-properties` file at the root of your repository
- `./gradle-properties` contains "version" variable with semver version format, e.g., "1.0.0"

### Example

Let's look at an example, assume our repo is called `amazing-app`:

```sh
λ amazing-app ❯ tree
.
├── README.md
├── gradle.properties
```

```yaml
# ci.yml
name: CI

on:
  push:
    branches:
      - main

jobs:
  update-version:
    uses: entur/gha-artifactory/.github/workflows/update-version.yml@v1

  publish-artifact:
    uses: entur/gha-artifactory/.github/workflows/publish-artifact.yml@v1
```

