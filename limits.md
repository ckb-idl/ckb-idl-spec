# Limits

The final 0.1.0 profile will define `MAX_DOCUMENT_BYTES`,
`MAX_FIELDS_PER_STRUCT`, `MAX_NESTING_DEPTH`, `MAX_VECTOR_ELEMENTS`, and
`MAX_VARIABLE_BYTES_LENGTH`. Implementations reject duplicate field names or
union tags, zero-length fixed bytes, invalid optional ordering, unsupported
types, and malformed prefixes or tags.
