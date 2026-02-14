# Enterprise Policy Templates (Phase 0)

These templates are starting points for enterprise policy baselines.

Files:
- `policy.paranoid.json`
- `policy.http_allowlist.json`
- `policy.fs_workspace_only.json`
- `policy.secrets_handles_only.json`

All templates target the v0 policy contract:
- `spec/policy/policy.schema.json`
- `spec/policy/policy.md`

## Important Notes

- Policies are deny-by-default. Omitted capability kinds are denied.
- Replace placeholder signer IDs with your own trusted signer set before use.
- Replace placeholder paths/hosts/keys with environment-specific values.

## Capability Vocabulary Mapping

- HTTP allowlisting maps to `capability_ceiling.net` URI-prefix matching.
- Filesystem restriction maps to `capability_ceiling.fs.read/write` absolute-path
  prefixes.
- Secret-handle restriction maps to `capability_ceiling.kv.read/write` exact-key
  allowlists.

Method-specific HTTP controls are not encoded in v0 policy schema. Enforce
method constraints in an upstream proxy/service policy layer.
