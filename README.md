> **DEPRECATED.** The `-all` aggregators are retired — the default bundle is defined by `@plurnk/plurnk-service`'s own dependencies; optional plugins are installed individually. See `plurnk/plurnk-service` MIGRATION.md.

# @plurnk/plurnk-schemes-all

Batteries-included bundle for [plurnk-service](https://github.com/plurnk/plurnk-service)'s external `scheme` discovery. **It ships no code** — it's a single dependency that pulls in every first-party [`@plurnk/plurnk-schemes-*`](https://github.com/plurnk/plurnk-schemes) sibling, **flat**, so one install surfaces them all to the service's scope-agnostic `node_modules` scan (`plurnk.kind:"scheme"`).

```
npm i @plurnk/plurnk-schemes-all
```

Bundles:

| | scheme |
|---|---|
| `@plurnk/plurnk-schemes-http` | `http://`, `https://` (fetch + headless-Chromium render) |

## Why a bundle, not framework deps

The framework — [`@plurnk/plurnk-schemes`](https://github.com/plurnk/plurnk-schemes) — stays **contract-only** so it has no circular deps and so service's discovery scan can find scheme siblings at the top level of `node_modules`. This aggregator depends on the daughters *directly*, so npm hoists them flat — discovery sees them. The framework arrives transitively as each daughter's exact peer; it is **not** a dependency here (it declares no `plurnk.kind`, so the scan ignores it anyway).

A **third party** publishes their own scheme under their own scope (`@acme/acme-scheme-foo`, `plurnk.kind:"scheme"`) and installs it alongside — service's scan finds it by kind, no bundle membership required (plurnk-service#227). The bundle is just the convenient first-party default, never a gate.

Want a subset? Skip this and depend on the individual scheme packages you want — discovery treats them identically.