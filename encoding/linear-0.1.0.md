# Linear Encoding Profile 0.1.0

`ckb-idl-linear-0.1.0` encodes fields sequentially in array order.

In IDL 0.1.0 it is declared on the sole `witness_args.lock` interface.

| Type | Encoding |
|---|---|
| `uint8`, `uint16`, `uint32`, `uint64`, `uint128` | little-endian unsigned integer |
| `bytes_fixed_N` | exactly `N > 0` bytes |
| `bytes` | u32 LE byte length then bytes |
| `vector` | u32 LE element count then elements |
| `union` | u32 LE tag then selected variant fields |

`type` is wallet-facing meaning; `wire_type`, when present, is the structural
type a decoder uses. Optional fields use `required: false`, must be trailing,
and are absent by buffer exhaustion. `bytes` with length zero remains present.

Nested `fields` arrays retain declaration/wire order. Union tags are unique,
stable, and variants are sorted by tag.

Trailing bytes MUST fail. Length, count, cursor, and allocation calculations
use checked arithmetic; overflow MUST fail before reading or allocating.

Structs, union variant lists, and encoded vectors MUST be non-empty. Typed
vector elements are limited to `uint16`, `uint32`, `uint64`, `uint128`, and
`bytes_fixed_N`; `Vec<u8>` is `bytes`. Vectors of structs, vectors, unions,
variable bytes, or optional elements are unsupported.

Optional structs and unions are unsupported. Union variants are not optional.
Fields inside a selected variant follow normal rules, including trailing-only
optional fields.

Identifiers match `[A-Za-z_][A-Za-z0-9_]*`. Standard semantic types are
unnamespaced. Custom semantic types use `namespace:name`.
