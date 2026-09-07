# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Changed

- Standardize repository settings, development checks, code style and documentation.
- Detailed Steam Workshop description, covering every setting, where to change it, and the required and optional dependencies.
- Extension id shortened to `drjele_player_builder_dispatch`. The Steam Workshop allows at most 32 characters for a folder name and the old id was 34.

### Added

- `publish.sh update` options `--minor`, `--namedesc` and `--readback`, for an update that leaves the version number alone, one that also pushes the name and description to Steam, and one that writes Steam's own text back into `content.xml.steam`.

### Fixed

- `publish.sh` passes `-batchmode`, so an upload no longer waits for a keypress a non-interactive run cannot give it.
- `publish.sh` runs the workshop tool inside the Steam snap's mount namespace. The snap has a private `/tmp`, so the Steam client IPC the tool needs is unreachable from outside it and the upload failed on a Steamworks assertion.
- `publish.sh` shows the tool's output, which Proton otherwise discards, and reads success or failure out of it rather than out of an exit code Proton does not pass on.
- `publish.sh` restores the local installation even when the upload fails, instead of leaving it holding the staged copy with the Workshop id in it.
- `publish.sh update` sends the preview image too, so a refreshed `extension/preview.jpg` reaches the Workshop item instead of leaving the one from the first upload in place.

## [v1.0.0] - 2026-08-30 - Initial release

### Added

- Automatic construction-vessel requests for player-owned station construction and reconstruction tasks once the required resources are available.
- Player-only request handling, so player stations can only auto-assign player-owned builders running **Find Build Tasks**, while NPC construction behavior remains unchanged.
- Blacklist-aware gate-route validation before a builder accepts a task, preventing unreachable builders from reserving it.
- Existing-save support, X4 9.00 compatibility, installation and Steam Workshop publishing helpers, and an in-game verified assignment flow.

[v1.0.0]: https://github.com/drjele/x4-player-builder-autodispatch/releases/tag/v1.0.0
