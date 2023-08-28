# `additionalProperties` example

[`additionalProperties`](https://json-schema.org/understanding-json-schema/reference/object.html#additional-properties) can accept three values:

1. `true` - this allows the schema to be extended with any properties, of any type and shape
2. `false` - this closes the schema, only allowing the defined properties to be used
3. a `$schema`, expressing the additional properties allowed

PactFlow explicitly disallows `true`, as it can lead to a false sense of security - that is, setting `additionalProperties: true` will allow a consumer to expect *anything*, and the test will pass.

If you have a valid scenario for allowing additional properties, you must set a schema (option 3) to express the expected allowed properties for a field.

In the case that the field truly can accept anything, there is a workaround that this example supports. 

The following definitions express a set of JSON types that allow any JSON to be added to a particular field. This of course should be used sparingly, but should be the equivalent to setting `additionalProperties` to `true`. In most circumstances, you should expect to reduce the set of possible allowed fields, in particular on a _response_ body. 

```yaml
    AnyJSON:
      anyOf: 
        - type: 'null'
        - type: string
        - type: number
        - type: boolean
        - $ref: '#/components/schemas/JSONArray'
    JSONArray:
      type: array
      items: 
        anyOf: 
          -  $ref: "#/components/schemas/AnyJSON"       # Array can accept any primitive
          -  $ref: "#/components/schemas/AnyJSONObject" # or an object with any type 
    AnyJSONObject:
      type: object
      additionalProperties: 
        $ref: "#/components/schemas/AnyJSON"          
```