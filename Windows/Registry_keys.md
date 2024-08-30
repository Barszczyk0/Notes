# Windows Registry Keys

## Hives directories
### System hives
1. DEFAULT 
2. SAM 
3. SECURITY 
4. SOFTWARE
5. SYSTEM 

```
C:\Windows\System32\Config\...
```
### User hives
1. NTUSER.DAT
2. USRCLASS.DAT
```
C:\Users\<username>\...
C:\Users\<username>\AppData\Local\Microsoft\Windows\...
```

### Ampcache hive

```
C:\Windows\AppCompat\Programs\Amcache.hve
```

## System information and User information
### OS Version
```
SOFTWARE\Microsoft\Windows NT\CurrentVersion
```

### Current Control set (machine’s configuratio)
```
HKLM\SYSTEM\CurrentControlSet
SYSTEM\Select\Current
SYSTEM\Select\LastKnownGood
```

### Computer Name
```
SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName
```

### Time Zone Information
```
SYSTEM\CurrentControlSet\Control\TimeZoneInformation
```

### Network Interfaces and Past Networks
```
SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces
```

### Autostart Programs
```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce
SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run
SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

### SAM hive and user information
```
SAM\Domains\Account\Users
```

## File/folder usage information
### Recent Files
```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
```

### Office Recent Files
```
NTUSER.DAT\Software\Microsoft\Office\VERSION
NTUSER.DAT\Software\Microsoft\Office\VERSION\UserMRU\LiveID_####\FileMRU
```

### ShellBags
```
USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags
USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU
NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU
NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags
```

### Open/Save and LastVisited Dialog MRUs
```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU
```

### Windows Explorer Address/Search Bars
```
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths
NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery
```

## Evidence of execution
```
UserAssist:
NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count
```

### ShimCache
```
SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache
```
### AmCache
```
Amcache.hve\Root\File\{Volume GUID}\
```

### BAM/DAM
```
SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}
SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}
```


## External devices information
### Device identification
```
SYSTEM\CurrentControlSet\Enum\USBSTOR
SYSTEM\CurrentControlSet\Enum\USB
```

### First/Last Times
```
SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####
    Oo64=first connection
    0066=last connection
    0067=last removal
```
### USB device Volume Name
```
SOFTWARE\Microsoft\Windows Portable Devices\Devices
```

