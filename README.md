# FusionSolar

This file contains a script for Home Assistant.
The script read data from the Huawei FusionSolar Kios API.

FusionSolar Version 6.0 (till 2021-04-26)

```
  - platform: rest
    name: pv_production_realtime
    resource: https://eu5.fusionsolar.huawei.com/kiosk/getRealTimeKpi
    method: POST
    force_update: true
    scan_interval: 30
    payload: '{"kk":"replace_with_your_kios_id"}'
    json_attributes:
      - buildCode
      - data
      - failCode
      - message
      - params
      - success
    headers:
      Content-Type: application/json

  - platform: template
    sensors:
      pv_production_lifetime:
        value_template: '{{ states.sensor.pv_production_realtime.attributes["data"]["allCapacity"]|float |round(0) }}'
        unit_of_measurement: "kWh"
        device_class: power
        icon_template: 'mdi:solar-panel'
      pv_production_year:
        value_template: '{{ states.sensor.pv_production_realtime.attributes["data"]["yearCapacity"]|float |round(0) }}'
        unit_of_measurement: "kWh"
        device_class: power
        icon_template: 'mdi:solar-panel'
      pv_production_month:
        value_template: '{{ states.sensor.pv_production_realtime.attributes["data"]["monthCapacity"]|float |round(0) }}'
        unit_of_measurement: "kWh"
        device_class: power
        icon_template: 'mdi:solar-panel'
      pv_production_today:
        value_template: '{{ states.sensor.pv_production_realtime.attributes["data"]["dailyCapacity"]|float |round(2) }}'
        unit_of_measurement: "kWh"
        device_class: power
        icon_template: 'mdi:solar-panel'
        entity_id: sensor.pv_production_realtime
      pv_production_now:
        value_template: '{{ states.sensor.pv_production_realtime.attributes["data"]["curPower"]|float * 1000|round(2) }}'
        unit_of_measurement: "Wh"
        device_class: power
        icon_template: 'mdi:solar-panel'
        entity_id: sensor.pv_production_realtime
```
