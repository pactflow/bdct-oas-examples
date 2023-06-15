# Parameters

We can’t currently compare non-primitive query string values to the OAS, because Pact does not encode the the parameter style. This means we can’t reliably differentiate the cases where an object or array is encoded and how the values should be compared. 

We can and do check primitive values match the schema. Where a pact interaction does not satisfy a parameter constraint, you will see a message such as

```
Path or method not defined in spec file: GET /path/style/simple/single/value/0 (the 0 here does not match the schema, which specifies the value must be > 0)
```