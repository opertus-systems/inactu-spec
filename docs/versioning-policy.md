# Versioning Policy

This policy defines how spec changes are versioned and consumed.

## Contract Levels

- `stable`: files listed in `SPEC.md` under Normative Sources.
- `experimental`: files containing `experimental` in the name and docs in
  `spec/rfcs/`.
- `informational`: guides and background docs not listed as normative.

## Semantic Rules

- Patch (`0.1.x`): clarifications, typo fixes, stricter invalid-case rejection,
  and additional conformance vectors. No change in valid payload semantics.
- Minor (`0.x+1.0`): additive optional fields/rules preserving backward
  verification compatibility.
- Major (`1.0.0+`): any breaking semantic change to stable contracts.

## Breaking Change Requirements

A breaking change to a stable schema/rule requires:

- a new schema version identifier
- migration guidance in `CHANGELOG.md`
- updated vectors for old and new behavior
- explicit compatibility statement in `docs/compatibility-matrix.md`

## Pinning Guidance

Consumers should pin by git tag and lock these paths:

- `SPEC.md`
- `spec/`
- `test-vectors/`

Never pin implementation behavior as a substitute for spec pinning.
