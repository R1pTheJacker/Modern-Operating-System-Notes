## 1. I/O Device Interface
- ***I/O Devices***
  - Keyboard
  - Mouse
  - PCI-e bus
  - USB
  - IDE
  - CD-ROM
  - SATA

- ***Device classification***
  - Block Device
  - Character Device

- ***Device Controller***
*“I/O devices have components: mechanical component and electronic component, the electronic component is the device controller.”*
- convert serial bit stream to byte blocks
- error correction
- communicate with memory

## 2. I/O Address Space Access
- Separate I/O and memory space
```
IN register, portaddr
OUT portaddr, register
``` 
- Memory-mapped I/O
```
MOV register, portaddr
```
- Hybrid
...



- Memory-Mapped I/O
  - single addr bus
  - dual bus
    - add a bus between CPU and Memory

- DMA (Direct Memory Access)
  - Fly-by mode
    - transmission between memory and I/O devices
  - Cached mode
    - load data in DMA
    - transmission from DMA to destination
## 3. Special Topics
- Precise Interrupt
- Imprecise Interrupt