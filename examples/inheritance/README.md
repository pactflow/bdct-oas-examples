# Inheritance example

This example takes demonstrates how type [inheritance and polymorphism](https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism/) can be used with PactFlow's BDCT feature.

### Inheritance

For inheritance to work, you must use the `discrimator` to constrain and clarify the potential matching types.

In this case, we support [polymorphism](https://spec.openapis.org/oas/v3.1.0#composition-and-inheritance-polymorphism) via two schemas - Dog and Cat.

```yml
      responses:
        "200":
          description: successful operation
          content:
            "application/json":
              schema:
                oneOf:
                  - $ref: '#/components/schemas/Cat'
                  - $ref: '#/components/schemas/Dog'
                discriminator:
                  propertyName: petType
                required:
                  - petType
```

In the Definition of the schemas, you can then create a parent type (e.g. `Pet`) and use the `discriminator` property to signal how to differentate the allowed subtypes.

```yml
components:
  schemas:
    Pet:
      type: object
      required:
        - petType
      properties:
        petType:
          type: string
          enum: [Cat, Dog] # You can either use an enum like this, or specify `const` values on the subschemas (used in the example)
    Cat:
      ... # the Cat specific fields
    Dog:
      ... # the Dog specific fields
```

## Use of `discriminator`

There are following requirements and limitations of using `discriminator` keyword:

* `mapping` in discriminator object is not supported.
* "implicit" discriminator values are not supported.
* `oneOf` keyword must be present in the same schema.
* `discriminator` property should be `required` either on the top level, or in all `oneOf` subschemas.
* each `oneOf` subschema must have the `properties` keyword with `discriminator` property. The subschemas should be either inlined or * included as direct references (only `$ref` keyword without any extra keywords is allowed).
* schema for `discriminator` property in each `oneOf` subschema must be `const` or `enum`, with unique values across all subschemas.

Not meeting any of these requirements would fail schema compilation.