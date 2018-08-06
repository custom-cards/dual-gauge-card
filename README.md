# Dual gauge card

Two gauges in one, built mostly with CSS.

Still WIP but usable.

![dual-gauge-card-screenshot](https://user-images.githubusercontent.com/2353088/43733272-5f59d8fe-99b4-11e8-8161-0c55e096b862.png)


Heavily inspired by [ciotlosm's gauge-card](https://github.com/ciotlosm/custom-lovelace/), but completly remimplented.

Why reimplement it? Just for fun with CSS and custom cards :wink:

## Config

| Name   | Type   | Default | Description                |
|--------|--------|---------|----------------------------|
| title  | string |         | Common title               |
| min    | int    | 0       | minimum value              |
| max    | int    | 100     | maximum value              |
| outer  | object |         | config for the outer gauge |
| inner  | object |         | config for the outer gauge |
| colors | object |         | color config (optional)    |

### gauge config

Both the gauges have the same attributes:

| Name      | Type   | Default | Description                                                      |
|-----------|--------|---------|------------------------------------------------------------------|
| entity    | string |         | entity id                                                        |
| attribute | string |         | use this attribute of the entity instead of its state (optional) |
| label     | string |         | label for this gauges value (optional)                           |
| unit      | object |         | unit to add to the value (optional)                              |
| colors    | object |         | color config (optional)                                          |

### color config

You may configure as many colors as you like.

Colors can be configured as simple list of color and value pairs. If a gauges value is above one of these values,
the according color is used for that gauge. If no color is found, the last color in the list is used as a fallback.
The list is automatically sorted so you don't need to do that in your config - but I recommend it anyways.

Colors may be configured for both gauges at once or individualy. In the latter case, colors for then inner gauge
are shaded by 25%.

To use a single color regardless of the value just use a single list entry with any value to always trigger the fallback.

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

