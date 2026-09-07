# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Changed

- Standardize repository settings, development checks, code style and documentation.

## [v1.0.0] - 2026-08-30 - Initial release

### Added

- Automatic construction-vessel requests for player-owned station construction and reconstruction tasks once the required resources are available.
- Player-only request handling, so player stations can only auto-assign player-owned builders running **Find Build Tasks**, while NPC construction behavior remains unchanged.
- Blacklist-aware gate-route validation before a builder accepts a task, preventing unreachable builders from reserving it.
- Existing-save support, X4 9.00 compatibility, installation and Steam Workshop publishing helpers, and an in-game verified assignment flow.

[v1.0.0]: https://github.com/drjele/x4-player-builder-autodispatch/releases/tag/v1.0.0
