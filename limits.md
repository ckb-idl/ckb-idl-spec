# IDL 0.1.0 Resource Limits

The values in this document are the candidate IDL 0.1.0 limits. They record the
current protocol decision, but remain provisional until they are benchmarked in
the registry, a browser/WASM client, and a representative mobile environment.
They MUST NOT be described as finalized normative limits until that validation
is complete.

| Resource | Candidate maximum |
|---|---:|
| Canonical IDL document bytes | 20,480 |
| Schema nesting depth | 5 |
| Interfaces | 1 |
| Fields in one `fields` array | 128 |
| Fields across the complete document | 256 |
| Variants in one union | 64 |
| Variants across the complete document | 128 |
| Identifier UTF-8 bytes | 128 |
| Description UTF-8 bytes per field | 4,096 |
| Fixed byte-array length `N` | 4,096 |
| Elements in one encoded vector | 4,096 |
| Values in one decoded object graph | 4,096 |
| Witness input or encoded output bytes | 1,048,576 |

Applications MAY apply stricter operational limits. Once finalized, every
compliant derive/exporter, commitment tool, registry, and client MUST enforce
the normative values consistently.

## Counting rules

### Document bytes

Document size is the length of the exact RFC 8785 canonical UTF-8 artifact.
Clients and registries check this limit before JSON parsing whenever possible.
For compressed transport, the limit applies after decompression.

### Schema depth

Fields directly inside an interface are at depth 1. Entering a struct's
`fields` array or a union variant's `fields` array increments depth by one.
Vectors do not increment recursive depth in IDL 0.1.0 because vector elements
cannot be structs, unions, vectors, variable bytes, or optional values.

### Aggregate fields and variants

Total counts include every declared field and every union alternative,
including alternatives that are not selected while decoding a particular
witness.

### Decoded values

Decoded-object accounting uses the following rules:

- a scalar or byte string counts as one value;
- a struct counts as one value plus all child values;
- a union counts as one value plus all values in the selected payload;
- a vector counts as one value plus every element;
- an absent optional counts as one value; and
- a present optional counts as one value plus its contained value.

### Strings

Identifier and description limits are measured as UTF-8 bytes, not Unicode
scalar values. IDL 0.1.0 identifiers are ASCII, so identifier byte and character
counts are identical.

## Enforcement points

Limits are checked at every stage where exceeding them could consume resources:

1. Derive/export tooling rejects an oversized schema during development.
2. Commitment tooling refuses to bind a document exceeding any document limit.
3. Registries enforce decompressed upload and response limits before parsing.
4. Clients enforce document limits before parsing and schema limits while
   validating.
5. Decoders and encoders check witness, vector, and object limits before
   allocating proportional memory.

An over-limit input uses the stable category `resource_limit_exceeded`. The
error identifies the resource, configured limit, actual value, and the nearest
logical or document path. For example:

```text
category: resource_limit_exceeded
path: /interfaces/0/fields
resource: total_fields
limit: 256
actual: 257
```

Every finalized limit requires conformance vectors for the exact boundary and
for one unit above it.

## Validation before finalization

The candidate values are finalized only after measuring maximum legal and
adversarial inputs for:

- peak heap usage during parsing, canonicalization, validation, decoding, and
  encoding;
- execution time in native Rust and browser/WASM;
- stack safety at maximum nesting depth;
- decompression and registry bandwidth behavior; and
- rejection before proportional allocation for every over-limit case.

Implementations also reject duplicate field or variant names, duplicate union
tags, zero-length fixed bytes, invalid optional ordering, unsupported types,
and malformed prefixes or tags. These are validity rules rather than resource
limits.
