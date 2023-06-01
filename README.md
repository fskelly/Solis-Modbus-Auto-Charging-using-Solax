# Solis-Modbus-Auto-Charging-using-Solax

Experimental code to transfer into your existing HA integration to support Automatic Battery Charging using Solax Modbus on a Solis inverter.  

This code brings together a hardware integration fomulated by @Jumpy07 and software by @Jevburchell to automate your solar PV battery charging.  

https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant/blob/main/README.md?fbclid=IwAR1A36MUN4-2RdS32RacsXdW2iAC5l51imUdrd5vLuUG15JsJTYAK58Y6Rs

Four files exist here - code for your Home Assistant dashboard, code for Template Sensors (config.yaml), code for Automations and definitions for Helpers.  Instructions on where to copy & paste exist within each repo file.

You must install HACS integrations and frontend as specified in the repo files.

Required HA integrations for this to work are Solax Modbus and Solcast (configured to your existing system).

Feedback welcomed.

Here is what the full Dashboard will look like (nb some graph data missing due to coding changes):

![HA Export Dashboard](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/assets/128035411/0e284912-03a1-4aca-8604-2e643d969eb3)


Alternatively, for those of you who are starting fresh with Home Assistant, you may simply install [this](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/HA%20Solis%20Solax%20Automation%20Backup%201.6.23.tar) Backup file to your system.  This will bring across all code contained in this Repo, but YOU WILL LOSE ANY EXISTING DATA ON YOUR HOME ASSISTANT INSTANCE.  

