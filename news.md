# Toontown Rewritten News API

## Requests

All requests must be submitted via HTTP GET to `https://www.toontownrewritten.com/api` with one of the following endpoints.

If you are frequently making calls to this API, we would appreciate it if you set a descriptive User-Agent.

## GET `/news`

Returns the latest `news` object.

## GET `/news/{postId}`

Uses `postId` to retrieve the corresponding `news` object. If no post is found, the text `null` is returned instead.

## GET `/news/list`

Returns an array of all `news` objects.

## `news` Values

| Name | Description |
|------|-------------|
| postId | Identifier for the news post. |
| title | Title of the news post. |
| author | Author of the news post. |
| body | HTML contents of the release note as a string. |
| date | Date and time the news post was published as a string, for example `June 15, 2025 at 12:00 PM`. |
| image | URL of the first image in the news post as a string, for example `https://cdn.toontownrewritten.com/media/news-site/img/25-06-15_pridedayteamspotlight.png`. |
