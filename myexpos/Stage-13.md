# Boot Module

boot.spl 

```
//loading the INIT program
loadi(65, 7);
loadi(66, 8);

//loading INT=10 routine
loadi(22, 35);
loadi(23, 36);

//loading INT=7 routine
loadi(16, 29);
loadi(17, 30);

//loading exception handler
loadi(2, 15);
loadi(3, 16);

//loading the timer interrupt handler
loadi(4, 17);
loadi(5, 18);


//loading the library
loadi(63, 13);
loadi(64, 14);

//Setting the Page Table for the INIT program (here pid = 1)
PTBR = PAGE_TABLE_BASE + 20;
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

//Storing the IP in the top of the user stack and setting the SP
[76 * 512] = [65 * 512 + 1];

//Setting the process table for the init program
[PROCESS_TABLE + 17] = 1;                       // pid
[PROCESS_TABLE + 20] = CREATED;                 // State
[PROCESS_TABLE + 27] = 83;                      // User area
[PROCESS_TABLE + 28] = 0;                       // Kernel SP
[PROCESS_TABLE + 29] = 8 * 512;                 // User SP
[PROCESS_TABLE + 30] = PAGE_TABLE_BASE + 20;    // PTBR
[PROCESS_TABLE + 31] = 10;                      // PTLR

return;
```

Output :

```
┌──(arjun㉿arjun)-[~/myexpos/xsm]
└─$ ./xsm            
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
1
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
Timer
2
...
50
Timer
Timer
Timer
Timer
Machine is halting.

```

