# Security Policy

Report vulnerabilities in this fork to **security@rocketedge.com**; do not open a public issue.
Acknowledgement within two business days (Singapore time).

Scope: the code on the `brokersre` branch and the release artefacts `IBC*-<version>.zip`
published from this repository. Upstream `IbcAlpha/IBC` is archived and no longer accepts
reports; issues that also affect upstream are posted to the IBC User Group.

IBC handles the Interactive Brokers username and password that the operator supplies in
`config.ini`. This fork does not change how those credentials are read or stored. Releases are
signed with Sigstore cosign (keyless, GitHub Actions identity) and carry SHA-256 checksums.
