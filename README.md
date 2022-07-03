# Coguard Docker Image Scan Action

This action is scanning Docker images using the
[coguard-cli](https://github.com/coguardio/coguard-cli).

# Example usage:

```
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
