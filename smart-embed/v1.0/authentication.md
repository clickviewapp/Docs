# Obtaining an Access Token

_Please feel free to create an issue if you have any questions not answered by this documentation._

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

**Resource URL**
```
POST https://auth.clickviewapp.com/connect/token
```

**Headers**
|Name|Required|Description|
|---|---|---|
|`Content-Type`|required|Specifies the type of content in the HTTP request body. In this case, it's set to `application/x-www-form-urlencoded` to indicate that the data is URL-encoded form data.|

**Body**
|Name|Required|Description|
|---|---|---|
|`grant_type`|required|Specifies the grant type for the authentication. In this case, it should be set to `client_credentials`.|
| `client_id`|required|Your client's unique identifier. This is required for client authentication.|
| `client_secret`|required|Your client's secret key. This is required for client authentication and should be kept confidential.|
|`scope`|required|Specifies the scope of access for the requested token. In this example, it is set to `smartembed.viewkey`.|


**Example usage**
```sh
curl --request POST \
  --url https://auth.clickviewapp.com/connect/token \
  --header 'Content-Type: application/x-www-form-urlencoded' \
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
- `token_type`: Indicates the type of token returned. In this case, it is a bearer token.
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

_More information on using your access token is provided in [Video Playback](video-playback.md)._

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
- Securely store the client secret. Ensure you NEVER expose this secret to your user's browser.
- Create a single token and cache it for all your user's requests, until it expires.
- Use a popular OAuth2 library for your technology stack. Doing so will ensure that you follow the OAuth2 specification, and will provide graceful error handling and token refreshing out of the box.
- Ensure that you handle token expiry gracefully by creating a new access token before your old one expires.

## Next Steps
After obtaining your access token, you may proceed to use it to request view keys. Please see [Video Playback](video-playback.md#2-creating-a-view-key) for information on how to use your access token.