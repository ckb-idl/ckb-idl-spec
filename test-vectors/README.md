# Conformance Vectors

Vectors bind an exact IDL fixture to `wire_hex` and either `expected_object`
or an exact error category/path. Add valid flat, nested, vector, union, and
optional cases plus malformed-prefix, malformed-tag, and truncation cases.

Error `path` values use RFC 6901 JSON Pointer as defined in [errors.md](../errors.md).
`valid.json` contains successful scalar and recursive cases; `malformed.json`
contains stable error categories and paths.

`malformed-documents.json` covers conditional schema and semantic validation.
`canonicalization.json` distinguishes valid JSON from valid canonical artifact
bytes.
