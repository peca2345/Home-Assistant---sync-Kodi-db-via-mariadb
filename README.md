# Home Assistant - sync Kodi watched database via MariaDB

## Description:
- shared database of watched videos between multiple Kodi installations on Home Assistant using the MariaDB add-on
- the markings of the videos you've watched are synchronised and you can resume watching the stopped video on another TV
- also works for streaming add-ons that do not use the kodi library

**Warning:**  
By changing the database you will lose the old database and start with an empty database.  
I recommend making a backup of the database beforehand. (folder Userdata\Database)

## Steps:

**1. install MariaDB addon in Home Assistant:**

Settings / addons, backup and supervisor / add-on store / find "MariaDB" and install it

<img align="right" src="https://github.com/peca2345/Home-Assistant---sync-Kodi-db-via-mariadb/blob/main/IMG/mariadb_settings.png?raw=true">

**2. MariaDB addon settings:**

Open add-on MariaDB and switch to the settings tab.  
Copy this setting from here:

```
databases:
  - homeassistant
logins:
  - username: homeassistant
    password: homeassistant
  - username: kodi
    password: kodi
    host: '%'
rights:
  - username: homeassistant
    database: homeassistant
  - username: kodi
    database: MyVideos119
    grant: ALL PRIVILEGES ON
```

Now go back to the first tab and run the addon.  
I recommend turning on the watchdog.  
If you are already using maridb with another database, leave it there and just add a new user and user permissions.

**3. Kodi - Create file advancedsettings.xml in userdata folder:**

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

**Kodi folder location on different platform:**

By default the file does not exist, you have to create it and copy the settings into it.  
- Windows: %AppData%\Kodi\userdata\advancedsettings.xml
- LibreELEC: \\IP_adress\Userdata\advancedsettings.xml
- OpenELEC: \\IP_adress\\Userdata\advancedsettings.xml

To access Kodi folders from PC to Libre/OpenELEC, enable samba and press Win+R on PC and paste address.  
If you use multiple profiles in Kodi, you must copy the advancedsettings.xml file to each profile.  
- \Userdata\profiles\ **username** \advancedsettings.xml

## Troubleshooting:

- Enable logging Kodi and check log file %AppData%\Kodi\kodi.log
- In log find server ip adress and myvideos.
- If kodi has a problem with writing to the database then there is a problem with the permissions on the server.
- If you will use mariadb without Home Assistant (e.g. in docker) you have to set user permissions for writing to the database and allow access from the network. 
- Also don't forget to enable the exception in the firewall for port 3306! 
- If this is not set you will see in the Kodi log that it cannot connect/write to the MariaDB database.
- Do not manually create the database in MariaDB. 
- Kodi will create it itself if the MariaDB user has write permissions. 
- If you create it manually, Kodi will freeze on startup.
