# Parameters

Unlike OAS which has a very expressive way of capturing parameter [serialization](https://swagger.io/docs/specification/serialization/) approaches, Pact does not encode this information for query strings.

This means that we can’t currently compare non-primitive query string values to the OAS, and we can’t reliably differentiate the cases where an object or array is encoded and how the values should be compared, because how the values are serialised changes the semantics.

We can and do check primitive values match the schema. Where a pact interaction does not satisfy a parameter constraint, you will see an error such as:

```
Path or method not defined in spec file: GET /path/style/simple/single/value/0 (the 0 here does not match the schema, which specifies the value must be > 0)
```

We also presenting a warning if a parameter is used that is not defined. For example, if the consumer sends a request `/users?id=1` to fetch a user, but the `id` parameter is not in the OAS, you will see a warning:

```
Query parameter is not defined in the spec file: id
```