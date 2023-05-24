# `oneOf` example

Note that in the pact specs, the body will **not match** either the `Dog` and the `Cat` if you remove all of the properties except for e.g. `name`. This is not allowed when using `oneOf`, as it must match exactly one of the schemas supplied