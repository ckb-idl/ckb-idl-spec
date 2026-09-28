# Writing an IDL-enabled CKB Script

## Files to create

```text
contracts/my-lock/
├── Cargo.toml
├── Makefile
├── src/
│   ├── main.rs       # on-chain validation logic
│   ├── witness.rs    # shared witness schema
│   └── error.rs
└── examples/
    └── export_idl.rs # host-side canonical-IDL exporter
```

Keep contract behavior in `main.rs`. Put only the public witness types in
`witness.rs`, so the contract and host exporter use the same definitions.

```rust
// src/witness.rs
use alloc::vec::Vec;
use ckb_idl_derive::CkbWitness;

#[derive(CkbWitness)]
pub struct Witness {
    pub proof: Vec<u8>,
}
```

```rust
// src/main.rs
extern crate alloc;
mod witness;
use witness::Witness;

// Decode and validate Witness in the normal contract entry point.
```

```rust
// examples/export_idl.rs
extern crate alloc;
#[path = "../src/witness.rs"]
mod witness;
ckb_idl_export::export_idl_main!(witness::Witness);
```

Add `ckb-idl-export` as a host-only dev dependency. Do not make the on-chain
contract generate or write IDL files.

## Build and package order

1. Build the CKB executable with the repository Makefile.
2. Run the host exporter to write the canonical IDL artifact.
3. Run `ckb-idl bind` with the clean executable and exported IDL.
4. Run `ckb-idl verify` against the three produced bundle members.
5. Deploy the bound executable unchanged.

```text
make package CONTRACT=my-lock
make test-bound CONTRACT=my-lock
make deploy CONTRACT=my-lock
```

The package contains the bound executable, byte-identical frozen IDL, and
canonical binding manifest. Never append a hash during deployment and never
pretty-print or regenerate the frozen IDL after binding.

## Design constraints

- Give unions explicit stable `#[witness(tag = N)]` tags.
- Preserve field declaration order; it is wire order.
- Treat exporter output as authoritative for recursive schemas.
- Keep the executable/IDL inputs immutable; binding writes a new bundle only.
