# Dual gauge card

Two gauges in one, built mostly with CSS.

![dual-gauge-card-screenshot](https://user-images.githubusercontent.com/2353088/43733272-5f59d8fe-99b4-11e8-8161-0c55e096b862.png)


Heavily inspired by [ciotlosm's gauge-card](https://github.com/ciotlosm/custom-lovelace/), but completly written
from scratch.

## Config

| Name      | Type   | Default | Description                            |
|-----------|--------|---------|----------------------------------------|
| title     | string |         | Common title                           |
| min       | int    | 0       | minimum value                          |
| max       | int    | 100     | maximum value                          |
| outer     | object |         | config for the outer gauge             |
| inner     | object |         | config for the outer gauge             |
| colors    | object |         | color config (optional)                |
| cardwidth | int    | 300     | width or the card in pixel (see below) |

### gauge config

Both the gauges have the same attributes:

| Name      | Type   | Default | Description                                                      |
|-----------|--------|---------|------------------------------------------------------------------|
| entity    | string |         | entity id                                                        |
| attribute | string |         | use this attribute of the entity instead of its state (optional) |
| label     | string |         | label for this gauges value (optional)                           |
| unit      | object |         | unit to add to the value (optional)                              |
| colors    | object |         | color config (optional)                                          |

### cardwidth

You may use the config value _cardwidth_ to set the overall width of the card as an absolute value in pixels.
All elements of the gauge are sized relative to this so that the gauge scales to this, _but_ the card is not
responsible for now, i.e. it doesn't resize automatically.


### color config

Colors can be configured as list of pairs of each a color and a value.

If a gauges value is above one of those values, the according color is used for that gauge.
If no color is found, the last color in the list is used as a fallback.
To use a single color regardless of the value just use a single list entry with any value to always trigger
the fallback.

Colors may be configured for both gauges at once or for each gauge individualy. In the latter case,
colors for then inner gauge are shaded by 25%.

The list is automatically sorted so you don't need to do that in your config - but I recommend it anyways.

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

