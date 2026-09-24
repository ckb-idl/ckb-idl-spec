# Client Object Model

Clients decode and encode structured objects. Structs become nested objects;
absent options are `null` / `None`; unions expose `$tag`, `$variant`, and
`value`.

```json
{"authorization":{"$tag":2,"$variant":"Signature","value":{"signature":"0x..."}},"memo":null}
```

Encoders reject missing required, unknown, and structurally invalid values.
