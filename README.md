# Tion Home Assistant
This component provides integration of Tion devices (breezers and climate sensors) into Home Assistant smart home system. Based on the [tion](https://github.com/airens/tion) package.
## Installation
### HACS:
1. Goto HACS->Settings->Custom repositories 
2. Add `airens/tion_home_assistant` to `ADD CUSTOM REPOSITORY` field and select `Integration` in `CATEGORY`. Click `Save` button
### No HACS:
1. download zip file with this repository
2. put content to your `config/custom_components/tion` directory
### ...
3. add to your configuration.yaml:
```yaml
tion:
  username: !secret tion_email
  password: !secret tion_password
```
4. optionally: set sensors update interval in secs (default - 120)
```yaml
  scan_interval: 600
```
5. optionally: set path to file to save auth information (default - "{homeassistant_config_dir}/tion_auth")
```yaml
  file_path: "/tmp/tion_auth"
```
6. add `tion_email` and `tion_password` to your secrets.yaml
7. restart Home Assistant
## Usage:
After restart you should see your breezer device as `climate.tion_...` and your MagicAir sensors as `sensor.magicair_..`.
Services, allowed to control your breezer:
### climate.set_fan_mode
`fan_mode` parameter defines the speed of the device in format:
- `off`, `0` - turned off
- `1`-`6` - on and manually controlled
- `auto` - automatic breezer control depending on the CO2 level
- `2-4`, `1-3`, `4-6`... etc - automatic control with set speed range
- `2-4:800`, `1-3:900`, `4-6:1000`... etc - automatic control with set speed range and target CO2 level
### climate.set_hvac_mode
`hvac_mode` defines your breezer's heater state:
- `heat` - heater on
- `fan_only` - heater off
### climate.set_temperature
can be used to set target temperature for heater by setting `temperature` parameter
## Troubleshooting
If something went wrong, turn on extended logs for this component and for the `tion` package in your `configuration.yaml`:
```yaml
logger:
  default: warning
  logs:
    custom_components.tion: info
    tion: info
```
