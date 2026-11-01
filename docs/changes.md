# Change Log — RocketEdge/ibc

Append-only; newest first. Fields: Date, What changed, Result, What did NOT work / root cause,
Next step.

## Change History

### 2026-11-01 — Fork bootstrapped; 3.24.2 re-released byte-identical

- **What changed:** Forked the archived `IbcAlpha/IBC` into `RocketEdge/ibc`; added branch
  `brokersre` (default) with `FORK.md`, security policy, CODEOWNERS, Dependabot, `build.yml`,
  `release.yml`, `verify-upstream.yml`, docs mandate and agent contract files; re-released
  upstream's 3.24.2 zips unchanged as `3.24.2-rocketedge.1` with SHA-256 checksums.
- **Result:** SHA-256 of the re-released artefacts: Linux
  `cc097ca1dfa75413a5fbe02e4743050af15f3308eb6a97c769b3cff9850c80c5`, macOS
  `2449ef36d758ea56c6ca15fc6b6c4cbe626c8f0a95e36f6455c717ee390add93`, Windows
  `ba8e95f61f3c7c252620baef41e550c6aab98f6034179156e11a9a1623fdd892`.
- **What did NOT work / root cause:** the upstream `.gitignore` pattern `.*` would have hidden
  `.github/` from git; a `!.github/` negation was added. The build cannot be reproduced byte for
  byte because Ant's jar and zip tasks stamp file times; the weekly verification therefore
  compares class lists, not bytes (`docs/limitations.md`).
- **Next step:** nothing until a Gateway UI change breaks login; then a patch per the policy.
