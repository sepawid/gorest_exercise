# GoREST Users API – Postman and Newman tests

This repository contains an automated test suite for the public [GoREST Users API](https://gorest.co.in/). It covers a complete authenticated CRUD chain plus representative negative and public-read cases.

## Coverage

- Positive chain: create → duplicate-email check → retrieve → `PATCH` → `PUT` → verify → delete → confirm `404`
- Validation: missing email or required fields, malformed email, invalid enum values, malformed JSON, and unsupported content type
- Authentication: no token and invalid token (`401`), plus unauthenticated update/delete that do not expose token-owned records (`404`)
- Invalid HTTP method on the users collection (rejected as `404` or `405`, depending on the API response)
- Public endpoint: pagination, filtered list, unknown user, and non-numeric identifier (`404`)

Each run generates unique test data and deletes the users it creates.

## Run locally

1. Create a GoREST access token. Do not commit it.
2. Create a local `.env` file (it is ignored by Git) containing:

   ```bash
   GOREST_TOKEN='your-token-here'
   ```

3. Load it and run the suite:

   ```bash
   set -a
   source .env
   set +a
   npm run test:api
   ```

Alternatively, import the collection and environment files into Postman, then set `gorest_token` only in your local environment.

## GitHub Actions

The workflow runs on pushes, pull requests, and manual dispatches. Set the repository secret `GOREST_TOKEN`; the JUnit report is uploaded as an artifact.

## Bearer token

An access token is required for authenticated requests. Keep it in `.env` locally and in the `GOREST_TOKEN` repository secret for CI; never commit it.
