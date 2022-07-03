# Coguard Docker Image Scan Action

This action is scanning Docker images using the
[coguard-cli](https://github.com/coguardio/coguard-cli).

# Example usage

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
        uses: actions/coguard-image-scan-action
        with:
          dockerImageName: YourImageName
          username: ${{ secrets.CoGuardUserName }}
          password: ${{ secrets.CoGuardPassword }}
```

# Parameters which this action accepts

| Parameter         | type     | meaning | required | default |
|--------------|-----------|------------|-----------|---------|
| dockerImageName | string | The Docker image name which the CoGuard CLI should scan. | true    | N/A |
| failLevel | int |  The minimum level of severity of failed checks to fail this build. | false | 1   |
| username | string | The username as registred on coguard.io. If you are not registered, please go to https://portal.coguard.io, and click on "Log In" to register. | true | N/A |
| password | string | The password for the user identified by username. | false | 1   | N/A |
