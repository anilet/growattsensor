# Growatt Solar Invertor Sensor for HA
I have hacked together a custom sensor for my Growatt Inverter using the client library from https://github.com/Sjord/growatt_api_client. This is an adaptation of PVOutput Sensor.
The sensor outputs Current energy output in kW and you can get the Day’s Total Output using a template sensor.
# Installation
Copy the growatt folder to your /config/custom_folder and add
```
sensor:
  - platform: growatt
    username: 'username_for_growatt_server'
    password: 'pwd_for_growatt_server'

  - platform: template
  sensors:
      energy_generation:
        value_template: '{% if is_state_attr("sensor.growatt", "power_generation", "NaN") %}0{% else %}{{ "%0.2f"|format(states.sensor.growatt.attributes.power_generation|float) }}{% endif %}'
        friendly_name: 'Generated'
        unit_of_measurement: 'kWh'
 ```
 to your configuration.yaml file
