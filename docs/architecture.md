# Architecture

## IBC process model (as shipped by upstream)

```mermaid
flowchart LR
  start["gatewaystart.sh / ibcstart.sh"] --> ibc["IBC (Java, ibcalpha.ibc.IbcGateway)"]
  ibc -- "launches in-process" --> gw["IB Gateway (Java Swing UI)"]
  ibc -- "watches dialogs by title, fills login, clicks buttons" --> gw
  cfg["config.ini"] --> ibc
  cmd["Command server (TCP, CommandServerPort)\nSTOP RESTART PAUSE RECONNECTDATA RECONNECTACCOUNT ENABLEAPI EXIT"] --> ibc
  gw -- "TWS API socket 4001/4002" --> api["API clients"]
```

## Fork and patch flow

```mermaid
flowchart LR
  up["IbcAlpha/IBC master (archived 2026-09-01)"] --> master["RocketEdge/ibc master (verbatim)"]
  master --> br["brokersre branch (default): FORK.md, docs, workflows, patches"]
  br -- "tag <upstream>-rocketedge.N" --> rel["release.yml: ant dist, SHA-256, cosign, provenance"]
  rel --> img["brokersre-ib-gateway image (versions.json pins IBC sha256)"]
  br -- weekly --> verify["verify-upstream.yml: class list == upstream 3.24.2"]
```

The build needs the IB Gateway jars on the classpath (`IBC_BIN`); CI downloads the current
stable installer from IBKR for that purpose only. No IBKR binary is redistributed from here.
