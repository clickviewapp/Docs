# ClickView Connect API

The ClickView Connect API is used to securely obtain the information about the signed in user or school. Please contact ClickView to obtain a **client ID** and **secret key** if you wish to use this API.

## Resource URL

```http
GET https://online.clickview.com.au/v1/connect
GET https://online.clickview.co.uk/v1/connect
GET https://online.clickview.co.nz/v1/connect
```

## Parameters

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| client_id | required | Your client ID. || `abc123` |
| redirect_uri | required | The URI ClickView will use to post information to. || `https://mydomain.com/hooks/clickview` |
| signature | required | The signature of the request. See [below](#creating-a-signature) for an example on how to generate a signature. | | `dGhpcyBpcyBub3QgYSByZWFsIHNpZ25hdHVyZSA6KA==` |

## Creating a signature

Creating a signature involves collecting all the parameters sent in the request, URL encoding them, combining all strings and finally HMAC-SHA1 hashing the string with your supplied secret key.

1. [Percent encode](https://tools.ietf.org/html/rfc3986#section-2.1) every key and value that will be signed (excluding the signature).
2. Sort the list of parameters alphabetically by the encoded key
3. For each key/value pair:
   1. Append the encoded key to the output string.
   2. Append a `=` character to the output string.
   3. Append the encoded value to the output string.
   4. If there are more key/value pairs, append a `&` character to the output string.
4. HMAC-SHA1 hash the output string using your provided `secret key`.
5. Base64 encode the binary output of the HMAC-SHA1.

### Example

For the following example on creating a signature we will be using the following parameters:

| Key | Value |
| ---- | ---- |
| `client_id` | `abc123` |
| `redirect_uri` | `https://mydomain.com/hooks/clickview` |

First we percent encode our keys and values (step 1), sort the parameters in alphabetical order (step 2) and append them together using the steps outlined in step 3. This should produce the following output string:

`client_id=abc123&redirect_uri=https%3A%2F%2Fmydomain.com%2Fhooks%2Fclickview`

Next we get your provided secret key (this is not your `client_id`) and the output string from the above steps and run that though the HMAC-SHA1 function. For this example we are using a secret key of "`mysecretkey`". This should output the following binary value:

`5C 71 86 85 EC 02 E9 E5 D6 3B D6 C0 CD 5A 6C 80 1B F3 67 AC`

Finally, we convert the binary into a base64 string to create the final signature string:

`XHGGhewC6eXWO9bAzVpsgBvzZ6w=`

## Response

ClickView will perform a HTTP `post` to the provided `redirect_uri`. The body will contain a `application/x-www-form-urlencoded` response. The data included in this response is detailed [below](#data).

The response will also contain a signature of the response parameters (excluding the signature). This will allow you to verify the payload being posted back to you. To verify the signature please see above.

### Data

| Key      | Type     | Description | Example |
| -------- | -------- | ----------- | ------- |
| schoolId | `string` | The School Id that the authenticated user is a member of. | `F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE`|
| region   | `string` | The region of the authenticated user. Region is in the format of [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). | `"AU"`|
| signature| `string` | The signed | `"SSB3b25kZXIgaWYgQ2FtIHdpbGwgZXZlciBkZWNvZGUgdGhpcyBzdHJpbmc"`|