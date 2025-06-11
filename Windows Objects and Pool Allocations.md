
2025-05-05 02:13

##### Learning Covered:
- Windows Executive Objects
- Kernel Pool Allocations
- Pool tag scanning
--------------------------
Tags: [[forensics]], [[Windows Objects]]


All the artifacts that you find in memory dumps share a common origin. They all start out as an allocation. How, when, and why the memory regions were allocated sets artifacts apart. From a memory forensics perspective studying theses characteristics can help you make inferences about the content of an allocation.

###### Keep in mind that objects are not code, but references metadata that the OS uses to manage how the code runs when it is called
### Windows Executive Objects
--------------------------------
A great deal of memory forensics involves finding and analyzing executive objects. Windows is written in C and makes heavy use of C structures. Several of these structures are called `Executive Objects`, because they are managed (protected, deleted, etc.) by the Windows Object Manager - a component of the kernel implemented by the NT module.

A structure becomes an executive object when the operating system prepends various headers in it to manage services such as naming, access control. By definition all executive objects are structures, but not all structures are executive objects.

A Windows Executive object run outside the kernel and utilize features of `kernel objects`, but with greater functionality.

The most relevant executive objects are:
- \_FILE\_OBJECT
- \_EPROCESS
- \_OBJECT\_SYMBOLIC\_LINK
- \_TOKEN
- \_ETHREAD
- \_KMUTANT
- tagWINDOWSTATION
- tagDESKTOP
- \_DRIVER\_OBJECT
- \_CM\_KEY\_BODY
- \_OBJECT\_TYPE


### Object Headers
----
One of the common traits shared between all executive object types is the presence of an `object header` and zero or more `optional headers`. The object header immediately precedes the executive object structure in memory. Any `optional headers` will precede the `object header` in a fixed order.

![[Pasted image 20250505025508.png]]

##### Optional Headers
An Objects `optional header` contains various information that help describe the object. They are not required for the executable to run but stored information that could be helpful to us as forensics investigators. It includes information such as:
- Creator info
- Name info
- Handle info
- Quota info
- Process Info

### Kernel Pool Allocations
----
A `kernel pool` is a range of memory that can be divided up into smaller blocks for storing any type of data that a kernel-mode component (device driver, etc.) requests. Each allocated block has a header `_POOL_HEADER` that contains accounting and debugging information.  The `Kernel Pool` is system wide-accessible and can be access from all kernel mode processes

### Allocation APIs
-----
Before creating an instance of an object, a memory block large enough to store all the objects and its headers must be allocated from one of the operating systems pools. This memory is given using common API interfaces between the user-mode, and kernel-mode. A common function to do this is `ExAllocatePoolWithTag`.

This function requires the number of bytes to allocate the pool.  And also a `Tag` which identifies the code path taken to produce the allocation.

###### However in the case of `executive objects`, the process of delegating pool space is more complex as these objects require headers. The windows function `ObCreateObject`, will allocate space after taking in the headers and any optional headers into the size for allocation.

#### Example:

Assuming you want to create a file on windows using the API, the following steps happen.
- The process calls `CreateFileA`, or `CreateFileW` from `kernel32.dll`
- The above functions call `ntdll.dll`, which calls into the kernel and provides the native function `NtCreateFile`
- The `NtCreateFile` will call `ObCreateObject` to request a new file object type
- `ObCreateObject` calculates the size of `_FILE_OBJECT`, including space for headers
- `ObCreateObect` finds the structure for File Objects and determines weather to used paged, or non-paged memory, as well as the four-byte tag to use
- `ExAllocatePoolWithTag` is called with the appropriate size, memory type and tag


### Deallocation and Reuse
-----
Once a process signals that the object is no longer necessary by calling `CloseHandle`, The block of memory will be released back into the pools `"free list"`, where it can be reallocated and the object be overwritten.

It is important to note that when an object is no longer used by a process, it may still sit in the pool until it is overwritten. This means that potentially evidence of activity could be viewed an indefinite time since the action regarding system activity, etc., Which would overwrite the freed kernel space

### Pool Tag Scanning
------
`Pool Tag Scanning`, refers to finding all allocations based on the four-byte `Tags`

When scanning the `Pool` a lot of false positives will occur and its up to the tools our yourself to establish guidlines to weed out false positives such as, a header time of creation can't equal zero

#### Tag Source:
- Proc - Process
- Thrd - Threads
- Desk - Desktops
- Wind - Window Stations
- Mute - Mutants
- File - File Objects
- Driv - Drivers
- Link - Symbolic Links

### Finding Terminated Processes
----
Since processes executive objects are in the pool, if they are not overwritten we can still find the previously ran commands to find commands like `ping`, or `ifconfig` that only touch the disk for a short period of time


### Limitations of Pool Scanning
------
- Untagged Pool memory
- False positives
- Allocations larger than 4096 bytes can't be scanned using the regular technique

- A hacker could append a generic tag such as `Ddk ` to not flag the allocation
- Hackers could modify the pool tags or values in the `_POOL_HEADER` to trick forensics tools
### References:




