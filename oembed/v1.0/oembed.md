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

**Share Links**:
* `https://clickv.ie/w/{shortCode}`

**Videos**:

* `/share?sharecode={shareCode}`
* `/share/embed?sharecode={shareCode}`

**Links**:
* `/exchange/video/{videoId}/*`
* `/exchange/videos/{videoId}/*`
* `/exchange/topics/{topicId}/*/videos/{videoId}/*`
* `/exchange/categories/{categoryId}/*/videos/{videoId}/*`
* `/exchange/series/{seriesId}/*/videos/{videoId}/*`
* `/exchange/channels/{channelId}/*/videos/{videoId}/*`
* `/exchange/channels/{channelId}/*/playlists/*/`

## Example URL
`GET https://online.clickview.com.au/oembed?url=https://clickv.ie/w/qbMl`

## Example Response
```json
{
    "type": "video",
    "version": "1.0",
    "title": "The Grinch",
    "width": 640,
    "height": 360,
    "author_name": "ClickView",
    "author_url": "https://online.clickview.com.au",
    "provider_name": "ClickView",
    "provider_url": "https://online.clickview.com.au",
    "cache_age": 600,
    "thumbnail_url": "https://img.clickviewapp.com/v1/thumbnails/2536805",
    "thumbnail_height": 256,
    "thumbnail_width": 144,
    "html": "<iframe frameborder=\"0\" allowfullscreen webkitallowfullscreen width=\"640\" height=\"360\" src=\"https://online.clickview.com.au/share/embed?sharecode=448e5ed\"></iframe>"
}
```