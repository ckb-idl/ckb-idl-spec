# Compatibility

`idl_version` is required. Implementations reject unsupported versions and
unknown keys at every document depth. IDL 0.1.0 has no extension mechanism.
Unknown `wire_type` values, or semantic `type` values lacking a decodable
`wire_type`, produce an unsupported-interface error.

0.1.0 implementations support exactly `0.1.0` and reject all other document
versions until explicitly implemented. Any document-schema change requires a
new IDL version. The semantic-type registry may be versioned independently when
a label does not alter structural encoding.

Standard semantic types are defined by this specification. Custom semantic
types MUST be namespaced as `namespace:name`; unnamespaced custom labels are
invalid. Extension namespaces are deferred to a later version.
