# Contributing

CKB IDL is language-neutral. Proposals should describe the problem, affected
wire/document behavior, compatibility impact, and a motivating use case.

Normative pull requests update the specification, JSON Schema, examples,
vectors, errors, and changelog together. Use `MUST`, `SHOULD`, and `MAY` only
for normative rules. Preserve RFC 8785 fixture bytes, add valid and malformed
vectors, and never change a released version in place.

Before submission, validate all JSON, reproduce fixture hashes, check links,
and run available implementations against the vectors. Protocol changes should
receive review from two independent implementations when possible. Security-
sensitive changes require explicit compatibility and threat-model discussion.
