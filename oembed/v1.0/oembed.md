# ClickView oEmbed API

[oEmbed](https://oembed.com/) is an open format designed to allow embedding content from a website into another page.

The ClickView oEmbed API can be used to obtain the the necessary information to embed ClickView videos into your website.


## Resource URL

```http
GET https://integrations.clickviewapp.com/oembed
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

* `https://www.clickview.net/share/{shareCode}`
* `https://www.clickview.net/share/embed/{shareCode}`

**Links**:

All the links below are also supported when prefixed with both a country code (e.g. `/us`) and learning level (e.g. `/elementary`, `/middle`, `/high`). For example `https://www.clickview.net/us/elementary/video/{id}/{name}`.

* `https://www.clickview.net/video/{id}/{name}`
* `https://www.clickview.net/clips/{id}/{name}`
* `https://www.clickview.net/interactive/{id}/{name}`
* `https://www.clickview.net/series/{id}/{name}`
* `https://www.clickview.net/playlists/{id}/{name}`
* `https://www.clickview.net/topics/{id}/{name}`
* `https://www.clickview.net/studios/{id}/{name}`

## Example URL
`GET https://integrations.clickviewapp.com/oembed?url=https://clickv.ie/w/D58w`

## Example Response
```json
{
    "type": "video",
    "version": "1.0",
    "title": "The Grinch",
    "author_name": "ClickView",
    "author_url": "https://www.clickview.net/",
    "provider_name": "ClickView",
    "provider_url": "https://www.clickview.net/",
    "cache_age": 600,
    "thumbnail_url": "https://img.clickviewapp.com/v2/thumbnails/xAxL5m?size=small",
    "thumbnail_width": 256,
    "thumbnail_height": 144,
    "width": 1014,
    "height": 576,
    "html": "<iframe frameborder=\"0\" allowfullscreen webkitallowfullscreen width=\"1014\" height=\"576\" src=\"https://www.clickview.net/share/embed/j3xP0b\"></iframe>"
}
```