# Release notes

## Version 1.0

### Features

#### Network signals

Network Signals services provide checks and signals around ownership and routing of phone numbers. The
features below help brands detect phone number or device changes and check call routing behaviour.

- SIM swap check: Detect whether a subscriber's SIM card was swapped within a configurable time window.
- SIM swap retrieve date: Retrieve the timestamp of the latest detected SIM swap (ISO 8601 timestamp or null).
- Device swap check: Detect whether the subscriber's device changed within a configurable time window.
- Device swap retrieve date: Retrieve the timestamp of the latest detected device change (ISO 8601 timestamp or null).
- Call forwarding check: Verify whether unconditional call forwarding is enabled for a phone number.


Spec

- OpenAPI 3.0 specification: `v1/network-signals.yaml`

Usage

- Base URL: `https://api.tyntec.com/identity/v1`
- Authentication: API Key header `apiKey` (see the spec securitySchemes)

For request/response examples and full endpoint documentation, see `v1/identity.yaml`.

