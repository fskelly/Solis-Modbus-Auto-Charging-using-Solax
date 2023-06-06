# Solis-Modbus-Auto-Charging-using-Solax

Code to transfer into your existing HA integration to support Automatic Battery Charging using Solax Modbus on a Solis inverter.  

This code brings together a [hardware integration](https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant) fomulated by @Jumpy07 and software by @Jevburchell to automate your solar PV battery charging.  

A video on the theory involved in Automatic Battery Charging based on Solar Forecasting can be found [here](https://youtu.be/fF0odNXTx48)

Five files exist here - code for your Home Assistant dashboard (full or minimalist variants), code for Template Sensors (config.yaml), code for Automations and definitions for Helpers.  Instructions on where to copy & paste exist within each repo file.

You must install HACS integrations and frontend as specified in the repo files.

Required HA integrations for this to work are [Solax Modbus](https://github.com/wills106/homeassistant-solax-modbus) and [Solcast](https://toolkit.solcast.com.au/register/hobbyist) (configured to your existing system).

## Full Dashboard

Here is what the [Full Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Full).md) looks like:

<img src="Images/HA Full Dashboard.png">

## Minimalist Dashboard

And for those of you who already have your own dashboards setup, you can add the [Minimalist Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Minimalist).md) code to your existing pages.  The only cards in this code pack are the ones which directly control or display paramaters associated with Automatic Battery Charging.  These are the parts which can be added to your existing setup to take advantage of the power of this code without ending up with my full dashboard.  It looks like this:

<img src="Images/HA Minimalist Dashboard.png" width="800">

## Home Assistant Backup Restore

Alternatively, for those of you who are starting fresh with Home Assistant, you may use the [Backup Restore Method](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/HA%20Backup%20Restore.md) to fully configure your system.  This will bring across *all code* contained in this Repo, but YOU WILL LOSE ANY EXISTING DATA ON YOUR HOME ASSISTANT INSTANCE.  Think of this as copying the full Solar Automation setup onto your own machine, which you can then add onto as you wish.  This may be the most suitable option for Home Assistant beginners.


# User Guide
## UI
### Solar Data

<img src="Images/Solar Data.png">

Split into three sections in the dashboard is your live solar data, taken directly from your inverter using your Modbus interface and polled into Home Assistant at whatever rate you set using the Solax Integration.  I find 30 seconds works well and displays nicely in the graphs without using up too much disk space on my instance, and is not too processor-intensive.  Colours can be chosen to suit your needs easily.  Graphs are drawn using Apex Charts.

* Battery - Soc, Daily Charge Amount and Daily Discharge Amount.

* Inverter - Real-time House Load, Daily Consumption, Daily Export and Daily Import. 

* Panels - Combined Output, String 1 and String 2.  (You may want to delete string 2 and the combined output if they are not required on your system).
-----
### Main Controls

This is the heart of the UI to control your Automatic Battery Charging.  The controls here are simple, yet feed data to the charge logic to make a relatively complex decision about whether to charge your batteries.  And if so, by how much.  Each control and display parameter does the following:

<img src="Images/Main Controls 1.png" width="500">

