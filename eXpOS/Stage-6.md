# Running user program 

Learn how to set up the address space for an application.
Run an init program in user mode from the OS startup code.

The first user program which is executed is called the INIT program *. The eXpOS design stipulates that the INIT program must be stored in blocks 7 and 8 of the XSM disk. See [Disk Organisation](https://exposnitc.github.io/os_implementation.html). In this stage, first you will write a user program in assembly language and load it into the disk as the INIT program using XFS-Interface. You will then write the OS startup code such that it loads the INIT program into the memory and initiate its execution at the time of system startup.

creating a file :

```
┌──(ajay㉿kali)-[~/myexpos/expl/expl_progs]
└─$ cat squares.xsm         
//Program to calculate Squares of first 5 numbers

// R0 will hold value of n
// R1 will hold value of n^2

//Initialising R0(n) to 1
MOV R0, 1

_L1:

// Exit loop if n > 5
MOV R2, 5
GE R2, R0
JZ R2, _L2

// Computing n^2 in R1
MOV R1, R0
MUL R1, R0

//breakpoint instruction (to view contents of R1)
BRKP

// n = n + 1
ADD R0, 1

JMP _L1

_L2:

EXIT

// End of Program.

```

```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface 
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# dump --inodeusertable 
# copy 7 8 $HOME/myexpos/inode_table.txt

```

now we can see that disk space 7 and 8 in the inode table is occupied by this program 

```
┌──(ajay㉿kali)-[~/myexpos]
└─$ cat inode_table.txt   
//Program to cal

// R0 will hold 

// R1 will hold 

//Initialising R

MOV R0,
1
_L1:

// Exit loop if 

MOV R2,
5
GE R2,
R0
JZ R2,
_L2
// Computing n^2

MOV R1,
R0
MUL R1,
R0
//breakpoint ins

BRKP

// n = n + 1

ADD R0,
1
JMP _L1

_L2:

EXIT

// End of Progra

```


setting up both init 10 and exhandler 

```
# load --exhandler ../spl/spl_progs/haltrpog.xsm
# load --init=10 ../spl/spl_progs/haltrpog.xsm
```

OS Startup Code

The OS startup code of any operating system, which is the first piece of OS code to be executed on bootstrap, is responsible for loading the rest of the OS into the memory, initialize OS data structures and set up the first user program for execution.

In this stage, we will write the OS startup code to load the init program and setup the OS data structures necessary to run the program as a process. Finally, the OS startup code will transfer control to the init program using the IRET instruction.

```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat os_startup.spl
loadi(65,7);
loadi(66,8);
loadi(22,35);
loadi(23,36);
loadi(2, 15);
loadi(3, 16);
PTBR = PAGE_TABLE_BASE;
PTLR = 3;
[PTBR+0] = 65;
[PTBR+1] = "0100";
[PTBR+2] = 66;
[PTBR+3] = "0100";
[PTBR+4] = 76;
[PTBR+5] = "0110";
[76*512] = 0;
SP = 2*512;
ireturn; 

```


```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface 
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# load --os $HOME/myexpos/spl/spl_progs/os_startup.xsm 
```

```
┌──(ajay㉿kali)-[~/myexpos/xsm]   
└─$ ./xsm --debug --timer 0
Previous instruction at IP = 12: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 14, Page No. = 0: ADD R0,1
debug> mem
Unknown command "mem". See "help" for more information.
debug> reg
R0: 1	R1: 1	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 1024	R17: 	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 1023	IP: 14	PTBR: 29696	PTLR: 3	
EIP: 	EC: 	EPN: 	EMA: 	
debug> c
Previous instruction at IP = 12: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 14, Page No. = 0: ADD R0,1
debug> reg
R0: 2	R1: 4	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 1024	R17: 	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 1023	IP: 14	PTBR: 29696	PTLR: 3	
EIP: 	EC: 	EPN: 	EMA: 	

```


