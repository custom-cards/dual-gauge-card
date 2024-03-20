# Dual gauge card

Two gauges in one, built mostly with CSS.

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![hacs_badge](https://img.shields.io/badge/HACS-Default-orange.svg)](https://github.com/custom-components/hacs)


![dual-gauge-card-screenshot](https://user-images.githubusercontent.com/2353088/43733272-5f59d8fe-99b4-11e8-8161-0c55e096b862.png)


Heavily inspired by [ciotlosm's gauge-card](https://github.com/ciotlosm/custom-lovelace/), but completly written
from scratch.

## Installation

Use [HACS](https://github.com/custom-components/hacs) (recommended)
or download [dual-gauge-card.js](https://github.com/custom-cards/dual-gauge-card/raw/master/dual-gauge-card.js) and place it in your www directory.

In your ui-lovelace.yaml add this:
```yaml
  - url: /community_plugin/dual-gauge-card/dual-gauge-card.js
    type: js
```

If you don't use HACS please change the url accordingly.

## Config

| Name             | Type   | Default | Description                                      |
|------------------|--------|---------|--------------------------------------------------|
| title            | string |         | Common title                                     |
| min              | int    | 0       | minimum value                                    |
| max              | int    | 100     | maximum value                                    |
| colors           | object |         | color config (optional)                          |
| background_color | string |         | background color of the gauges                   |
| shadeInner       | bool   | true    | shade (darken) colors of the inner gauge by 25%  |
| cardwidth        | int    | 300     | width of the card in pixels (see below)          |
| outer            | object |         | config for the outer gauge                       |
| inner            | object |         | config for the inner gauge                       |
| precision        | int    | 2       | decimal precision                                |

### gauge config

Both gauges have the same attributes:

| Name      | Type   | Default | Description                                                      |
|-----------|--------|---------|------------------------------------------------------------------|
| entity    | string |         | entity id                                                        |
| attribute | string |         | use this attribute of the entity instead of its state (optional) |
| label     | string |         | label for this gauges value (optional)                           |
| unit      | object |         | unit to add to the value (optional)                              |
| min       | int    |         | minimum value                                                    |
| max       | int    |         | maximum value                                                    |
| colors    | object |         | color config (optional)                                          |
| precision | int    | 2       | decimal precision                                                |

### cardwidth

You may use the config value _cardwidth_ to set the overall width of the card as an absolute value in pixels.
All elements of the gauge are sized relative to this so that the gauge scales to this, _but_ the card is not
responsive for now, i.e. it doesn't resize automatically.


### color config

Colors can be configured as list of pairs of each a color and a minimum value.

If a gauges value is greater than or equal to one of those minimum values, the according color 
is used for that gauge. If no color is found, the last color in the list is used as a fallback.
To use a single color regardless of the value just use a single list entry with any value to always trigger
the fallback.

By default, colors for the inner gauge are shaded by 25% (see option _shadeInner_).

The list is automatically sorted so you don't need to do that in your config - but I recommend it anyways.

### common config vs. individual config

Colors, as well as the min and max values, may be configured once for both gauges or individually for each gauge. Individual values override common values.

## Example

The example on the screenshot is configured like this:
```
- type: custom:dual-gauge-card
  title: Living room
  min: -20
  max: 40
  outer:
    entity: climate.living_room
    attribute: current_temperature
    label: "Current"
    unit: "°C"
  inner:
    entity: climate.living_room
    label: "Target"
    attribute: temperature
    unit: "°C"
  colors:
    - color: "var(--label-badge-red)"
      value: 27.5
    - color: "var(--label-badge-green)"
      value: 25
    - color: "var(--label-badge-yellow)"
      value: 18
    - color: "var(--label-badge-blue)"
      value: 0
    - color: "var(--paper-blue-400)"
      value: -40
```

In this example, the outer gauge has individual min and max values and uses default colors, whereas the inner
gauge has individual colors and uses the common min and max values.
```
- type: custom:dual-gauge-card
  title: Living room
  min: -20
  max: 40
  precision: 2
  outer:
    entity: climate.living_room
    attribute: current_temperature
    label: "Current"
    unit: "°C"
    min: -30
    max: 50
  inner:
    entity: climate.living_room
    label: "Target"
    attribute: temperature
    unit: "°C"
    colors:
      - color: "var(--label-badge-green)"
        value: 25
      - color: "var(--label-badge-yellow)"
        value: 18
      - color: "var(--label-badge-blue)"
        value: 0
```

