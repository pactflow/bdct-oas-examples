# Negative testing examples

It is common in Pact and consumer tests, to want to ensure the "unhappy" scenarios are appropriately covered by tests to ensure their behaviour is documented and understood.

For example, ensuring your API client can handle `40x`, `50x` and related error codes.

PactFlow supports this scenario, provided the status code is explicitly documented in the OAS. It is not recommended to use the "default" keyword for responses, as this makes the set of possible responses the API actually supports ambiguous.