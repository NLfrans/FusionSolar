# FusionSolar

This file contains a script for Home Assistant.
The script read data from the Huawei FusionSolar Kios API.

FusionSolar Version 7.0 (from 2022-02-23)

For more info check out https://community.home-assistant.io/t/integration-solar-inverter-huawei-2000l/132350/362

```
  - platform: command_line  
    command: curl -s https://region04eu5.fusionsolar.huawei.com/rest/pvms/web/kiosk/v1/station-kiosk-file?kk=YOURTOKEN | python3 -c 'import json,sys;raw=sys.stdin.read();clean=raw.replace("&quot;",r"\"");obj=json.loads(clean);data_obj=json.loads(obj["data"]);print(data_obj["realKpi"]["realTimePower"]);'
    name: solar_real_time
    unit_of_measurement: 'KW'
    scan_interval: 60
    command_timeout: 30
  - platform: command_line  
    command: curl -s https://region04eu5.fusionsolar.huawei.com/rest/pvms/web/kiosk/v1/station-kiosk-file?kk=YOURTOKEN | python3 -c 'import json,sys;raw=sys.stdin.read();clean=raw.replace("&quot;",r"\"");obj=json.loads(clean);data_obj=json.loads(obj["data"]);print(data_obj["realKpi"]["cumulativeEnergy"]);'
    name: solar_cumulative
    unit_of_measurement: 'KW'
    scan_interval: 60
    command_timeout: 30
  - platform: command_line  
    command: curl -s https://region04eu5.fusionsolar.huawei.com/rest/pvms/web/kiosk/v1/station-kiosk-file?kk=YOURTOKEN | python3 -c 'import json,sys;raw=sys.stdin.read();clean=raw.replace("&quot;",r"\"");obj=json.loads(clean);data_obj=json.loads(obj["data"]);print(data_obj["realKpi"]["monthEnergy"]);'
    name: solar_month
    unit_of_measurement: 'KW'
    scan_interval: 60
    command_timeout: 30
  - platform: command_line  
    command: curl -s https://region04eu5.fusionsolar.huawei.com/rest/pvms/web/kiosk/v1/station-kiosk-file?kk=YOURTOKEN | python3 -c 'import json,sys;raw=sys.stdin.read();clean=raw.replace("&quot;",r"\"");obj=json.loads(clean);data_obj=json.loads(obj["data"]);print(data_obj["realKpi"]["dailyEnergy"]);'
    name: solar_daily
    unit_of_measurement: 'KW'
    scan_interval: 60
    command_timeout: 30
  - platform: command_line  
    command: curl -s https://region04eu5.fusionsolar.huawei.com/rest/pvms/web/kiosk/v1/station-kiosk-file?kk=YOURTOKEN | python3 -c 'import json,sys;raw=sys.stdin.read();clean=raw.replace("&quot;",r"\"");obj=json.loads(clean);data_obj=json.loads(obj["data"]);print(data_obj["realKpi"]["yearEnergy"]);'
    name: solar_year
    unit_of_measurement: 'KW'
    scan_interval: 60
    command_timeout: 30

```
