# Client Object Model

The logical model is normative: unsigned integers, byte strings, lists,
records, absent optional values, and tagged unions have consistent meaning.

```json
{"authorization":{"$tag":2,"$variant":"Signature","value":{"signature":"0x..."}},"memo":null}
```

Language mappings are informative. Rust may use `Vec`, `Option`, structs, and
enums; TypeScript may use `bigint`, `Uint8Array`, objects, and discriminated
unions. Each mapping MUST round-trip the same logical values and pass the
conformance vectors. Encoders reject missing, unknown, or invalid values.
