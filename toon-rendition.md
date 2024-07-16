# Toontown Rewritten Rendition API

## Overview

This API generates a screenshot of a toon based on a DNA string.

## Requests

An HTTP GET to the rendition endpoint, https://rendition.toontownrewritten.com/render/{dna}/{pose}/{width}x{height}.{extension}, will return the generated render.

## Parameters

| Name        | Details |
|-------------|---------|
| dna | The DNA string for the toon to be rendered. (Use Shift+F11 in-game to copy your toon DNA) |
| pose   | Pose your toon makes. At the moment these are the 8 options. (**head, laffmeter, portrait, portait-sleep, portrait-delighted, portrait-surprise, portrait-thinking, portrait-birthday, portrait-fall, portrait-grin, cake-topper, crying, waving**) |
| width   | Width of the returned render (ex. **1024**). |
| height   | Height of the returned render (ex. **1024**). |
| extension   | File extension can be either **png** or **webp** |

## Response

A toon from the provided DNA string will be generated.

Example: https://rendition.toontownrewritten.com/render/7424010101021d021d8b1b160016160104001c0000040000000000000000000000/portrait-birthday/1024x1024.png
