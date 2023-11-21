# ClickView Smart Embed

_Please feel free to create an issue if you have any questions not answered by this documentation._

## Overview
The Smart Embed API allows you to embed ClickView videos within your platform and allows for playback without requiring your users to sign up or sign into ClickView. This allows you and your users access to our high quality video library.

_NOTE: If you are building an integration into an LMS or VLE, you may be looking for the [ClickView Plugin API](https://github.com/clickviewapp/plugin-api)._

## Prerequisites
Access to ClickView's Smart Embed API is currently granted on a case by case basis. This will happen via direct communication between our team and yourself. Once we have agreed on an implementation, we will exchange a few pieces of information required to get Smart Embeds working.

You will provide ClickView
- A list of domains from which you intend to use Smart Embeds from.

ClickView will provide you:
- **Client ID**: A public identifier for your use of Smart Embeds.
- **Client Secret**: A secret known only to you and the authorization server.

Once this exchange has happened, you are ready to start building your Smart Embed integration.

## Video Selection
This section outlines how your platforms users may select a ClickView video to be embedded. You may not need this section if you plan to 

1. [Video Selection](v1.0/video-selection.md)
2. [Video Playback](v1.0/video-playback.md)