# Key Management Runbook

This runbook defines Phase 0 operator practices for signer keys and trust
anchors across the Provenact ecosystem.

Scope:
- trust anchor file: `public-keys.json`
- trust anchor pin: `--keys-digest sha256:<64 lowercase hex>`
- verified flows: `verify`, `run`, and receipt verification paths

## Day-0 Bootstrap

1. Create signer keypairs offline.
- Use an approved process/HSM for Ed25519 key generation.
- Keep private keys out of Git repositories and CI logs.

2. Publish trust anchors.
- Build `public-keys.json` with approved signer public keys.
- Commit/distribute this file through controlled release channels.

3. Pin the trust anchor digest.
- Compute digest:
  `KEYS_DIGEST="$(shasum -a 256 ./public-keys.json | awk '{print "sha256:"$1}')"`
- Require this value anywhere verified execution is allowed.

4. Validate before rollout.
- Run golden path:
  `pack -> sign -> verify -> run -> verify-receipt`.
- Confirm `verify`/`run` fail closed when digest pin is missing or stale.

## Planned Rotation Drill

Run quarterly, or before major release milestones.

1. Add the new public key to `public-keys.json` while keeping old key(s) for overlap.
2. Compute and publish a new digest pin.
3. Re-sign current release bundles with the new key.
4. Validate verified execution using the new pin.
5. Roll out updated trust anchors and digest pin atomically where possible.
6. Remove retired key after overlap, then repeat digest-pin rollout.

## Emergency Revocation

Use when a signer key is suspected compromised.

1. Remove compromised key from `public-keys.json` immediately.
2. Compute new digest pin and distribute with highest priority.
3. Block execution of artifacts signed only by revoked key.
4. Re-sign required artifacts with healthy signer keys.
5. Record incident evidence:
- previous/new trust-anchor files (or redacted fingerprints)
- old/new digest pins
- affected artifacts and environments
- timeline of detection, containment, and recovery

## Operational Controls

- Treat trust-anchor updates as change-controlled releases.
- Require peer review on signer set changes.
- Store approved digest pins in deployment configuration, not ad-hoc shell state.
- Keep rotation/revocation logs with timestamps for audits.
