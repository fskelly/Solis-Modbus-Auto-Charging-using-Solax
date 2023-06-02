# Solis-Modbus-Auto-Charging-using-Solax

Experimental code to transfer into your existing HA integration to support Automatic Battery Charging using Solax Modbus on a Solis inverter.  

This code brings together a [hardware integration](https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant) fomulated by @Jumpy07 and software by @Jevburchell to automate your solar PV battery charging.  

A video on the theory involved in Automatic Battery Charging based on Solar Forecasting can be found [here](https://youtu.be/fF0odNXTx48)

Five files exist here - code for your Home Assistant dashboard (full or minimalist variants), code for Template Sensors (config.yaml), code for Automations and definitions for Helpers.  Instructions on where to copy & paste exist within each repo file.

You must install HACS integrations and frontend as specified in the repo files.

Required HA integrations for this to work are [Solax Modbus](https://github.com/wills106/homeassistant-solax-modbus) and [Solcast](https://toolkit.solcast.com.au/register/hobbyist) (configured to your existing system).

##Full Dashboard

Here is what the full [Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Full).md) will look like:

<img src="Images/HA Full Dashboard.png">

##Minimalist Dashboard

And for those of you who already have your own dashboards setup, you can add the [Dashboard (Minimalist)](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Minimalist).md) code to your existing pages.  The only cards in this code pack are the ones which directly control or display paramaters associated with Automatic Battery Charging.  These are the parts which can be added to your existing setup to take advantage of the power of this code without ending up with my full dashboard.  It looks like this:

<img src="Images/HA Minimalist Dashboard.png" width="800">

Alternatively, for those of you who are starting fresh with Home Assistant, you may use the [Backup Restore Method](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/HA%20Backup%20Restore.md) to fully configure your system.  This will bring across *all code* contained in this Repo, but YOU WILL LOSE ANY EXISTING DATA ON YOUR HOME ASSISTANT INSTANCE.  Think of this as copying the full Solar Automation setup onto your own machine, which you can then add onto as you wish.  This may be the most suitable option for Home Assistant beginners.

Feedback welcomed!
