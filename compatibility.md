# Compatibility

`idl_version` is required. Implementations reject unsupported versions and
unknown keys at every document depth. IDL 0.1.0 has no extension mechanism.
Unknown `wire_type` values, or semantic `type` values lacking a decodable
`wire_type`, produce an unsupported-interface error.

Standard semantic types are defined by this specification. Custom semantic
types MUST be namespaced as `namespace:name`; unnamespaced custom labels are
invalid. Extension namespaces are deferred to a later version.
