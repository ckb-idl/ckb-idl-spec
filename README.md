# CKB IDL Specification

CKB IDL is a machine-readable interface-description format for CKB scripts.

It describes externally supplied script data, including witness layouts, script arguments, encodings, and wallet-facing field metadata. It does not describe script implementation, source provenance, audits, deployment history, or publisher identity.

The `0.1.0` release defines:

- the IDL document format;
- linear witness encoding;
- fixed bytes, integers, bytes, vectors, nested structs, and unions;
- canonical JSON bytes;
- executable-to-IDL SHA-256 commitments;
- normative conformance vectors.

Reference implementations are maintained separately