# Library.Net.ContinuousDelivery
Continuous delivery workflow for releasing DotNet libraries on NuGet.org.

[![Continuous Delivery](https://github.com/Fresa/Library.Net.ContinuousDelivery/actions/workflows/cd.yml/badge.svg)](https://github.com/Fresa/Library.Net.ContinuousDelivery/actions/workflows/cd.yml)

## Getting Started
Releases of the reusable workflow produces minor and major tags that can be referenced instead of a release tag, branch or commit. [Recommended](https://docs.github.com/en/actions/sharing-automations/creating-actions/about-custom-actions#using-tags-for-release-management) is to follow a major tag, i.e `v0`. 

Example workflow that releases on every push:
```yaml
name: Continuous Delivery

on:
  push:
    branches:
      - "**"
    tags-ignore:
      - '**'

permissions:
  contents: write  

jobs:
  release:
    name: Release
    uses: https://github.com/Fresa/Library.Net.ContinuousDelivery/actions/workflows/release.yml@main
    with:
      project_path: src/Project
      project_name: Project
    secrets: 
      nuget_api_key: ${{ secrets.NUGET_API_KEY }}
```

## What does it do?
- Determines a semantic version based on conventional commits, see [Trunk Based Release Versioning](https://github.com/marketplace/actions/trunk-based-release-versioning).
- Generates release notes since last release, see [Semantic Release Notes Generator](https://github.com/marketplace/actions/semantic-release-notes-generator).
- Packages a project as a NuGet package by using the `Project.PropertyGroup.PackageId` project property from the referenced project.
- Generates a Github release
- Updates latest minor and major tags
- Publishes the NuGet package to nuget.org

# Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

# License
[MIT](LICENSE)