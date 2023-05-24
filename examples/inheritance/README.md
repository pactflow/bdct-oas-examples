# Inheritance example

This example takes the `allOf` example from the [OpenAPI](https://swagger.io/docs/specification/data-models/oneof-anyof-allof-not/#allof) specification and demonstrates how it can be used in BDCT.

As this inheritance pattern involves the use of `allOf` where each sub-schema needs to be combined before testing, The OAS needs to have the `allOf`s dereferenced first into a single schema.

The transformed OAS uses the strategy outlined [here](https://docs.pactflow.io/docs/bi-directional-contract-testing/contracts/oas/keyword-support/#example-oneof-schema), using the [`oas-merge`](https://github.com/YOU54F/oas-merge) npm utility.