# Home-Assistant - sync Kodi db via MariaDB

## Description:

This tutorial describes how to create a shared database of watched videos between multiple Kodi installations on home assistant via the MariaDB addon.
This allows you to resume watching on another TV where you left off.

## Steps:
1. install MariaDB addon in Home Assistant
2. copy the MariaDB add-on settings
3. create file advancedsettings.xml on all Kodi devices (userdata folder)

## 2. MariaDB addon settings
<img align="right" src="https://github.com/peca2345/Home-Assistant---sync-Kodi-db-via-mariadb/blob/main/IMG/mariadb_settings.png?raw=true">
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



## 3. Kodi - Create file advancedsettings.xml in userdata folder
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

## advancedsettings.xml file location on different platform

By default the file does not exist, you have to create it and copy the settings into it.

**Windows: %AppData%\Kodi\userdata\advancedsettings.xml

To access Kodi folders from PC to Libre/OpenELEC, enable samba and press Win+R on PC and paste this address. (adjust according to your IP)

**LibreELEC: \\IP_adress\Userdata\advancedsettings.xml

**OpenELEC: \\IP_adress\\Userdata\advancedsettings.xml

If you use multiple profiles in Kodi, you must copy the advancedsettings.xml file to each profile.

\Userdata\profiles\username\advancedsettings.xml
