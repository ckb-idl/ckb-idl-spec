# Canonicalization

IDL commitment bytes are UTF-8 JSON canonicalized under RFC 8785. Producers
MUST write canonical bytes before binding; binders MUST validate and hash those
same bytes or reject them. They MUST NOT silently rewrite, pretty-print, or
minify input.

Object key order is non-semantic and canonically lexicographic. Interface and
nested field arrays are semantic wire order. Union variants are serialized by
ascending tag.

`canonicalization-fixtures.json` records the required SHA-256 digest of each
canonical example. Implementations MUST reproduce those hashes.
