# Medfin's fork of tlx

This is Medfin's fork of [tlx](https://github.com/tlaplus-x/tlx), forked from upstream
commit [`bec5985`](https://github.com/tlaplus-x/tlx/commit/bec5985) on 2026-11-09.
Medfin's monorepo uses tlx to check its TLA+ models.

We keep the fork so that we own a copy we can fix, and so that we can publish prebuilt
binaries. The Medfin monorepo installs them with mise and never builds Rust:

```toml
[tools]
"github:Medfin-AI/tlx" = "0.1.0"
```

The upstream README and docs are unchanged; read them for how tlx works.

## Releases

`.github/workflows/release.yml` builds `tlx` for macOS on Apple silicon and for Linux on
x86_64 and arm64, then publishes one archive per platform and a `SHA256SUMS` file. The
Linux binaries link against glibc 2.17, so they run on Ubuntu 24.04 and Amazon Linux 2023
alike.

To cut a release:

1. If the code changed since the last release, bump `version` under
   `[workspace.package]` in `Cargo.toml` and run `cargo check` to update `Cargo.lock`.
   Commit both.
2. Tag the commit with the same version and push it:
   `git tag v0.1.1 && git push origin v0.1.1`. The workflow fails if the tag and the
   `Cargo.toml` version differ.
3. Update the version in the monorepo's `mise.toml`.

Running the workflow by hand (Actions, Release, Run workflow) builds and smoke-tests the
archives without publishing a release.

## Changes from upstream

Only the files below differ from upstream. List any fix to upstream's code here, with the
reason.

- `MEDFIN.md`: this file.
- `.github/workflows/release.yml`: the release workflow.
