# Changelog

## 6.0 - 2022-11-05

### Changed

- `step--python-install.yml` now expects `make install-python`.

### Removed

- `step--yarn-provision.yml` has been removed.

### Added

- Add `step--node-provision.yml`.
- Add `step--node-install.yml`.

## 5.1 - 2022-10-29

### Added

- Add support for Python 3.11.

## 5.0 - 2022-02-13

### Changed

- Jobs and tasks now expect `make` targets instead of `scripts/`. (Pull #2)

## 4.0 - 2021-10-18

### Added

- Add support for Python 3.10.

### Changed

- `job--python-publish.yml` now requires an explicit `pythonVersion` (previously defaulted to `3.8`).

## 3.4 - 2021-09-09

### Added

- Add `job--python-docs-build.yml`.

### Fixed

- Ensure all job templates use `ubuntu-18.04` by default. This prevents using `ubuntu-16.04` as a default, as AZP is phasing it out by 2021-09-20.

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
