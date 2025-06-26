# Volatility
## Basics
```
vol -h
vol -f dump.mem <os>.<module> -h
```

```
vol -f dump.mem windows.info
vol -f dump.mem linux.info
vol -f dump.mem mac.info
```

## Gathering information
```
vol -f dump.mem windows.info                              --> Show system information
vol -f dump.mem windows.sessions                          --> Lists all active user sessions
vol -f dump.mem windows.netscan                           --> Scan for network objects
vol -f dump.mem windows.netstat                           --> Show active and closed TCP/UDP connections, associated process IDs, local and remote ports, and IPs
vol -f dump.mem windows.pslist                            --> List processes list
vol -f dump.mem windows.pstree                            --> Show processes tree
vol -f dump.mem windows.psscan                            --> Find hidden processes (evasion countermeasures)
vol -f dump.mem windows.psxview                           --> Find hidden processes (cross-references)
vol -f dump.mem windows.handles                           --> Show handles
vol -f dump.mem windows.filescan                          --> Look for file objects
vol -f dump.mem windows.registry.hivelist                 --> List registry hives that were loaded in memory
vol -f dump.mem windows.registry.userassist               --> List with which programs a user interacted with through the graphical interface
vol -f dump.mem windows.ssdt                              --> Resolve addresses for system calls based on SSDT
vol -f dump.mem windows.modules                           --> List drivers and kernel modules currently loaded into memory
vol -f dump.mem windows.driverscan                        --> Scan raw memory for DRIVER_OBJECT structures 
vol -f dump.mem windows.mftscan.MFTScan                   --> Scan alternate data streams
vol -f dump.mem windows.dlllist                           --> Show DLLs used
vol -f dump.mem windows.dlllist --pid 1234                --> Show DLLs for PID or name (regex)
vol -f dump.mem windows.dlllist | grep -vi system32       --> Show more interestings DLLs
vol -f dump.mem windows.malfind                           --> Look for code injections
vol -f dump.mem windows.vadinfo                           --> Display detailed information about virtual memory descriptors,
vol -f dump.mem windows.yarascan                          --> Use YARA rules
vol -f dump.mem windows.cmdline                           --> Look for command line arguments
```

## Dumping files
```
vol -f dump.mem -o output windows.memmap --dump --pid 1234         --> Dump process memory segments
vol -f dump.mem -o output windows.dlllist --dump --pid 1234        --> Dump all DLLs used by prosses with PID or with name (regex)
vol -f dump.mem -o output windows.dumpfiles --dump --pid 1234      --> Dump files related to PID
ll outoput | grep -Ei ".exe|.dat"                                              --> Filter dumped files
ll outoput | grep -Ei ".docx|.xlsx|.pptx"                                      --> Filter dumped files
ll outoput | grep -Ei ".dotm|.docm|.xlsm|.xltm|.xlsb|.pptm|.potm|.ppsm"        --> Filter dumped files
```

## Extra information

### Hidden processes
Some malware (rootkits) will, in an attempt to hide their processes, unlink themselves from the list. By unlinking themselves from the list, you will no longer see their processes when using pslist. `psscan` locate processes by finding data structures that match `_EPROCESS`. `_EPROCESS` is a kernel-mode structure that represents a process in memory. It stands for Executive Process Block. \
\
The `_EPROCESS` structure holds all the information the Windows kernel needs to manage a process, such as:
- Process ID (PID)
- Parent process ID
- Image name
- Memory layout, including VADs
- Handle tables
- Loaded modules (DLLs, EXEs)

`psxview` does multiple tests in one and cross-reference the results. This module includes visibility checks in other modules `pslist`, `psscan`, `thrdscan`. Moreover `psxview` provides information about exit time and presence of handles to CSRSS. CSRSS (Client/Server Runtime Subsystem) is responsible for handling the user-mode side of the Win32 subsystem. It plays a key role in console window management, process/thread creation, and shutdown operations. There are usually two instances of csrss.exe running: one for Session 0 (system processes and services) and one for the current user session. Legitimate user processes often hold handles to csrss.exe because it's essential for process/thread interaction. If a process is not linked to CSRSS, or CSRSS is missing or tampered with, it's a strong indicator of process hiding attempt.

### SSDT Hook Detection
SSDT stands for System Service Descriptor Table. It’s a critical kernel data structure that maps system calls made by user-mode applications to the corresponding kernel-mode functions. Rootkits may overwrite SSDT entries to redirect legitimate system calls to their malicious counterparts.

### DRIVER_OBJECT
`DRIVER_OBJECT` structure represents a loaded device driver in memory. It’s created by the Windows I/O Manager when a driver is loaded and is used to manage how the driver interacts with the system.\
\
DRIVER_OBJECT is a kernel structure that stores:
- The entry points for the driver's routines (like handling I/O requests),
- A pointer to the driver's device objects,
- The driver's name and state.

### Malware Analysis
`MalFind` will attempt to detect injected processes and their PIDs along with the offset address and the infected area's Hex, Ascii, and Disassembly views. The plugin works by scanning the heap and identifying processes that have the executable bit set RWE or RX and/or no memory-mapped file on disk (file-less malware).

### Virtual Address Descriptor (VAD)
VAD stands for Virtual Address Descriptor. It's an internal data structure used by the Windows memory manager to track and manage the virtual memory allocations of a process.\
\
A VAD describes a range of virtual memory allocated within a process. It contains information about:
- The start and end addresses of the memory region.
- The protection (e.g., read/write/execute) of that region.
- The type of memory (e.g., private memory, mapped file, image, etc.).
- Flags that indicate if the region is committed, reserved, or free.
- Whether the memory is backed by a file (like a DLL or memory-mapped file).



