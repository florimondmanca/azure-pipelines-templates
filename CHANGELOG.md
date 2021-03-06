# Changelog

## 3.3 - 2020-11-01

### Added

- Add support for Python 3.9.

## 3.2.1 - 2020-11-01

_Also available as `3.2`._

### Fixed

- Improve resilience to Codecov unavailability by allowing coverage uploads to fail in `step--python-test.yml`.

## 3.2.0 - 2020-06-07

_Also available as `3.2`._

### Added

- Add `job--python-publish--tag.yml`.

## 3.1 - 2020-05-02

### Added

- Add `step--python-provision.yml`.
- Add `step--yarn-provision.yml`.

## 3.0 - 2020-04-12

### Changed

- `job--python-test.yml` now expects a `jobs` mapping.

### Added

- Add `step--python-test.yml` (extracted from `job--python-test.yml`).

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
