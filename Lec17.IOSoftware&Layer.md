## 1. I/O Software Layer Structure
### 1.1 I/O Software Layers
- Hardware
- Interrupt handlers
- Device drivers 
- Device-independent OS software
- User-level I/O software

> Notice
> - The difference between Interrupt Layer and Device Driver Layer.
>   - The former handles interrupts with Interrupt Procedure, the latter handlers data access.

### 1.2 Interrupt Handlers
- Some steps that may be performed in I/O software after an interrupt.
1. Save regs not already saved by interrupt 
hardware

2. Set up context for interrupt service 
procedure(TLB, Page Table,..etc)
3. Set up stack for interrupt service procedure
4. Ack interrupt controller, reenable interrupts
5. Copy registers from where saved to the process 
table
6. Run service procedure 
7. Set up MMU context for process to run next
8. Load new process' registers
9. Start running the new process


### 1.3 Device Drivers
- OS owns interface of Device Drivers
- Device Drivers are normally positioned at the lower part of OS
- Drivers and Controllers communicates through some bus

### 1.4 Device-Independent I/O Software
- Provide uniform interfacing for device drivers
- Buffering
  - multiple buffering, just like network 
- Error reporting
- Allocating and releasing dedicated devices
- Provide device-independent block size

### 1.5 User-Level I/O Software
- How does user manipulate I/O functions? 
  - syscall
    - write()
    - read()
... 
- Layer
  - User Processes
    - Make I/O call
    - format I/O
    - spooling 
  - Device-independent software
    - naming
    - protection
    - blocking
    - buffering
    - allocation 
  - Device drivers
    - set up device registers
    - check status 
  - Interrupt handlers
    - wake up driver when I/O completed 
  - Hardware
    - peform I/O operation 


## 2. I/O Interface Access Method
***Printing a string.***
### 2.1 Programmed I/O
```C
copy_from_user(buffer, p, count); /* p is the kernel buffer */
for (i = 0; i < count; i++) { /* loop on every character */
    while (*printer_status_reg != READY) ; /* loop until ready */
    *printer_data_register = p[i]; /* output one character */
}
return_to_user( );

```


### 2.2 Interrupt-driven I/O
- Code executed at the time the print syscall is made
```C
copy_from_user(buffer, p, count);
enable_interrupts();
while(*printer_status_reg != READY) ;
*printer_data_register = p[0];
scheduler();
```

- Interrupt service procedure for the printer
```C
if(count == 0) {
    unblock_user();
} else {
    *printer_data_register = p[i];
    count--;
    i++;
}
acknowledge_interrupt();
return_from_interrupt();
```


### 2.3 DMA I/O
- Code executed when print syscall is made
```C
copy_from_user(buffer, p, count);
set_up_DMA_controller();
scheduler();
```
- Interrupt-service procedure
```C
acknowledge_interrupt();
unblock_user();
return_from_interrupt();
```

## 3. Key Issues
- Device independence
  - programs can access I/O devices without specifying device in advance
    - when reading USB0, it could be a HDD or a CD 
- Uniform naming
  - naming should not depend on particular devices
- Error handling
  - it should handle errors as close to hardware as possible

- Synchronous or Asynchronous
  - blocked transfers VS. interrupt-driven

- Buffering
    - avoiding problems happen during transmisson

- Sharable devices or Dedicated devices
  - disks are sharable
  - tape drivers are dedicated 

