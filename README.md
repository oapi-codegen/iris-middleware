# Iris Middleware

⚠️ This README may be for the latest development version, which may contain unreleased changes. Please ensure you're looking at the README for the latest release version.

Middleware for the [Iris web server](https://github.com/kataras/iris/) for use with [oapi-codegen](https://github.com/oapi-codegen/oapi-codegen).

Licensed under the Apache-2.0.

## Validated request body

The middleware enables kin-openapi's `openapi3filter.Options.KeepValidatedValue` by default. After a request body passes validation, the body that handlers see (`ctx.Request().Body`) exposes the decoded value that was validated through a `ValidatedValue() any` method, and remains readable with its original bytes. An [oapi-codegen](https://github.com/oapi-codegen/oapi-codegen) strict server can bind that value instead of decoding the body a second time, so the handler receives exactly what was validated.

To turn this off, for instance to limit memory retention for very large request bodies, set `DiscardValidatedValue: true` in `Options`. This setting overrides `Options.Options.KeepValidatedValue`.

Middleware that replaces the request body after the validator has run (decompression, size limiting, logging wrappers and the like) hides the validated value from handlers. Register such middleware before the validator.
