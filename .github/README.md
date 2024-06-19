<h1 align="center">
      <img src="logo.png" width="96px" height="96px" />
      <br>entur/gha-artifactory<br>
</h1>

[![Entur/Artifactory/CI](https://github.com/entur/gha-artifactory/actions/workflows/ci.yml/badge.svg?event=pull_request)](https://github.com/entur/gha-artifactory/actions/workflows/ci.yml)

GitHub Actions for working with Artifactory

## Golden Path

- Using the [Maven Publish Plugin](https://docs.gradle.org/current/userguide/publishing_maven.html)
- `./gradle-properties` file at the root of your repository
- `./gradle-properties` contains "version" variable with semver version format, e.g., "1.0.0"
- Job needs write permissions to the repository to push back the version change
- Use after Gradle build to have the artifact ready for publishing
- Use on main branch push events, to avoid pushing back to the repo unnecessarily

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
    permissions:
    contents: write
    uses: entur/gha-artifactory/.github/actions/update-version@v1

  publish-artifact:
    uses: entur/gha-artifactory/.github/actions/publish-artifact.yml@v1
```

