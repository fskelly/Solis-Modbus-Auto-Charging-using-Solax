# Installation

1. Download the below .tar file (click Raw in the linked page if it doesn't auto download)
2. In Home Assistant, go to Settings > System > Backups
3. Hit the three dots top right and choose "Upload Backup"
4. Navigate to the .tar file and upload it
5. The backup file will now appear in your HA list. Double click on it, choose "full backup", then hit "Restore". The process will install all code.
6. You will need to alter a couple of settings to suit your own installation.
* Solcast API Key
* Openweathermap API Key
* Solax Integration settings (you must enter the correct IP address of your Modbus device which connects to your inverter)
* Battery Heat and Cooling Fans buttons will need to be linked to your own devices, if you have them.

HA Credentials:

* user: default_user
* password: abcde12345
* Please change these...

## .tar File

[Download Here](https://github.com/jevburchell/Solis-Modbus-Auto-Charging-using-Solax/blob/main/Images/HA%20Solis%20Solax%20Automation%20Backup%201.6.23.tar)
