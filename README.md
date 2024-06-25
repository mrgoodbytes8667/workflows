# workflows
Reusable workflows

## Examples
### code-coverage
- Note the inclusion of `secrets: inherit`

```yaml
name: Code Coverage

on:
  pull_request:
  workflow_dispatch:
  push:
    branches:
      - main
      - 0.*
      - 1.*

jobs:
  coverage:
    uses: mrgoodbytes8667/workflows/.github/workflows/code-coverage.yml@php8.1-8.3
    secrets: inherit
    with:
      phpUnitVersion: 9.6
```

### prerelease
- Matches [release](#release) below except for tags and the `prerelease` flag

```yaml
name: prerelease

on:
  push:
    tags:
      - 'v*ALPHA*'
      - 'v*BETA*'
      - 'v*RC*'
  workflow_dispatch:

jobs:
  release:
    uses: mrgoodbytes8667/workflows/.github/workflows/release.yml@php8.1-8.3
    with:
      phpUnitVersion: 9.6
      prerelease: true
```

### release
- Matches [prerelease](#prerelease) above except for tags and the `prerelease` flag

```yaml
name: release

on:
  push:
    tags:
      - v*
      - '!v*ALPHA*'
      - '!v*BETA*'
      - '!v*RC*'
  workflow_dispatch:

jobs:
  release:
    uses: mrgoodbytes8667/workflows/.github/workflows/release.yml@php8.1-8.3
    with:
      phpUnitVersion: 9.6
```

### run-tests
```yaml
name: tests

on:
  pull_request:
  workflow_dispatch:
  repository_dispatch:
  push:
    branches:
      - main
      - 0.*
      - 1.*
  schedule:
    # Weekly on Thursdays at 2pm UTC
    - cron:  '0 14 * * 4'

jobs:
  test:
    uses: mrgoodbytes8667/workflows/.github/workflows/run-tests.yml@php8.1-8.3
    with:
      phpUnitVersion: 9.6
      failFast: false
```

### run-tests-by-version
```yaml
name: Tests By Symfony Version

on:
  pull_request:
  workflow_dispatch:
  repository_dispatch:
  push:
    branches:
      - main
      - 0.*
      - 1.*
  schedule:
    - cron:  '0 15 * * 4'

jobs:
  symfony62:
    uses: mrgoodbytes8667/workflows/.github/workflows/run-tests-by-version.yml@php8.1-8.3
    with:
      phpUnitVersion: 9.6
      symfony: 6.2

  symfony63:
    uses: mrgoodbytes8667/workflows/.github/workflows/run-tests-by-version.yml@php8.1-8.3
    with:
      phpUnitVersion: 9.6
      symfony: 6.3

  symfony64:
    uses: mrgoodbytes8667/workflows/.github/workflows/run-tests-by-version.yml@php8.1-8.3
    with:
      phpUnitVersion: 9.6
      symfony: 6.4

  symfony70:
    uses: mrgoodbytes8667/workflows/.github/workflows/run-tests-by-version.yml@php8.2-8.3
    with:
      phpUnitVersion: 9.6
      symfony: 7.0

  symfony71:
    uses: mrgoodbytes8667/workflows/.github/workflows/run-tests-by-version.yml@php8.2-8.3
    with:
      phpUnitVersion: 9.6
      symfony: 7.1
```