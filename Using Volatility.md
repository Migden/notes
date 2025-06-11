2025-05-04 05:27

##### Learning Covered:

--------------------------
Tags: [[Volatility]], [[Memory Dump Formats]]


### Basic Commands
--------------------------------
The most basic Volatility command is constructed as follows:

```
python vol.py -f <FILENAME> --profile=<PROFILE> <PLUGIN> [ARGS]
```

Here's an example:
```
python vol.py -f /home/mike/memory.dmp --profileWin7sp1x64 pslist
```


### Selecting a Profile
------------
One of the options from the help menu is the `--profile` option. This option tells volatility what type of system your memory dump came from.

If you do not know the profile of an image. In this case we can use a plugin called `imageinfo`

```
python vol.py -f memory.raw imageinfo
```

###### Volatility scans for the `_KDEDEBUGGER_DATA64` Structure, included in this structure is a signature of `KDBG`. This signature give vital information for determining the Profile. This signature does not need to be accurate for the OS to run and malware can change this signature to avoid forensics tools correctly recognizing memory dumps


### Memory Dump Formats
----------
- Crash Dump - crashinfo
- Hibernation File - hibinfo
- HPAK - hpakinfo
- Mach-o - machoinfo
- WMware - vmwareinfo
- VirtualBox - vboxinfo

Luckily volatility has a way to automatically convert into usable memory files. Volatility also has plugins to return information on the above memory dumps

We can convert these files using the volatility `imagecopy` plugin to copy out a raw memory dump from the above formats.

We can also use volatility `raw2dump` to turn raw memory files into windows crash dumps from use with WinDBG debugger


### References:
https://repository.root-me.org/Forensic/EN%20-%20Volatility%20cheatsheet%20v2.4.pdf



