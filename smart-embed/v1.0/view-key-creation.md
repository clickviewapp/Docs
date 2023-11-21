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
	  "mediaId": "YOUR_MEDIA_ID"
  }'
```

Replace `YOUR_ACCESS_TOKEN` and `YOUR_MEDIA_ID` with your actual Client ID and Client Secret.

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
Once you have create a view key, you may embed it into your site using an iframe. Here is a simple example of an iframe for playing back a video. Video playback will not require the user to sign in or have an account.

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