
------------------------
2025-03-04 03:18

##### Learning Covered:
--------------------------

Tags: [[forensics]]

### How to install Volatility
---------------

```
git clone https://github.com/volatilityfoundation/volatility3.git
```

```
pip3 install -r requirements
```

### Identifying Malicious Processes
------------
The first thing i like to do when i have received a RAM dump is to look at the active processes that where running on the device.

The first command to list processes it `pslist`

```
python3 vol.py -f file windows.pslist
```

If a malicious process is running we can use the `pstree` command to see what parent process spawned a child process.

`Attackers will commonly name malware after trusted windows processes such as svchost.exe, looking at the tree can show if it is spawning from a different parent process`

```
python3 vol.py -f file windows.pstree
```

### Identifying Malicious Network Connections
---------------------
When a RAM dump is captured any network connection at the time will be stored in the captured memory. It includes destination and port addresses

To view network connection we can do the following

```
python3 vol.py -f file windows.netscan
```

### Identifying Injected Code
-----------
Malware is often packed so that the code written by the malware author is obfuscated. Packed malware is essentially wrapped with a layer of code. When a piece of malware is packed it needs to be unpacked, this step is done on the RAM.

Using the Volatility `malfind` feature, will display any potential suspicious processes that may contain injected code

### Extracting DLLs
----------

```
python3 vol.py -f file -o /home/procfiles windows.dumpfiles -pid 1902
```


### References
---------
https://www.varonis.com/blog/how-to-use-volatility
