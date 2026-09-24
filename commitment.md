# Commitment

```text
idl_digest = SHA-256(canonical_idl_bytes)
code_cell_data = clean_risc_v_executable || idl_digest
```

The final 32 bytes bind an exact IDL artifact to executable data. This proves
binding only, not source, audit, publisher, or registry trust. A future
self-describing trailer with magic bytes and optional discovery hints is a
separate binding-format version and MUST preserve an exact IDL digest.
