# ESPHome Heating Controller
ESPHome Yaml for heating and hot water relay outputs with local fallback if Home Assistant is disconnected.

Designed for the attached ESP Relay board: https://www.aliexpress.com/item/1005006043227197.html with DHT11 Temperature sensor attached to pin 4. https://www.aliexpress.com/item/1005009268179353.html
I use this in conjunction with the Generic Thermostat Home Assistant Integration and Zigbee temperature sensors (https://www.aliexpress.com/item/1005007755890938.html)

The Home Assistant Instance has full control of the heating and hot water outputs unless the API is disconnected for 1 hour, at this point the ESPHome reverts to a preset setpoint and controls on the local temperature sensor. 
This ensures a failsafe mode if your Home Assistant or Network etc has any issues. 

# How to Use:
1. Install ESPHome as per: https://esphome.io/guides/getting_started_hassio/
2. In ESPHome Press + New Device
3. On the Create Configuration Menu Press > New Device Setup
4. Enter a device name e.g "Heating Controller"
5. Connect to the ESP32: https://esphome.io/guides/physical_device_connection/
6. Once Initial configuration is completed press "edit" to edit the devices YAML
7. Copy the heating_controller.yaml into your device configuration.
8. Replace the API encryipton key with the API key generated, can be found in the device menu > Show API Key
9. Replace the OTA and Wi-Fi AP passwords for a password of your choice.
10. Install the heating_controller.yaml
11. Once installed and rebooted go to Settings > Devices & Services, Home assistant should automatically see the new ESP Heating Controller, add the integration.
12. If it is not automatically recognised, find the IP address of the ESP from your router and manually add the integration "+ Add Integration" > ESPHome
13. The device will now be added and the Heating Output and Hot Water Output entites available to control from Home Assistant.

## Temperature Sensors
Use temperature sensors of your choice and add to Home assistant as per the device type. I have used these Zigbee Temperature Sensors: (https://www.aliexpress.com/item/1005007755890938.html)
In my use case I have multiple sensors around the house and I have averaged these using the Average Helper to control one Generic Thermostat but you could have individual Thermostats for each sensor if required. 
### How to Setup an average temperature sensor:
1. Go to Settings > Devices & Services > Helpers > "+ Create Helper"
2. Select "Combine the state of several sensors"
3. Give the sensor a name e.g. "Average House Temperature"
4. Select the temperature sensor entities you wish to average
5. Select Statistic characteristic > Arithmetic mean
   
## Generic Thermostat
Configure the Generic Thermostat to control the Heating Output
https://www.home-assistant.io/integrations/generic_thermostat/
If you are using 1 temperature sensor the thermostat can be configured in the UI, if you are using an averaged temperature sensor as shown above this must be configured in the yaml.
### UI Configuration: 
1. Go to Settings > Devices & Services > Helpers > "+ Create Helper"
2. Select "Generic Thermostat"
3. Give it a Name
4. Select the Temperature Sensor you wish to use.
5. Select the "Actuator Switch": Heating Controller > Heating Output

### Yaml Configuration:
Add the included climate.yaml to your configuration.yaml

## Scheduler
I have used the brilliant Scheduler Component (https://github.com/nielsfaber/scheduler-component) to add custom temperature schedules for the generic thermostat and hot water schedules.


