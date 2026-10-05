# Contributing to com.soulfiremc.soulfire

This repository is the SoulFire organization fork of the Flatpak packaging manifest.
This guide covers local development, validation, and pull requests.

## Before you start

Search [open and closed issues](https://github.com/soulfiremc-com/com.soulfiremc.soulfire/issues) before reporting a problem or proposing a feature.
Small fixes can go directly to a pull request. Discuss substantial changes in an issue before implementation.
For usage questions and issue routing, read [SUPPORT.md](SUPPORT.md).
Follow the [community code of conduct](https://github.com/soulfiremc-com/.github/blob/main/CODE_OF_CONDUCT.md).
Report vulnerabilities privately through the [security policy](https://github.com/soulfiremc-com/.github/blob/main/SECURITY.md).

## Repository scope

The [Flathub repository](https://github.com/flathub/com.soulfiremc.soulfire) owns the published package.
A push to this organization fork does not publish a Flathub update.
Use this repository for proposed packaging work. Use SoulFireClient for desktop application code.
Keep documentation accurate for the manifest checked into this fork, which can differ from the current upstream package.

## Prepare a local build

Use Linux with Git, Flatpak, and a Flatpak Builder installation.
Clone this fork or your own fork, then initialize the pinned shared modules:

```bash
git submodule update --init --recursive
```

The manifest declares the required runtime and SDK. Install those declared versions through your Flatpak setup.
Follow [Flathub's build and validation instructions](https://docs.flathub.org/docs/for-app-authors/submission) for the builder environment.
With the Flathub builder installed and its remote configured, run:

```bash
flatpak run --command=flathub-build org.flatpak.Builder com.soulfiremc.soulfire.yml
flatpak run --command=flatpak-builder-lint org.flatpak.Builder manifest com.soulfiremc.soulfire.yml
flatpak run --command=flatpak-builder-lint org.flatpak.Builder repo repo
```

Use `--install` with `flathub-build` if you want to install the completed package for a local run.
Then start it with `flatpak run com.soulfiremc.soulfire`.
Record the architecture, runtime version, and exact commands.

## Manifest and update changes

- `com.soulfiremc.soulfire.yml`: runtime, sources, architecture filters, install commands, and sandbox permissions.
- `shared-modules/`: pinned upstream submodule. Do not update it as an unrelated side effect.
- `.github/workflows/update.yaml`: release discovery and proposed source updates.

Use two spaces in new YAML and keep source URLs tied to exact releases.
For each source update, download the architecture-specific artifact and calculate its SHA-256 digest.
Keep each URL, checksum, and architecture filter paired correctly.
Inspect the actual archive layout before changing its extraction commands.
A newer client release can use a different toolkit, runtime, or package format.
Do not treat a URL-only update as proof that the package still builds.

Explain every new sandbox permission and verify the behavior that requires it.
Keep permissions limited to the application's actual needs.
For update workflow changes, verify the manifest diff for both supported architectures without publishing artifacts.
Do not use production tokens to exercise the updater locally.

## Validate and submit

Run the manifest and repository lint checks after a build.
Verify desktop integration, launch, and the affected feature in the sandbox on each available target architecture.
If one architecture or a device integration is unavailable, record that limit.
Exclude `.flatpak-builder/`, `builddir/`, and `repo/` from commits.
There is no application unit test suite in this packaging repository.
Coordinate Flathub submissions with the package maintainers after reviewing the fork change.

## Submit a pull request

Keep the change focused on one problem. Avoid unrelated formatting and dependency updates.
Use Conventional Commit subjects such as `docs(contributing): clarify local setup` or `fix(build): correct packaging`.
Use a meaningful scope, imperative wording, and a subject under 72 characters.
For non-trivial changes, add a body that explains the motivation and important tradeoffs.
For breaking changes, include a `BREAKING CHANGE:` footer and migration instructions.
Do not bypass Git hooks. Let all configured checks finish.

Complete the pull request template with the problem, resulting behavior, and affected files.
If a related issue exists, link it.
Use `Closes #123` only if the change fully resolves that issue.
Record builder and lint results, sandbox observations, and architecture coverage.
Explain any checks that you could not perform.
For visible changes, include screenshots and the environment used to capture them.
Open a draft for early feedback on substantial changes.
Respond to review comments and rerun affected checks after revisions.

Update documentation and examples with behavior changes. Remove obsolete code rather than leaving placeholders or shims.
Do not commit credentials, private logs, dependency directories, or generated build artifacts.
Respect existing license notices and submit only material that you have the right to contribute.
