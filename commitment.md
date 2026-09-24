# Commitment

IDL 0.1.0 uses Binding Trailer 1:

```text
idl_digest = SHA-256(canonical_idl_bytes)
payload = version_u8 || flags_u8 || hash_algorithm_u8 || idl_digest_32
code_cell_data = executable || payload || payload_length_u32_le || magic_8
```

`version` is 1, `flags` is 0, `hash_algorithm` is 1 (SHA-256), and
`payload_length` is 35. The eight-byte magic is hex `434b4249444c0000`
(`CKBIDL` followed by two zero bytes).

A reader checks the final magic, reads the preceding u32 length, validates that
the payload fits, then reads the payload immediately before the length.
Everything before the payload is the executable. Unknown versions, flags,
algorithms, or invalid lengths MUST be rejected. URI hints are deferred.

The trailer proves binding only, not source, audit, publisher, or registry trust.
