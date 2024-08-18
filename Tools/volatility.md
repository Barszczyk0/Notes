# Volatility
## Basics
```
vol --help
vol -f memorydump.mem --help
```

```
vol -f memorydump.mem windows.info
vol -f memorydump.mem linux.info
vol -f memorydump.mem mac.info
```

## Gathering information
```
vol -f memorydump.mem windows.info                              --> Show system information
vol -f memorydump.mem windows.netscan                           --> Scan for network objects
vol -f memorydump.mem windows.netstat                           --> Show network connections
vol -f memorydump.mem windows.pslist                            --> List processes list
vol -f memorydump.mem windows.pstree                            --> Show processes tree
vol -f memorydump.mem windows.psscan                            --> Deal with evasion countermeasures
vol -f memorydump.mem windows.filescan                          --> Look for file objects
vol -f memorydump.mem windows.mftscan.MFTScan                   --> Scan alternate data streams
vol -f memorydump.mem windows.memmap -o . --dump --pid 1234     --> Dump process memory
vol -f memorydump.mem windows.dlllist                           --> Show DLLs used
vol -f memorydump.mem windows.malfind                           --> Look for code injections
vol -f memorydump.mem windows.yarascan                          --> Use YARA rules
vol -f memorydump.mem windows.cmdline                           --> Look for command line arguments
```