# Soulfire Flatpak packaging fork

This repository is the Soulfire organization's fork of [flathub/com.soulfiremc.soulfire](https://github.com/flathub/com.soulfiremc.soulfire).
It contains the package manifest, its shared-module submodule, and a release update workflow.
Application code belongs in [SoulFireClient](https://github.com/soulfiremc-com/SoulFireClient).

A push here does not publish an update to Flathub.
The published package and this fork can use different source revisions, runtime versions, or packaging methods.
Inspect the manifest in the checkout you want to build.

## Development and validation

Read [CONTRIBUTING.md](CONTRIBUTING.md) for builder setup, source checksums, sandbox permissions, and architecture validation.
Initialize the shared modules before building:

```bash
git submodule update --init --recursive
```

The manifest declares the runtime and SDK. Use the [Flathub build instructions](https://docs.flathub.org/docs/for-app-authors/submission) to prepare them.

## Support and contributions

Read [SUPPORT.md](SUPPORT.md) to distinguish packaging problems from application problems.
Follow the [code of conduct](https://github.com/soulfiremc-com/.github/blob/main/CODE_OF_CONDUCT.md) and use the [private security contacts](https://github.com/soulfiremc-com/.github/blob/main/SECURITY.md) for vulnerabilities.
