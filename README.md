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
        uses: coguardio/coguard-scan-action@v0.2.37
        with:
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
        uses: coguardio/coguard-scan-action@v0.2.37
        with:
          dockerImageName: YourImageName
          username: ${{ secrets.CoGuardUserName }}
          password: ${{ secrets.CoGuardPassword }}
```

## Scanning and upload as SARIF

```yaml
name: Including CoGuard into your GitHub Action and upload as SARIF
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
        uses: coguardio/coguard-scan-action@v0.2.37
        with:
          dockerImageName: YourImageName
          username: ${{ secrets.CoGuardUserName }}
          password: ${{ secrets.CoGuardPassword }}
          outputFormat: sarif
      - name: Upload SARIF file
        if ${{ failure() }}
        uses: github/codeql-action/upload-sarif@a57c67b89589d2d13d5ac85a9fc4679c7539f94c
        with:
          sarif_file: result.sarif.json
          category: CoGuard
```

# Parameters which this action accepts

| Parameter         | type     | meaning | required | default |
|--------------|-----------|------------|-----------|---------|
| `dockerImageName` | `string` | The Docker image name which the CoGuard CLI should scan. | `true`    | `""` |
| `repositoryScan`    | `bool`  | The indicator if you wish to scan the repository | `false` | `true` |
| `getLatestReport`    | `string`  | Lets you download the latest report .zip for your cluster | `false` | `""` |
| `failLevel` | `int` |  The minimum level of severity of failed checks to fail this build. | `false` | `1`   |
| `outputFormat` | `string` | The output format of the results. Supported are `json`, `sarif`, `formatted` | `false` | `formatted` |
| `username` | `string` | The username as registered on coguard.io. If you are not registered, please go to https://portal.coguard.io, and click on "Log In" to register. | `true` | N/A |
| `password` | `string` | The password for the user identified by username. | `false` | N/A |

# How to obtain a CoGuard account

You can either register on [https://portal.coguard.io](https://portal.coguard.io) or
by running the [coguard-cli](https://github.com/coguardio/coguard-cli) locally.