* Restore Defaults (Button) - Returns your Expected Usage Numbers, Target SoC, Boost Charge, Base Load and Charge Current to their default values - which are chosen by you in the Automation ["Solar - Restore Consumption Defaults"](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#solar---restore-consumption-defaults).  My numbers will be different to yours, but may be a good starting point.

* Flux Discharge (Button) - This is for us Octopus Flux customers who may want to discharge the battery to the grid between 16:00 and 19:00 on the peak rate.  This boolean control sets an [automation to set](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#flux---discharge-on) those times, or to [cancel those times](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#flux---discharge-off).  Another Automation also [cuts off the discharge](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#flux---discharge-cutout) if battery SoC drops below 50% during the Flux discharge - edit or delete this if you wish.

* Auto Charge (Button) - Very simply, this turns the [automated battery charging](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#solar---battery-charge-automation) function on or off.  When on, you can sit back and watch it do it's thing.  When off, you can manually control the battery charging through the UI, or revert back to Solis Cloud.  Or climb into the loft.

* Update Times (Button) - Sends the currently set charging times to your inverter via [an automation](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#solar---update-times).  Only really needed if you're in manual mode or if you've changed settings and want to push them to your inverter.  The Solax integration has a button which sends all of the commanded charge times to the inverter at the same time, so a button is required to start that process.
-----
<img src="Images/Main Controls 2.png" width="500">

* Usage Today (Input Number) - Allows you to alter your expected consumption for today.  This is fed into the algorithm to calculate charge.  An [automation](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#solar---expected-consumption-low-state-tracker) also notices if your actual consumption exceeds this number, and increases it to follow in real time.  Also at 23:55, when the ["Solar - Battery Charge Automation"](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#solar---battery-charge-automation) runs, it automatically syncs the two to ensure no anomailies in the charge calculation.

* Usage Tomorrow (Input Number) - Allows you to alter your expected consumption for tomorrow.  This is fed into the algorithm to calculate charge. 

* Target SoC (Input Number) - Allows you to set your Target SoC (in kWh) that your battery will have at the start of the Offpeak period not tomorrow, but the next day. This is fed into the algorithm to calculate charge. 
-----
<img src="Images/Main Controls 3.png" width="500">

* Solcast Rem Today (Sensor) - The remaining expected output of your solar system for the remainder of today.

* Solcast Tomorrow (Sensor) - Solcast Forecast for Tomorrow.

* Usable SoC Now (Template Sensor) - How much charge is left in your battery in kWh.  This is calculated by taking the full capacity of your battery and subtracting your Overdischarge Soc; that leaves the useful amount of capacity before your battery goes into trickle discharge.  The *remainder* of this amount is your 'Usable SoC Now'.

* Usage Left Today (Template Sensor) - Your Usage Today minus your actual Daily House Load.  Essentially how many kWh you have left to burn before midnight.

* Auto Charge (Template Sensor) - Shows the calculated amount of Automatic Battery Charging that the system is planning on adding.  Changes dynamically as input numbers and sensors feed variable data into the algorithm.

* Charge Power (Template Sensor) - The calculated Wattage that the algorithm uses to charge your batteries.  This is worked out using the Battry Config section below, and/or manually controlled using the "Charge Current" Input Number below.  Calculated at 55v - you may alter this in configuration.yaml if you wish.

* Total Charge Time (Template Sensor) - Calculated amount of charge time.  Shows Auto charge time in Auto mode or your own configured charge time in Manual mode.

* Charge Start (Template Sensor) - The time battery charging will start.  This is manually controlled from the Solax Integration, as you might be on a different Tariff which starts at something other than 2am.  Note that the minutes will only show 2 digits if it shows 10 or above; just a quirk of making this work with Solax.

* Charge End (Template Sensor) - The charge start time + the total charge time = the charge end time.
-----
<img src="Images/Main Controls 4.png" width="500">

* Boost Charge (Input Number) - No matter what auto charge or manual charge you have set, boost charge simply adds an amount on to it.  So if auto charge calculates it wants to add 3kWh and you want 4, then add 1 kWh of charge from the Boost Charge control.  Easy.

* Base Load (Input Number) - The amount of base load / background load your house uses.  Think when you're all asleep and everything is on standby.  Might seem frivolous, but it's an important part of calculating charge as accurately as possible.

* Charge Current (Input Number) - You can manually control this, but it is set automatically by Battery Config section below.  It directly controls the rate at which your batteries will charge.

-----
### Auto Charge Status

<img src="Images/Auto Charge Status.png" width="500">

* Auto Charge Status (Template Sensor) - Uses ifelse statement to show either "Charge Scheduled" or "Not Required".

* SoC at Start of Offpeak Tonight 2am (Template Sensor) - Shows the Battery SoC at the beginning of tonight's Offpeak period.  

* SoC at End of Offpeak Tonight 5am (Template Sensor) - Shows the Battery SoC at the end of tonight's Offpeak period.  

* SoC at Start of Offpeak Tomorrow 2am (Template Sensor) - Shows the Battery SoC at the beginning of tomorrow night's Offpeak period.  

-----
### Inverter Stats & Future Solcast Data

<img src="Images/Inverter Stats 1.png" width="500">

* Gauges to show live inverter stats:
  * Today's Yield (kWh)
  * Battery Charge Power (W)
  * Battery Discharge Power (W)
  * Import Export Power (W)
  * Inverter Temperature (C)

* Cooling Fans Button - Note that this will be unconfigured when you import this code into your system.  You will need to set this up to control your fans (or delete if you don't have any)

-----

<img src="Images/Inverter Stats 2.png" width="500">

* Solcast Day 3/4/5/6 (Template Sensors) - Forecast data for days 3 - 6 in the future.  

* API Polled (Sensor) - Shows the last time the Solcast servers were polled for data.

* API Used (Sensor) - Number of API calls that you have made to the Solcast servers today.

* Flux Discharge Start (Number) - The time in 24h format when the Flux Battery Discharge is set to begin.

* Flux Discharge End (Number) - The time in 24h format when the Flux Battery Discharge is set to finish.  This is controlled by two [automations](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#flux---discharge-on) which alter the end time from 16:00 to 19:00.

-----
### Battery Config

This is a very important section and contributes a key element to the algorithm.  As Solar customers with differing installations, we have different size battery packs and have alterations in our settings depending on how deep we dare discharge our batteries.  These 3 elements have a direct impact on our useful amount of battery storage in kWh, and thus how fast we need to charge those batteries in a given charge window.  

As an example, with my 10kWh battery and a Force Charge SoC set at 10%, the maximum charge that I could apply to my batteries in an Off-Peak charge window would be 9kWh.  Given the charge window is 3 hours long on Octopus Flux, I need to charge 3kWh per hour to achieve a full charge - or 3000W charge power for those 3 hours.  The inverter needs to know that as a charge current, and at 55V a charge current of 55A gives me 3,025W which is sufficient to charge my batteries.  My neighbour down the street with a 15kWh battery and Force Charge SoC at 10% will need to charge at 4,500W or 82A, and so on.  These numbers can be "set-and-forget" - in fact you may even want to set them and remove from your dashboard altogether.  

-----

<img src="Images/Battery Config.png" width="500">

* Battery Capacity (Number Input) - The full size of your battery storage system.

* Overdischarge SoC (Number Input) - Match the percentage that you have set this to in your inverter settings.  This is the % SoC below which your inverter will go into trickle discharge mode, and you will be importing electricity from the grid until your solar panels produce enough out put to charge your batteries again.

* Forcecharge SoC (Number Input) - Match the percentage that you have set this to in your inverter settings.  This is the % SoC at which your battery Force Charges itself from the grid no matter what is happening.  This is a functionality preservation system built into pretty much all modern battery systems, and prevents your batteries from going into a deep discharge state.  Reduce this setting at your peril!!

* Useful System Capacity (Template Sensor) - System Capacity in kWh from 100% to your Overdischarge SoC.  

* System Capacity above Forcecharge (Template Sensor) - System Capacity in kWh from 100% to your Forcecharge SoC. 

* Calculated Charge Current (Template Sensor) - using the above variables, a charge current is calculated and displayed here.  An [automation](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Automations.md#solar---charge-current-settings) "Solar - Charge Current Settings" also runs in the background so that this figure is updated and sent to the inverter in real-time whenever any of the Battery Config settings are altered.

-----

<img src="Images/Inverter Stats 3.png" width="500">

* Battery Heat Button - Note that this will be unconfigured when you import this code into your system.  You will need to set this up to control your battery heater (or delete if you don't have one).

* OAT (Sensor) - Outside Air Temperature (useful for automating battery heat if you don't have a temperature sensor on the batteries themselves).

* Chrg Limit (Sensor) - Battery Charge Limit from your BMS via Solax.

* Disch Limit (Sensor) - Battery Discharge Limit from your BMS via Solax.

-----

### Weather Data

<img src="Images/Weather Data.png" width="500">

* Openweathermap card - classic weather widget.  Remember to set up your own API on their website.
* Hourly Weather Card - shows basic pictoral weather over the next 24 hours.
* Horizon Card - visual representation of the Azimuth & Elevation of the sun in the sky.

-----

# Charge Logic

![Slide53](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/assets/128035411/ca7ad0ef-5a44-4dbf-8d79-15e8a1e531dd)
![Slide54](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/assets/128035411/42a2e100-3845-4162-82dd-acb5cb859be6)


Feedback welcomed in the [Discussions Section](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/discussions)
