You must create the following Helpers in HA.  This is more of a manual process as there is no way to directly copy the code across, but should take no more than 5 minutes.

# Installation

1. Click Settings > Devices & Services > Helpers > + "Create Helper"

2. Use the 3rd line of each of the items below to choose helpers (number, toggle or button).  Name them exactly the same as specified here.  Your max/min and step sizes will be dependant on your own needs, but my numbers here should serve as a suitable starting point.


### Base Load
* input_number.base_load
* Number
* Minimum Value: 0
* Maximum Value: 1
* Step Size: 0.01
* Unit of Measurement: kW

### Battery Capacity
* input_number.battery_capacity
* Number
* Minimum Value: 1
* Maximum Value: 50
* Step Size: 1
* Unit of Measurement: kWh

### Battery Heat
* input_button.battery_heat
* Button

### Boost Charge
* input_number.boost_charge
* Number
* Minimum Value: 0
* Maximum Value: 15
* Step Size: 1
* Unit of Measurement: kWh

### Cooling Fans
* input_button.cooling_fans
* Button

### Expected Consumption
* input_number.expected_consumption
* Number
* Minimum Value: 0
* Maximum Value: 50
* Step Size: 0.5
* Unit of Measurement: kWh

### Expected Consumption Tomorrow
* input_number.expected_consumption_tomorrow
* Number
* Minimum Value: 0
* Maximum Value: 50
* Step Size: 0.5
* Unit of Measurement: kWh

### Flux Discharge
* input_boolean.flux_discharge
* Toggle

### Force Charge SoC
* input_number.force_charge_soc
* Number
* Minimum Value: 0
* Maximum Value: 50
* Step Size: 1
* Unit of Measurement: %

### Overdischarge SoC
* input_number.overdischarge_soc
* Number
* Minimum Value: 0
* Maximum Value: 50
* Step Size: 1
* Unit of Measurement: %

### Reset Consumption Defaults
* input_button.reset_consumption_defaults
* Button

### Target Usable SoC
* input_number.target_usable_soc
* Number
* Minimum Value: 0
* Maximum Value: 20
* Step Size: 1
* Unit of Measurement: kWh
