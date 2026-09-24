# CKB IDL 0.1.0 Specification

This is the entry point for the language-neutral CKB IDL draft.

## Normative documents

- [JSON schema](schema/idl-0.1.0.schema.json)
- [Linear encoding profile](encoding/linear-0.1.0.md)
- [Canonicalization](canonicalization.md)
- [Commitment](commitment.md)
- [Compatibility](compatibility.md)
- [Limits](limits.md)
- [Client object model](client-object-model.md)
- [Conformance vectors](test-vectors/README.md)

Every document has `idl_version` and `interfaces`. IDL 0.1.0 permits exactly one
interface, of kind `witness_args.lock`:

```json
{"idl_version":"0.1.0","interfaces":[{"encoding":{"id":"ckb-idl-linear-0.1.0"},"fields":[],"id":"lock_witness","kind":"witness_args.lock"}]}
```

Interface and field identifiers MUST match `[A-Za-z_][A-Za-z0-9_]*`.
Interface ids MUST be unique. Extensions are not supported in 0.1.0; unknown
keys MUST be rejected. Future interface kinds are listed in [ROADMAP.md](ROADMAP.md).
