# Toontown Rewritten Invasions API

## Overview
APIs about the current status of the game world are always fun, so TTR has published our internal invasion tracker to the world via a publicly consumable API.

The design for this API is driven by the implementation of actual invasion tracking on TTR servers. Each district periodically sends current invasion data to a central server (though that server isn't our web server), where it is stored in memory. On a separate timer, the TTR web layer periodically queries this central server for the latest invasion data, which is then cached and returned to everyone who queries the invasions API. This design is flexible and requires few extra resources to operate, though the data isn't as fresh as a result.

**Note:** The header Access-Control-Allow-Origin is set to * on this API.

## Requests

An HTTP GET to the invasions API endpoint, https://www.toontownrewritten.com/api/invasions, will return the latest JSON response. No parameters are required, however, if you are frequently making calls to this API, I'd appreciate it if you set a descriptive User-Agent.

## Response

| Name        | Details |
|-------------|---------|
| error       | When data is present, `error` will be set to null. If `error` isn't null, then no other fields will be present, and `error` will be set to an error message |
| invasions   | A dictionary of district names to invasion data. |
| lastUpdated | The epoch timestamp of when the web layer last queried for data. |

### Invasion data
| Name | Details |
|------|---------|
| type | The name of the invading cog. The localized name will always be in English, and will always be the singular form of the cog. If the cog is a skelecog, ` (Skelecog)` will be appended. If the cog is version 2.0, `Version 2.0 ` will be prepended. |
| asOf | The epoch timestamp of when the district last reported its invasion status. |
| progress | A string, of the form `%d/%d`, where the first number represents the number of cogs already despawned during the invasion and the second number represents the total size of the invasion. |