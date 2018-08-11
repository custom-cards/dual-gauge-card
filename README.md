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

Both gauges have the same attributes:

| Name      | Type   | Default | Description                                                      |
|-----------|--------|---------|------------------------------------------------------------------|
| entity    | string |         | entity id                                                        |
| attribute | string |         | use this attribute of the entity instead of its state (optional) |
| label     | string |         | label for this gauges value (optional)                           |
| unit      | object |         | unit to add to the value (optional)                              |
| colors    | object |         | color config (optional)                                          |
| min       | int    | min from Config   | minimum value (optional)                               |
| max       | int    | max from Config   | maximum value (optional)                               |

### cardwidth

You may use the config value _cardwidth_ to set the overall width of the card as an absolute value in pixels.
All elements of the gauge are sized relative to this so that the gauge scales to this, _but_ the card is not
responsive for now, i.e. it doesn't resize automatically.


### color config

Colors can be configured as list of pairs of each a color and a value.

If a gauges value is above one of those values, the according color is used for that gauge.
If no color is found, the last color in the list is used as a fallback.
To use a single color regardless of the value just use a single list entry with any value to always trigger
the fallback.

Colors may be configured for both gauges at once or for each gauge individualy. In the latter case,
colors for then inner gauge are shaded by 25%.

The list is automatically sorted so you don't need to do that in your config - but I recommend it anyways.

### min and max config

There is 3 ways to config the minimum and maximum value of the gauge:

1. No configuration - The vaule for outer and inner will be 0-100 (as default)
2. Configuration in the "Config" part - The vaule for outer and inner will be the same.
3. Configuration in outer and inner separately - outer and inner will have different values , as you set



## Examples

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
Example for gauge with separately min and max values and colors-inside outer gauge and inner gauge:
```
      - type: custom:dual-gauge-card
        title: SpeedTest
        outer:
          entity: sensor.speedtest_download        
          min: 0
          max: 400
          label: "Down"
          colors:
           - color: 'var(--label-badge-red)'
             value: 90
           - color: 'var(--label-badge-yellow)'
             value: 250
           - color: 'var(--label-badge-green)'
             value: 350
        inner:
          entity: sensor.speedtest_upload        
          min: 0
          max: 100
          label: "Up"
          colors:
          - color: 'var(--label-badge-red)'
            value: 30
          - color: 'var(--label-badge-green)'
            value: 50
          - color: 'var(--label-badge-blue)'
            value: 70  
```
