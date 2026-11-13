# Silo-Server/.github

Organization-wide community health files (`CONTRIBUTING.md`, the pull request
template), the organization profile (`profile/README.md`), and reusable
workflows shared by Silo-Server repositories.

## Shared workflows

### `plugin-release.yml`

Builds, signs, and publishes a Silo-Server plugin release. Each plugin
repository's `.github/workflows/release.yml` calls it on a tag push:

```yaml
name: Release

on:
  push:
    tags: ['v*']

permissions: {}

jobs:
  release:
    permissions:
      contents: write
      id-token: write
      attestations: write
    uses: Silo-Server/.github/.github/workflows/plugin-release.yml@main
    secrets:
      dispatch_token: ${{ secrets.SILO_PLUGINS_DISPATCH_TOKEN }}
```

**Reference it only at `@main`.** The signing certificate's subject
(`job_workflow_ref`) records the ref the caller used, and Silo servers accept
only
`https://github.com/Silo-Server/.github/.github/workflows/plugin-release.yml@refs/heads/main`.
That identity proves only that the workflow file ran from whatever this
repository's `main` branch held at the time. A SHA or tag reference could point
at any commit, including one pushed to a fork, so a release called at any other
ref fails the workflow's own verification step and is not published.

The identity is only as trustworthy as this repository's `main`: anyone who
can push to `main` can change what every plugin release runs and signs. The
guarantee depends on protecting `main` (required review, no direct or force
pushes) and on a tag ruleset that blocks creating a tag named `main`, since a
tag takes precedence over a branch of the same name in `uses:`.

Contract:

- Trigger: a `push` of a tag `vMAJOR.MINOR.PATCH` (optionally `-PRERELEASE`).
  The tagged commit must be on the first-parent history of the plugin
  repository's `main`, its `manifest.json` `version` must equal the tag
  without the `v`, and that version must be strictly greater, by semver
  precedence (`1.2.0-rc.1` < `1.2.0`), than its first parent's (a root commit
  or a parent without `manifest.json` passes). No later first-parent commit on
  `main` may set a lower version; a reverted bump is not releasable. Only one
  commit per version is releasable. To release, merge a pull request that
  bumps `manifest.json`, then tag the commit on `main` that bumped it: the
  squash commit, or the merge commit for a merge-commit PR.
- Prereleases (`vX.Y.Z-rc.1`) publish a GitHub prerelease and do not notify
  the catalog.
- Permissions: the calling job grants `contents: write`, `id-token: write`,
  and `attestations: write`. The workflow narrows them per job; only the
  signing job, which runs no plugin code and downloads nothing, can request a
  signing token.
- Input `platforms` (optional): comma-separated `GOOS/GOARCH` pairs. Default
  `linux/amd64,linux/arm64,darwin/arm64`.
- Input `catalog_repository` (optional): the catalog to notify,
  `Silo-Server/silo-plugins` (the default) or `Silo-Community/silo-plugins`.
  Any other value fails the run before anything is built. An approved
  community plugin passes `catalog_repository: Silo-Community/silo-plugins`
  under `with:`.
- Secret `dispatch_token` (optional): when set, a non-prerelease sends a
  `plugin_release_published` `repository_dispatch` to the catalog repository
  with `{"repo": "<owner>/<name>", "tag": "<tag>"}`. When unset, it skips the
  dispatch. The dispatch is its own job after the release, so a failed
  dispatch can be re-run alone.
- Build: one job builds every platform from the main package at the
  repository root, with Go from `go.mod`,
  `CGO_ENABLED=0 go build -trimpath -ldflags="-s -w -X main.version=<version>"`,
  cross-compiled on Ubuntu. A `silo-plugin-sdk` replace, or a replace to an
  absolute or `../` path, in `go.mod` fails the build.
- Integrity between jobs: the build job returns the binaries' `sha256sum`
  lines as a job output, and the signing job attests exactly those digests.
  The release job publishes the downloaded binaries only after
  `sha256sum --check` against that output and `gh attestation verify`
  against the bundle, so a replaced artifact fails before anything is
  published.
- Release assets: `plugin-<os>-<arch>` for each platform, `checksums.txt`
  (`sha256sum` format, one line per binary), and `plugin.sigstore.json`, a
  single Sigstore bundle from GitHub artifact attestations that lists every
  binary as a subject.

The signing certificate carries Source Repository URI = the plugin repository
and Source Repository Ref = `refs/tags/vX.Y.Z`. Verify a binary with:

```sh
gh attestation verify plugin-linux-amd64 \
  --bundle plugin.sigstore.json \
  --repo Silo-Server/<plugin-repo> \
  --cert-identity https://github.com/Silo-Server/.github/.github/workflows/plugin-release.yml@refs/heads/main \
  --source-ref refs/tags/vX.Y.Z \
  --deny-self-hosted-runners
```

Changing the inputs, assets, or certificate identity breaks every plugin
repository and the servers that verify their releases. Coordinate such changes
across those repositories first.
