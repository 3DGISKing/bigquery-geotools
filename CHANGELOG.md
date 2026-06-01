# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.0.4] - 2026-06-01

### Added

- GeoTools **34.3** / GeoServer **2.28.x** support (Java **17+**).
- Maven `gt-bom` dependency management; standalone build without the GeoTools `plugin` parent POM.
- Release ZIP now includes **`gt-geojson`** (required at runtime; not shipped with GeoServer 2.28).
- Maven profile **`integration`** to run BigQuery integration tests that need GCP credentials.
- `GEOSERVER_DATA_DIR` fallback via system property in `BigqueryDataStoreFactory.getCompatibleKeyPath()`.

### Changed

- Version bumped to **0.0.4**.
- Migrated API packages for GeoTools 34:
  - `org.opengis.*` → `org.geotools.api.*`
  - `org.geotools.data.*` (interfaces) → `org.geotools.api.data.*`
  - `FilterFactory2` → `FilterFactory`
- DataStore SPI registration file moved to  
  `META-INF/services/org.geotools.api.data.DataStoreFactorySpi`.
- Cloud Build image: `maven:3-jdk-8` → `maven:3.9-eclipse-temurin-17`.
- Google Cloud Libraries BOM updated to **26.50.0**.
- Assembly / `copy-dependencies` excludes GeoTools JARs already provided by GeoServer; bundles Google Cloud deps and `gt-geojson` only.
- `BigqueryFilterVisitorTest` rewritten to use JTS geometry types (removed deprecated ISO geometry stack).
- README updated for GeoServer 2.28.x build and deploy instructions.

### Removed

- GeoTools **30-SNAPSHOT** parent POM and Google Artifact Registry Maven repository/wagon (build uses OSGeo release repo only).
- `picocontainer` and legacy `gt-geometry` test dependencies.
- Default Surefire run for integration tests (`BigqueryDataStoreTest`, `BigqueryFeatureReaderTest`, `BigqueryFeatureSourceTest`, `GoogleSDKTest`).

### Fixed

- Layer preview / WMS rendering `ClassNotFoundException` for `org.geotools.geojson.geom.GeometryJSON` by including `gt-geojson` in the release ZIP.
- `BigqueryDataStoreFactoryTest.testGetKeyFileFromPath` on Windows when `GEOSERVER_DATA_DIR` is unset.

## [0.0.3-alpha2] - 2023-05-04

### Changed

- Simplified materialized view pregeneration options (`MV_NONE`, `MV_USE_EXISTING`, `MV_PREGEN_ALL`).
- Fixed null pointer on estimated bounds.

## [0.0.3-alpha] - 2023-03-30

### Added

- Pregenerated materialized view support for simplified geometries at multiple tolerances.

## [0.0.2-alpha] - 2023-03-10

### Changed

- Version bump and stability fixes for views and materialized views.

## [0.0.1-alpha] - 2023-02-10

### Added

- Initial public release: BigQuery vector datastore for GeoServer (GeoTools 30 / Java 8).

[Unreleased]: https://github.com/GoogleCloudPlatform/bigquery-geotools/compare/0.0.3-alpha2...HEAD
[0.0.3-alpha2]: https://github.com/GoogleCloudPlatform/bigquery-geotools/compare/0.0.3-alpha...0.0.3-alpha2
[0.0.3-alpha]: https://github.com/GoogleCloudPlatform/bigquery-geotools/compare/0.0.2-alpha...0.0.3-alpha
[0.0.2-alpha]: https://github.com/GoogleCloudPlatform/bigquery-geotools/compare/0.0.1-alpha...0.0.2-alpha
[0.0.1-alpha]: https://github.com/GoogleCloudPlatform/bigquery-geotools/releases/tag/0.0.1-alpha
