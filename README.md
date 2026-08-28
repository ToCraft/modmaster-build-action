# ModMaster Build Action

This GitHub Action is solely for using the [ModMaster Gradle Plugin](https://github.com/ToCraft/ModMaster).

Here's a working example:

```yml
name: Build

on:
  push:
    paths:
      - '**.gradle'
      - '**.gradle.kts'
      - '**.properties'
      - '**/src/**'
    branches-ignore:
      - "1.**"
      - "main"
      - "master"
  workflow_dispatch:

permissions:
  contents: write
  actions: write

jobs:
  build:
    runs-on: ubuntu-latest
    if: |
      !contains(github.event.head_commit.message, '[ci skip]')
    steps:
      - uses: ToCraft/modmaster-build-action@v1.2
        with:
          java-version: '25'
```

---

Using the script at `.github/workflows/update-tags.yml` you can auto-update the tags by running:
```bash
git tag v2.0.1
git push origin v2.0.1
```
