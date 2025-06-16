# Toontown Rewritten Local (Companion App) API

## Requests

All requests must be submitted via HTTP GET to `localhost` with a default port of `1547`, this port is incremented if already in use to allow for multitoons (from `1547` through to `1552`).

All requests must ensure compliance with the following:

- Must have the `Host` header set as `localhost:1547` (or other port as mentioned above).
- Must have the `User-Agent` header set descriptively, this will be shown on the in-game consent prompt.
- Must set the `Authorization` header to a random value unique to each session of the application.

Requests which do not honour these requirements will be rejected by the API server.

When possible the API server listens on both `127.0.0.1` and `::1`, with a bias towards IPv6.

## GET `/all.json`

| Name | Details |
|------|---------|
| [toon](#get-toonjson) | Toon details. |
| [laff](#get-laffjson) | Toon laff. |
| [location](#get-locationjson) | Toon location and District. |
| [gags](#get-gagsjson) | Toon Gag details. |
| [tasks](#get-tasksjson) | Toon Task details. |
| [invasion](#get-invasionjson) | District invasion details, or `null` if no invasion active. |
| [fish](#get-fishjson) | Toon Fish details. |
| [flowers](#get-flowersjson) | Toon Flower details. |
| [cogsuits](#get-cogsuitsjson) | Toon Cogsuit details. |
| [golf](#get-golfjson) | Toon Golf details. |
| [racing](#get-racingjson) | Toon Racing details. |
| [beans](#get-beansjson) | Toon Beans details. |
| [rewards](#get-rewardsjson) | Toon Rewards details. |
| [cattlelog](#get-cattlelogjson) | Toon Cattlelog details. |

## GET `/info.json`

| Name | Details |
|------|---------|
| [toon](#get-toonjson) | Toon details. |
| [laff](#get-laffjson) | Toon laff. |
| [location](#get-locationjson) | Toon location and District. |
| [gags](#get-gagsjson) | Toon Gag details. |
| [tasks](#get-tasksjson) | Toon Task details. |
| [invasion](#get-invasionjson) | District invasion details, or `null` if no invasion active. |

## GET `/toon.json`

| Name | Description |
|------|-------------|
| id | Toon identifier, for example `TTID-ABCD-EFGH`. |
| name | Toon name. |
| species | Toon species name. |
| headColor | Toon head color in hex format. |
| style | Toon DNA string for use with Rendition. |

## GET `/laff.json`

| Name | Description |
|------|-------------|
| current | Current Toon laff. |
| max | Maximum Toon laff. |

## GET `/location.json`

| Name | Description |
|------|-------------|
| zone | Zone as a string, for example `Silly Street`. |
| neighborhood | Neighborhood as a string, for example `Toontown Central`. |
| district | District as a string, for example `Zapwood`. |

## GET `/gags.json`

`gags` contains a dictionary of Gags with the value being either `null` if the Toon does not have access to that track, or an object with the following values if they do.

| Name | Description |
|------|-------------|
| gag | `gag` object |
| organic | `gag` object or `null` if no organic Gags in the track. |
| experience | `experience` object. |

### `gag` Values

| Name | Description |
|------|-------------|
| level | Level as an integer of the highest Gag unlocked/organic in the track, starting at 1. |
| name | Localised name of the highest Gag unlocked/organic in the track. |

### `experience` Values

| Name | Description |
|------|-------------|
| current | Current experience as an integer. |
| next | Next milestone as an integer. |

## GET `/tasks.json`

`tasks` is an array of `task` objects.

### `task` Values

| Name | Description |
|------|-------------|
| objective | `objective` object. |
| from | `npc` object containing the NPC the task was accepted from. |
| to | `npc` object containing the NPC the task will be turned in to. |
| reward | Localised reward text for the task or `null` if there is no reward. |
| type | Localised flavor text describing the task, for example `Just for fun!`. If there is no flavor text, this will be `null`. |
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

## GET `/invasion.json`

| Name | Description |
|------|-------------|
| cog | Name of invading Cog, for example `Version 2.0 Flunky`. |
| quantity | The total amount of Cogs invading the District. |
| mega | Boolean value indicating if it's a mega-invasion. |

## GET `/fish.json`

| Name       | Description |
|------------|-------------|
| rod        | `rod` object containing details about the fishing rod. |
| collection | Dictionary where keys are fish IDs and values are `fish` objects. |

### `rod` Values

| Name | Description |
|------|-------------|
| id   | Identifier for the fishing rod. |
| name | Localised name of the fishing rod. |

#### `fish` Values

| Name      | Description |
|-----------|-------------|
| name      | Localised name of the fish species. |
| album     | Dictionary where keys are subspecies IDs and values are subspecies objects. |

#### `subspecies` Values

| Name   | Description |
|--------|-------------|
| name   | Localised name of the fish variant. |
| weight | Weight of the fish variant in ounces. |

## GET `/flowers.json`

| Name          | Description |
|---------------|-------------|
| shovel        | `shovel` object containing details about the player's shovel. |
| wateringCan   | `wateringCan` object containing details about the player's watering can. |
| collection    | Dictionary where keys are flower IDs and values are `flower` objects. |

### `shovel` Values

| Name      | Description |
|-----------|-------------|
| id        | Identifier for the shovel. |
| name      | Localised name of the shovel. |
| curSkill  | Current skill level for the shovel. |
| maxSkill  | Maximum skill level for the shovel. |

### `wateringCan` Values

| Name      | Description |
|-----------|-------------|
| id        | Identifier for the watering can. |
| name      | Localised name of the watering can. |
| curSkill  | Current skill level for the watering can. |
| maxSkill  | Maximum skill level for the watering can. |

### `flower` Values

| Name      | Description |
|-----------|-------------|
| name      | Localised name of the flower species. |
| album     | Dictionary where keys are variant IDs and values are localised variant names. |

## GET `/cogsuits.json`

`cogsuits` contains a dictionary where the keys represent the Cog departments (`c`, `l`, `m`, `s` for Bossbot, Lawbot, Cashbot, and Sellbot). Each value is an object with the following values.

### `cogsuit` Values

| Name         | Description |
|--------------|-------------|
| department   | The name of the Cog department |
| hasDisguise  | Boolean indicating if the Toon has a disguise for this department. |
| suit         | `suit` object containing details about the Cog suit, or omitted if `hasDisguise` is false. |
| version      | Version of the Cog suit as an integer, or omitted if `hasDisguise` is false. |
| level        | Current level of the Cog suit as an integer, or omitted if `hasDisguise` is false.|
| promotion    | `promotion` object. Omitted if no promotion is available or `hasDisguise` is false. |

#### `suit` Values

| Name | Description |
|------|-------------|
| id   | Identifier for the Cog suit. |
| name | Localised name of the Cog suit. |

#### `promotion` Values

| Name    | Description |
|---------|-------------|
| current | Current promotion progress as an integer. |
| target  | Target promotion progress as an integer. |

## GET `/golf.json`

`golf` is an array of `stats` objects.

| Name | Description |
|------|-------------|
| name | Localised name of the golf statistic. |
| num  | Numeric value representing the statistic. |

## GET `/racing.json`

`racing` is an array of `stats` objects.

| Name | Description |
|------|-------------|
| name | Localised name of the racing statistic. |
| num  | Numeric value representing the statistic. |

## GET `/beans.json`

| Name | Description |
|------|-------------|
| jar  | `jar` object containing details about the Toon's jellybean jar. |
| bank | `bank` object containing details about the Toon's jellybean bank. |

### `jar` Values

| Name    | Description |
|---------|-------------|
| current | Current amount of jellybeans in the jar. |
| max     | Maximum amount of jellybeans the jar can hold. |

### `bank` Values

| Name    | Description |
|---------|-------------|
| current | Current amount of jellybeans in the bank. |
| max     | Maximum amount of jellybeans the bank can hold. |

## GET `/rewards.json`

| Name      | Description |
|-----------|-------------|
| [sos](#get-sosjson) | Toon SOS cards details.  |
| [unites](#get-unitesjson) | Toon Unites details. |
| [summons](#get-summonsjson) | Toon summons details. |
| [pinkslips](#get-pinkslipsjson) | Toon pinkslips details. |
| [remotes](#get-remotesjson) | Toon remotes details. |

## GET `/sos.json`

`sos` contains a dictionary where keys are SOS toon names and values are their quantity.

## GET `/unites.json`

`unites` contains a dictionary where keys are Unite types, for example `Gag-Up`. Values are nested dictionaries where keys are Unite variants, for example `Gag-Up Squirt`, and values are their quantity.

## GET `/summons.json`

`summons` contains a dictionary where keys are Cog identifiers and values are `summon` objects.

### `summon` Values

| Name     | Description |
|----------|-------------|
| name     | Localised name of the Cog summon. |
| single   | Boolean indicating if a single Cog summon is available. |
| building | Boolean indicating if a building summon is available. |
| invasion | Boolean indicating if an invasion summon is available. |

## GET `/pinkslips.json`

`pinkslips` contains the Toon's current quantity of pink slips.

## GET `/remotes.json`

`remotes` contains a dictionary where keys are remote types (`Damage Remote`, `Healing Remote`). Values are nested dictionaries, where keys are the levels (`1`, `2`, `3`) and values are their quantity.

## GET `/cattlelog.json`

| Name   | Description |
|--------|-------------|
| series | Current series of the Cattlelog. |
| issue  | Current issue of the Cattlelog. |
