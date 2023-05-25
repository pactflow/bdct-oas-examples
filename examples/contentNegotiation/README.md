# Content Negotiation Example

This example uses the `Accept` header to disambiguate expected response content types.

Note that PactFlow supports quality values (e.g. `;q=1`), media ranges (e.g. `image/*` or `*/*`), parameter matching and follows the precedence rules layed out in RFC rfc9110 (https://www.rfc-editor.org/rfc/rfc9110.html#content.negotiation).