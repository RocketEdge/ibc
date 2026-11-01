# Limitations

| # | Limitation | What resolves it |
|---|---|---|
| L01 | Builds are not byte-reproducible: Ant stamps jar and zip entries with build time. `verify-upstream.yml` compares class lists and sizes instead. | Add `modificationtime` to the jar/zip tasks as a declared patch if byte identity is ever required. |
| L02 | The build classpath needs the IB Gateway jars, fetched from IBKR's unversioned stable URL at build time; a Gateway release that changes the jar layout can break compilation without any change here. | Pin the installer SHA-256 from the BrokerSRE archive once it exists; watch `build.yml`. |
| L03 | No paper or live login is exercised in CI; a Gateway UI change is only detected when the BrokerSRE sandbox or a client gateway fails to log in. | The BrokerSRE regression suite on the paper environment (operator-gated). |
| L04 | Upstream intended an IBC 4.0 that never shipped; outstanding upstream issues remain open with no maintainer. | Triage upstream's open issues when a patch is needed; nothing proactive. |
