# Audit Envelope (Phase 0)

This document defines the minimum NDJSON export contract for execution audit
events.

Goal:
- enable local Phase 0 audit exports now
- provide a stable line format that can be forwarded to SIEM pipelines later

One line equals one JSON object (UTF-8, newline-delimited).

## Required Fields

- `schema_version`: envelope schema version (`1.0.0`)
- `timestamp`: RFC3339 UTC timestamp when decision was recorded
- `request_id`: execution request correlation ID
- `tool_digest`: artifact digest (`sha256:...`)
- `policy_hash`: effective policy hash (`sha256:...`)
- `receipt_hash`: receipt hash (`sha256:...`) when available
- `decision`: `allow` or `deny`
- `reason`: short machine-readable/analyst-readable decision reason

## Optional Fields

- `context_id`: control-plane context or tenant execution context
- `signer_ids`: signer identities evaluated for trust
- `caps_requested`: capabilities requested by manifest
- `caps_granted`: capabilities granted by policy
- `caps_used`: capabilities used at runtime
- `input_hash`: canonical input hash
- `output_hash`: canonical output hash
- `runtime_profile`: runtime profile label (for example `v0`, `v1-draft`)

## Schema and Example

- Schema: `docs/audit/execution-event.schema.json`
- Example: `docs/audit/execution-event.example.json`

## Example NDJSON Lines

```json
{"schema_version":"1.0.0","timestamp":"2026-02-14T06:40:00Z","request_id":"req_01JABCDXYZ","tool_digest":"sha256:aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","policy_hash":"sha256:bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb","receipt_hash":"sha256:cccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccc","decision":"allow","reason":"verified_execution_success","caps_used":["env:HOME"]}
{"schema_version":"1.0.0","timestamp":"2026-02-14T06:41:00Z","request_id":"req_01JABCDXY2","tool_digest":"sha256:aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa","policy_hash":"sha256:bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb","receipt_hash":"sha256:0000000000000000000000000000000000000000000000000000000000000000","decision":"deny","reason":"capability_denied:net.http:https://example.com/api"}
```
