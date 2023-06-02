# Installation

Paste the following directly into your HA overview.

1. In overview (or your main HA view whatever that is called), click the 3 dots top right and "edit dashboard".

2. Click the 3 dots top right again and choose "raw configuration editor"

3. After "views:" on line 1, click and hit return, then paste the code below into the new line

4. Hit save, then X (top left) to exit

5. Install the following HACS Frontend:
	* [Horizon Card](http://homeassistant.local:8123/hacs/repository/614083491)
	* [Apexcharts-card](http://homeassistant.local:8123/hacs/repository/331701152)
	* [Mushroom Themes](http://homeassistant.local:8123/hacs/repository/456201687)
	* [Mushroom](http://homeassistant.local:8123/hacs/repository/444350375)
	* [Hourly Weather Card](http://homeassistant.local:8123/hacs/repository/499270202)

6. You must have "Solcast PV Solar" and "Solax Modbus" HACS Integrations installed and configured to your own system
	* [Solcast](https://github.com/oziee/ha-solcast-solar) note: I find that hitting the code button and downloading the sip has more success with install.
	* [Solax Modbus](https://github.com/wills106/homeassistant-solax-modbus)

7. Install Openweathermap integration from devices & services > add integration

Note: Solcast and Openweathermap require you to set up and use your own API Keys.  You can sign up for a free account and get your API key at their websites
https://toolkit.solcast.com.au/register/hobbyist
https://home.openweathermap.org/users/sign_up


## Dashboard (Full) Code
```
  - theme: minimalist-mobile
    title: Solar
    path: solar
    icon: mdi:white-balance-sunny
    badges: []
    cards:
      - square: false
        columns: 1
        type: grid
        title: Battery
        cards:
          - type: custom:apexcharts-card
            graph_span: 24h
            yaxis:
              - id: first
                min: 10
                max: 100
                decimals: 0
                apex_config:
                  tickAmount: 6
              - id: second
                min: 0
                max: 12
                decimals: 1
                opposite: true
                apex_config:
                  tickAmount: 6
            chart_type: line
            span:
              start: day
            header:
              show: true
              show_states: true
              colorize_states: true
            experimental:
              color_threshold: true
            series:
              - entity: sensor.solax_battery_soc
                yaxis_id: first
                name: SoC
                color: yellow
                stroke_width: 1
                extend_to: now
              - entity: sensor.solax_battery_charge_today
                yaxis_id: second
                name: Charged
                color: green
                stroke_width: 1
                extend_to: now
              - entity: sensor.solax_battery_discharge_today
                yaxis_id: second
                name: Discharged
                color: blue
                stroke_width: 1
                extend_to: now
          - square: false
            type: grid
            cards:
              - show_name: true
                show_icon: true
                type: button
                tap_action:
                  action: toggle
                entity: input_button.reset_consumption_defaults
                name: Restore Defaults
                show_state: false
                icon_height: 20px
              - show_name: true
                show_icon: true
                type: button
                tap_action:
                  action: toggle
                entity: input_boolean.flux_discharge
                icon_height: 20px
                name: Flux Discharge
                show_state: true
              - show_name: true
                show_icon: true
                type: button
                tap_action:
                  action: toggle
                entity: automation.solar_battery_charge_automation
                show_state: true
                icon: mdi:battery-charging-40
                icon_height: 20px
                name: Auto Charge
              - show_name: true
                show_icon: true
                type: button
                entity: automation.solar_update_times
                icon_height: 20px
                name: Update Times
                show_state: false
                tap_action:
                  action: call-service
                  service: automation.trigger
                  target:
                    entity_id: automation.solar_update_times
                  data:
                    skip_condition: false
                icon: mdi:clock-time-eight-outline
            columns: 4
          - square: false
            type: grid
            cards:
              - type: custom:mushroom-number-card
                entity: input_number.expected_consumption
                fill_container: false
                icon_type: none
                name: Usage Today
                display_mode: buttons
                secondary_info: none
              - type: custom:mushroom-number-card
                entity: input_number.expected_consumption_tomorrow
                name: Usage Tomorrow
                icon_type: none
                fill_container: false
                display_mode: buttons
                secondary_info: none
              - type: custom:mushroom-number-card
                entity: input_number.target_usable_soc
                display_mode: buttons
                icon_type: none
                fill_container: false
                name: Target SoC
                primary_info: name
                secondary_info: none
            columns: 3
          - square: false
            type: grid
            cards:
              - show_name: true
                show_icon: false
                show_state: true
                type: glance
                entities:
                  - entity: sensor.forecast_remaining_today
                    name: Solcast Rem Today
                  - entity: sensor.forecast_tomorrow
                    name: Solcast Tomorrow
                  - entity: sensor.soc_usable_kwh
                    name: Usable SoC Now
                  - entity: sensor.remaining_consumption_today
                    name: Usage Left Today
                  - entity: sensor.soc_required_charge
                    name: Auto Charge
                  - entity: sensor.battery_charge_power
                    name: Charge Power
                  - entity: sensor.soc_charge_time_hhmm
                    name: Total Charge Time
                  - entity: sensor.charge_start_time
                    name: Charge Start
                  - entity: sensor.soc_charge_end_time_hhmm
                    name: Charge End
                columns: 3
            columns: 1
          - square: false
            type: grid
            cards:
              - type: custom:mushroom-number-card
                entity: input_number.boost_charge
                icon_type: none
                layout: vertical
                display_mode: buttons
              - type: custom:mushroom-number-card
                entity: input_number.base_load
                layout: vertical
                fill_container: false
                icon_type: none
                display_mode: slider
                name: Base Load
              - type: custom:mushroom-number-card
                entity: number.solax_timed_charge_current
                icon_type: none
                name: Charge Current
                fill_container: false
            columns: 3
          - type: entities
            entities:
              - entity: sensor.auto_charge_scheduled
                name: Auto Charge Status
              - entity: sensor.soc_at_start_of_offpeak_tonight
                name: SoC at Start of Offpeak Tonight (2am)
              - entity: sensor.soc_at_end_of_offpeak_tonight_with_charge
                name: Soc at End of Offpeak Tonight (5am)
              - entity: sensor.soc_at_start_of_offpeak_tomorrow_display
                name: Soc at Start of Offpeak Tomorrow (2am +1)
            show_header_toggle: true
      - square: false
        columns: 1
        type: grid
        title: Inverter
        cards:
          - type: custom:apexcharts-card
            graph_span: 24h
            span:
              start: day
            yaxis:
              - id: first
                min: 0
                max: 5000
                decimals: 0
                apex_config:
                  tickAmount: 5
              - id: second
                min: 0
                max: 20
                decimals: 1
                opposite: true
                apex_config:
                  tickAmount: 5
            chart_type: line
            header:
              show: true
              show_states: true
              colorize_states: true
            series:
              - entity: sensor.solax_house_load
                yaxis_id: first
                name: House Load
                stroke_width: 1
                color: white
                extend_to: now
              - entity: sensor.solax_house_load_today
                yaxis_id: second
                name: Consumption
                stroke_width: 1
                color: orange
                extend_to: now
              - entity: sensor.solax_grid_export_today
                yaxis_id: second
                name: Export
                stroke_width: 1
                color: green
                extend_to: now
              - entity: sensor.solax_grid_import_today
                yaxis_id: second
                name: Import
                stroke_width: 1
                color: red
                extend_to: now
          - square: false
            type: grid
            cards:
              - type: gauge
                needle: true
                severity:
                  green: 12
                  yellow: 6
                  red: 0
                entity: sensor.solax_power_generation_today
                name: Today’s Yield
                max: 40
              - type: gauge
                entity: sensor.solax_battery_input_energy
                name: Batt Charge
                needle: false
                min: 0
                max: 4000
                severity:
                  green: 0
                  yellow: 4000
                  red: -4000
              - type: gauge
                entity: sensor.solax_battery_output_energy
                name: Batt Discharge
                min: 0
                max: 4000
                needle: false
              - type: gauge
                name: Import/Export
                min: -4000
                max: 4000
                needle: true
                severity:
                  green: 0
                  yellow: 4000
                  red: -4000
                entity: sensor.solax_meter_active_power
              - type: gauge
                entity: sensor.solax_inverter_temperature
                severity:
                  green: 0
                  yellow: 50
                  red: 80
                name: Inverter Temp
              - show_name: true
                show_icon: true
                type: button
                tap_action:
                  action: toggle
                entity: input_button.cooling_fans
                show_state: false
                icon_height: 40px
            columns: 3
          - show_name: true
            show_icon: false
            show_state: true
            type: glance
            entities:
              - entity: sensor.forecast_d3
                name: Solcast Day 3
              - entity: sensor.forecast_d4
                name: Solcast Day 4
              - entity: sensor.forecast_d5
                name: Solcast Day 5
              - entity: sensor.forecast_d6
                name: Solcast Day 6
              - entity: sensor.api_last_polled
                name: API Polled
              - entity: sensor.api_used
                name: API Used
              - entity: number.solax_timed_discharge_start_hours
                name: Flux disch Start
              - entity: number.solax_timed_discharge_end_hours
                name: Flux disch End
            columns: 4
          - square: false
            type: grid
            cards:
              - show_name: true
                show_icon: true
                type: button
                tap_action:
                  action: toggle
                entity: input_button.battery_heat
                icon_height: 20px
              - type: custom:mushroom-entity-card
                entity: sensor.openweathermap_temperature
                icon_type: none
                name: OAT
                layout: vertical
                fill_container: true
              - type: custom:mushroom-entity-card
                entity: sensor.solax_bms_battery_charge_limit
                icon_type: none
                name: Chrg Limit
                fill_container: true
                layout: vertical
              - type: custom:mushroom-entity-card
                entity: sensor.solax_bms_battery_discharge_limit
                name: Disch Limit
                icon_type: none
                fill_container: true
                layout: vertical
            columns: 4
          - square: false
            type: grid
            cards:
              - type: custom:mushroom-number-card
                entity: input_number.battery_capacity
                display_mode: buttons
                fill_container: false
                icon_type: none
              - type: custom:mushroom-number-card
                entity: input_number.overdischarge_soc
                display_mode: buttons
                icon_type: none
                name: Overdischarge SoC
              - type: custom:mushroom-number-card
                entity: input_number.force_charge_soc
                display_mode: buttons
                icon_type: none
                name: Forcecharge SoC
            columns: 3
          - type: entities
            entities:
              - entity: sensor.soc_total_usable
                name: Useful System Capacity
              - entity: sensor.soc_usableforcecharge
                name: System Capacity Above Forcecharge
              - entity: sensor.calculated_charge_current
                name: Calculated Charge Current
      - square: false
        columns: 1
        type: grid
        title: Panels
        cards:
          - type: custom:apexcharts-card
            graph_span: 21h
            span:
              start: day
              offset: +3h
            chart_type: line
            header:
              show: true
              show_states: true
              colorize_states: true
            series:
              - entity: sensor.solax_pv_total_power
                name: Combined Output
                stroke_width: 1
                color: yellow
                extend_to: now
              - entity: sensor.string_1_output
                name: String 1
                stroke_width: 1
                color: cyan
                extend_to: now
              - entity: sensor.string_2_output
                name: String 2
                stroke_width: 1
                color: magenta
                extend_to: now
      - square: false
        type: grid
        cards:
          - show_current: true
            show_forecast: true
            type: weather-forecast
            entity: weather.openweathermap
            name: Home
          - type: custom:hourly-weather
            entity: weather.openweathermap
            num_segments: '10'
            icons: true
            show_precipitation_probability: false
            name: null
          - type: custom:horizon-card
            fields:
              azimuth: true
              elevation: true
              dawn: true
              dusk: true
              noon: true
        columns: 1
```
