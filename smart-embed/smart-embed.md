# ClickView Smart Embed

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
The Smart Embed API allows you to embed ClickView videos within your platform and allows for playback without requiring your users to sign up or sign into ClickView. This API provides your users access to our high quality video library.

_NOTE: If you are building an integration into an LMS or VLE, you may be looking for the [ClickView Plugin API](https://github.com/clickviewapp/plugin-api)._

## Prerequisites
Access to ClickView's Smart Embed API is currently granted on a case by case basis. This will happen via direct communication between our team and yourself. Once we have agreed on an implementation, we will exchange a few pieces of information required to get you started.

You will provide ClickView
- A list of domains from which you intend to use the Smart Embed API from.

ClickView will provide you:
- **Client ID**: A public identifier for your use of Smart Embeds.
- **Client Secret**: A secret known only to you and the authorization server.

Once this exchange has happened, you are ready to start building your Smart Embed integration.

## Getting started
The Smart Embed API comprises of two different workflows.

### 1. Video Selection
This workflow will allow yours users to either sign up or sign into ClickView, then browse or search our video library and select the video that they wish to embed. Once they have selected a video, we will pass you a media id that can be used to play the video back to any user.

See [Video Selection](v1.0/video-selection.md) for more information.

### 2. Video Playback
After a user has selected a video and you have obtained an id. You may use that id to create a view key for each user that you wish to display the video to. This step will not require users to sign up or sign into ClickView.


See [Video Playback](v1.0/video-playback.md) for more information.

## Pages reference
This is a list of all the pages in Smart Embed API documentation.
- [Video selection](v1.0/video-selection.md)
- [Video Playack](v1.0/video-playback.md)
- [Obtaining an Access Token](v1.0/authentication.md)
- [Data required for creating a view key](v1.0/view-key-data.md)
- [Error handling and troubleshooting](v1.0/troubleshooting.md)