# Handling Kernel Stack 

Modified os_Startup.spl and sample_timer.spl

```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat sample_timer.spl

[PROCESS_TABLE + ( [SYSTEM_STATUS_TABLE + 1] * 16) + 13] = SP;
// Setting SP to UArea Page number * 512 - 1
SP = [PROCESS_TABLE + ([SYSTEM_STATUS_TABLE + 1] * 16) + 11] * 512 - 1;
backup;
print "TIMER";
restore;
SP = [PROCESS_TABLE + ( [SYSTEM_STATUS_TABLE + 1] * 16) + 13];
ireturn;

┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat os_startup.spl  
loadi(65,7);
loadi(66,8);
loadi(4, 17);
loadi(5, 18);
loadi(22,35);
loadi(23,36);
loadi(2, 15);
loadi(3, 16);

PTBR = PAGE_TABLE_BASE;
PTLR = 10;
//Library
[PTBR+0] = 63;
[PTBR+1] = "0100";
[PTBR+2] = 64;
[PTBR+3] = "0100";

//Heap
[PTBR+4] = 78;
[PTBR+5] = "0110";
[PTBR+6] = 79;
[PTBR+7] = "0110";

//Code
[PTBR+8] = 65;
[PTBR+9] = "0100";
[PTBR+10] = 66;
[PTBR+11] = "0100";
[PTBR+12] = -1;
[PTBR+13] = "0000";
[PTBR+14] = -1;
[PTBR+15] = "0000";

//Stack
[PTBR+16] = 76;
[PTBR+17] = "0110";
[PTBR+18] = 77;
[PTBR+19] = "0110";
SP = 8*512;
[PROCESS_TABLE + 11] = 80;
[PROCESS_TABLE + 1] = 0;
[SYSTEM_STATUS_TABLE + 1] = 0;
[76*512] = [65 * 512 + 1];

ireturn; 

```
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
