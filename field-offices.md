# Toontown Rewritten Field Offices API

## Overview

Field Offices were added to the game as part of the Sellbot Task Force expansion on [December 3, 2021](https://toontownrewritten.com/taskforce/fieldoffices).

This API provides information about all active Field Offices in the game.

## Requests

An HTTP GET to the Field Office API endpoint, https://www.toontownrewritten.com/api/fieldoffices, will return the latest JSON response. No parameters are required. However, if you are frequently making calls to this API, we would appreciate it if you set a descriptive User-Agent.

## Response

| Name        | Details |
|-------------|---------|
| lastUpdated | The epoch timestamp of when the web layer last queried for data. |
| fieldOffices   | A dictionary of Zone IDs (4-digit integers) to Field Office data. |

## Field Office Data

| Name        | Details |
|-------------|---------|
| department  | A string containing a single letter that corresponds to the Cog Department that this Field Office belongs to. |
| difficulty  | The number of Stars for this Field Office (zero-indexed). |
| annexes     | The number of Annexes remaining until this Field Office is defeated. |
| open        | A boolean that notes whether this Field Office is open for Toons to enter. A Field Office will close its elevator doors if there are roughly more groups of Toons inside than the number of Annexes. |
| expiring    | After the last Annex of a Field Office has been defeated, this will provide the epoch timestamp in seconds of when all groups inside will be kicked from the Field Office. |

## Zone ID Lookup

| Zone ID | Street Name |
|---------|-------------|
| 3100    | Walrus Way |
| 3200    | Sleet Street |
| 3300    | Polar Place |
| 4100    | Alto Avenue |
| 4200    | Baritone Boulevard |
| 4300    | Tenor Terrace |
| 5100    | Elm Street |
| 5200    | Maple Street |
| 5300    | Oak Street |
| 9100    | Lullaby Lane |
| 9200    | Pajama Place |