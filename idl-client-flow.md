# Using an IDL-enabled CKB Script

## Inputs you need

To construct a witness safely, obtain:

1. the deployed code cell data or a verified deployment receipt;
2. the exact frozen IDL JSON bytes;
3. the bound executable's Binding Trailer 1 or binding manifest; and
4. the script's expected witness interface (`witness_args.lock` in IDL 0.1.0).

Do not trust an IDL merely because it parses. Verify its exact bytes against
the deployed bound code data before using it to encode or sign a witness.

## Verification order

```text
fetch bound code data + frozen IDL
        ↓
validate canonical IDL bytes
        ↓
parse Binding Trailer 1 from code-data end
        ↓
SHA-256(frozen IDL) == trailer digest
        ↓
validate the selected witness_args.lock interface
        ↓
decode/encode witness values in declared field order
```

With the Rust client, commitment verification and document validation must occur
before using decoded fields as trusted wallet data. Parsing alone is not an
authentication step.

## Constructing a witness

1. Select the `witness_args.lock` interface.
2. Supply all required fields in declaration order.
3. Encode optional trailing fields only according to their declared schema.
4. Use explicit union tags; do not infer a tag from variant order.
5. Re-encode and validate the witness before signing/submitting the transaction.

Define whether the deployed code hash means the code cell's data hash or
`Script.code_hash`. With `hash_type = type`, `Script.code_hash` identifies the
type script, not one specific code-cell version. Clients must verify the
selected code cell before trusting its IDL. The trailer identifies the exact
IDL bytes bound to that code data.
exact IDL bytes bound to that executable. A registry may help locate artifacts,
but it is not a replacement for local commitment verification.
