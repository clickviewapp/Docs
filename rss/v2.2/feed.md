# RSS Feed

The ClickView RSS Feed is used to obtain the contents of a ClickView Online school's library in an RSS format. The feed contains multiple [RSS Item object](data/item.md)s.

## Resource URL

```
GET https://online.clickview.com.au/v2.2/rss/feed
GET https://online.clickview.co.uk/v2.2/rss/feed
GET https://online.clickview.co.nz/v2.2/rss/feed
GET https://online.clickview.us/v2.2/rss/feed
```

## Parameters

| Name | Required | Description | Example |
| ---- | -------- | ----------- | ------- |
| schoolId | required | The ID of the school | `F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE` |
| max | optional | The maximum number of items to return | `5` |
| since | optional | Filter records that have been added since the date provided | `2019-01-01` |
| maxRatingCode | optional | The maximum rating code allowed to be returned. Value must be URL encoded. See [here](ratings.md) for a list of ratings | `MA15%2B` |

## Headers

| Name | Required | Description | Example |
| ---- | -------- | ----------- | ------- |
| x-rss-auth-token | required | The authentication token used to access the feed. This is given to you by ClickView | `umeqSLGrYj6vLlQu` |

## Example Response

```xml
<rss xmlns:a10="http://www.w3.org/2005/Atom" version="2.0">
  <channel xmlns:media="http://search.yahoo.com/mrss/">
    <title>ClickView - RSS</title>
    <link>httpd://www.clickview.com.au/</link>
    <description>ClickView - RSS</description>
    <language>en-AU</language>
    <copyright>2003 - 2018 © ClickView Pty Limited</copyright>
    <a10:author>
      <a10:name>ClickView</a10:name>
      <a10:uri>httpd://www.clickview.com.au</a10:uri>
    </a10:author>
    <item>
      <guid isPermaLink="false">10078432</guid>
      <link>https://online.clickview.com.au/libraries/videos/10078432/enough-time?customerId=F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE&amp;ssoRedirect=true</link>
      <category>Mathematics</category>
      <title>View and Do: Maths Investigations : S01E07 - Enough Time</title>
      <pubDate>Thu, 02 May 2019 00:47:13 Z</pubDate>
      <a10:updated>2019-10-09T23:14:57Z</a10:updated>
      <a10:content type="video/mp4" src="https://online.clickview.com.au/share/embed?p=cv&amp;customerId=F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE" />
      <media:content medium="video" duration="1047000" expression="full" url="https://online.clickview.com.au/share/embed?p=cv&amp;customerId=F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE">
        <media:thumbnail url="https://img.clickviewapp.com/v1/thumbnails/953173" width="256" height="144" />
        <media:player url="https://online.clickview.com.au/libraries/videos/10078432/enough-time?customerId=F437FEA9-F21A-4CA6-9C2F-E1792CF87CFE&amp;ssoRedirect=true" />
        <media:title type="plain">Enough Time</media:title>
        <media:description type="plain">Paul has an appointment with the bank manager but has a list of jobs to do first. How can he be sure that he will get there on time? What if his appointment is delayed and he has more jobs to do?

This episode explores the passage of time, reading and showing time, half and quarter hours, and adding times.

This video includes a chapter targeted at junior, middle, and senior primary. These chapters cover the same scenario with increasing complexity. Select the chapter that is best suited to your class.</media:description>
        <media:rating>E</media:rating>
        <media:category scheme="urn:clickview:category">Mathematics</media:category>
        <media:category scheme="urn:clickview:series">View and Do: Maths Investigations</media:category>
        <media:category scheme="urn:clickview:tag">time</media:category>
        <media:category scheme="urn:clickview:tag">timeline</media:category>
        <media:credit role="production company">Blake Education</media:credit>
        <media:credit role="distributor">Blake Education</media:credit>
        <media:season number="1">Season 1</media:season>
        <media:episodeNumber>7</media:episodeNumber>
        <media:productionYear>2019</media:productionYear>
      </media:content>
    </item>
  </channel>
</rss>
```
