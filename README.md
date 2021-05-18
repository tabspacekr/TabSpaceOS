# TabSpaceOS
TabSpaceOS is Armbian Based Customized OS

Debian Linux기반인 Armbian을 OrangePi Zero에서 홈오토메이션을 손쉽게 활용할 수 있는 

오픈소스 IoT 플랫폼 HomeAssistant 및 각종 애드온을 탭스페이스의 노하우로 맞춤 커스터마이징 한 운영체제(OS)입니다.

# Download
See Release page : https://github.com/tabspacekr/TabSpaceOS/releases

# Use
Download zipped binary file, extract, write microsd card, and joy.

# Prework Code

## 1. Armbian 21.05.1 Buster for OrangePi Zero 설치

<pre>
   https://www.armbian.com/orange-pi-zero/

   https://redirect.armbian.com/orangepizero/Buster_current

   Armbian Login Information
   
   ID : root
   PW : tabspace
</pre>

## 2. OLED Support

<pre>
   SDD1306 Package Install
   
   Add Cron Job on Reboot
</pre>

## 3. HOSTNAME Autochange

<pre>
   Add Cron Job on Reboot
</pre>   

## 4. TimeZone Change

<pre>
   Asia/Seoul
</pre>

## 5. Docker CE Install (20.10.6)

<pre>
Use 'armbian-config'
</pre>

## 6. HomeAssistant Install (Core 2021.05.4, Supervisor-2021.04.3)

### 6-1. HomeAssistant Login Information
<pre>   
   ID : admin
   PW : tabspace
</pre>

## 7. HomeAssistant Add-On Install 


### 7-1. File Editor (5.3.0)

#### 7-1-1. Enable WatchDog
    
#### 7-1-2. Enable Show Sidebar
    
#### 7-1-3. Edit Configuration to Directory First shown
<pre>
dirsfirst: true
enforce_basepath: true
git: true
ignore_pattern:
  - __pycache__
  - .cloud
  - .storage
  - deps
ssh_keys: []
</pre>

### 7-2. Zigbee2MQTT


#### 7-2-1. Add Repository ( https://github.com/danielwelch/hassio-zigbee2mqtt ) and Install
    
#### 7-2-2. Change Zigbee Channel to 25 on Z2M Configuration
    
#### 7-2-3. Enable WatchDog
    
#### 7-2-4. Enable Show Sidebar
 
### 7-3. MariaDB (2.3.0)

#### 7-3-1. Setting Password is 'tabspace'
    
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
    
#### 7-3-2. Edit Configuration to use HA Recorder setting.
 
<pre>
# on configuration.yaml

# Use MariaDB for Recording
recorder:
  db_url: mysql://homeassistant:tabspace@core-mariadb/homeassistant?charset=utf8mb4
</pre>

### 7-4. Mosquitto broker (5.1.1)

#### 7-4-1. Install Mosquitto Broker
    
#### 7-4-2. Add login credential on HomeAssistant User

<pre>
ID : mqtt
PW : tabspace
</pre>

### 7-5. ZeroTier One  (0.11.0)
<pre>
참고 : ZeroTier One은 자동실행(autostart)되지 않으며, 관리효율성을 위해 사전설치되어 있습니다. 향후 TabSpace B2C망을 통한 서비스시에 사용됩니다.
</pre>

## 8. HomeAssistant Configuration Setting

### 8-1. Include Dummy files
  
### 8-2. Exclude something laggy settings
<pre>
Remove HA Update Check
- binary_sensor.updater
</pre>
### 8-3. Add theme (Google Dark theme by TabSpace)
<pre>
# add configuration.yaml
# 테마 적용
frontend:
  themes: !include themes.yaml
</pre>

<details><summary>themes.yaml</summary>
<p>

