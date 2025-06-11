
This challenge involved a memory dump from a windows machine, we need to return the hostname of the machine. Basic configuration and settings information are stored in the `registry hive`. Reading the key at `\REGISTRY\MACHINE\SYSTEM\ControlSet001\Control\ComputerName` will return the current computer hostname


The volatility command = `vol -f ch2.dmp windows.registry.printkey --offset=0x8b21c008 --key='ControlSet001\Control\ComputerName' --recurse`