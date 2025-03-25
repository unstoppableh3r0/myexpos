
# Handling Timer interrupt 

setting up timer  

```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat sample_timer.spl
print "TIMER";
ireturn;
 
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat sample_timer.xsm
MOV R16, "TIMER"
PORT P1, R16
OUT
IRET
HALT           
```

```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface 
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# load --int=timer $HOME/spl/spl_progs/sample_timer.xsm 
Can't open source file.
File  not found.
Error while trying to delete temporary file
# load --int=timer $HOME/spl/spl_progs/os_startup.xsm
Can't open source file.
File  not found.
Error while trying to delete temporary file
# load --int=timer ../spl/spl_progs/os_startup.xsm
# load --library ../expl/library.lib 
# load --os ../spl/spl_progs/os_startup.xsm
# load --int=timer ../spl/spl_progs/sample_timer.xsm

```

output:

```
┌──(ajay㉿kali)-[~/myexpos/xsm]
└─$ ./xsm --timer 2
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
TIMER
Machine is halting.

```

