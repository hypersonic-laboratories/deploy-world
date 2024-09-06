# Deploy HELIX World

This Github Action will automatically zip your world and upload it as a new version to HELIX.

## Using this Action

In your development repository, create a workflow file in `.github/workflows` that utilizes this Github Action and provides `world_name` and `access_token` as inputs. For example, in `.github/workflows/upload.yml`:

```yaml
name: Deploy World to HELIX

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
          # Required inputs:
          access_token: ${{ secrets.ACCESS_TOKEN }}
          world_name: 'my-world-name'

          # Optional inputs:
          # this Action supports access to private repositories using deploy keys
          private_ssh_key: ${{ secrets.PRIVATE_SSH_KEY }}

          # If your Packages folder is in another place you can specify it here 
          packages_path: './Packages'

```

## Recommended Repository Structure

Since this Action uploads your world to HELIX, we recommend structuring your repository as follows:


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

This Action will pack the Packages folder and upload it to HELIX.


## Setting Up Secrets

Ensure that the ACCESS_TOKEN secret is set in the repository where you use this action. Navigate to Settings > Secrets > Actions and add a new secret named ACCESS_TOKEN. You can generate an Access Token on the [HELIX Hub](https://hub.helixgame.com/account/tokens).
