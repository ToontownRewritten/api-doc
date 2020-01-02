# Toontown Rewritten Population API

## Requests

An HTTP GET to the population API endpoint, https://www.toontownrewritten.com/api/population, will return the latest JSON response. No parameters are required, however, if you are frequently making calls to this API, I'd appreciate it if you set a descriptive User-Agent.

## Response

| Name        | Details |
|-------------|---------|
| error       | When data is present, `error` will be set to null. If `error` isn't null, then no other fields will be present, and `error` will be set to an error message |
| totalPopulation   | The total population of Toontown Rewritten. |
| populationByDistrict   | A dictionary of district names to population values. |
| lastUpdated | The epoch timestamp of when the web layer last queried for data. |

