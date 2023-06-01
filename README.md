# Solis-Modbus-Auto-Charging-using-Solax

Experimental code to transfer into your existing HA integration to support Automatic Battery Charging using Solax Modbus on a Solis inverter.  

This code brings together a hardware integration fomulated by @Jumpy07 and software by @Jevburchell to automate your solar PV battery charging.  

https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant/blob/main/README.md?fbclid=IwAR1A36MUN4-2RdS32RacsXdW2iAC5l51imUdrd5vLuUG15JsJTYAK58Y6Rs

Four files exist here - code for your Home Assistant dashboard, code for Template Sensors (config.yaml), code for Automations and definitions for Helpers.  Instructions on where to copy & paste exist within each repo file.

You must install HACS integrations and frontend as specified in the repo files.

Required HA integrations for this to work are Solax Modbus and Solcast (configured to your existing system).

Here is what the full [Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard) will look like (nb some graph data missing in this screenshot due coding work):

![HA Export Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/assets/128035411/0e284912-03a1-4aca-8604-2e643d969eb3)

And for those of you who already have your own dashboards setup, you can add the [Dashboard (Minimalist](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Dashboard%20(Minimalist)) code to your existing pages.  It looks like this:

![HA Minimalist Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/assets/128035411/7388e7b2-9a84-4611-a3ab-7f69d628d7d9)

Alternatively, for those of you who are starting fresh with Home Assistant, you may simply install [this](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/HA%20Solis%20Solax%20Automation%20Backup%201.6.23.tar) Backup file to your system.  This will bring across all code contained in this Repo, but YOU WILL LOSE ANY EXISTING DATA ON YOUR HOME ASSISTANT INSTANCE.  

INSTALLATION:

1. Download the above .tar file (click Raw in the linked page if it doesn't auto download)
2. In Home Assistant, go to Settings > System > Backups
3. Hit the three dots top right and choose "Upload Backup"
4. Navigate to the .tar file and upload it
5. The backup file will now appear in your HA list.  Double click on it, choose "full backup", then hit "Restore".  The process will install all code.
6. You will need to alter a couple of settings to suit your own installation.  
    - Solcast API Key
    - Openweathermap API Key
    - Solax integration settings (you must enter the correct IP address of your Modbus device which connects to your inverter)
    - Battery Heat and Cooling Fans buttons will need to be linked to your own devices, if you have them.

HA Credentials: 
* user: default_user
* password: abcde12345
* Please change these...
    
Feedback welcomed!