```python
# create themes.yaml
Google Dark Theme:
  # Header:
  app-header-background-color: rgb(23, 23, 23)
  app-header-text-color: rgb(198, 203, 210)
  # Main Interface Colors
  #검색 및 조회버튼 배경색임
  #primary-color: rgb(138, 180, 248)
  #primary-color: rgb(223, 194, 113)
  primary-color: rgb(130, 130, 130)
  light-primary-color: var(--primary-color)
  primary-background-color: rgb(23, 23, 23)
  secondary-background-color: rgb(32, 33, 36)
  divider-color: var(--primary-background-color)
  #accent-color: rgb(138, 180, 248)
  #accent-color: rgb(223, 194, 113)
  #accent-color: rgb(255, 255, 0)
  accent-color: rgb(130, 130, 130)
  # Text
  primary-text-color: rgb(242, 242, 242)
  secondary-text-color: rgb(166, 166, 166)
  text-primary-color: var(--primary-text-color)
  disabled-text-color: rgba(184, 190, 199, 0.4)
  # Sidebar Menu
  sidebar-icon-color: rgb(169, 177, 188)
  sidebar-text-color: rgb(198, 203, 210)
  sidebar-background-color: rgb(32, 33, 36)
  sidebar-selected-background-color: var(--primary-background-color)
  #sidebar-selected-icon-color: rgb(138, 180, 248)
  #sidebar-selected-icon-color: rgb(223, 194, 113)
  sidebar-selected-icon-color: rgb(255, 255, 0)
  sidebar-selected-text-color: var(--sidebar-selected-icon-color)
  # Buttons
  paper-item-icon-color: rgb(169, 177, 188)
  #paper-item-icon-active-color: rgb(138, 180, 248)
  #paper-item-icon-active-color: rgb(223, 194, 113)
  #버튼 활성화 색
  paper-item-icon-active-color: rgb(255, 255, 0)
  # States and Badges
  #state-icon-color: rgb(138, 180, 248)
  #state-icon-color: rgb(223, 194, 113)
  state-icon-color: rgb(255, 255, 0)
  state-icon-active-color: rgb(169, 177, 188)
  state-icon-unavailable-color: var(--disabled-text-color)
  # Sliders
  #paper-slider-knob-color: rgb(138, 180, 248)
  paper-slider-knob-color: rgb(255, 255, 0)
  paper-slider-knob-start-color: var(--paper-slider-knob-color)
  paper-slider-pin-color: var(--paper-slider-knob-color)
  paper-slider-active-color: var(--paper-slider-knob-color)
  paper-slider-secondary-color: var(--light-primary-color)
  # Labels
  label-badge-background-color: rgb(32, 33, 36)
  label-badge-text-color: rgb(198, 203, 210)
  label-badge-red: rgb(208, 101, 104)
  label-badge-green: rgb(128, 200, 132)
  label-badge-blue: rgb(138, 180, 248)
  label-badge-yellow: rgb(223, 194, 113)
  label-badge-gray: rgb(95, 98, 103)
  # Cards
  card-background-color: rgb(32, 33, 36)
  ha-card-border-radius: "10px" 
  ha-card-box-shadow: 1px 1px 5px 0px rgb(12, 12, 14)
  paper-dialog-background-color: var(--card-background-color)
  paper-listbox-background-color: var(--card-background-color)
  paper-card-background-color: var(--card-background-color)
  # Switches
  #switch-checked-button-color: rgb(138, 180, 248)
  switch-checked-button-color: rgb(255, 255, 0)
  #switch-checked-track-color: rgb(138, 180, 248)
  switch-checked-track-color: rgb(255, 255, 0)
  switch-unchecked-button-color: rgb(172, 176, 185)
  switch-unchecked-track-color: rgb(154, 160, 166)
  # Toggles
  paper-toggle-button-checked-button-color: var(--switch-checked-button-color)
  paper-toggle-button-checked-bar-color: var(--switch-checked-track-color)
  paper-toggle-button-unchecked-button-color: var(--switch-unchecked-button-color)
  paper-toggle-button-unchecked-bar-color: var(--switch-unchecked-track-color)
  # Table
  table-row-background-color: var(--primary-background-color)
  table-row-alternative-background-color: var(--secondary-background-color)
  data-table-background-color: var(--primary-background-color)
  mdc-checkbox-unchecked-color: rgb(169, 177, 188)
  # Dropdowns
  material-background-color: var(--secondary-background-color)
  material-secondary-background-color: var(--primary-background-color)
  mdc-theme-surface: var(--primary-background-color)
  # Pre/Code
  markdown-code-background-color: rgb(23, 23, 23)

Google Blue Theme:
  # Header:
  app-header-background-color: rgb(23, 23, 23)
  app-header-text-color: rgb(198, 203, 210)
  # Main Interface Colors
  #검색 및 조회버튼 배경색임
  primary-color: rgb(138, 180, 248) #블루
  #primary-color: rgb(223, 194, 113)
  #primary-color: rgb(130, 130, 130) #오렌지
  light-primary-color: var(--primary-color)
  primary-background-color: rgb(23, 23, 23)
  secondary-background-color: rgb(32, 33, 36)
  divider-color: var(--primary-background-color)
  accent-color: rgb(138, 180, 248) #블루
  #accent-color: rgb(223, 194, 113)
  #accent-color: rgb(255, 255, 0)
  #accent-color: rgb(130, 130, 130) #오렌지
  # Text
  primary-text-color: rgb(242, 242, 242)
  secondary-text-color: rgb(166, 166, 166)
  text-primary-color: var(--primary-text-color)
  disabled-text-color: rgba(184, 190, 199, 0.4)
  # Sidebar Menu
  sidebar-icon-color: rgb(169, 177, 188)
  sidebar-text-color: rgb(198, 203, 210)
  sidebar-background-color: rgb(32, 33, 36)
  sidebar-selected-background-color: var(--primary-background-color)
  sidebar-selected-icon-color: rgb(138, 180, 248) #블루
  #sidebar-selected-icon-color: rgb(223, 194, 113)
  #sidebar-selected-icon-color: rgb(255, 255, 0)
  sidebar-selected-text-color: var(--sidebar-selected-icon-color)
  # Buttons
  #paper-item-icon-color: rgb(169, 177, 188)
  paper-item-icon-active-color: rgb(138, 180, 248) #블루
  #paper-item-icon-active-color: rgb(223, 194, 113)
  #버튼 활성화 색
  #paper-item-icon-active-color: rgb(255, 255, 0)
  # States and Badges
  state-icon-color: rgb(138, 180, 248) #블루
  #state-icon-color: rgb(223, 194, 113)
  #state-icon-color: rgb(255, 255, 0)
  state-icon-active-color: rgb(169, 177, 188)
  state-icon-unavailable-color: var(--disabled-text-color)
  # Sliders
  paper-slider-knob-color: rgb(138, 180, 248) #블루
  #paper-slider-knob-color: rgb(255, 255, 0)
  paper-slider-knob-start-color: var(--paper-slider-knob-color)
  paper-slider-pin-color: var(--paper-slider-knob-color)
  paper-slider-active-color: var(--paper-slider-knob-color)
  paper-slider-secondary-color: var(--light-primary-color)
  # Labels
  label-badge-background-color: rgb(32, 33, 36)
  label-badge-text-color: rgb(198, 203, 210)
  label-badge-red: rgb(208, 101, 104)
  label-badge-green: rgb(128, 200, 132)
  label-badge-blue: rgb(138, 180, 248)
  label-badge-yellow: rgb(223, 194, 113)
  label-badge-gray: rgb(95, 98, 103)
  # Cards
  card-background-color: rgb(32, 33, 36)
  ha-card-border-radius: "10px" 
  ha-card-box-shadow: 1px 1px 5px 0px rgb(12, 12, 14)
  paper-dialog-background-color: var(--card-background-color)
  paper-listbox-background-color: var(--card-background-color)
  paper-card-background-color: var(--card-background-color)
  # Switches
  switch-checked-button-color: rgb(138, 180, 248) #블루
  #switch-checked-button-color: rgb(255, 255, 0)
  switch-checked-track-color: rgb(138, 180, 248) #블루
  #switch-checked-track-color: rgb(255, 255, 0)
  switch-unchecked-button-color: rgb(172, 176, 185)
  switch-unchecked-track-color: rgb(154, 160, 166)
  # Toggles
  paper-toggle-button-checked-button-color: var(--switch-checked-button-color)
  paper-toggle-button-checked-bar-color: var(--switch-checked-track-color)
  paper-toggle-button-unchecked-button-color: var(--switch-unchecked-button-color)
  paper-toggle-button-unchecked-bar-color: var(--switch-unchecked-track-color)
  # Table
  table-row-background-color: var(--primary-background-color)
  table-row-alternative-background-color: var(--secondary-background-color)
  data-table-background-color: var(--primary-background-color)
  mdc-checkbox-unchecked-color: rgb(169, 177, 188)
  # Dropdowns
  material-background-color: var(--secondary-background-color)
  material-secondary-background-color: var(--primary-background-color)
  mdc-theme-surface: var(--primary-background-color)
  # Pre/Code
  markdown-code-background-color: rgb(23, 23, 23)
```
</details>

