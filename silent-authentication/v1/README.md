# Release notes

## Version 1.0

### Features

#### Silent Authentication

Silent Authentication services provide OAuth2-based authentication that verifies whether an authentication
request originates from the same subscriber by resolving network session information and returning a `mobile_id`.

- OAuth2 Authorization: Initiate authentication flow with MSISDN verification via `/oauth2/authorize`.
- OAuth2 Token Exchange: Exchange authorization code for access token and ID token (containing mobile_id) via `/oauth2/token`.

Spec

- OpenAPI 3.0 specification: `v1/silent-authentication.yaml`

Usage

- Base URL: `https://api.tyntec.com/silent-auth/v1`
- Authentication: Client credentials (client_id and client_secret) for token endpoint

For request/response examples and full endpoint documentation, see `v1/silent-authentication.yaml`.
