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
vol -f memorydump.mem windows.netstat                           --> Show active and closed TCP/UDP connections, associated process IDs, local and remote ports, and IPs
vol -f memorydump.mem windows.pslist                            --> List processes list
vol -f memorydump.mem windows.pstree                            --> Show processes tree
vol -f memorydump.mem windows.psscan                            --> Find hidden processes (evasion countermeasures)
vol -f memorydump.mem windows.handles                           --> Show handles
vol -f memorydump.mem windows.filescan                          --> Look for file objects
vol -f memorydump.mem windows.ssdt                              --> Resolve addresses for system calls based on SSDT
vol -f memorydump.mem windows.modules                           --> List drivers and kernel modules currently loaded into memory
vol -f memorydump.mem windows.driverscan                        --> Scan raw memory for DRIVER_OBJECT structures 
vol -f memorydump.mem windows.mftscan.MFTScan                   --> Scan alternate data streams
vol -f memorydump.mem windows.memmap -o . --dump --pid 1234     --> Dump process memory
vol -f memorydump.mem windows.dlllist                           --> Show DLLs used
vol -f memorydump.mem windows.dlllist | grep -vi system32       --> Show more interestings DLLs
vol -f memorydump.mem windows.malfind                           --> Look for code injections
vol -f memorydump.mem windows.vadinfo                           --> Display detailed information about virtual memory descriptors,
vol -f memorydump.mem windows.yarascan                          --> Use YARA rules
vol -f memorydump.mem windows.cmdline                           --> Look for command line arguments
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



