# Creating and using a view key

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
After a user has selected a video, you will have received and saved a Media Id. This Media Id, along with user information can be exchanged for a view key via server to server communication. Once you've created a view key, it may be used to embed a video player into the user's browser via an iframe.

## Prerequisites
Before you begin you should have obtained the following via other steps listed in this documentation.
- **Media Id**: A unique identifier pointing to the video that was selected.
- **Access Token**: An OAuth2 client credentials bearer token.

## Steps to create and use a view key

### 1. Creating the view key
To obtain a view key, make a POST request to the view key endpoint provided by the API. Here is an example using `curl`:

```sh
curl --request POST \
  --url https://integrations.clickviewapp.com/api/v1/smart-embed/create-view-key \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
    "mediaId": "YOUR_MEDIA_ID",
    "additionalData": {
      "isStudent": false,
      "firstName": "Valerie",
      "surname": "Frizzle",
      "email": "valerie.frizzle@school.gov"
    }
  }'
```

- Replace `YOUR_ACCESS_TOKEN` and `YOUR_MEDIA_ID` with your actual Client ID and Client Secret.
- Please see [additional data](#additional-data) for information on populating the `additionalData` option.

#### Additional Data
The `additionalData` property on the create view key request will be used to pass user information to ClickView. Below is a generic outline of the expected properties, however the data being sent here will be an agreement between you and ClickView, additional properties outside of what is specified may be expected by ClickView. Similarly certain properties may be required that are listed as optional below.

|Property Name|Required|Description|
|---|---|---|
|`isStudent`|Required|A boolean value identifying if the user is a student.|
|`firstName`|Required for teachers|The users first name.|
|`surname`|Required for teachers|The users surname.|
|`email`|Required for teachers|The user's email address.|
|`jobTitle`|Optional|The user's job title in their school or district.|
|`schoolName`|Optional|The name of the school the user belongs to.|
|`schoolId`|Optional|An identifier you may have on hand for the school.|
|`districtName`|Optional|The name of the district the user belongs to.|
|`districtId`|Optional|Any identifier you may have on hand for the district.|

_NOTE: If `isStudent` is set to `true` and `firstName`, `surname` or `email` are populated, the required will error out._

**Example teacher payload**

Here is an example of a create view key request payload with all the metadata populated.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "additionalData": {
    "isStudent": false,
    "firstName": "Valerie",
    "surname": "Frizzle",
    "email": "valerie.frizzle@school.gov",
    "jobTitle": "Bus driver",
    "schoolName": "Walkerville Elementary School",
    "schoolId": "S123",
    "districtName": "Riverside Unified School District",
    "districtId": "D123"
  }
}
```

**Example student payload**

Here is an example of a create view key request payload for a student.

```json
{
  "mediaId": "YOUR_MEDIA_ID",
  "additionalData": {
    "isStudent": true,
    "districtName": "Riverside Unified School District",
    "districtId": "D123"
  }
}
```

### 2. View key response
A successful response will return a JSON object containing the `viewKey` field, which you will use to embed a ClickView video. Here is an example of a successful JSON response:

```json
{
	"viewKey": "eyJz93a...k4laUWw",
	"embedUrl": "https://integrations.clickviewapp.com/smart-embed/play?viewKey=eyJz93a...k4laUWw"
}
```

- `viewKey`: A view key that can be used to playback the selected video via an iframe.
- `embedUrl`: A url that can be used in the `src` attribute of an iframe, this can be used in place of the viewKey if you do not want to build out the url yourself.

_Note: The created view key has a lifetime of 8 hours. A new view key should be created every time a user attempts to watch a video. However an already loaded view key will refresh it's own lifetime, so playback will continue to work for a user who has already loaded the video._

### 3. Video playback
Once you have create a view key, you may use it to embed the video into your site using an iframe. Here is a simple example of an iframe for playing back a video. Video playback will not require the user to sign in or have an account.

```html
<iframe
  src="https://integrations.clickviewapp.com/smart-embed/play?viewKey=eyJz93a...k4laUWw"
  width="640"
  height="360"
  frameborder="0"
  allowfullscreen
  allow="autoplay">
</iframe>
```