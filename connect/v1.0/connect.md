# ClickView Connect API

# RSS Feed

The ClickView Connect API is used to securly obtain the information about the signed in user or school. Please contact ClickView to obtain a `clientId` if you wish to use this API.

## Resource URL

```http
GET https://online.clickview.com.au/v1/connect
GET https://online.clickview.co.uk/v1/connect
GET https://online.clickview.co.nz/v1/connect
```

## Parameters

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| clientId | required | You clientId || `F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE` |
| redirectUri | required | The URI ClickView will use to post information to || `https://mydomain.com/hooks/clickview` |
| redirectMethod | optional | The method for ClickView to call the `redirectUri`. | `post` | `post` |

## Response
ClickView will perform a HTTP `post` to the provided `redirectUri`. The body will contain a `application/x-www-form-urlencoded` response.



### Serialized Example Response
```
{
    "schoolId" : "F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE"
}
```

### Data

| Key      | Type     | Description | Example |
| -------- | -------- | ----------- | ------- |
| schoolId | `String` | The SchoolId that the authenticated user is part of. | `F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE`|