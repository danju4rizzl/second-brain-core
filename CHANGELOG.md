# Changelog

All notable changes to the Kavara Brain Engine. Format: [Keep a Changelog](https://keepachangelog.com); versions follow [SemVer](https://semver.org).

## [1.1.0] - 2026-11-01

### Added
- **One-link install:** `.claude-plugin/marketplace.json` lets Claude Code users install the [Kavara Brain for Claude](https://github.com/danju4rizzl/kavara-brain-claude) plugin straight from this repo (`/plugin marketplace add danju4rizzl/second-brain`).
- README: "Install: pick your tool" table and a Kavara Brain suite overview.
- `docs/FAQ.md`: FAQ & troubleshooting.
- `SECURITY.md`: how to report security or privacy issues.
- `CHANGELOG.md`.

### Changed
- `.gitignore` allowlist now also permits `CHANGELOG.md`, `SECURITY.md` and `.claude-plugin/`.
- No changes to prompts, scripts or templates.

## [1.0.0] - 2026-11-01

### Added
- First public release: install, compile, query, file-back, lint and research prompts; `kb.mjs` (index · lint · bundle · stats, `--root`); `notion_extract.py`; templates; `docs/method.md`; fictional `example/` vault; allowlist `.gitignore`; GitHub check that lints the example and fails if private files are tracked.
