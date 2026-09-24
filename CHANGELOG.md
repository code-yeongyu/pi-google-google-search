# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Docs: install from GitHub (`pi install git:github.com/code-yeongyu/pi-google-google-search`).

## [0.1.1] - 2026-09-24

### Changed

- **BREAKING**: Migrate peer dependencies from `@mariozechner/pi-*` to `@earendil-works/pi-*` (v0.87.1).
- Update `@biomejs/biome` to 2.5.14.
- Update `vitest` to 5.0.1.
- Update `typescript` to 7.0.2.
- Update `@types/node` to 26.6.2.
- Update `@typescript/native-preview` to 7.0.0-dev.20260707.2.
- Require Node.js >=22.19.0.
- Add GitHub Actions CI workflow with Bun 1.4.2.

## [0.1.0] - 2026-05-07

### Added

- Initial release. Native Google `googleSearch` policy extension for the pi coding agent. Injects `{ googleSearch: {} }` into `google-generative-ai` and `google-vertex` requests when `PI_GOOGLE_GOOGLE_SEARCH` is enabled (default-on).
