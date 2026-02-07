# Compatibility Matrix

Compatibility snapshot for active repositories against `inactu-spec` v0.

Status legend:
- `compatible`: validated against v0 stable contracts and vectors.
- `partial`: implements subset, missing full vector parity.
- `planned`: not yet aligned to public conformance gates.

| Repository | Role | Status | Notes |
| --- | --- | --- | --- |
| `inactu-cli` | Reference runtime and verifier CLI | compatible | Primary source of current v0 implementation evidence |
| `inactu-sdk` | SDK parsers/bindings and developer APIs | partial | Conformance smoke tests exist; full vector parity is in progress |
| `inactu-control` | Control plane services | planned | Must consume schema-validated receipts and policy docs |
| `inactu-control-web` | Control plane UI | planned | Must treat receipts/events as external schema contracts |
| `inactu-agent-kit` | Integration adapters | partial | Should pin and validate manifests/receipts before invocation |
| `inactu-skills` | Released/pinned skill bundles | partial | Should enforce manifest/signature schema checks at publish time |

## Compatibility Process

When a repo claims `compatible` status:

- CI must pin `inactu-spec` by tag.
- CI must pass schema/vector checks relevant to that repo's surface.
- Any divergence must be recorded with a dated exception note.
