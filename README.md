# ha-tdv-bar
A Home Assistant lovelace card to display bar chart  oriented to display power sensors

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=for-the-badge)](https://github.com/hacs/integration)


![Simple example card](img/main-image.png)


## Installation

Download and install the plugin like any other custom resource in Home Assistant.

<a href="https://my.home-assistant.io/redirect/hacs_repository/?owner=tdvtdv&repository=ha-tdv-bar&category=plugin" target="_blank" rel="noreferrer noopener"><img src="https://my.home-assistant.io/badges/hacs_repository.svg" alt="Open your Home Assistant instance and open a repository inside the Home Assistant Community Store." /></a>


## Installation

For installation you should have [HACS](https://hacs.xyz/docs/setup/download/) installed. Then add this repository https://github.com/tdvtdv/ha-tdv-bar in HACS and install the card. You have to reload you browser after installation.

Then you can add the new card into your dashboard.

### Easiest method

Install via HACS

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=tdvtdv&repository=ha-tdv-bar&category=plugin)

### Alternative method

1. Download `ha-tdv-bar.js` from the [Releases](https://github.com/tdvtdv/ha-tdv-bar/releases) page
2. Upload to `/www/tdv-bar-card/ha-tdv-bar.js` (via Samba, File Editor, SSH, etc.)
3. Visit the Resources page in your Home Assistant install and add `/tdv-bar-card/ha-tdv-bar.js` as a
   JavaScript Module.
   [![Open your Home Assistant instance and show your dashboard resources.](https://my.home-assistant.io/badges/lovelace_resources.svg)](https://my.home-assistant.io/redirect/lovelace_resources/)
4. Refresh your browser



## Options

| Name              | Type    | Requirement  | Default             | Description                                 |
| ----------------- | ------- | ------------ | ------------------- | ------------------------------------------- |
| type              | string  | **Required** |                     | `custom:tdv-bar-card`
| title             | string  | **Optional** |                     | Optional header title for the card
| height            | number  | **Optional** |                     | The height of the card in pixels
| rangemax          | number  | **Optional** | 2000                | Maximum bar scale range
| histmode          | number  | **Optional** | 1                   | Historical chart display mode<br>0-hide<br>1-show
| animation         | number  | **Optional** | 1                   | Bar chart animation<br>0-disable<br>1-enable
| trackingmode      | number  | **Optional** | 1                   | Mouse tracking mode<br>0-disable<br>1-bar only<br>2-history<br>3-bar and history
| trackingvalue     | string  | **Optional** | max                 | Type of value to be tracked (min, avg, max)
| scaletype         | string  | **Optional** | log10               | Scale type (linear or log10 )
| entities          | object  | **Required** |                     | Displayed entities. See [Entities](#Entities)

### Entities

| Name              | Type    | Requirement  | Default              | Description                                 |
| ----------------- | ------- | ------------ | -------------------- | ------------------------------------------- |
| entity            | string  | **Required** |                      | Entity id of the sensor
| icon              | string  | **Optional** |                      | Icon for this entity
| name              | string  | **Optional** |                      | Custom label for this entity
| state             | string  | **Optional** |                      | Change state entity id (e.g. switch)
| barcolor          | string  | **Optional** | Prymary system color | Individual bar color


### Example

```yaml
type: custom:tdv-bar-card
title: Energy consumers
scaletype: log10
rangemax: 2500
histmode: 1
trackingmode: 1
trackingvalue: max
entities:
  - entity: sensor.energomonitor_power
    icon: mdi:power-standby
    name: Total consumption
    barcolor: '#008000'
  - entity: sensor.speaker_power
    icon: mdi:speaker
    name: Speaker
    state: switch.dinamiki_na_kukhne
  - entity: sensor.energomonitor_fridge_power
    icon: mdi:fridge
    name: Fridge
  - entity: sensor.iot_power
    icon: mdi:alert-octagram-outline
    name: IOT
    state: switch.iot
```