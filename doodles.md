# Toontown Rewritten Doodles API

## Overview

This API provides a listing of all Doodles currently available to purchase from the Pet Shops around Toontown.

**Note:** The header Access-Control-Allow-Origin is set to * on this API.

## Requests

An HTTP GET to the Doodles API endpoint, https://www.toontownrewritten.com/api/doodles, will return the latest JSON response. No parameters are required, however, if you are frequently making calls to this API, we'd appreciate it if you set a descriptive User-Agent.

## Response

The response consists of a dictionary of Districts each containing a dictionary of Playgrounds.

Each Playground entry contains an array of currently available [Doodles](#doodle-data).

### Doodle data

| Name   | Details |
|--------|---------|
| dna    | A string form of the DNA that makes up the Doodle, used when requesting an image of the Doodle from [Rendition](#rendition). |
| traits | An array of the traits for the Doodle, as visible in the Pet Shop. |
| cost   | An integer of the cost of the Doodle in Jellybeans. |

## Rendition

Rendition is our rendering service for Toon and Doodle images, an example of the images produced being used in production can be found at [Toon HQ](https://toonhq.org).

### Requests

URLs for Doodles on Rendition are formatted like so:
> rendition.toontownrewritten.com/render/**{dna}**/doodle/**{width}**x**{height}**.**{extension}**

#### Parameters

| Name      | Details | Valid Options |
|-----------|---------|---------------|
| dna       | The DNA string from the API response. | Any valid Doodle DNA string. |
| width     | The requested width of the output. | `>=128` and `<=2048` |
| height    | The requested height of the output. | `>=128` and `<=2048` |
| extension | The format to encode the rendered image to. | `.webp`, `.png` |

**Note:** It's preferable to stick to requesting images with the width and height the same value, and the value being 256 or 512.