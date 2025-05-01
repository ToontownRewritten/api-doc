# Toontown Rewritten Local (Companion App) API

## Requests

All requests must be submitted via HTTP GET to `localhost` with a default port of `1547`, this port is incremented if already in use to allow for multitoons (from `1547` through to `1552`).

All requests must ensure compliance with the following:

- Must have the `Host` header set as `localhost:1547` (or other port as mentioned above).
- Must have the `User-Agent` header set descriptively, this will be shown on the in-game consent prompt.
- Must set the `Authorization` header to a random value unique to each session of the application.

Requests which do not honour these requirements will be rejected by the API server.

When possible the API server listens on both `127.0.0.1` and `::1`, with a bias towards IPv6.

## GET `/info.json`

| Name | Details |
|------|---------|
| toon | Toon details. |
| laff | Toon laff. |
| location | Toon location and District. |
| gags | Toon Gag details. |
| tasks | Toon Task details. |
| invasion | District invasion details, or `null` if no invasion active.

### `toon` Values

| Name | Description |
|------|-------------|
| name | Toon name. |
| species | Toon species name. |
| headColor | Toon head color in hex format. |
| style | Toon DNA string for use with Rendition. |

### `laff` Values

| Name | Description |
|------|-------------|
| current | Current Toon laff. |
| max | Maximum Toon laff. |

### `location` Values

| Name | Description |
|------|-------------|
| zone | Zone as a string, for example `Silly Street`. |
| neighborhood | Neighborhood as a string, for example `Toontown Central`. |
| district | District as a string, for example `Zapwood`. |

### `gags` Values

`gags` contains a dictionary of Gags with the value being either `null` if the Toon does not have access to that track, or an object with the following values if they do.

| Name | Description |
|------|-------------|
| gag | `gag` object |
| organic | `gag` object or `null` if no organic Gags in the track. |
| experience | `experience` object. |

#### `gag` Values

| Name | Description |
|------|-------------|
| level | Level as an integer of the highest Gag unlocked/organic in the track, starting at 1. |
| name | Localised name of the highest Gag unlocked/organic in the track. |

#### `experience` Values

| Name | Description |
|------|-------------|
| current | Current experience as an integer. |
| next | Next milestone as an integer. |

### `tasks` Values

`tasks` is an array of `task` objects.

#### `task` Values

| Name | Description |
|------|-------------|
| objective | `objective` object. |
| from | `npc` object containing the NPC the task was accepted from. |
| to | `npc` object containing the NPC the task will be turned in to. |
| reward | Localised reward text for the task. |
| deletable | Boolean indicating if the task can be deleted from the Shticker book. |

#### `objective` Values

| Name | Description |
|------|-------------|
| text | Localised objective text for the task. |
| where | Localised location name for the task criteria or `"Anywhere"`. |
| progress | `progress` object. |

#### `progress` Values

| Name | Description |
|------|-------------|
| text | Localised progress text for the task. |
| current | Current task progress as an integer. |
| target | Target task progress as an integer. |

#### `npc` Values

| Name | Description |
|------|-------------|
| name | Localised name of the NPC. |
| building | Localised building name where the NPC is situated, or an empty string. |
| zone | Localised zone name where the NPC is situated. |
| neighborhood | Localised neighborhood name where the NPC is situated. |

### `invasion` Values

| Name | Description |
|------|-------------|
| cog | Name of invading Cog, for example `Version 2.0 Flunky`. |
| quantity | The total amount of Cogs invading the District. |
| mega | Boolean value indicating if it's a mega-invasion. |
