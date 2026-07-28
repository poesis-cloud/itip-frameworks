# HTTP Protocol

Crosses the network boundary — analogous to a **syscall** or **FFI call**. The Operator sends HTTP requests to external targets via WebClient and captures full responses.

**Source**: RFC 9110 (HTTP Semantics, 2022), RFC 9112 (HTTP/1.1), RFC 6570 (URI Template), RFC 5789 (PATCH).

## Archetype Quad

| File                                  | Role        | Description                                                             |
| ------------------------------------- | ----------- | ----------------------------------------------------------------------- |
| `HttpRequest.schema.json`             | Data        | Request payload: `method`, `targetUri`, `contentType`, `accept`, `body` |
| `HttpResponse.schema.json`            | Data        | Response payload: `statusCode`, `contentType`, `body`                   |
| `HttpRequestEffector.schema.json`     | Effector    | Port archetype — identity-bound by `method` + `targetUri`               |
| `HttpRequestReceptor.schema.json`     | Receptor    | Port archetype — identity-bound by `targetUri`                          |
| `HttpRequestInteraction.schema.json`  | Interaction | Causal link: request Effector → request Receptor                        |
| `HttpResponseEffector.schema.json`    | Effector    | Port archetype — response emission                                      |
| `HttpResponseReceptor.schema.json`    | Receptor    | Port archetype — response reception                                     |
| `HttpResponseInteraction.schema.json` | Interaction | Causal link: response Effector → response Receptor                      |

## Two Directions

- **Request** (outbound): Operator sends an HTTP request to an external target.
  - Effector identity-bound by `method` + `targetUri`.
  - Supported methods: GET, HEAD, POST, PUT, PATCH, DELETE, OPTIONS.
- **Response** (inbound): Operator receives an HTTP response.
  - `statusCode` (100–599), `contentType`, `body`.

## Dispatcher

`MechanismHttpEffectorExecutionService` (`@Order(0)`) — matches effects where `data` contains `targetUri` and `method`. Sends the request via reactive `WebClient`, captures the full response including status code and content type.

## Extension

Domain-specific HTTP interactions extend these base archetypes via `$ref`/`allOf` composition to constrain body shapes and add custom headers.
