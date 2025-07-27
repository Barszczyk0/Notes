# Logs
## Tools 
Logs files are located at `C:\Windows\System32\winevt\Logs`. They can be viewed using:
- `Event Viewer` - GUI application
- `wevtutil.exe` - terminal application
- `Get-WinEvent` - terminal applicaiton

## Event IDs and Sysmon IDs
[Encyclopedia](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx)

## Event ID logs
### Authentication logs
Acquire `LogonID` to track user action later.

| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 4624 | Security | Successful Logon |
| 4625 | Security | Failed Logon |

### User Management logs
Use `LogonID` to track user action like those below.

| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 4720 | Security | A user account was created |
| 4722 | Security | A user account was enabled |
| 4738 | Security | A user account was changed |
| 4725 | Security | A user account was disabled |
| 4726 | Security | A user account was deleted |
| 4723 | Security | A user changed their password |
| 4724 | Security | User's password was reset |
| 4732 | Security | A user was added to a security group |
| 4733 | Security | A user was removed from a security group |
| 4624 | Security | An account was successfully logged on |
| 4625 | Security | An account failed to log on |

### Process logs
| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 4688 | Security | New process is launched |

### Powershell logs
Powershell history file: `%AppData%\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`

| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 600 | Applications and Services Logs/Windows PowerShell | PowerShell Event Channel |
| 4104 | Apps and Services Logs/Microsoft/Windows/PowerShell/Operational | PowerShell ScriptBlock Logging |

### RDP logs
| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 21 | Applications and Services Logs/Microsoft/Windows/TerminalServices-LocalSessionManager/Operational | Successful RDP connect |
| 24 | Applications and Services Logs/Microsoft/Windows/TerminalServices-LocalSessionManager/Operational | Successful RDP disconnect |
| 25 | Applications and Services Logs/Microsoft/Windows/TerminalServices-LocalSessionManager/Operational | Successful RDP reconnect |
| 4624 | Security | An account was successfully logged on |
| 4625 | Security | An account failed to log on |

### Task Scheduler Logs

| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 4698 | Apps and Services Logs/Microsoft/Windows/TaskScheduler/Operational | A scheduled task was created |
| 4699 | Apps and Services Logs/Microsoft/Windows/TaskScheduler/Operational | A scheduled task was deleted |
| 4700 | Apps and Services Logs/Microsoft/Windows/TaskScheduler/Operational | A scheduled task was enabled |
| 4701 | Apps and Services Logs/Microsoft/Windows/TaskScheduler/Operational | A scheduled task was disabled |
| 4702 | Apps and Services Logs/Microsoft/Windows/TaskScheduler/Operational | A scheduled task was updated |


### Service Scheduler Logs
| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 4697 | Security | A service was installed |


### Windows Defender Logs
| Event ID | Type | Description |
| :--------: | :----: | :------- |
| 1116 | Apps and Services Logs/Microsoft/Windows/Windows Defender/Operational | Threat is detected |
| 1117 | Apps and Services Logs/Microsoft/Windows/Windows Defender/Operational | Threat is remediated |
| 5001 | Apps and Services Logs/Microsoft/Windows/Windows Defender/Operational | Protection engines are disabled |
| 5007 | Apps and Services Logs/Microsoft/Windows/Windows Defender/Operational | Modification of its settings |
| 5013 | Apps and Services Logs/Microsoft/Windows/Windows Defender/Operational | Exclusion creation |

<!-- -------------------------------------------------------------------------------------------------------------------------- -->

## Sysmon
### Process logs
| Event code | Type | Description |
| :--------: | :----: | :------- |
| 1 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Process Creation |
| 5 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Process Terminated |
| 7 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Image Loaded |
| 8 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | CreateRemoteThread |
| 10 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Process Access |

### Files logs
| Event code | Type | Description |
| :--------: | :----: | :------- |
| 2 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | A process changed a file creation time |
| 11 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | File Create |
| 13 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Registry Value Set |
| 15 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | File stream created |

### Network logs 

| Event code | Type | Description |
| :--------: | :----: | :------- |
| 3 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Network Connection |
| 22 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | DNS Query |


### Commands Logs

| Event code | Type | Description |
| :--------: | :----: | :------- |
| 3 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | Network Connection |
| 22 | Applications and Services Logs/Microsoft/Windows/Sysmon/Operational | DNS Query |


