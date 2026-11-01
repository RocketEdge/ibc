# ADR 0002 — Releases `<upstream>-rocketedge.N`; first release byte-identical; class-list verification

- **Status:** Accepted (2026-11-01)

## Context

The BrokerSRE gateway image pins IBC by SHA-256 and downloads it from this repository rather
than from an archived one. The image repository's own build needs an IBC release to exist
before it can be built, while building IBC needs Gateway jars that only the image repository
archives: a circular dependency on day one.

## Decision

- Release names are `<upstream version>-rocketedge.<N>`; the version string is injected at
  build time with `-Dver=<tag>` so `IbcVersionInfo` reports the exact release.
- `3.24.2-rocketedge.1` is a byte-identical re-upload of upstream's three zips with SHA-256
  checksums, created by hand; this breaks the cycle. From the first patched release onwards,
  `release.yml` builds from source, signs with cosign (keyless) and attaches provenance.
- `verify-upstream.yml` rebuilds weekly and compares the class list and sizes of the produced
  `IBC.jar` with upstream's; byte identity is not claimed because Ant stamps timestamps.

## Consequences

### Positive

Consumers get a stable, checksummed, signed download path; drift in the toolchain is noticed
weekly.

### Negative

The first release is not built by CI (documented in its notes); the build depends on IBKR's
unversioned installer URL for classpath jars.

## Revisit trigger

A patched release is needed (then `release.yml` is exercised for real), or IBKR publishes
versioned, checksummed installers.
