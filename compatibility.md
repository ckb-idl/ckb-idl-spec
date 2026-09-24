# Compatibility

`idl_version` is required. Implementations reject unsupported versions and
unknown required top-level keys. Optional extensions use an `x-` prefix.
Unknown `wire_type` values, or semantic `type` values lacking a decodable
`wire_type`, produce an unsupported-interface error.
