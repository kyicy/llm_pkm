# Supply Chain Attack Prevention

> Sources: Rei, 2026-05-24
> Raw: [preventing-supply-chain-attacks.md](../../raw/security/2026-05-28-preventing-supply-chain-attacks.md)

## Overview

Supply chain attacks via package managers and editor extensions have become increasingly common in 2026. The core defense strategy is to introduce a "cooldown" period before automatically applying package or extension updates, reducing the window of exposure to malicious code published to registries.

## 2026 Supply Chain Attack Incidents

Three notable incidents occurred in 2026:

- **March 2026** — axios npm package attack
- **May 2026** — TanStack npm package attack
- **May 2026** — VS Code extension supply chain attack (suspected vector for GitHub breach)

Package registries generally lack proactive security scanning for newly published versions, making cooldown mechanisms on the developer side the primary practical defense.

## Package Manager Cooldown Settings

### GitHub Dependabot

Dependabot supports a cooldown configuration for version updates (not security updates):

```yaml
- package-ecosystem: <name>
  cooldown:
    default-days: 7
```

Only applies to non-security version updates.

### NPM

NPM v11.10.0+ supports `min-release-age`:

```
npm config set min-release-age 7
```

Other JavaScript package managers offer similar mechanisms.

### Bundler (Ruby)

Bundler does not yet support cooldown. A community discussion is ongoing: https://github.com/ruby/rubygems/discussions/9113

## Editor Extension Auto-Update Controls

### VS Code

VS Code allows disabling automatic extension updates in settings. Documentation: https://code.visualstudio.com/docs/configure/extensions/extension-marketplace#_extension-autoupdate

### Zed

Zed does not yet support disabling automatic extension updates. A feature request is under discussion: https://github.com/zed-industries/zed/discussions/38661
