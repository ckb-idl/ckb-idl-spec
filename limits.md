# Limits

The following are normative protocol limits for IDL 0.1.0.

| Limit | Value | Reason |
|---|---:|---|
| Maximum IDL document | 256 KiB | Enough for rich docs, still safe to fetch/cache |
| Fields in one struct | 128 | Large enough for real interfaces, prevents pathological schemas |
| Total fields recursively | 512 | Stops schema expansion abuse |
| Nesting depth | 16 | More than enough for practical witness models |
| Union variants | 64 | Keeps UI and decoder dispatch manageable |
| Vector element count | 4,096 | Prevents unbounded decode loops |
| Variable bytes per field | 1 MiB | Safe generic-client default; scripts may impose stricter limits |
| Total decoded witness payload | 2 MiB | Prevents a client from allocating indefinitely |
| Field/type name length | 128 bytes | Enough for readable identifiers |
| Description length | 4 KiB | Enough for UI/help text |

Every compliant implementation MUST enforce these limits. Applications MAY
apply stricter limits. Implementations also reject duplicate field names or
union tags, zero-length fixed bytes, invalid optional ordering, unsupported
types, and malformed prefixes or tags.
