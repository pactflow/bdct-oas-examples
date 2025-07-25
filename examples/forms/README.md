# Form, multipart uploads and binary body examples

Form bodies encoded as `x-www-form-urlencoded` are decoded as URL query strings and validated against their schema (via https://nodejs.org/api/querystring.html).

Multipart (`multipart/form-data`) form submissions have basic support. Only the metadata of the request such as the correct `content-type` header are checked. Schema matching on request bodies is not performed.

Binary bodies (request/response) are similarly ignored, with only `content-type` being checked to match.