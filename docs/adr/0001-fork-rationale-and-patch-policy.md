# ADR 0001 — Fork the archived IBC; patches only for breakage, security and log stability

- **Status:** Accepted (2026-11-01)

## Context

IBC automates the IB Gateway login by watching Swing dialogs by title. Upstream
(`IbcAlpha/IBC`, GPL-3.0) was retired and archived on 2026-09-01 (README, discussion 347);
3.24.2 (2026-08-21) is the last release and supports Gateway 10.48 onwards. Every headless
Gateway deployment, including BrokerSRE's container image, depends on it. A future Gateway
build can rename a dialog and break login with nobody to fix it.

## Decision

Fork into `RocketEdge/ibc`. `master` mirrors upstream verbatim; `brokersre` (default) carries
documentation, CI and patches. Patches are accepted only for Gateway/TWS UI changes that
break login or dialog handling, security fixes and log-line stability required by the
BrokerSRE agent's log contract. No features. Each patch carries a GPL section 5(a) change
notice, a green build, a paper-gateway verification and is offered to the IBC User Group.

## Consequences

### Positive

BrokerSRE owns its most fragile dependency; a fix can ship in hours.

### Negative

RocketEdge now carries IBC maintenance risk and GPL obligations (complete corresponding
source = the tagged commit; notices on modified files).

## Revisit trigger

A maintained community successor with equivalent coverage appears, or IBKR ships a headless
Gateway that needs no UI automation.
