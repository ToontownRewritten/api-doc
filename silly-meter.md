# Toontown Rewritten Silly Meter API

## Overview
The Silly Meter was a major update added to the game on [March 6th, 2019](https://www.toontownrewritten.com/news/item/541/introducing-the-silly-meter).

This API provides insights into the current state of the feature in-game.

## Requests

An HTTP GET to the Silly Meter API endpoint, https://www.toontownrewritten.com/api/sillymeter, will return the latest JSON response. No parameters are required, however, if you are frequently making calls to this API, I'd appreciate it if you set a descriptive User-Agent.

## Response

| Name        | Details |
|-------------|---------|
| state       | The current state of the Silly Meter. Valid options are `Active` (currently accumulating Silly Particles), `Reward` (currently providing rewards to all of Toontown), or `Inactive` (currently cooling down).|
| hp          | The current HP of the Silly Meter. Silly Meter HP ranges from 0 to 5,000,000. |
| rewards     | A list of three strings, which are the current Silly Teams that players are eligible to join. |
| nextUpdateTimestamp | The epoch timestamp in seconds of when the Silly Meter will next update itself. In the `Active` state, this means the next time that Silly Points will be calculated and added in to the current HP. In the `Reward` state, this timestamp will indicate when the rewards end. In the `Inactive` state, this timestamp will indicate when the Silly Meter will re-enter the `Active` state. |
| asOf | The epoch timestamp at which the Silly Meter server generated this data. Multiple layers of caching are used in the implementation, so this timestamp is provided by the Silly Meter Gameserver itself. |
| error | (optional) Present iff the web server has no cached response to serve. |
