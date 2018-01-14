# xmr_dace_stak_cpu, a xmr stak mod by Dace following work by fireice-uk and psychocrypt 
- Modified by Dace for uninterrupted CPU mining with no automatic donation pool redirections.
- Added coloured command line interface for highlighting success, fails and information.

If you find this tool useful and like to support its continued development, then consider a donation to any of the relevant developers below.

## Dace's donation addresses:
* ETN donation address: etnjwVuF4zuC8q2zfxCX4RgdV7jNcM5pkZdDdC6GaTy68Qb4Wu9vfJwPd3ctp6mGFgfiYyoKn14BhPErDpFy8obD39rN9zHUPe
* FTC donation address: 6s1mzQ21zxD8DSF3Gnyj73dN25XUdJMjQa

## fireice-uk's donation addresses:
* XMR donation address: 4581HhZkQHgZrZjKeCfCJxZff9E3xCgHGF25zABZz7oR71TnbbgiS7sK9jveE6Dx6uMs2LwszDuvQJgRZQotdpHt1fTdDhk

## psychocrypt's donation addresses:
* XMR donation address: 43NoJVEXo21hGZ6tDG6Z3g4qimiGdJPE6GRxAmiWwm26gwr62Lqo7zRiCJFSBmbkwTGNuuES9ES5TgaVHceuYc4Y75txCTU

## Introduction

This is an optimized CPU mining application for use with Monero, Electronium and other coins based on the Cryptonight algorithm with no donation pool mining.
THIS PROGRAM IS PROVIDED "AS-IS", USE IT AT YOUR OWN RISK!

## AUTHORS

Notable contributors to this application are:

Dace: 
- some minor performance improvements to retry times and removal of automated pool donations.
- updated readme.md for optional manual donations by address if user chooses to do so and wants to further support development.
- added coloured command line interface
- optimized for x64

Initial work done by fireice-uk and psychocrypt.

Source code is included to satisfy GNU GPL V3 requirements.

#### CPU mining performance 
Performance is nearly identical to the closed source paid miners. Here are some numbers:

* **I7-2600K** - 266 H/s
* **I7-6700** - 276 H/s (with a separate GPU miner)
* **Dual X5650** - 466 H/s (depends on NUMA)
* **Dual E5640** - 365 H/s (same as above)

## Common Issues

**SeLockMemoryPrivilege failed**

Please see [config.txt](config.txt) under section **LARGE PAGE SUPPORT**

For Windows 7 pro, or Windows 8 and above see [this article](https://msdn.microsoft.com/en-gb/library/ms190730.aspx)  (make sure to reboot afterwards!).

For Windows 7 Home :

1) Download and install [Windows Server 2003 Resource Kit Tools](https://www.microsoft.com/en-us/download/details.aspx?id=17657).  Ignore incompatiablity warning during installation.

2) In cmd or power shell: `ntrights -u %USERNAME% +r SeLockMemoryPrivilege`  (where %USERNAME% is the user that will be running the program.  This command needs to be run as admin)

3) Reboot.

Reference: http://rybkaforum.net/cgi-bin/rybkaforum/topic_show.pl?pid=259791#pid259791

*Warning: do not download ntrights.exe from any other site other then the offical Microsoft download page.*

**VirtualAlloc failed**

If you set up the user rights properly (see above), and your system has 4-8GB of RAM (50%+ use), there is a significant chance that there simply won't be a large enough chunk of contiguous memory because Windows is fairly bad at mitigating memory fragmentation.

If that happens, disable all auto-starting applications and run the miner after a reboot.

**msvcp140.dll and vcruntime140.dll not available errors**

Download and install this [runtime package](https://go.microsoft.com/fwlink/?LinkId=746572) from Microsoft.  *Warning: Do NOT use "missing dll" sites - dll's are exe files with another name, and it is a fairly safe bet that any dll on a shady site like that will be trojaned.  Please download offical runtimes from Microsoft above.*


**Error: MEMORY ALLOC FAILED: mmap failed**

From [config.txt](config.txt):

On Linux you will need to configure large page support `sudo sysctl -w vm.nr_hugepages=128` and increase your
ulimit -l. To do do this you need to add following lines to /etc/security/limits.conf:

    * soft memlock 262144
    * hard memlock 262144
    
Save file.  You WILL need to log out and log back in for these settings to take affect on your user (no need to reboot, just relogin in your session).
   
You can also do it Windows-style and simply run-as-root, but this is NOT recommended for security reasons.

**Illegal instruction (core dumped)**

This typically means you are trying to run it on a CPU that does not have [AES](https://en.wikipedia.org/wiki/AES_instruction_set).  This only happens on older version of miner, new version gives better error message (but still wont' work since your CPU doesn't support the required instructions).
