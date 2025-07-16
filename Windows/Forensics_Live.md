# Live Forensics of Windows System

## Forensic tools for live analysis
[Sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/)\
[DB Browser for Sqlite](https://sqlitebrowser.org/)\
[Hindsight](https://github.com/obsidianforensics/hindsight)

## Environment variables
List the environmental variables:
```cmd
set set/env_vars.txt
set | findstr "ComSpec Path PSModulePath Public TEMP TMP"
type env_vars.txt
```

## Powershell profiles

| Scope                              | Profile file |
|------------------------------------|-----------------|
| Current User and Current Host      | `$HOME\Documents\WindowsPowerShell\profile.ps1`  |
| All Users and Current Host         | `$PSHOME\Microsoft.PowerShell_profile.ps1` |
| Current User and and All Hosts     | `$HOME\Documents\profile.ps1` |
| All Users and All Hosts            | `$PSHOME\profile.ps1` |

List the Available Profiles:
```cmd
if exist "C:\Windows\System32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1" (echo PROFILE EXISTS) else (echo PROFILE DOES NOT EXIST)
if exist "C:\Users\Administrator\Documents\profile.ps1" (echo PROFILE EXISTS) else (echo PROFILE DOES NOT EXIST)
if exist "C:\Users\Administrator\Documents\WindowsPowerShell\profile.ps1" (echo PROFILE EXISTS) else (echo PROFILE DOES NOT EXIST)
if exist "C:\Windows\System32\WindowsPowerShell\v1.0\profile.ps1" (echo PROFILE EXISTS) else (echo PROFILE DOES NOT EXIST)
```

Restore the clean profile:
```
ren PS-DFIR-Profile.ps1 profile.ps1
ren C:\Windows\System32\WindowsPowerShell\v1.0\\profile.ps1 profile.bak
copy profile.ps1 C:\Windows\System32\WindowsPowerShell\v1.0\
```

## Loaded modules
List loaded modules:
```powershell
Get-Module | ft ModuleType, Version, Name
Get-Module -ListAvailable | select ModuleType, Version, Name
```

## System Profile
### System Name and Network Information
List system and network information:
```powershell
Get-CimInstance win32_networkadapterconfiguration -Filter IPEnabled=TRUE | ft DNSHostname, IPAddress, MACAddress
```

### OS Version and Installation Details
List OS Details
```powershell
Get-CimInstance -ClassName Win32_OperatingSystem | fl CSName, Version, BuildNumber, InstallDate, LastBootUpTime, OSArchitecture
```

### Date and TimeZone Info
List date and timeZone information
```powershell
Get-Date ; Get-TimeZone
```

### Reviewing Policies
Extract the system policies:
```powershell
Get-GPResultantSetOfPolicy -ReportType HTML -Path (Join-Path -Path (Get-Location).Path -ChildPath "RSOPReport.html")
```

## Users and Sessions
### Users
List the Users:
```powershell
Get-CimInstance -Class Win32_UserAccount -Filter "LocalAccount=True" | Format-Table  Name, PasswordRequired, PasswordExpires, PasswordChangeable | Tee-Object "user-details.txt"
```

List the User Groups:
```powershell
Get-LocalGroup | ForEach-Object { $members = Get-LocalGroupMember -Group $_.Name; if ($members) { Write-Output "`nGroup: $($_.Name)"; $members | ForEach-Object { Write-Output "`tMember: $($_.Name)" } } } | tee gp-members.txt
```

### Sessions
List infroamtion about users sessions:
```powershell
Get-LocalUser | select * | tee l-users.txt
```

List the Current Sessions:
```powershell
.\PsLoggedon64.exe | tee sessions.txt
```

### NTDS
`NTDS.dit` is the Active Directory database file used by domain controllers in Windows Server environments. The `SYSTEM` hive contains the system's boot key, essential for decrypting specific data within the `NTDS.dit` file.

The NTDS can provide the following information:
- Usernames and full names of domain users
- Security Identifiers (SIDs) for each user
- Detailed group memberships, including global, domain local, and universal groups
- Hashed representations of user passwords for domain accounts
- Account activation, disablement, and expiration status
- Login timestamps and failed login attempts
- Password last set and password expiration times

```powershell
ntdsutil.exe "activate instance ntds" "ifm" "create full C:\Exports" quit quit
$bootKey = Get-BootKey -SystemHivePath 'C:\Exports\registry\SYSTEM'
Get-ADDBAccount -All -DBPath 'C:\Exports\Active Directory\NTDS.dit' -BootKey $bootKey
```

### Group Policy Artefacts
GUI application - Group Policy Management: `Group Policy Management` and `Group Policy Editor`

List of policies:
```
domain.com/Domains.domain.com/Group Policy Objects
```

Choose interesting policy and right click `Edit` to open `Group Policy Editor`.

List Defender configuration:
```
Computer Configuration/Policies/Administrative Templates/Windows Components/Windows Defender Antivirus/Real-time Protection
```

List firewall configuration:
```
Computer Configuration/Policies/Administrative Templates/Network/Network Connections/Windows Defender Firewall/Domain
```

List Log-on scripts:
```
User Configuration/Policies/Windows Settings/Scripts (Logon/Logoff)
```


## Network 
### Active Ports and Connections
GUI application - Resource Monitor: `resmon`


List the TCP Connections:
```powershell
Get-NetTCPConnection | select Local*, Remote*, State, OwningProcess,` @{n="ProcName";e={(Get-Process -Id $_.OwningProcess).ProcessName}},` @{n="ProcPath";e={(Get-Process -Id $_.OwningProcess).Path}} | sort State | ft -Auto | tee tcp-conn.txt
```

### Network Shares
List the Network Shares:
```powershell
Get-CimInstance -Class Win32_Share | tee net-shares.txt
```

### Firewall
Check the firewall configuration:
```powershell
Get-NetFirewallProfile | ft Name, Enabled, DefaultInboundAction, DefaultOutboundAction | tee fw-profiles.txt
```

## Startup and Registry
### Boot-Time Execution Entries
List the Boot Startup Programs:
```powershell
.\autorunsc64.exe -a b * -h | tee boot.txt
```

### Startup Programs and Commands
List the programs and commands executed in the startup sequence:
```powershell
Get-CimInstance Win32_StartupCommand | Select-Object Name, command, Location, User | fl | tee autorun-cmds.txt
```

### Logon-Time Execution Entries
List the User Logon Startup Programs:
```powershell
.\autorunsc64.exe -a l * -h | tee logon.txt
```

### Registry
Enumerate Registry Key:
```powershell
$winlogonPath = "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"; "Userinit: $((Get-ItemProperty -Path $winlogonPath -Name 'Userinit').Userinit)"; "Shell: $((Get-ItemProperty -Path $winlogonPath -Name 'Shell').Shell)"
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\NetSh" | tee netsh-records.txt
```

## Services, Scheduled Items, Processes
### Services
GUI application - Services: `services.msc`

List services' creation information:
```powershell
Get-WinEvent -FilterHashTable @{LogName='System';ID='7045'} | fl
Get-WinEvent -FilterHashTable @{LogName='Security';ID='4697'} | fl
```

List the Current Running services:
```powershell
"Running Services:"; Get-CimInstance -ClassName Win32_Service | Where-Object { $_.State -eq "Running" } | Select-Object Name, DisplayName, State, StartMode, PathName, ProcessId | ft -AutoSize | tee services-active.txt
```

List the Idle services:
```powershell
"Non-Running Services:"; Get-CimInstance -ClassName Win32_Service | Where-Object { $_.State -ne "Running" } | Select-Object @{Name='Name'; Expression={if ($_.Name.Length -gt 22) { "$($_.Name.Substring(0,19))..." } else { $_.Name }}}, @{Name='DisplayName'; Expression={if ($_.DisplayName.Length -gt 45) { "$($_.DisplayName.Substring(0,42))..." } else { $_.DisplayName }}}, State, StartMode, PathName, ProcessId | Format-Table -AutoSize | Tee-Object services-idle.txt
```

Listt services set to run automatically:
```powershell
$services = Get-Service | Where-Object {$_.Status -eq "Running" -and $_.StartType -eq "Automatic"}

foreach ($service in $services) {
    $serviceName = $service.Name
    $serviceDisplayName = $service.DisplayName
    $serviceStatus = $service.Status
    $serviceWMI = (Get-WmiObject Win32_Service | Where-Object { $_.Name -eq $serviceName })
    $servicePath = $serviceWMI.PathName
    $serviceUser = $serviceWMI.StartName

    Write-Host "Service Name: $serviceName"
    Write-Host "Display Name: $serviceDisplayName"
    Write-Host "Service Status: $serviceStatus"
    Write-Host "Executable Path: $servicePath"
    Write-Host "User Context: $serviceUser"
    Write-Host ""
}
```

There might be cases where the malicious service has stopped after running its initial payload, like when the service binary immediately migrates into another process by injecting a malicious shellcode. Given this, reviewing all the stopped services that run automatically on boot is also essential to determine potential outliers ([script](https://github.com/WiredPulse/PowerShell/blob/master/Registry/Get-RegWriteTime.ps1)):
```powershell
powershell.exe -ep bypass

Import-Module C:\Tools\Get-RegWriteTime.ps1;
$services = Get-Service | Where-Object {$_.Status -eq "Stopped" -and $_.StartType -eq "Automatic"}
foreach ($service in $services) {
    $serviceName = $service.Name
    $serviceWMI = (Get-WmiObject Win32_Service | Where-Object { $_.Name -eq $serviceName })
    $serviceDisplayName = $service.DisplayName
    $serviceStatus = $service.Status
    $servicePath = $serviceWMI.PathName
    $serviceUser = $serviceWMI.StartName
    $serviceLastWriteTime = Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\$serviceName | Get-RegWriteTime | Select LastWriteTime

    Write-Host "Service Name: $serviceName"
    Write-Host "Display Name: $serviceDisplayName"
    Write-Host "Service Status: $serviceStatus"
    Write-Host "Executable Path: $servicePath"
    Write-Host "User Context: $serviceUser"
    Write-Host "Last Write Time: $serviceLastWriteTime"
    Write-Host ""
}
```

### Scheduled Tasks and Scheduled Jobs
GUI application - Task Scheduler: `taskschd.msc`

List tasks' creation information:
```powershell
Get-WinEvent -FilterHashTable @{LogName='Security';ID='4698'} | fl
Get-WinEvent -FilterHashTable @{LogName='Security';ID='4702'} | fl
```

List scheduled tasks:
```powershell
$tasks = Get-CimInstance -Namespace "Root/Microsoft/Windows/TaskScheduler" -ClassName MSFT_ScheduledTask; if ($tasks.Count -eq 0) { Write-Host "No scheduled tasks found."; exit } else { Write-Host "$($tasks.Count) scheduled tasks found." }; $results = @(); foreach ($task in $tasks) { foreach ($action in $task.Actions) { if ($action.PSObject.TypeNames[0] -eq 'Microsoft.Management.Infrastructure.CimInstance#Root/Microsoft/Windows/TaskScheduler/MSFT_TaskExecAction') { $results += [PSCustomObject]@{ TaskPath = $task.TaskPath.Substring(0, [Math]::Min(50, $task.TaskPath.Length)); TaskName = $task.TaskName.Substring(0, [Math]::Min(50, $task.TaskName.Length)); State = $task.State; Author = $task.Principal.UserId; Execute = $action.Execute } } } }; if ($results.Count -eq 0) { Write-Host "No tasks with 'MSFT_TaskExecAction' actions found." } else { $results | Format-Table -AutoSize | tee scheduled-tasks.txt }
```

List scheduled tasks:
```powershell
$tasks = Get-ScheduledTask | Where-Object {$_.Date —ne $null —and $_.State —ne "Disabled" —and $_.Actions.Execute —ne $null} | Sort-Object Date

foreach ($task in $tasks) {
    $taskName = $task.TaskName
    $taskDate = $task.Date
    $taskPath = $task.TaskPath
    $taskAuthor = $task.Author
    $taskCommand = $task.Actions.Execute
    $taskArgs = $task.Actions.Arguments
    $taskRunAs = $task.Principal.UserId

    # Output service information
    Write-Host "Task Name: $taskName"
    Write-Host "Task Author: $taskAuthor"
    Write-Host "Creation Date: $taskDate"
    Write-Host "Task Path: $taskPath"
    Write-Host "Command: $taskCommand $taskArgs"
    Write-Host "Run As: $taskRunAs"
    Write-Host ""
}
```
### Processes
List the Current Running Processes:
```powershell
Get-WmiObject -Class Win32_Process | ForEach-Object {$owner = $_.GetOwner(); [PSCustomObject]@{Name=$_.Name; PID=$_.ProcessId; P_PID=$_.ParentProcessId; User="$($owner.User)"; CommandLine=if ($_.CommandLine.Length -le 60) { $_.CommandLine } else { $_.CommandLine.Substring(0, 60) + "..." }; Path=$_.Path}} | ft -AutoSize | tee process-summary.txt
```


## Files and Directories
### Information about Program or File
Dispaly details about program or file:
```powershell
Get-Item -Path "C:\path\to\file.exe" | select *
```

### Directories
Details of the Temp Folders:
```powershell
Get-ChildItem -Path "C:\Users" -Force | Where-Object { $_.PSIsContainer } | ForEach-Object { Get-ChildItem -Path "$($_.FullName)\AppData\Local\Temp" -Recurse -Force -ErrorAction SilentlyContinue | Select-Object @{Name='User';Expression={$_.FullName.Split('\')[2]}}, FullName, Name, Extension } | ft -AutoSize | tee temp-folders.txt
```

List the Disk Volumes of the System:
```powershell
Get-CimInstance -ClassName Win32_Volume | ft -AutoSize DriveLetter, Label, FileSystem, Capacity, FreeSpace | tee disc-volumes.txt
```

List contents of `Temp` directory for a given user:
```powershell
Get-ChildItem -Path "C:\Users\Default\AppData\Local\Temp" -File -Force -Recurse
```

## Windows Event Logs
GUI application - Windows Event Viewer: `eventvwr.msc`

Sysmon Logs:
```
Applications and Services Logs/Microsoft/Windows/Sysmon/Operational
```

Windows Defender Logs:
```
Applications and Services Logs/Microsoft/Windows/Windows Defender/Operational
```

RDP Logs:
```
Applications and Services Logs/Microsoft/Windows/Terminal-Services-RemoteConnectionManager/Operational
```

User Artefacts in Authentication Protocols:
```
Windows Logs/Security
```

## Browser forensincs
### Firefox
List location of Firefox artefacts:
```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Roaming\Mozilla\Firefox\Profiles" 2>$null}
```

Databases below can be viewed in DB Browser for SQLite\
Browsing history can be found at: `places.sqlite`\
Cookies can be found at: `cookies.sqlite`

### Google Chrome
List location of Google Chrome artefacts:
```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Local\Google\Chrome\User Data\Default" 2>$null | findstr Directory}
```

List browser extensions:
```powershell
ls 'C:\Users\mike.myers\AppData\Local\Google\Chrome\User Data\Default\Extensions\'
```

Databases below can be viewed in DB Browser for SQLite\
Browsing history can be found at: `History`\
Saved credentials by browser can be found at: `Login Data`

### Microsoft Edge
List location of Microsoft Edge artefacts:
```powershhell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Local\Microsoft\Edge\User Data\Default" 2>$null | findstr Directory}
```

IE/Edge history includes browsing history and opened files by browser (`file://*`). Records can be viewed in Autopsy or FTKImager. It is stored in:
```
C:\Users\<username>\AppData\Local\Microsoft\Windows\WebCache\WebCacheV*.dat
```

Analysis can be simplified by using [Hindsight](https://github.com/obsidianforensics/hindsight). In order to use this tool:
- Run it `hindsight_gui.exe`
- Open `http://localhost:8080/`
- Provide `Input Path` from above
- Download sqlite database and query it via DB Browser via SQLite

Example queries:
```sql
SELECT timestamp,url,title,visit_duration,visit_count,typed_count FROM 'timeline' WHERE type = 'url'
SELECT timestamp,url,title,value FROM timeline WHERE type = 'download'
SELECT type,origin,key,value FROM 'storage'
```


## Office applications forensics
### Outlook
List location of Outlook artefacts:
```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Local\Microsoft\Outlook\" 2>$null | findstr Directory}
```

`OST` files (Offline Storage Table files) are data files used by Microsoft Outlook to store a local copy of mailbox data from an Exchange server, Microsoft 365, or Outlook account. These files can analysed using [XstReader](https://github.com/Dijji/XstReader).

### Teams
List location of Microsoft Teams artefacts:
```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Roaming\Microsoft\Teams" 2>$null | findstr Directory}
ls C:\Users\ | foreach {ls "C:\Users\$_\AppData\Roaming\Microsoft\Teams\IndexedDB" 2>$null}
```

`IndexDB` folder will have `.blob` and `.leveldb` files. They can be analysed using [Forensicsim](https://github.com/lxndrblz/forensicsim/). This is a Autopsy module that can be used as standalone binary to parse the Microsoft Teams data:
```powershell
C:\Tools\ms_teams_parser.exe -f C:\Users\<username>\AppData\Roaming\Microsoft\Teams\IndexedDB\https_teams.microsoft.com_0.indexeddb.leveldb\ -o output.json
```

Display messages and attached files (if any):
```powershell
$teams_metadata = cat .\output.json | ConvertFrom-Json
$users = @{}
$messages = @{}

# Initialise user hashtable for correlation
foreach ($data in $teams_metadata) {
   if ($data.record_type -eq "contact") {
     $users.add($data.mri, $data.userPrincipalName)
   }
}

# Combine all conversations/messages with the same ID
foreach ($data in $teams_metadata) {
  if ($data.record_type -eq "message") {
    if ($messages.keys -notcontains $data.conversationId) {
      $messages[$data.conversationId] = [System.Collections.ArrayList]@()
    }
    $messages[$data.conversationId].add($data) > $null
  }
}

# Print the parsed output focused on the significant values
foreach ($conversationID in $messages.keys) {
  Write-Host "Conversation ID: $conversationID`n"
  $conversation = $messages[$conversationID] | Sort createdTime
  foreach ($message in $conversation) {
    $createdTime = $message.createdTime
    $fromme = $message.isFromMe
    $content = $message.content
    $sender = $users[$message.creator]
    $direction = if ($message.isFromMe) { 'Outbound' } else { 'Inbound' }
    $attachments = if ($message.properties.files) { 'True' } else {'False'}

    Write-Host "Created Time: $createdTime"
    Write-Host "Sent by: $sender"
    Write-Host "Direction: $direction"
    Write-Host "Message content: $content"
    Write-Host "Has attachment: $attachments"
    
    # Parse file attachment details
    if ($attachments -eq "True") {
      foreach ($attachment in $message.properties.files) {
        $filename = $attachment.fileName
        $location = $attachment.fileInfo.fileUrl
        $type = $attachment.fileType
        
        Write-Host "Attachment name: $filename"
        Write-Host "Attachment location: $location"
        Write-Host "Attachment type: $type"
      }
    }
    Write-Host "`n"
  }

  Write-host "----------------`n"
}
```
### OneDrive
List location of Onedrive artefacts:
```powershell
ls C:\Users\ | foreach {ls "C:\Users\$_\Appdata\Local\Microsoft\OneDrive\logs" 2>$null | findstr Directory}
ls C:\Users\ | foreach {ls "C:\Users\$_\Appdata\Local\Microsoft\OneDrive\logs\Business1" 2>$null}
```

Important files:
- `SyncEngine.odl` - Contains all operations performed, including the information of each file processed. 
- `SyncDiagnostics.log` - A log file that contains the diagnostic information related to the synchronisation process of OneDrive.


`ODL` (Object Description Language) files are used primarily in Microsoft development environments to define COM (Component Object Model) interfaces. These file can by analysed using [OneDriveExplorer](https://github.com/Beercow/OneDriveExplorer).

