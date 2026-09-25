# CKB IDL Specification

CKB IDL is a machine-readable interface-description format for CKB scripts.

It describes externally supplied script data, including witness layouts,
encodings, and wallet-facing field metadata. IDL 0.1.0 supports the
`WitnessArgs.lock` interface. It does not describe script implementation,
script arguments, source provenance, audits, deployment history, or publisher
identity.

The `0.1.0` release defines:

- the IDL document format;
- linear witness encoding;
- fixed bytes, integers, bytes, vectors, nested structs, and unions;
- canonical JSON bytes;
- executable-to-IDL SHA-256 commitments;
- normative conformance vectors.

Reference implementations are maintained separately. Start with [SPEC.md](SPEC.md).
Deferred features are listed in the non-normative [ROADMAP.md](ROADMAP.md).
