# Example BDCT comparisons for OAS with logical keywords 

This repository showcases a few examples of BDCT scenarios that tend to trip people up, and the strategies used to fix them.

| Example | Problem | 
|---------|---------|
| [`oneOf`](./examples/oneOf) | How to properly use `oneOf` logical operator |
| [`anyOf`](./examples/anyOf) | How to properly use `anyOf` logical operator |
| [`inheritance`](./examples/inheritance) | How to properly use `allOf` with `discriminator` to leverage schema inheritance |
| [Media Types](./examples/mediaTypes) | How to use [media types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) on requests to differentiate request body schemas, using the `Content-Type` header |
| [Content negotiation](./examples/contentNegotiation) | How to use [content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) on responses to differentiate expected response body schemas, using the `Accept` header |
| [`security`](./examples/security) | How to use security schemes |