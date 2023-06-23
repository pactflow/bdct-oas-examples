# PactFlow BDCT examples

This repository showcases use cases and features in OpenAPI, how they are compared to pact files and in some cases, how to ensure you get the most out of the comparison checks.

| Example | Problem | 
|---------|---------|
| [`oneOf`](./examples/oneOf) | How to properly use `oneOf` logical operator |
| [`anyOf`](./examples/anyOf) | How to properly use `anyOf` logical operator |
| [`inheritance`](./examples/inheritance) | How to properly use `allOf` with `discriminator` to leverage schema inheritance |
| [Media Types](./examples/mediaTypes) | How to use [media types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) on requests to differentiate request body schemas, using the `Content-Type` header |
| [Content Negotiation](./examples/contentNegotiation) | How to use [content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) on responses to differentiate expected response body schemas, using the `Accept` header |
| [Security](./examples/security) | How to use Authentication and [security schemes](https://swagger.io/docs/specification/authentication/) |
| [Parameters](./examples/parameters) | Understanding request [Parameter](https://swagger.io/docs/specification/describing-parameters/) use cases |
| [Forms, Uploads and Binary](./examples/forms) | Forms, uploads and binary [request content](https://swagger.io/docs/specification/describing-request-body/) use cases |
| [XML](./examples/xml) | XML content use cases |
| [Servers](./examples/servers) | How to test with the use of `servers` |