# Forensics
## Mounting disk image
```
mkdir mountpoint
apfsutil mac-disk.img                      # Displayd volumes
apfs-fuse -v 4 mac-disk.img ./mountpoint   # Mount data volume
```

## Tools
### Plistutil
Plist files (short for Property List files) are used by the operating system and applications to store configuration settings, preferences, and other structured data. Plist files come in two main formats: XML and Binary.

Extension: `.plist`\
Location Examples:
- `/Library/Preferences/`
- `~/Library/Preferences/`
- Inside app bundles or configuration directories

```
plistutil -p filename.plist
```

### DB Browser
[DB Browser for SQLite](https://sqlitebrowser.org/) is a high quality, visual, open source tool designed for people who want to create, search, and edit SQLite or SQLCipher database files.

### APOLLO
[APOLLO](https://github.com/mac4n6/APOLLO) tool can be used to gather/extract information about MAC. \
Queries from `/modeles` directory can be used directly in [DB Browser for SQLite](https://sqlitebrowser.org/).

### Mac_apt
[Mac_apt](https://github.com/ydkhatri/mac_apt) is a tool to process Mac computer full disk images (or live machines) and extract data/metadata useful for forensic investigation

### DS_Store-parser
[.DS_Store-parser](https://github.com/hanwenzhu/.DS_Store-parser) parses everything from the `.DS_Store` files.

## OS Information
### OS Version
List OS vervion:
```
plistutil -p /System/Library/CoreServices/SystemVersion.plist
```

### Serial Number
List serial number:
```
/private/var/folders/*/<DARWIN_USER_DIR>/C/locationd/consolidated.db
/private/var/folders/*/<DARWIN_USER_DIR>/C/locationd/cache_encryptedA.db
```

### OS Installation Date
Retrieve isntallation date:
```
stat /private/var/db/.AppleSetupDone
cat /private/var/db/softwareupdate/journal.plist
```
### Time Zone
List time zone:
```
ls -la /etc/localtime 
plistutil -p /Library/Preferences/.GlobalPreferences.plist
```
### Boot, Reboot and Shutdown Times
List boot, beboot and shutdown times:
```
cat /private/var/log/system.log.*
```

## Network Information
### Network Interfaces
List network interfaces:
```
cat /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist
```

### DHCP Settings
List DHCP related information:
```
cat /private/var/db/dhcpclient/leases/<interface>.plist
```

### Wireless Connections
List WIFI related information:
```
plistutil -p /Library/Preferences/com.apple.wifi.known-networks.plist
```

## Account Activity
### Downloads
List the contents and metadata of download history:
```
plistutil -p Users/<user>/Library/Safari/Downloads.plist
```

### User Accounts and Passwords
List user account information with user's password hash:
```
cat /private/var/db/dslocal/nodes/Default/users/<user>.plist
```

### User Login History
List user login history:
```
plistutil -p /Library/Preferences/com.apple.loginwindow.plist
cat /private/var/log/system.log
```

## Connected Devices
### Mounted Volumes
List of drives mounted on the system can be found in location `/Users/<user>/Library/Preferences/com.apple.finder.plist`.
```
plistutil -p /Users/<user>/Library/Preferences/com.apple.finder.plist
```
### Connected iDevices
List of connected iDevices can be found in location `/Users/<user/Library/Preferences/com.apple.iPod.plis`.
```
plistutil -p /Users/<user/Library/Preferences/com.apple.iPod.plis
```

### Bluetooth Connections
Information about historical Bluetooth device connections is stored in `knowledgeC`. It can be extracted using APOLLO's `knowledge_audio_bluetooth_connected` module.

### Connected Printers
List of printers installed and used on the system can be found in location `/Users/<user>/Library/Preferences/org.cups.PrintingPrefs.plist`.
```
plistutil -p /Users/<user>/Library/Preferences/org.cups.PrintingPrefs.plist
```

## Logs
### Apple System Logs
The Apple System Logs (ASL) are in the location `/private/var/log/asl/`. This directory contains multiple types of logs, such as utmp, wtmp, and login details.
```
python3 mac_apt.py
```

### System Logs
System Logs are in the location `/private/var/log/system.log` and they are similar to syslog in Linux. These logs are in text format so they can be inspected using text editors. 

### Unified Logs
Unified Logs are in the locations /private/var/db/diagnostics/*.tracev3 and /private/var/db/uuidtext.

## File System Activity
### File System Events Store DB
File System Events Store DB or `fseventsd` is a database that is present in every volume connected to a macOS device. It is locatated at `/.fseventsd` and serves similar purpuse to `USN` Journal in NTFS.

```
python3 mac_apt.py -o . -c MOUNTED / FSEVENTS
```

### DS Store
`.DS_Store` are hidden files that are automatically created whenever user accesses folder using Finder. They can be found in every directory. They store custom view settings and metadata about the folder’s contents.
```
python3 parse.py ../.DS_Store 
```

### Most Recently Used
The most recently used folders in the plist file at `/Users/<user>/Library/Preferences/com.apple.finder.plist`

```
plistutil -p "/Users/<user>/Library/Preferences/com.apple.finder.plist"
```

### Contacts, Calls, and Messages
#### Contacts
Inspect interpersonal interactions i.e. communications with contacts:
```
/private/var/db/CoreDuet/People/interactionC.db
```

#### Calls
Inspect calls hisotry:
```
~/Library/Application Support/CallHistoryDB/CallHistory.storedata
```

#### Messages
Inspect messages:
```
~/Library/Messages/chat.db
~/Library/Messages/Attachments
```

### SSH Connections
List SSH `known_hosts`:
```
cat .ssh/known_hosts
```

### Privileged Accounts
List `sudoers`:
```
cat /etc/sudoers
```

## Evidence of Execution

### Application Install History
List installed applicaitons:
```
cat /var/log/install.log | grep Installed
plistutil -p /Library/Receipts/InstallHistory.plist
plistutil -p /private/var/db/receipts/<app-name>.plist
```

### Terminal History
List terminal history:
```
cat /Users/<user>/.zsh_history
ls -la /Users/<user>/.zsh_sessions/
```

### Application Usage
Inspect application usage:
```
/Users/<user>/Library/Application\ Support/Knowledge/knowledgeC.db
/private/var/db/CoreDuet/Knowledge/knowledgeC.d
/private/var/db/powerlog/Library/BatteryLife/CurrentPowerlog.PLSQL
```

## Productivity Apps
### Mail
List email information and attachments:
```
ls ~/Library/Mail/V#/<UUID>/*.mbox
plistutil -p ~/Library/Mail/V#/<UUID>/<directory>.mbox/Info.plist
```

### Calendar
Inspect calendar:
```
~/Library/Group\ Containers/group.com.apple.calendar/Calendar.sqlitedb
```

### Notes
Inspect notes:
```
~/Library/Group\ Containers/group.com.apple.notes/NoteStore.sqlite
~/Library/Group\ Containers/group.com.apple.notes/Accounts/<UUID>/Media
```

```
python3 mac_apt.py -o <output path> -c DD <path to disk image> NOTES
```

### Reminders
Inspect reminders:
```
~/Library/Group\ Containers/group.com.apple.reminders/Container_v1/Stores
```

### Office Applications 
Inspect office applications logs:
```
~/Library/Containers/com.microsoft.<app>/Data
~/Library/Containers/com.microsoft.<app>/Data/Library/Preferences
```

## Browsers
### Safari
List Safari history and caches:
```
ls ~/Library/Safari/
ls ~/Library/Safari/History.db
ls ~/Library/Containers/com.apple.Safari/Data/Library/Caches
```

### Chrome
List Chrome History and extensions:
```
ls ~/Library/Application\ Support/Google/Chrome/Default
ls ~/Library/Application\ Support/Google/Chrome/Default/Sessions/
ls ~/Library/Application\ Support/Google/Chrome/Default/Extensions
```

## Photos
Inspect photos library:
```
~/Pictures/Photos Library.photoslibrary
```

## Notifications
Inspect notifications history:
```
/Users/<user>/Library/Group\ Containers/group.com.apple.usernoted/db2
```

## Autostart applications
### Launch Agents and Daemons
`LaunchAgents` are user applications that execute at login, and `LaunchDaemons` are system applications that run with elevated privileges. `LaunchAgents` and `LaunchDaemons` are present in the `/System/Library`, `/Library` and `~/Library` directories.
```
find . \( -name *LaunchAgents* -o -name *LaunchDaemons* \) 2>/dev/null
```

## Permisssions
Application permissions are in the Transparency, Consent, and Control (TCC) database.
```
/Library/Application Support/com.apple.TCC/TCC.db
~/Library/Application Support/com.apple.TCC/TCC.db
```

### Saved Application State
```
~/Library/Saved Application State/<application>.savedState
~/Library/Containers/<application>/Data/Library/Application Support/<application>/Saved Application State/<application>.savedState
```

