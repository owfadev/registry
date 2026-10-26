# vault-wiki package registry

The official package index of the [vault-wiki](https://github.com/owfadev/owfa) framework — the Obsidian-model registry: packages self-host in their own repos; a one-line PR here is the listing (and trust) gate.

- **Agents / users**: `kernel list-remote` reads [INDEX.yaml](INDEX.yaml); `kernel install <pkg>` resolves against it
- **Authors**: see [how to register](#registering-a-package) below; until listed, your package is still installable directly (`kernel install <owner/repo> --yes`, trust: unknown)

## Packages

| Package | Version | Compat | Contents | Trust | Summary |
|---|---|---|---|---|---|
| [cuhksz](https://github.com/owfadev/pkg-cuhksz) | 0.2 | ≥ 0.2 | cuhksz · bb · bb-map · bb-track · bb-teach · bb-quiz · sis · registry | framework-bundled | CUHK-SZ school domain — bb course ops · sis records · registry |
| [lark](https://github.com/owfadev/pkg-lark) | 0.2 | ≥ 0.2 | lark · lark-docs · lark-im · lark-calendar | framework-bundled | Feishu/Lark domain — docs · im · calendar |
| [email](https://github.com/owfadev/pkg-email) | 0.2 | ≥ 0.2 | email | framework-bundled | personal mailbox domain — mail-cli |
| [bili](https://github.com/owfadev/pkg-bili) | 0.2 | ≥ 0.2 | bili | framework-bundled | bilibili content domain — bili-cli |
| [project](https://github.com/owfadev/pkg-project) | 0.2 | ≥ 0.2 | project | framework-bundled | project container domain |

## Registering a package

One PR, one line in `INDEX.yaml`:

```yaml
  <name>: {repo: https://github.com/<owner>/<repo>, version: X.Y, compat: ">= X.Y", trust: reviewed-3rd-party, members: <slash/separated>, summary: one line — this is the discovery surface, write it for agents}
```

The PR **is** the human-review gate (issue #12 security faces: `inject` text is a constitution-level instruction channel; connectors hold credentials and execute code). Review checks: manifest shape, members == family closure, connector disclosure. On merge: listed in `list-remote`, installable without `--yes`.

Landing rules are mechanical, not editorial — where a plugin lives follows its `depends`:

| Your plugin is… | It lands… |
|---|---|
| a domain member (depends chain reaches a domain root) | that domain package's repo (PR there — the family closure claims it) |
| a new domain of its own | your own repo (PKG.yaml package) + a registry PR here |
| cross-cutting / non-domain | the framework repo's `core/` (owner-reviewed) |
