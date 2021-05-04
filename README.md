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

7-1. Zigbee2MQTT

    7-1-1. Add Repository
    
    7-1-2. Change Zigbee Channel to 25 on Z2M Configuration

7-3. MariaDB

    7-3-1. Setting Password is 'tabspace'
    
    7-3-2. Edit Configuration to use HA Recorder setting.
    
8. HomeAssistant Configuration Setting

  8-1. Include Dummy files
  
  8-2. Exclude something laggy settings
