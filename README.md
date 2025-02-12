# testing-action-adapter

Shared Github Actions for ioBroker testing workflows: Adapter tests

## Inputs

| Input             | Description                                                                                                                                                                                          | Required? |      Default      |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | :---------------: |
| `node-version`    | Node.js version to use in tests. Should be LTS.                                                                                                                                                      | ✔         |         -         |
| `install-command` | Overwrite the default install command. When changing this, `package-cache` may need to be disabled.                                                                                                  | ❌        |    `'npm ci'`     |
| `package-cache`   | For which package manager dependencies should be cached. Set to `'false'` or `''` to disable caching. More documentation [here](https://github.com/actions/setup-node#caching-global-packages-data). | ❌        |      `'npm'`      |
| `os`              | The operation system to use                                                                                                                                                                          | ✔         |         -         |
| `build`           | Set to `'true'` when the adapter needs a build step before testing                                                                                                                                   | ❌        |     `'false'`     |
| `build-command`   | Overwrite the default build command                                                                                                                                                                  | ❌        | `'npm run build'` |
| `extra-tests`     | Add an additional command to run before ioBroker's tests                                                                                                                                             | ❌        |         -         |

## Usage

```yml
# ... rest of your workflow ...

jobs:
  adapter-tests:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x]
        os: [ubuntu-latest, windows-latest, macos-latest]

    steps:
      - uses: ioBroker/testing-action-adapter@v1
        with:
          node-version: ${{ matrix.node-version }}
          os: ${{ matrix.os }}
          # build: 'true' # optional

  # ... other jobs
```
