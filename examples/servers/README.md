# `servers` example

OpenAPI provides the option to specify one or more [`server`](https://spec.openapis.org/oas/v3.1.0#serverObject) objects are various places in the spec. These are commonly used to specify one or more environments in which the API Provider is running. It will often include a context or base path in the URL that the API will behind - for example `/v1` for a versioned API.

However, the spec does not assign any semantic meaning to the component and users are free to use them in various ways. Let's explore the complexity behind this 

PactFlow _does not_ support using URLs specified in `server` objects in matching resources in an OAS.

## Background

Let’s assume a consumer contract has a request to path `/mybaseurl/resource` while the OAS has the following:

```
servers:
  - url: https://foo.com/mybaseurl
```

and then defines the resource as:

```
  /resource
    post:
      ...
```

This is easy enough for us to support - the resource identified in the OAS to compare against the pact file is `/resource`, as we can join the path in servers and get a “resolved” URL of `/mybaseurl/resource`.

Let's further assume that the are in fact two environments:

```
servers:
  - url: https://foo.com/mybaseurl
  - url: https://staging.foo.com/mybaseurl
```

This is also resolvable, as both server URLs provided have the same base path `/mybaseurl` in them.

However, very quickly you can build conflicting or ambiguous scenarios. e.g.

```
servers:
  - url: https://foo.com/mybaseurl
  - url: https://bar.com/adifferenturl
```

Now there are two different top level base paths! These effectively rewrite the actual URLs that would be present in different servers.

You can also specify them at different levels, such as at the `paths` component:

```
paths:
  '/fruits/apple'
    servers:
      - url: https://hostname/
  '/apple'
    servers:
      - url: https://hostname/fruits
```

These two would result in same “resolved” path.

Servers can also be built dynamically:
```
servers:
  - description: SwaggerHub API Auto Mocking
    url: https://k8-swaggerhub.mwhiggins.com/virts/SmartBear_Org/Book/1.3.0
  - description: Static server
    url: https://books.mhiggins.com/v1.3
  - description: Live Bookstore dynamic servers
    url: https://{host}:{port}/{basePath}
    variables:
      host:
        enum:
          - test.book.com
          - staging.book.com
          - sandbox.book.com
          - production.book.com
        default: test.book.com
      port:
        enum:
          - '443'
          - '8443'
        default: '443'
      basePath:
        enum:
          - v1.0
          - v1.1
          - v1.2
          - v1.3
        default: v1.3
```

This condenses the possible servers and creates a more expressive language, and supports visual editors like SwaggerHub to provide helpful "try it out" capabilities. It also shows the point of how flexible servers can be:

<img width="539" alt="Screenshot 2023-06-23 at 9 24 32 am" src="https://github.com/pactflow/swagger-mock-validator/assets/53900/a605ca03-7cfe-4a79-8660-8db64bacad8e">

However, now there are multiple divergent base paths to consider and the resolution rules are more likely to cause confusion and complexity.

So given the above we cannot reliably infer how 

## Workaround

If your OAS has the basic use case of a single `server` entry with a consistent base URL, you can either:

1. Remove the base URL from your server (e.g. `https://foo.com/v1/` would become `https://foo.com`) and simply have the URLs represent what they would look like as consumed by your API clients (e.g. `/resource` would become `/v1/resource`) (preferred)
2. Transform your OAS to transpose the base URL as a prefix to each of the resources
3. Transform your pact file before publishing to strip the base URL from all paths

this way, you will have alignment.

If you use one of the more complicated schemes above, you'll need to apply a more complicated transformation, taking into consideration the concerns noted above.

## Example

In the example, there are two tests. One that uses the `/v1` prefix currently defined in the `servers` (fails with an error) and one that doesn't (passes as it matches the defined resources).