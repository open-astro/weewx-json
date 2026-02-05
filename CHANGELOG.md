# Changelog
All notable changes to WeeWX-JSON will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.4] - 2026-02-05
- Added new `lcd_datasheet.json` output template for NOAA-style layered reporting.
- Included 15-minute raw captures for daily rows in `lcd_datasheet.json`.
- Added aggregated summaries to limit file growth: weekly/monthly daily summaries and yearly monthly summaries.
- Updated `skin.conf` to generate `lcd_datasheet.json` without changing existing `weewx.json` or `current_minimal.json`.
- Updated `README.md` with new output details, report regeneration, and packaging guidance.
- Updated installer template to register the extension as `weewx-json`.
- Ignored macOS metadata files in `.gitignore`.

## [1.3] - 2024-10-30
- Fixed template comparisons to avoid literal-comparison warnings.
- Updated GitHub Actions steps (`checkout`, `upload-artifact`) in the packaging workflow.
- Logged the release in this changelog.

## [1.2] - 2024-01-01
- Added automated package build support (`build_package.py`) and GitHub Actions packaging workflow.
- Added distributable install template at `dist-template/install.py.template`.
- Switched default timestamp output to ISO8601 in JSON templates and skin config.
- Renamed `changelog` to `CHANGELOG.md` and recorded the 1.2 release notes.

## [1.1] - 2020-10-07
- Added `current_minimal.json.tmpl` for a smaller output with no computed or archived values.
- Updated `skin.conf` and installer file lists to include the minimal JSON template.
- Expanded docs with install/uninstall details and example output.
- Included critical measurement updates and syntax fixes from PR #2.

## [1.0] - 2020-10-03
- Initial extension release from imported prior work.
- Added extension packaging/install support (`install.py`) and `skins/JSON/skin.conf`.
- Included baseline project description and repository scaffolding.
