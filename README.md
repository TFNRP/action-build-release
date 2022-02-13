# Build Release Action

GitHub Action for building .NET solutions and automatically releasing the built solution.

`.github/workflows/release.yml`

```yml
name: Build
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: TFNRP/action-build-release@v1
      with:
        ## Personal access token used to create a release.
        ## Default: github.token
        token: ${{ secrets.GH_TOKEN }}
        ## Whether the release should be a draft.
        ## Default: true
        draft: false
        ## The version of this release.
        ## Default: Tag name
        # version: ${{ github.ref_name }}
        ## The project name.
        ## Default: Repository name
        # project: 'Framework Core'
        ## Include a pre-filled fxmanifest.lua in the build.
        ## This is prepended with "fx_version" and "game" entries.
        ## Default: No manifest
        manifest: >
          author 'Reece Stokes <hagen@hyena.gay>'

          client_script 'Core.Framework.Client.net.dll'
          server_script 'Core.Framework.Server.net.dll'
        
```

To trigger an automatic release, push a SemVer tag, i.e. `git push origin v2.6.1`.  
With the above workflow, the action will also trigger on pull requests - which will verify if the PR's solution can be built.
