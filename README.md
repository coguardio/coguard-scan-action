# Coguard Scan Action

This action is scanning Docker images or repositories using the
[coguard-cli](https://github.com/coguardio/coguard-cli).

# Example usage

## Scanning your local repository

```yaml
name: Including CoGuard into your GitHub Action
on: [push]
jobs:
  create-image-and-run-coguard:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Run the CoGuard CLI Action
        uses: actions/coguard-scan-action
        with:
          dockerImageName: YourImageName
          username: ${{ secrets.CoGuardUserName }}
          password: ${{ secrets.CoGuardPassword }}
```

## Scanning a Docker image

```yaml
name: Including CoGuard into your GitHub Action
on: [push]
jobs:
  create-image-and-run-coguard:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Build your docker image
        run: |
          echo "Your build commands go here"

      - name: Run the CoGuard CLI Action
        uses: actions/coguard-docker-image-scan
        with:
          dockerImageName: YourImageName
          username: ${{ secrets.CoGuardUserName }}
          password: ${{ secrets.CoGuardPassword }}
```


# Parameters which this action accepts

| Parameter         | type     | meaning | required | default |
|--------------|-----------|------------|-----------|---------|
| `dockerImageName` | `string` | The Docker image name which the CoGuard CLI should scan. | `true`    | N/A |
| `repositoryScan`    | `bool`  | The indicator if you wish to scan the repository (automatically run if `dockerImageName` is not provided) | `false` | `true` |
| `failLevel` | `int` |  The minimum level of severity of failed checks to fail this build. | `false` | `1`   |
| `username` | `string` | The username as registered on coguard.io. If you are not registered, please go to https://portal.coguard.io, and click on "Log In" to register. | `true` | N/A |
| `password` | `string` | The password for the user identified by username. | `false` | N/A |

# How to obtain a CoGuard account

You can either register on [https://portal.coguard.io](https://portal.coguard.io) or
by running the [coguard-cli](https://github.com/coguardio/coguard-cli) locally.
