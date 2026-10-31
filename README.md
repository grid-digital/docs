# Cconnect developer documentation

Mintlify source for https://developers.cconnect.online.

The customer API is implemented in `grid-digital/grid-connect-api`. Its committed `docs/openapi/customer-v1.json` is generated from Omni endpoint metadata; do not hand-edit the copy in this repository.

## Refresh the contract

From the backend repository, run:

```sh
dotnet run --project backend/Omni.Api.csproj -- --export-customer-openapi /absolute/path/to/this/docs/repository/openapi.json
```

Export requires no database connection and does not run migrations. Set `CustomerApi__PublicBaseUrl` if the API origin differs from `https://cconnect.online`.

Copy only the customer document. Internal Swagger documents must not be committed here; Mintlify may publish specifications even when they are absent from navigation.

## Validate and preview

```sh
npx mint@latest validate
npx mint@latest broken-links
npx mint@latest dev --no-open
```

The portal uses copyable request examples (`api.playground.display=simple`). Enable an interactive playground only after choosing a test environment and reviewing request routing and credential handling.

## Release order

Deploy and migrate the backend, verify HTTPS and `/api/v1` routing, enable `CustomerApi:Enabled`, test an administrator-issued credential, then merge the documentation update into the Mintlify deployment branch. Remove the preview banner only after verifying the deployed API.

This repository does not control DNS or Cloud Run deployment. The API hostname and the documentation hostname are separate.
