# Video Selection

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
The Smart Embed selection has been developed as a single page web application, designed to be implemented within your platform via two components; an Iframe and a small Events API JavaScript library.

## Prerequisites
Before you begin, you should have obtained the following from ClickView:
- **Client ID**: A public identifier for your use of Smart Embeds.

## Steps to select a video

### 1. Prompt a user to select a video
Our video selection should happen in an iframe embedded into your site. This Iframe displays an interface that allows signed in users to browse their videos and select the video which they wish to embed. Users will be required to either sign in or sign up, in order to select a video to embed.

#### Iframe example
Here is a simple example of an iframe linking to your web application.

```html
<div style="padding: 56.25% 0 0 0; position: relative; border: 1px solid #eaeaea;">
  <iframe
    id="clickview-video-select"
    src="https://integrations.clickviewapp.com/smart-embed/select?clientId=YOUR_CLIENT_ID"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
    frameborder="0"
  ></iframe>
</div>
```

Replace `YOUR_CLIENT_ID` with your actual Client ID.

_NOTE: The div wrapping this iframe is optional, but provides an example of how to allow your iframe to display itself responsively._

### 2. Capture the selected video
In order to capture information about the user's selected video, we have created a simple JavaScript API. When a user selects a video, an event will be triggered. Use ClickView's CVEvents API to listen to this event in order to retrieve metadata about the selected video.

#### Loading in our CVEvents API

The CVEvents API is available on our CDN: https://static.clickview.com.au/cv-events-api/1.1.1/cv-events-api.min.js. Feel free to embed this directly into your platform like so.

```html
<script src="https://static.clickview.com.au/cv-events-api/1.1.1/cv-events-api.min.js" type="text/javascript"></script>
```

Or alternatively you may download the file and host it directly from your platform.

#### Capturing a selected video event

To use the `CVEventsApi`, first create an instance passing in your iframe:

```js
// your iframe markup
//<iframe id="clickview-video-select" ...></iframe>

const cvEventsApi = new CVEventsApi(document.getElementById('clickview-video-select').contentWindow);
cvEventsApi.on('cv-lms-addvideo', (event, details) => {
  // Your logic to save the mediaId here
});
```

- `event` will be a MessageEvent object (you will generally not need to use this object). See: [https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent);
- `details` An object with details about the video the user has selected. 


Here is an example of a details object:
```js
{
  title: 'Example video',
  thumbnailUrl: 'https://example.com/video-image.png',
  mediaId: '123456'
}
```

- `title`: The title of the selected video.
- `thubmnailUrl`: A url pointing to an image for the selected video. These images will always be a 16:9 aspect ratio. Please see [ClickView Image Api](../../image/image.md) for information about the query parameters that are available on our thumbnails.
- `mediaId`: An identifier for the video which may be used to create a view key.

### 3. Save the selected mediaId
The `mediaId` which is returned on the `details` property of the `cv-lms-addvideo` event will be used by you to create a view key each time a user attempts to watch the selected video. You will need to store this selected `mediaId`.

## Best practices
- Ensure that the ClickView Picker is rendered into your site with enough realestate for your users to have a comfortable browsing experience. The preferred approach is to render the picker into a modal that occupies most of the available screen realestate. The minimum recommended size is 800px by 600px.
- Remove the picker iframe from your page once the `cv-lms-addvideo` event is fired. The picker will render a loading spinner, allowing you time to make any http requests you may need to make. However the spinner will spin indefinitely, waiting for your application to either close a modal, or navigate elsewhere.
- Reach out to ClickView if you have a need to use the `csp` or `sandbox` attributes on your iframes.

## Next Steps
Once you have allowed your user to select a video, and saved the `mediaId`. You can move onto implementing [Video Playback](video-playback.md).