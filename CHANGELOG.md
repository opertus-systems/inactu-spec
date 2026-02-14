# Changelog

## Unreleased

- Security remediation for `RUSTSEC-2026-0009`:
  - verified `Cargo.lock` resolves `time` at `0.3.47`
  - verified no `time 0.3.36` remains in the workspace lockfile
  - `cargo audit` clean for the advisory

## 0.1.0 - 2026-02-07

Initial standalone `provenact-spec` release:

- promoted normative spec sources into an implementation-neutral repo
- published JSON schemas for v0 skill, pipeline, policy, registry, and receipts
- published conformance vectors for positive and negative validation cases
- added repository-local conformance runner (`npm run conformance`)
- added versioning and compatibility policy docs
