# Home-Assistant - sync Kodi db via MariaDB

## Description:

This tutorial describes how to create a shared database of watched videos between multiple Kodi installations on home assistant via the MariaDB addon.
This allows you to resume watching on another TV where you left off.

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
  - username: kodi
    password: kodi
    host: '%'
rights:
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

- \Userdata\profiles\username\advancedsettings.xml

**Troubleshooting:**
Enable logging Kodi and check log file %AppData%\Kodi\kodi.log
In log find server ip adress and myvideos.
If kodi has a problem with writing to the database then there is a problem with the permissions on the server.

