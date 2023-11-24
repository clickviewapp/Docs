# Video Playback

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
After a user has selected a video, you will have received and saved a `MediaId`. This `MediaId`, along with user information may be exchanged for a View Key via server to server communication. Once you've created a View Key, it may be used to embed a video player into the user's browser via an iframe.

## Prerequisites
Before you begin you should have obtained the following via other steps listed in this documentation.
- **MediaId**: A unique identifier pointing to the video that was selected.
- **Access Token**: An OAuth2 client credentials bearer token.

## Creating a View Key

### 1. Obtain an access token
In order to create a View Key, you first must obtain an OAuth2 access token, via a client credentials grant.

Please see [Obtaining an Access Token](authentication.md) for details on how to acheive this.

### 2. Creating a View Key
To obtain a View Key, make a POST request to the View Key endpoint provided by the API.

**Resource URL**
```
POST https://integrations.clickviewapp.com/api/v1/smart-embed/create-view-key
```

**Headers**
|Header|Required|Description|
|---|---|---|
|`Authorization`|required|Specifies the type of authentication and includes an access token. In this case, it's a Bearer token.|
|`Content-Type`|required|Specifies the type of content in the HTTP request body. In this case, it's set to `application/json`.|

**Body**
|Name|Required|Description|
|---|---|---|
|`mediaId`|required|Unique identifier for the media to create a view key for.|
|`data`|required|Please see [Data required for creating a view key](view-key-data.md) for information on populating the `data` property|

**Example usage**
Here is an example using `curl`:

```sh
curl --request POST \
  --url https://integrations.clickviewapp.com/api/v1/smart-embed/create-view-key \
  --header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
    "mediaId": "YOUR_MEDIA_ID",
    "data": {
      "student": false,
      "firstName": "Valerie",
      "surname": "Frizzle",
      "email": "valerie.frizzle@school.gov",
      "jobTitle": "Bus driver",
      "schoolName": "Walkerville Elementary School",
      "schoolId": "S123",
      "districtName": "Riverside Unified School District",
      "districtId": "D123"
    }
  }'
```

- Replace `YOUR_ACCESS_TOKEN` and `YOUR_MEDIA_ID` with your actual access token and `MediaId`.
- Please see [Data required for creating a View Key](view-key-data.md) for information on populating the `data` property.

### 3. View Key response
A successful response will return a JSON object containing the `viewKey` field, which can be used to embed a ClickView video. Here is an example of a successful JSON response:

```json
{
  "mediaId": "123",
  "viewKey": "eyJz93a...k4laUWw",
  "embedUrl": "https://integrations.clickviewapp.com/smart-embed/play?viewKey=eyJz93a...k4laUWw"
}
```

- `mediaId`: The id of the media you sent in the request.
- `viewKey`: A View Key that can be used to playback the selected video via an iframe.
- `embedUrl`: A url that can be used in the `src` attribute of an iframe, this can be used in place of the viewKey if you do not want to build out the url yourself.

At this point you've created a View Key and are able to see what playing a video looks like 🎉. Go ahead and paste the `embedUrl` into your browser to give it a try!

_Note: The created View Key has a lifetime of 8 hours. A new View Key should be created every time a user attempts to watch a video. However an already loaded View Key will refresh it's own lifetime, so playback will continue to work for a user who has already loaded the video._

## Using your View Key to play a video
Once you have created a View Key, you may use it to embed the video using an iframe. 

Here is a simple example of an iframe for playing back a video. Video playback will not require the user to sign in or have an account.

```html
<div style="padding:56.25% 0 0 0; position:relative;">
  <iframe
    src="https://integrations.clickviewapp.com/smart-embed/play?viewKey=eyJz93a...k4laUWw"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
    frameborder="0"
    allowfullscreen
    allow="autoplay"
  ></iframe>
</div>
```

_NOTE: The div wrapping this iframe is optional, but provides an example of how to allow your iframe to display itself responsively. The vast majority of our videos are in a 16:9 aspect ratio, and our player will handle videos that are not gracefully when rendered in a 16:9 ratio._

## Best practices
- Request a new View Key each time a user requests to watch a video in your site. Do not re-use View Keys.
- Ensure the iframe has the `allowfullscreen` and `autoplay` attributes, to ensure your users have a good experience.
- Ensure that the iframe is rendered responsively, and enough realestate is given for your users to enjoy the video comfortably.
- Ensure you are following the best practices in [Obtaining an Access Token](authentication.md#best-practices) and [Data required for creating a View Key](view-key-data.md#best-practices).
- Reach out to ClickView if you have a need to use the `csp` or `sandbox` attributes on your iframes.

## Next steps
If you've made it this far, congratulations you're almost done. There is just one thing left to do, which is make sure any failure states are gracefully handled. Please see [Error handling and troubleshooting](troubleshooting.md).