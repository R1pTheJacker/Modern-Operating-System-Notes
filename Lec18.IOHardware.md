## 1. Disk
- Difference between Server Disk and PC 
Disk
  - Storage density is lower in Server Disk
  - Server usually contains multiple disks, using Overlapped Seeks
    - Overlapped Seeks: A controller doing seeks on two or more drives at the same time

### 1.1 RAID 
  - RAID
    - Redundant Array of Inexpensive Disks
    - but industry redefined the I to be “Independent rather than “Inexpensive” 
  - SLED
    - Single Large Expensive Disk
  - Why RAID
    - Fault Tolerance
    - Improve Performance of Disk

### 1.2 Disk Formatting
  - Category
    - No interleaving
    - Single interleaving
    - Double interleaving
  - Why Interleaving
    - improve performance
  - Low-level Format
    - format sectors 
  - High-level Format 
    - format boot block, superblock etc.

### 1.3 Disk Arm Scheduling Algorithm
  - time-determined factors
    - seek time
      - it domainates
    - rotational delay
    - transfer time
  - Shortest Seek First (SSF)
    - go for the shortest seek currently
  - Elevator Algorithm
    - first pick the shortest
    - then all the way up or down and come back

### 1.4 Error Handling
- find a disk track with a bad sector
- substitute the bad one with a spare one 
- shift all sectors to bypass the bad one

### 1.5 Stable Storage
When a write is issued to it, the disk either correctly writes the data or it does nothing, leaving the existing data intact. Such as system is called stable storage.


## 2. Clock
- Clock Hardware

- Soft Timer

## 3. User Interface

## 4. Thin Client

## 5. Power Management
- Telling the programs to use less energy
  - may mean poorer user experience
- Examples
  - change from colored output to black and white
  - speech recognition reduces vocabulary
  - less resolution or detail in an image