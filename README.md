# Solis-Modbus-Auto-Charging-using-Solax

Experimental code to transfer into your existing HA integration to support Automatic Battery Charging using Solax Modbus on a Solis inverter.  

This code brings together a [hardware integration](https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant) fomulated by @Jumpy07 and software by @Jevburchell to automate your solar PV battery charging.  

A video on the theory involved in Automatic Battery Charging based on Solar Forecasting can be found here: https://youtu.be/fF0odNXTx48

Five files exist here - code for your Home Assistant dashboard (full or minimalist variants), code for Template Sensors (config.yaml), code for Automations and definitions for Helpers.  Instructions on where to copy & paste exist within each repo file.

You must install HACS integrations and frontend as specified in the repo files.

Required HA integrations for this to work are [Solax Modbus](https://github.com/wills106/homeassistant-solax-modbus) and [Solcast](https://toolkit.solcast.com.au/register/hobbyist) (configured to your existing system).

Here is what the full [Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Full).md) will look like:

![HA Export Dashboard2](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/assets/128035411/451abbf0-af92-4203-b706-1d481615832e)

And for those of you who already have your own dashboards setup, you can add the [Dashboard (Minimalist)](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Minimalist)) code to your existing pages.  The only cards in this code pack are the ones which directly control or display paramaters associated with Automatic Battery Charging.  These are the parts which can be added to your existing setup to take advantage of the power of this code without ending up with my full dashboard.  It looks like this:

![HA Minimalist Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Minimalist).md)

Alternatively, for those of you who are starting fresh with Home Assistant, you may simply install [this](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/HA%20Solis%20Solax%20Automation%20Backup%201.6.23.tar) Backup file to your system.  This will bring across all code contained in this Repo, but YOU WILL LOSE ANY EXISTING DATA ON YOUR HOME ASSISTANT INSTANCE.  

INSTALLATION:

1. Download the above .tar file (click Raw in the linked page if it doesn't auto download)
2. In Home Assistant, go to Settings > System > Backups
3. Hit the three dots top right and choose "Upload Backup"
4. Navigate to the .tar file and upload it
5. The backup file will now appear in your HA list.  Double click on it, choose "full backup", then hit "Restore".  The process will install all code.
6. You will need to alter a couple of settings to suit your own installation.  
    - [Solcast](https://toolkit.solcast.com.au/register/hobbyist) API Key
    - [Openweathermap](https://home.openweathermap.org/users/sign_up) API Key
    - [Solax Integration](https://github.com/wills106/homeassistant-solax-modbus) settings (you must enter the correct IP address of your Modbus device which connects to your inverter)
    - Battery Heat and Cooling Fans buttons will need to be linked to your own devices, if you have them.

HA Credentials: 
* user: default_user
* password: abcde12345
* Please change these...
    
Feedback welcomed!
