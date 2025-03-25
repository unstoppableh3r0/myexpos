
# ABI and XEXE Format


Familiarise with the Application Binary Interface(ABI) of eXpOS.
Modify the INIT program to comply with the eXpOS ABI.

creating a file with .xexe extension 

```
┌──(ajay㉿kali)-[~/myexpos/expl/expl_progs]
└─$ cat okok.xexe  
0
2056
0
0
0
0
0
0
MOV R0, 1
MOV R2, 5
GE R2, R0
JZ R2, 2074
MOV R1, R0
MUL R1, R0
BRKP
ADD R0, 1
JMP 2058
INT 10 

```

now lets modify the os_startup.spl code and compile it

```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat os_startup.spl
loadi(65,7);
loadi(66,8);
loadi(22,35);
loadi(23,36);
loadi(2, 15);
loadi(3, 16);
loadi(63,13);
loadi(64,14);

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

[76*512] = [65 * 512 + 1];
ireturn; 

```


making it work 

```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# load --library ../expl/library.lib 
# load --init ../expl/expl_progs/okok.xexe
# load --os ../spl/spl_progs/os_startup.xsm 

```

output :

```
┌──(ajay㉿kali)-[~/myexpos/xsm]
└─$ ./xsm --debug --timer 0
Previous instruction at IP = 2068: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 2070, Page No. = 4: ADD R0,1
debug> reg
R0: 1	R1: 1	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 38912	R17: 2056	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 4095	IP: 2070	PTBR: 29696	PTLR: 10	
EIP: 	EC: 	EPN: 	EMA: 	
debug> c
Previous instruction at IP = 2068: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 2070, Page No. = 4: ADD R0,1
debug> reg
R0: 2	R1: 4	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 38912	R17: 2056	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 4095	IP: 2070	PTBR: 29696	PTLR: 10	
EIP: 	EC: 	EPN: 	EMA: 	
debug> c
Previous instruction at IP = 2068: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 2070, Page No. = 4: ADD R0,1
debug> reg
R0: 3	R1: 9	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 38912	R17: 2056	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 4095	IP: 2070	PTBR: 29696	PTLR: 10	
EIP: 	EC: 	EPN: 	EMA: 	
debug> c
Previous instruction at IP = 2068: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 2070, Page No. = 4: ADD R0,1
debug> reg
R0: 4	R1: 16	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 38912	R17: 2056	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 4095	IP: 2070	PTBR: 29696	PTLR: 10	
EIP: 	EC: 	EPN: 	EMA: 	
debug> c
Previous instruction at IP = 2068: BRKP
Mode: USER 	 PID: 0
Next instruction at IP = 2070, Page No. = 4: ADD R0,1
debug> reg
R0: 5	R1: 25	R2: 1	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 38912	R17: 2056	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 4095	IP: 2070	PTBR: 29696	PTLR: 10	
EIP: 	EC: 	EPN: 	EMA: 	
debug> c
Machine is halting.

```

