# Stable Errors and Paths

IDL 0.1.0 categories are `invalid_document`, `unsupported_version`,
`unsupported_interface`, `unsupported_encoding`, `unknown_type`,
`non_canonical_document`, `field_too_short`, `invalid_length`,
`invalid_vector_count`, `unknown_union_tag`, `trailing_bytes`,
`integer_overflow`, `resource_limit_exceeded`, `invalid_trailer`, and
`commitment_mismatch`.

`path` uses RFC 6901 JSON Pointer over the logical object: `/signature`,
`/authorization/value/signature`, or `/signatures/1`. Document-validation
errors use pointers such as `/interfaces/0/fields/1/type`. Whole-document or
whole-buffer errors use the empty path `""`.
