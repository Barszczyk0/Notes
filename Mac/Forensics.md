# Forensics
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
[APOLLO](https://github.com/mac4n6/APOLLO) tool can be used to gather/extract information about MAC. Queries from `/modeles` directory can be used directly in [DB Browser for SQLite](https://sqlitebrowser.org/).

### Mac_apt
[Mac_apt](https://github.com/ydkhatri/mac_apt) is a tool to process Mac computer full disk images (or live machines) and extract data/metadata useful for forensic investigation

### DS_Store-parser
[.DS_Store-parser](https://github.com/hanwenzhu/.DS_Store-parser) parses everything from the `.DS_Store` files.

## Mounting disk image
```
mkdir mountpoint
apfsutil mac-disk.img
apfs-fuse -v 4 mac-disk.img ./mountpoint
```

## OS Information
### OS Version
```
/System/Library/CoreServices/SystemVersion.plist
```

### Serial Number
```
/private/var/folders/*/<DARWIN_USER_DIR>/C/locationd/consolidated.db
/private/var/folders/*/<DARWIN_USER_DIR>/C/locationd/cache_encryptedA.db
```

### OS Installation Date
```
stat /private/var/db/.AppleSetupDone
cat /private/var/db/softwareupdate/journal.plist
```
### Time Zone
```
ls -la /etc/localtime 
plistutil -p "/Library/Preferences/.GlobalPreferences.plist"
```
### Boot, Reboot and Shutdown Times
```
cat /private/var/log/system.log.*
```

## Network Information
### Network Interfaces
```
cat /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist
```

### DHCP Settings
```
cat /private/var/db/dhcpclient/leases/<interface>.plist
```

### Wireless Connections
```
plistutil -p "/Library/Preferences/com.apple.wifi.known-networks.plist"
```

## Account Activity
### User Accounts and Passwords
```
cat /private/var/db/dslocal/nodes/Default/users/<user>.plist
```

### User Login History
```
plistutil -p "/Library/Preferences/com.apple.loginwindow.plist"
cat /private/var/log/system.log
```

### SSH Connections
```
cat .ssh/known_hosts
```

### Privileged Accounts
```
cat /etc/sudoers
```

## Evidence of Execution

### Terminal History
```
cat /Users/<user>/.zsh_history
ls -la /Users/<user>/.zsh_sessions/
```

### Application Usage
```
/Users/<user>/Library/Application\ Support/Knowledge/knowledgeC.db
/private/var/db/CoreDuet/Knowledge/knowledgeC.d
/private/var/db/powerlog/Library/BatteryLife/CurrentPowerlog.PLSQL
```

## Connected Devices
### Mounted Volumes
List of drives mounted on the system can be found in location `/Users/<user>/Library/Preferences/com.apple.finder.plist`.
```
plistutil -p "/Users/<user>/Library/Preferences/com.apple.finder.plist"
```
### Connected iDevices
List of connected iDevices can be found in location `/Users/<user/Library/Preferences/com.apple.iPod.plis`.
```
plistutil -p "/Users/<user/Library/Preferences/com.apple.iPod.plis"
```

### Bluetooth Connections
Information about historical Bluetooth device connections is stored in `knowledgeC`. It can be extracted using APOLLO's `knowledge_audio_bluetooth_connected` module.

### Connected Printers
List of printers installed and used on the system can be found in location `/Users/<user>/Library/Preferences/org.cups.PrintingPrefs.plist`.
```
plistutil -p "/Users/<user>/Library/Preferences/org.cups.PrintingPrefs.plist"
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