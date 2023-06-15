# Form, multipart uploads and binary body examples

Current support for forms (`x-www-form-urlencoded`) and multipart (`multipart/form-data`) is basic, only checking the metadata of the request such as the correct `content-type` is set. Schema matching on request bodies is not performed.

Binary bodies (request/response) are similarly ignored, with only `content-type` being checked to match.