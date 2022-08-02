# Toontown Rewritten Population API

## Requests

An HTTP GET to the population API endpoint, https://www.toontownrewritten.com/api/population, will return the latest JSON response. No parameters are required, however, if you are frequently making calls to this API, I'd appreciate it if you set a descriptive User-Agent.

## Response

| Name        | Details |
|-------------|---------|
| error       | When data is present, `error` will be set to null. If `error` isn't null, then no other fields will be present, and `error` will be set to an error message |
| totalPopulation   | The total population of Toontown Rewritten. |
| populationByDistrict   | A dictionary of district names to population values. |
| statusByDistrict | A dictionary of district names to [status values](#status-values). |
| lastUpdated | The epoch timestamp of when the web layer last queried for data. |

### Status Values

| Name       | Description |
|------------|-------------|
| offline    | District is in the process of starting up and will become `online` shortly. |
| online     | District is online and open to players |
| draining   | District is undergoing a drain (unintrusively migrating players to another district) and cannot be entered via the district list. Usually takes place when the district is being restarted for fixes. |
| closed     | District is closed to players. Usually happens after a drain has completed but some players have not yet finished activites. |