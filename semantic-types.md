# Semantic Type Registry 0.1.0

Semantic `type` labels give wallets and humans meaning while `wire_type`
remains authoritative for encoding.

| Type | Required wire type | Meaning |
|---|---|---|
| `secp256k1_sig` | `bytes_fixed_65` | 64-byte compact ECDSA signature plus one recovery-id byte |
| `secp256k1_pubkey` | `bytes_fixed_33` | Compressed secp256k1 public key |
| `schnorr_sig` | `bytes_fixed_64` | 64-byte Schnorr signature |
| `blake2b_hash` | `bytes_fixed_32` | CKB Blake2b-256 digest |

Standard labels are unnamespaced. Custom labels MUST use
`project-name:type_name`, for example `acme-wallet:withdrawal_proof`. The
namespace identifies the project defining the meaning; IDL 0.1.0 does not
provide global namespace ownership or resolution. Registries MAY associate a
namespace with project metadata, but that association does not change the
committed IDL bytes.

Unknown semantic labels are usable only when a supported structural
`wire_type` is present. A client may decode such a value opaquely while
reporting that its semantic meaning is unsupported.
