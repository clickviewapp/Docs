# ClickView oEmbed API

[oEmbed](https://oembed.com/) is an open format designed to allow embedding content from a website into another page.

The ClickView oEmbed API can be used to obtain the the necessary information to embed ClickView videos into your website.


## Resource URL

```http
GET https://online.clickview.com.au/oembed
GET https://online.clickview.co.uk/oembed
GET https://online.clickview.co.nz/oembed
```

## Parameters

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| url | required | The URL of the resource you are trying to embed || `https://clickv.ie/w/{short-code}` |
| format | optional | The response format. Supported values are `json` and `xml`. | `json` | `json` |

## Supported URLs
oEmbed is supported on the following pages:

**Shared Links**:
* `https://clickv.ie/w/{short-code}`

**Videos**:

* `share?sharecode={share-code}`
* `share/embed?sharecode={share-code}`
* `exchange/video/{video-id}/*`
* `exchange/videos/{video-id}/*`
* `exchange/topics/{topic-id}/*/videos/{video-id}/*`
* `exchange/categories/{category-id}/*/videos/{video-id}/*`
* `exchange/series/{series-id}/*/videos/{video-id}/*`
* `exchange/channels/{channel-id}/*/videos/{video-id}/*`

**Playlists**:

* `playlists/share/{share-code}/*`
* `playlists/{playlist-id}/videos/{video-id}/*`
* `exchange/channels/{channelId}/*/playlists/*/`

## Example Response
```
{
    "type": "link",
    "version": "1.0",
    "title": "Jane Eyre",
    "width": 640,
    "height": 360,
    "author_name": null,
    "author_url": "https://online.clickview.co.uk/exchange/channels/",
    "provider_name": "ClickView",
    "provider_url": "https://online.clickview.co.uk",
    "cache_age": 600,
    "thumbnail_url": "https://img.clickviewapp.com/v1/thumbnails/187817",
    "thumbnail_height": 256,
    "thumbnail_width": 144,
    "html": ...
}
```