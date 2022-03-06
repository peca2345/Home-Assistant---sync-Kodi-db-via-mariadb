# Home-Assistant - sync Kodi db via MariaDB

1. install MariaDB addon in Home Assistant

<img align="right" src="https://github.com/peca2345/ESPHome-code-examples/blob/main/images/sensors/DA18B20.png?raw=true">

**MariaDB addon settings**

```
databases:
  - homeassistant
logins:
  - username: kodi
    password: kodi
    host: '%'
rights:
  - username: kodi
    database: MyVideos119
    grant: ALL PRIVILEGES ON
```
Don't forget to configure port 3306 in the addon settings


Kodi - Create file advancedsettings.xml in userdata folder
```
<advancedsettings>
  <videodatabase>
    <type>mysql</type>
    <host>192.168.1.50</host>
    <port>3306</port>
    <user>kodi</user>
    <pass>kodi</pass>
  </videodatabase> 
  <videolibrary>
    <importwatchedstate>true</importwatchedstate>
    <importresumepoint>true</importresumepoint>
  </videolibrary>
</advancedsettings>
```

Windows: %AppData%\Kodi\userdata\advancedsettings.xml
LibreELEC: \\IP_adress\Userdata\advancedsettings.xml
