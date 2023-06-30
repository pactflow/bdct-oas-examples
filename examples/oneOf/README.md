# `oneOf` example

One of the challenges with `oneOf` is when applying the test to a given JSON data structure, it should only match a single schema. Consumer's may need only a subset of the data from a provider, which increases the chances it will match multiple schemas and cause a failure.

Usually, the body will **not match** either the `Dog` and the `Cat` if you remove all of the properties except for one of the common ones such as `name`. This is not allowed when using `oneOf`, as it must match exactly one of the schemas supplied.

However, we can leverage the `discriminator` property of OpenAPI to address this problem (see annotated document). 

The 3rd example in the pact file demonstrates this working. It would usually fail because the JSON would match multiple schemas, however because a discriminator value is provided (`petType`) we can be sure the expectations are satisfied.