### 8-4. 비밀번호 취약 알림 해제 자동화 추가
    
<details><summary>remove_pwned-passwords-notice.yaml</summary>
<p>
   
```python
alias: (TabSpace) 비밀번호 취약 알림 해제
description: Insecure secrets in ADD-ON_NAME의 알림을 자동으로 해제
trigger:
  - platform: event
    event_type: call_service
    event_data:
      domain: persistent_notification
      service: create
condition:
  - condition: template
    value_template: >
      {{ 'supervisor_issue_pwned' in
      trigger.event.data.service_data.notification_id }}
action:
  - service: persistent_notification.dismiss
    data:
      notification_id: |
        {{ trigger.event.data.service_data.notification_id }}
mode: parallel
max: 10
```
</details>

### 8-5. 시스템 시작 시 Google Dark Theme by TabSpace 자동 적용
<details><summary>theme_apply_on_startup.yaml</summary>
<p>
   
```
alias: (TabSpace) 시스템 시작 시 테마 자동적용
description: '시스템 시작 시에, Google Dark by TabSpace 테마를 자동으로 적용합니다.'
trigger:
  - platform: homeassistant
    event: start
condition: []
action:
  - service: frontend.set_theme
    data:
      name: Google Dark Theme
mode: single
```
</details>
    
### 8-6. Tasmota Integration 추가
<pre>
SONOFF WIFI 스위치의 활용을 손쉽게 하기 위한 Tasmota Integration Pre Install
</pre>
### 8-7. smartir custom_components 추가
    
https://github.com/smartHomeHub/SmartIR
```
   # on ssh
   43  cd  /usr/share/hassio/homeassistant/
   52  mkdir custom_components
   53  cd custom_components/
   55  git clone https://github.com/smartHomeHub/SmartIR
   57  cd SmartIR/
   59  cd custom_components/
   61  mv smartir/ ../../../
   62  cd ../../../
   64  cd custom_components/
   66  rm -rf SmartIR/
   69  mv smartir/ ./custom_components/
   70  cd custom_components/
   72  cd smartir/
   73  ls
   # edit configuration.yaml
   # adding smartir custom components
   # IR리모콘 사용을 손쉽게 할 수 있는 smartir 커스텀 컴포넌트 호출 ( https://github.com/smartHomeHub/SmartIR )  
smartir:
```
