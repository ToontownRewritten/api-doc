# Toontown Rewritten Rendition API

## Overview

This API provides a screenshot of your a toon generated from a DNA string.

## Requests

An HTTP GET to the Field Office API endpoint, https://rendition.toontownrewritten.com/render/{dna}/{render-type}/{width}x{height}.{extension}, will return the generated render.

## Parameters

| Name        | Details |
|-------------|---------|
| dna | The DNA string of your toon generated. |
| render-type   | Pose your toon makes. At the moment these are the 7 options. (**head, portrait, portait-sleep, portrait-delighted, portrait-surprise, portrait-thinking, portrait-birthday**) |
| width   | Width of the returned render (ex. **1024**). |
| height   | Height of the returned render (ex. **1024**). |
| extension   | File extension can be either **png** or **webp** |

## Response

A toon from the provided DNA string will be generated.

Example: https://rendition.toontownrewritten.com/render/7424010101021d021d8b1b160016160104001c0000040000000000000000000000/portrait-birthday/1024x1024.png

## DNA Data

The DNA string is in hexadecimals.

Hexadecmal 1: DNA Type (74 is Toon)

Hexadecmal 2: Head Type/Species (Between 00-29)

Hexadecmal 3: Torso Type (Between 00-02)

Hexadecmal 4: Legs Type (Between 00-02)

Hexadecmal 5: Eyelashes (01 = None, 00 = Yes)

Hexadecmal 6: Shirt Style/Texture: (Between 00-9f, ex. 0a, 2d, 68, 99, 00, 0f, 27)

Hexadecmal 7: Shirt Color: (Between 00-2d, (1b is default), NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 8: Sleeves Style-Texture: (Between 00-cc, ex. 0a, 2d, 68, 99, 00, 0f, 27, aa, af, bd, ca)

Hexadecmal 9: Sleeves Color: (Between 00-2d, (1b is default), NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 10: Shorts/Skirt Texture: (Between 00-bb, ex. 0a, 2d, 68, 99, 00, 0f, 27, aa, af, 8d, 5e)

Hexadecmal 11: Shorts/Skirt Color: (Between 00-2d, (1b is default), NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 12: Torso Color: (Between 00-2a, NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 13: Glove Color: (Between 00-2a, NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 14: Legs Color: (Between 00-2a, NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 15: Head Color: (Between 00-2a, NOTE: No bigger than 29 (ex. 30, 99, 58))

Hexadecmal 16: Shoes Item ID

Hexadecmal 17: Shoes Texture ID

Hexadecmal 18: Shoes Color ID

Hexadecmal 19: Hat Item ID (Between 00-2a, NOTE: No bigger than 41 (ex. 42, 53, 70))

Hexadecmal 20: Hat Texture ID (Between 00-5b, NOTE: No bigger than 59 (ex. 60, 74, 83))

Hexadecmal 21: Hat Color ID

Hexadecmal 22: Glasses Item ID (Between 00-1a, NOTE: No bigger than 15 (ex. 16, 19, 68))

Hexadecmal 23: Glasses Texture ID (Between 00-2f, NOTE: No bigger than 30 (ex. 31, 46, 72))

Hexadecmal 24: Glasses Color ID

Hexadecmal 25: Neckwear Item ID (Between 00-03)

Hexadecmal 26: Neckwear Texture ID (Between 00-4d, NOTE: No bigger than 49 (ex. 50, 67, 84))

Hexadecmal 27: Neckwear Color ID

Hexadecmal 28: Backpack Item ID (Between 00-22, NOTE: Can use 0a-1f)

Hexadecmal 29: Backpack Texture ID

Hexadecmal 30: Backpack Color ID

Hexadecmal 31: Unknown
