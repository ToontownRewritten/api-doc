# Toontown Rewritten Release Notes API

## Requests

All requests must be submitted via HTTP GET to `https://www.toontownrewritten.com/api` with one of the following endpoints.

If you are frequently making calls to this API, we would appreciate it if you set a descriptive User-Agent.

## GET `/releasenotes`

Returns an array of all `note` objects, excluding the `body` field.

| Name | Description |
|------|-------------|
| noteId | Identifier for the release note. |
| slug | Version number as a string, for example `ttr-live-v4.1.7d`. |
| date | Date and time the note was published as a string, for example `April 20, 2025 at 5:25 AM`. |

## GET `/releasenotes/{noteId}`

Uses `noteId` to retrieve the corresponding `note` object. If no note is found, an `error` object is returned instead.

### `note` Values

| Name | Description |
|------|-------------|
| noteId | Identifier for the release note. |
| slug | Version number as a string, for example `ttr-live-v4.1.7d`. |
| date | Date and time the note was published as a string, for example `April 20, 2025 at 5:25 AM`. |
| body | HTML contents of the release note as a string. |

### `error` Values

| Name | Description |
|------|-------------|
| error | `Unknown release note` |
