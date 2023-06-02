# Solis-Modbus-Auto-Charging-using-Solax

Experimental code to transfer into your existing HA integration to support Automatic Battery Charging using Solax Modbus on a Solis inverter.  

This code brings together a [hardware integration](https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant) fomulated by @Jumpy07 and software by @Jevburchell to automate your solar PV battery charging.  

A video on the theory involved in Automatic Battery Charging based on Solar Forecasting can be found [here](https://youtu.be/fF0odNXTx48)

Five files exist here - code for your Home Assistant dashboard (full or minimalist variants), code for Template Sensors (config.yaml), code for Automations and definitions for Helpers.  Instructions on where to copy & paste exist within each repo file.

You must install HACS integrations and frontend as specified in the repo files.

Required HA integrations for this to work are [Solax Modbus](https://github.com/wills106/homeassistant-solax-modbus) and [Solcast](https://toolkit.solcast.com.au/register/hobbyist) (configured to your existing system).

## Full Dashboard

Here is what the full [Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Full).md) will look like:

<img src="Images/HA Full Dashboard.png">

## Minimalist Dashboard

And for those of you who already have your own dashboards setup, you can add the [Dashboard (Minimalist)](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Minimalist).md) code to your existing pages.  The only cards in this code pack are the ones which directly control or display paramaters associated with Automatic Battery Charging.  These are the parts which can be added to your existing setup to take advantage of the power of this code without ending up with my full dashboard.  It looks like this:

<img src="Images/HA Minimalist Dashboard.png" width="800">

## Home Assistant Backup Restore

Alternatively, for those of you who are starting fresh with Home Assistant, you may use the [Backup Restore Method](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/HA%20Backup%20Restore.md) to fully configure your system.  This will bring across *all code* contained in this Repo, but YOU WILL LOSE ANY EXISTING DATA ON YOUR HOME ASSISTANT INSTANCE.  Think of this as copying the full Solar Automation setup onto your own machine, which you can then add onto as you wish.  This may be the most suitable option for Home Assistant beginners.


# User Guide

### Solar Data

<img src="Images/Solar Data.png">

Split into three sections in the dashboard is your live solar data, taken directly from your inverter using your Modbus interface and polled into Home Assistant at whatever rate you set using the Solax Integration.  I find 30 seconds works well and displays nicely in the graphs without using up too much disk space on my instance, and is not too processor-intensive.  Colours can be chosen to suit your needs easily.  Graphs are drawn using Apex Charts.
* Battery - Soc, Daily Charge Amount and Daily Discharge Amount.
* Inverter - Real-time House Load, Daily Consumption, Daily Export and Daily Import. 
* Panels - Combined Output, String 1 and String 2.  (You may delete a string if it is not required on your system).

### Main Controls

Under Construction
<img src="" width="800">

### Auto Charge Status

Under Construction
<img src="Images/Auto Charge Status.png" width="800">

### Inverter Stats & Future Solcast Data

Under Construction
<img src="Images/Inverter Stats.png" width="800">

### Battery Config

Under Construction
<img src="Images/Battery Config.png" width="800">

### Weather Data

Under Construction
<img src="Images/Weather Data.png" width="800">



Feedback welcomed in the [Discussions Section](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/discussions)
