# Bootstrap Loader

Use the XSM Instruction set to write a small _OS startup_ code.
Load your _OS startup code_ into the _boot block_ of the disk and get this code executed on bootstrap.

creating a xsm file in spl/spl_progs
```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat helloworld.xsm 
MOV R0, "HELLO_WORLD"
MOV R16, R0
PORT P1, R16
OUT 
HALT

```

loading the xsm in the os
```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# load --os $HOME/myexpos/spl/spl_progs/helloworld.xsm

```

running the program 

```
┌──(ajay㉿kali)-[~/myexpos/xsm]
└─$ ./xsm             
HELLO_WORLD
Machine is halting.

```


The XSM simulator given to you is an assembly language interpeter for XSM. Hence, it is possible to load and run assembly language programs on the simulator