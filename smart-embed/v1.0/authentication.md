# Obtaining a Client Credentials Access Token

## Overview
Our API uses the OAuth 2.0 Client Credentials Grant type, which is suitable for server-to-server authentication where the client is acting on its own behalf (the "client" is the application that makes protected resource requests on behalf of the resource owner).

## Prerequisites
Before you begin, you should have obtained the following from ClickView:
- **Client ID**: A public identifier for your use of Smart Embeds.
- **Client Secret**: A secret known only to you and the authorization server.

Please keep your Client Secret confidential to protect the security of your API access.

## Steps to Obtain an Access Token

### 1. Request an Access Token
To obtain an access token, make a POST request to the token endpoint provided by the API. Here's an example using `curl`:

```sh
curl --request POST \
  --url https://auth.clickviewapp.com/connect/token \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --header 'User-Agent: insomnia/2023.5.8' \
  --data grant_type=client_credentials \
  --data client_id=YOUR_CLIENT_ID \
  --data client_secret=YOUR_CLIENT_SECRET \
  --data scope=smartembed.viewkey
```

Replace `YOUR_CLIENT_ID` and `YOUR_CLIENT_SECRET` with your actual Client ID and Client Secret.

### 2. Response
A successful response will return a JSON object containing the `access_token` field, which you will use for authentication in subsequent API requests. Here is an example of a successful JSON response:

```json
{
  "access_token": "eyJz93a...k4laUWw",
  "token_type": "Bearer",
  "expires_in": 86400,
  "scope": "smartembed.viewkey"
}
```

- `access_token`: The token that must be used in API requests to authenticate.
- `token_type`: Indicates the type of token returned. In this case, it is a Bearer token.
- `expires_in`: The number of seconds until the token expires (86400 means the token is valid for 24 hours).
- `scope`: Represents the permissions granted to the access token.

### 3. Making Authenticated Requests
With the access token, you can now make authenticated requests to the API. Include the access token in the Authorization header of your HTTP request like so:

```sh
curl -request GET \
  https://integrations.clickviewapp.com/api/v1/example \
  -header 'Authorization: Bearer YOUR_ACCESS_TOKEN'
```

Replace `YOUR_ACCESS_TOKEN` with the actual token you received from the token endpoint.

## Handling Errors
If the request for an access token fails, the server will return an error payload. For example:

```json
{
  "error": "invalid_client",
  "error_description": "Client authentication failed."
}
```

Refer to the [OAuth 2.0 Specification](https://tools.ietf.org/html/rfc6749#section-5.2) for a detailed list of potential error codes and their meanings.

## Best Practices
- Securely store the `client_secret`.
- Handle token expiration gracefully by either retrying the request or prompting the user to re-authenticate.
- Ensure all communications with the authorization server are performed over HTTPS to keep credentials secure.

## Next Steps
After obtaining your access token, you may proceed to use it to request view keys or any other secured resources provided by our API.