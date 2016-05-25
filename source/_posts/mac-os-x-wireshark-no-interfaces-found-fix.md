title: （转）mac os x wireshark no interfaces found fix
date: 2016-03-28 01:25:49
tags: 
 - wireshark
 - network capture
 - osx
---

Alright, quick fix for a problem I always forget. When running Wireshark on OS X, when I go to select an interface to capture on, I get an error telling me there are no available interfaces to capture on. This is because Wireshark is running as a user that doesn’t have ownership on these interfaces.


Solution, open up the terminal and run the command:

``` bash
	sudo chown <username> /dev/bpf*
```

After a reboot, these permissions get reset, so you need to do it after each reset (and hence why I need this every now and then but can never remember the command).