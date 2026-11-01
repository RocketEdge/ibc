# RocketEdge maintenance fork of IBC

This repository is RocketEdge's maintenance fork of [IbcAlpha/IBC](https://github.com/IbcAlpha/IBC),
the login-automation tool for Interactive Brokers Trader Workstation and IB Gateway. The
upstream project was retired and archived on **2026-09-01**; its last release is **3.24.2**
(2026-08-21). RocketEdge depends on IBC inside the `brokersre-ib-gateway` container image and
keeps this fork so a future Gateway UI change can be patched without an upstream maintainer.

## What this fork is

- Branch `master`: upstream history, verbatim, never moved unless upstream un-archives.
- Branch `brokersre` (default): upstream plus this notice, documentation, CI workflows and,
  when necessary, patches.
- Releases `<upstream>-rocketedge.N`. The first, `3.24.2-rocketedge.1`, re-publishes the
  upstream 3.24.2 zips **byte-identical** with SHA-256 checksums so consumers can pin a
  checksum without depending on an archived repository staying online.

## Patch policy

Patches are accepted only for: IB Gateway or TWS UI changes that break login or dialog
handling; security fixes; log-line stability needed by the BrokerSRE agent's log contract. No
features. Every patch ships with an issue carrying reproduction evidence, a minimal diff, a
GPL section 5(a) change notice in each modified file, a green build and a paper-gateway
verification. Patches are offered back to the IBC User Group.

## Licence

IBC is licensed under the GNU General Public License v3.0 (`LICENSE.txt`). This fork is
distributed under the same licence. The complete corresponding source for every release is the
tagged commit in this repository.

Interactive Brokers, IBKR, Trader Workstation, TWS and IB Gateway are trademarks of Interactive
Brokers LLC. RocketEdge is an independent engineering firm and is not affiliated with, sponsored
by or endorsed by Interactive Brokers. IBC is not an Interactive Brokers product.
