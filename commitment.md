# Commitment

IDL 0.1.0 uses Binding Trailer 1:

```text
idl_digest = SHA-256(canonical_idl_bytes)
payload = version_u8 || flags_u8 || idl_digest_32
code_cell_data = executable || payload || payload_length_u32_le || magic_8
```

`version` is 1, `flags` is 0, and `payload_length` is 34. SHA-256 is the only
hash algorithm in Trailer 1. The eight-byte magic is hex `434b4249444c0000`
(`CKBIDL` followed by two zero bytes).

A reader with total length `N` requires `N >= 46`, compares `[N-8,N)` exactly
with the magic, reads `[N-12,N-8)` as a little-endian u32, requires length 34,
and computes `payload_offset = N - 46`. Bytes before that offset are the clean
executable. Unknown versions, non-zero flags, and invalid lengths are rejected.
Digest mismatch immediately returns `commitment_mismatch`.

Binding tools MUST reject an input already ending in a valid trailer. Rebinding
starts from the preserved clean executable. URI hints are deferred.

The trailer proves binding only, not source, audit, publisher, or registry trust.
