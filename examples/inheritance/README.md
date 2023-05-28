# Inheritance example

This example takes demonstrates how type [inheritance and polymorphism](https://swagger.io/docs/specification/data-models/inheritance-and-polymorphism/) can be used with PactFlow's BDCT feature.

As this inheritance pattern involves the use of `allOf` where each sub-schema needs to be combined before testing, the OAS needs to have the `allOf`s dereferenced first into a single schema.

The transformed OAS uses the strategy outlined [here](https://docs.pactflow.io/docs/bi-directional-contract-testing/contracts/oas/keyword-support/#example-oneof-schema), using the [`oas-merge`](https://github.com/YOU54F/oas-merge) npm utility.

### Inheritance

The value of `discrimator` should be narrowly specified by `enum` to a set that restricts its value to the desired possible schema subtypes. Otherwise, no subtype schema will be found, and any input will pass. In this case, we support [polymorphism](https://spec.openapis.org/oas/v3.1.0#composition-and-inheritance-polymorphism) via two schemas - Dog and Cat.

Where the polymorphic content is supplied, you need to set the `additionalProperties: true`:

```yml
      responses:
        "200":
          description: successful operation
          content:
            "application/json":
              schema:
                additionalProperties: true # <- take note!
                oneOf:
                  - $ref: '#/components/schemas/Cat'
                  - $ref: '#/components/schemas/Dog'
                discriminator:
                  propertyName: pet_type
```

In the Definition of the schemas, you can then create a parent type (e.g. `Pet`) and use the `discriminator` property to signal how to differentate the allowed subtypes.

```yml
components:
  schemas:
    Pet:
      type: object
      required:
        - pet_type
      properties:
        pet_type:
          type: string
          enum: [Cat, Dog] # <- take note. If this isn't specified it can accept any object
      discriminator:
        propertyName: pet_type
    Cat:
      ... # the Cat specific fields
    Dog:
      ... # the Dog specific fields
```