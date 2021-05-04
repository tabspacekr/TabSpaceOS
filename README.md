# TabSpaceOS
Armbian Based TabSpace Customized OS


# Prework Code

1. Armbian 21.02.3 for OrangePi Zero 설치

   https://www.armbian.com/orange-pi-zero/

   https://redirect.armbian.com/orangepizero/Buster_current

   Armbian Login Information
   
   ID : root
   PW : tabspace
   
2. OLED Support

   SDD1306 Package Install
   
   Add Cron Job on Reboot

3. HOSTNAME Autochange

   
   Add Cron Job on Reboot
   
4. TimeZone Change

   Asia/Seoul


5. Docker CE Install


6. HomeAssistant Supervisor Install

   HomeAssistant Login Information
   
   ID : admin
   PW : tabspace

7. HomeAssistant Add-On Install 

7-1. File Editor (5.3.0)
    
    7-1-1. Enable WatchDog
    
    7-1-2. Enable Show Sidebar

7-2. Zigbee2MQTT

    7-2-1. Add Repository ( https://github.com/danielwelch/hassio-zigbee2mqtt ) and Install
    
    7-2-2. Change Zigbee Channel to 25 on Z2M Configuration
    
    7-2-3. Enable WatchDog
    
    7-2-4. Enable Show Sidebar

7-3. MariaDB (2.3.0)

    7-3-1. Setting Password is 'tabspace'
    
<pre>
databases:
  - homeassistant
logins:
  - username: homeassistant
    password: tabspace
rights:
  - username: homeassistant
    database: homeassistant
</pre>
    
    7-3-2. Edit Configuration to use HA Recorder setting.

7-4. Mosquitto broker (5.1.1)

    7-4-1. Install Mosquitto Broker
    
    7-4-2. Add login credential on HomeAssistant User
    
    ID : mqtt
    PW : tabspace

8. HomeAssistant Configuration Setting

  8-1. Include Dummy files
  
  8-2. Exclude something laggy settings
  

