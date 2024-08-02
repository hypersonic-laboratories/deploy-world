# Deploy Helix World

Tired of zipping your Packages from your world, drag'n'drop them into Hub and not knowing exactly if you are doing it right?. This action will automatically zip your world and upload it to the Helix Platform.

## Using this your repository

In your other repository, create a workflow file that uses the custom action and provides the `world_name` and `access_token` as an input. For example, in `.github/workflows/upload.yml`:

```yaml
name: Upload World to Helix

on:
  push:
    branches:
      - main

jobs:
  upload-package:
    runs-on: ubuntu-latest

    steps:
      - name: Use deploy world action
        uses: hypersonic-laboratories/deploy-world@main
        with:
          access_token: ${{ secrets.ACCESS_TOKEN }}
          world_name: 'my-world-name'

```

## Folder Structure

Since this action uploads a world to depot, it should be structured as follows:


```
.
├── Assets
├── Config.toml
├── HELIXCore.log
├── HELIXGameServer
├── Modules
├── Packages
│   ├── api-benchmark
│   │   ├── Client
│   │   ├── Package.toml
│   │   ├── Server
│   │   │   ├── Discord.lua
│   │   │   ├── Index.lua
│   │   │   └── Utils.lua
│   │   └── Shared
│   │       └── Index.lua
│   ├── my-roleplay
│   └── other-packages
└── .github/workflows/upload.yml
```

This action will Pack the Packages folder and sent it to the depot.


## Setting Up Secrets

Ensure that the ACCESS_TOKEN secret is set in the repository where you use this action. Navigate to Settings > Secrets > Actions and add a new secret named ACCESS_TOKEN.
