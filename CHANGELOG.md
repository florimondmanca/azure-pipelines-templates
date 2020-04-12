# Changelog

## 2.0 - 2020-04-12

### Changed

- Renamed `python-install.yml` to `step--python-install.yml`.

### Added

- Coverage XML reporting, which is required for Codecov, is now automatically handled by `job--python-test.yml` — no need to configure it on the tested repo anymore.

## 1.0 - 2020-04-11

### Added

- Add `job--python-check.yml`.
- Add `job--python-test.yml`.
- Add `python-install.yml`.
