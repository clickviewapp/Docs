# RSS Item object

The RSS Item complies with the RSS 2.0 specification https://validator.w3.org/feed/docs/rss2.html and the Media RSS 1.5.1 specification  http://www.rssboard.org/media-rss where possible.

## Data

| Elements | Type | Description |
| --------- | ---- | ----------- |
| guid | `string` | The unique identifier of the video |
| link  | `string` | The URL to the video in Online |
| category | `string` | The first category which the video is filed under. <br><br> **Note:** We recommend using `media:category scheme=urn:clickview:category` instead (*see below*) |
| title | `string` | The display title of the video (includes series name) |
| pubDate | `Date` *RFC 822* | The date the video was added to the Library |
| a10:updated | `Date` | The date the video was last updated |
| a10:content |  | The embed link for the video |
| media:content | | Contains the URL for the embed link and duration |
| media:thumbnail | | The thumbnail for the video |
| media:player | | The URL to the video in Online |
| media:title | `string` | The title of the video |
| media:description | `string` | The description of the video |
| media:rating | `string` | The rating of the video |
| media:category | `string` | The categories the video belongs too. The type of the category is defined by the scheme. For more information see [<media:category>](#<media:category>) |
| media:credit | `string` | Any credits associated with the video. The type of the credit is defined by the role. For more information see [<media:credit>](#<media:credit>) |
| media:season | `string` | The season name of the video. The `number` attribute contains the number value of the season |
| media:episodeNumber | `int` | The episode number of the video |
| media:productionYear | `int` | The production year of the video |

### <a10:content>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| type | `string` | The type of the content |
| src | `string` | The URL to the video embed |

### <media:content>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| medium | `string` | The type of object |
| duration | `long` | The duration of the video in milliseconds |
| url | `string` | The URL to the video embed |

### <media:thumbnail>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| url | `string` | The URL to the image |
| width | `int` | The width of the image in pixels |
| height | `int` | The height of the image in pixels |

### <media:player>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| url | `string` | The URL to the video in Online |

### <media:category>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| scheme | `string` | The type of the category |

#### Schemes

| Scheme | Description |
| ------ | ----------- |
| `urn:clickview:category` | The name category the video is in. There could be more than one. **Note:** This is preferred over the other category field |
| `urn:clickview:series` | The series of the video |
| `urn:clickview:tag` | A tag describing the video. There could be more than one. |

### <media:credit>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| scheme | `string` | The type of the category |

#### Roles

| Role | Description |
| ------ | ----------- |
| `production company` | The company who produced the video. In the case of multiple production companies, there will be multiple elements |
| `distributor` | The company who distributes the video. In the case of multiple distributors, there will be multiple elements |
| `director` | The person who directed the video. In the case of multiple directors, there will be multiple elements |
| `producer` | The person who produced the video. In the case of multiple producers, there will be multiple elements |

### <media:season>

| Attribute | Type | Description |
| --------- | ---- | ----------- |
| number | `int` | The number value of the season |
