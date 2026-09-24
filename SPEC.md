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

Every document has `idl_version`, `encoding`, and `witness`:

```json
{"idl_version":"0.1.0","encoding":{"id":"ckb-idl-linear-0.1.0"},"witness":[]}
```
```
