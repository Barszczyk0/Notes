# File system

## File Allocation Table (FAT)
Data structures of the FAT file system:
- Clusters - storage unit of the FAT file system
- Directory - information about file identification, like file name, starting cluster, and filename length
- File Allocation Table - linked list of all the clusters

| Item              | FAT12 | FAT16 | FAT32 |
| :---------------- | :-----: | :---: | :---: |
| Addressable bits  |   12   | 16 | 28 |
| Max number of clusters |  2^12  | 2^16 | 2^28 |
| Maximum Volume size    | `32 MB`  | `2 GB` | `2 TB` |


Maximum file size in FAT32 (and FAT16) - `4 GB`

## Extensible File Allocation Table (exFAT)

Maximum file size in FAT32 (and FAT16) - `4 PB`

## New Technology File System (NTFS)

New Technology File System (NTFS) features:
- Journaling
- Access Controls
- Volume Shadow Copy
- Alternate Data Streams

Master File Table (MFT) is more complex version of File Allocation Table. Critical records from MFT:
- `$MFT` - stores information about the clusters
- `$LOGFILE` - stores the transactional logging of the file system
- `$UsnJrnl` (Update Sequence Number Journal) - contains information about all the files that were changed in the file system
