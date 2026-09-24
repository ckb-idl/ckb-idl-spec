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

Identifiers match `[A-Za-z_][A-Za-z0-9_]*`. Standard semantic types are
unnamespaced. Custom semantic types use `namespace:name`.
