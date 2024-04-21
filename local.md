# Toontown Rewritten Local (Companion App) API

## Requests

All requests must be submitted via HTTP GET to `localhost` with a default port of `1547`, this port is incremented if already in use to allow for multitoons (from `1547` through to `1552`).

All requests must have the `Host` header set as `localhost:1547` (or other port as mentioned above), and the `User-Agent` set descriptively. Requests which do not honour these requirements will be aborted by the API server.

When possible the API server listens on both `127.0.0.1` and `::1`, with a bias towards IPv6.

## GET `/info.json`

| Name | Details |
|------|---------|
| toon | Toon details. |
| laff | Toon laff. |
| location | Toon location and District. |
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

### `invasion` Values

| Name | Description |
|------|-------------|
| cog | Name of invading Cog, for example `Version 2.0 Flunky`. |
| quantity | The total amount of Cogs invading the District. |
| mega | Boolean value indicating if it's a mega-invasion. |
