# XSM debugging


In this stage you will write an SPL program with a **breakpoint** statement. The breakpoint statement translates to the [BRKP](https://exposnitc.github.io/arch_spec-files/instruction_set.html) machine instruction and is used for debugging. If the XSM machine is run in the [Debug mode](https://exposnitc.github.io/support_tools-files/xsm-simulator.html) , on encountering the BRKP instruction, the machine simulator will suspend the program execution and allow you to inspect the values of the registers, memory, os data structures etc. Execution resumes only after you instruct the simulator to proceed.

creating debug.spl file

```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat debug.spl
alias counter R0;
counter = 0;
while(counter <= 10) do
  if(counter%2 != 0) then
    breakpoint;
  endif;
  counter = counter + 1;
endwhile; 

```

and the usual steps to load and execute but this time we execute it with the debug flag

```
┌──(ajay㉿kali)-[~/myexpos/xsm]
└─$ ./xsm --debug
Previous instruction at IP = 530: BRKP
Mode: KERNEL 	 PID: -1
Next instruction at IP = 532, Page No. = 1: JMP 534
debug> 

```


```
┌──(ajay㉿kali)-[~/myexpos/xsm]
└─$ ./xsm --debug
Previous instruction at IP = 530: BRKP
Mode: KERNEL 	 PID: -1
Next instruction at IP = 532, Page No. = 1: JMP 534
debug> reg
R0: 1	R1: 	R2: 	R3: 	R4: 	
R5: 	R6: 	R7: 	R8: 	R9: 	
R10: 	R11: 	R12: 	R13: 	R14: 	
R15: 	R16: 1	R17: 0	R18: 	R19: 	
P0: 	P1: 	P2: 	P3: 	
BP: 	SP: 	IP: 532	PTBR: 	PTLR: 	
EIP: 	EC: 	EPN: 	EMA: 	
debug> s
Previous instruction at IP = 532: JMP 534
Mode: KERNEL 	 PID: -1
Next instruction at IP = 534, Page No. = 1: MOV R16,R0
debug> c
Previous instruction at IP = 530: BRKP
Mode: KERNEL 	 PID: -1
Next instruction at IP = 532, Page No. = 1: JMP 534
debug> s
Previous instruction at IP = 532: JMP 534
Mode: KERNEL 	 PID: -1
Next instruction at IP = 534, Page No. = 1: MOV R16,R0
debug> s
Previous instruction at IP = 534: MOV R16,R0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 536, Page No. = 1: ADD R16,1
debug> s
Previous instruction at IP = 536: ADD R16,1
Mode: KERNEL 	 PID: -1
Next instruction at IP = 538, Page No. = 1: MOV R0,R16
debug> s
Previous instruction at IP = 538: MOV R0,R16
Mode: KERNEL 	 PID: -1
Next instruction at IP = 540, Page No. = 1: JMP 514
debug> s
Previous instruction at IP = 540: JMP 514
Mode: KERNEL 	 PID: -1
Next instruction at IP = 514, Page No. = 1: MOV R16,10
debug> s
Previous instruction at IP = 514: MOV R16,10
Mode: KERNEL 	 PID: -1
Next instruction at IP = 516, Page No. = 1: GE R16,R0
debug> s
Previous instruction at IP = 516: GE R16,R0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 518, Page No. = 1: JZ R16,542
debug> s
Previous instruction at IP = 518: JZ R16,542
Mode: KERNEL 	 PID: -1
Next instruction at IP = 520, Page No. = 1: MOV R16,R0
debug> s
Previous instruction at IP = 520: MOV R16,R0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 522, Page No. = 1: MOD R16,2
debug> s
Previous instruction at IP = 522: MOD R16,2
Mode: KERNEL 	 PID: -1
Next instruction at IP = 524, Page No. = 1: MOV R17,0
debug> s
Previous instruction at IP = 524: MOV R17,0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 526, Page No. = 1: NE R16,R17
debug> s
Previous instruction at IP = 526: NE R16,R17
Mode: KERNEL 	 PID: -1
Next instruction at IP = 528, Page No. = 1: JZ R16,534
debug> s
Previous instruction at IP = 528: JZ R16,534
Mode: KERNEL 	 PID: -1
Next instruction at IP = 534, Page No. = 1: MOV R16,R0
debug> s
Previous instruction at IP = 534: MOV R16,R0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 536, Page No. = 1: ADD R16,1
debug> s
Previous instruction at IP = 536: ADD R16,1
Mode: KERNEL 	 PID: -1
Next instruction at IP = 538, Page No. = 1: MOV R0,R16
debug> s
Previous instruction at IP = 538: MOV R0,R16
Mode: KERNEL 	 PID: -1
Next instruction at IP = 540, Page No. = 1: JMP 514
debug> s
Previous instruction at IP = 540: JMP 514
Mode: KERNEL 	 PID: -1
Next instruction at IP = 514, Page No. = 1: MOV R16,10
debug> s
Previous instruction at IP = 514: MOV R16,10
Mode: KERNEL 	 PID: -1
Next instruction at IP = 516, Page No. = 1: GE R16,R0
debug> s
Previous instruction at IP = 516: GE R16,R0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 518, Page No. = 1: JZ R16,542
debug> s
Previous instruction at IP = 518: JZ R16,542
Mode: KERNEL 	 PID: -1
Next instruction at IP = 520, Page No. = 1: MOV R16,R0
debug> s
Previous instruction at IP = 520: MOV R16,R0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 522, Page No. = 1: MOD R16,2
debug> s
Previous instruction at IP = 522: MOD R16,2
Mode: KERNEL 	 PID: -1
Next instruction at IP = 524, Page No. = 1: MOV R17,0
debug> s
Previous instruction at IP = 524: MOV R17,0
Mode: KERNEL 	 PID: -1
Next instruction at IP = 526, Page No. = 1: NE R16,R17
debug> s
Previous instruction at IP = 526: NE R16,R17
Mode: KERNEL 	 PID: -1
Next instruction at IP = 528, Page No. = 1: JZ R16,534
debug> s
Previous instruction at IP = 528: JZ R16,534
Mode: KERNEL 	 PID: -1
Next instruction at IP = 530, Page No. = 1: BRKP
debug> s
Previous instruction at IP = 530: BRKP
Mode: KERNEL 	 PID: -1
Next instruction at IP = 532, Page No. = 1: JMP 534
debug> c
Previous instruction at IP = 530: BRKP
Mode: KERNEL 	 PID: -1
Next instruction at IP = 532, Page No. = 1: JMP 534
debug> c
Previous instruction at IP = 530: BRKP
Mode: KERNEL 	 PID: -1
Next instruction at IP = 532, Page No. = 1: JMP 534
debug> c
Machine is halting.

```

