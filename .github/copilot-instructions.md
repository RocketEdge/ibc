# CLAUDE.md — RocketEdge/ibc (maintenance fork of IbcAlpha/IBC)

This repository is the RocketEdge maintenance fork of IBC (GPL-3.0), kept because upstream was
archived on 2026-09-01 and the BrokerSRE gateway image depends on it. This file and
`.github/copilot-instructions.md` are the same contract; keep them identical.

## THE COMMANDS

```bash
export IBC_BIN=/path/to/ibgateway/jars      # IB Gateway jars (classpath only)
ant -noinput -buildfile build.xml -Dver=3.24.2 clean dist
ls dist/IBC*-3.24.2.zip
```

CI: `.github/workflows/build.yml` on every push to `brokersre`; `release.yml` on tags
`<upstream>-rocketedge.N`; `verify-upstream.yml` weekly class-list comparison with upstream.

## Rules

1. `master` is upstream history, verbatim. All work happens on `brokersre` (the default branch).
2. **Patch policy** (FORK.md): only Gateway/TWS UI breakage, security fixes and log-line
   stability for the BrokerSRE log contract. No features. Each patch: issue with evidence,
   minimal diff, GPL section 5(a) notice in every modified file, green build, paper-gateway
   verification before release, offered back to the IBC User Group.
3. Release names `<upstream>-rocketedge.N`; the version string is injected with
   `-Dver=<tag>` at build time, so `IbcVersionInfo` reports it. `3.24.2-rocketedge.1` is a
   byte-identical re-upload of upstream's artefacts (SHA-256 in the release notes).
4. No credentials in this repository, ever. `config.ini` in `resources/` is the upstream sample.
5. Docs mandate: `docs/architecture.md`, append-only `docs/changes.md`, `docs/adr/`,
   `docs/limitations.md`.
6. Public repository: no BrokerSRE pricing, client names or Azure identifiers.

## Layout

```text
src/ibcalpha/ibc/   upstream Java sources (83 classes); IbcVersionInfo.java is rewritten by Ant
resources/          scripts, sample config.ini, prebuilt IBC.jar (upstream artefact)
build.xml           Ant build: init -> compile (javac --release 17) -> jar -> dist
userguide.md        upstream user guide (the authoritative IBC documentation)
FORK.md             fork notice, patch policy, licence
docs/, tasks/       RocketEdge additions
```
