# Learning the SPL language

Use the SPL language to write a small _OS startup code_ and generate target using the SPL compiler.

SPL (Systems Programming Language) allows high level programs to be written for the XSM machine (eliminating the need to write all the code in assembly language). SPL is not a full fledged programming language, but is an extension to the XSM assembly language with support for high level constructs like if-then-else, while-do etc. Programs written in SPL language needs to be compiled to XSM assembly code using the SPL compiler supplied along with the eXpOS package before loading for execution on the XSM simulator. You will be writing the eXpOS kernel using the SPL language.

creating a .spl file 

```
┌──(ajay㉿kali)-[~/myexpos/spl/spl_progs]
└─$ cat oddnos.spl     
alias counter R0;
counter = 0;
while(counter <= 20) do
  if(counter%2 != 0) then
    breakpoint;
  endif;
  counter = counter + 1;
endwhile; 

```

compiling the spl file 

```
cd $HOME/myexpos/spl
./spl $HOME/myexpos/spl/spl_progs/oddnos.spl
```

loading and executing the file

```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# load --os $HOME/myexpos/spl/spl_progs/oddnos.xsm

```


```
┌──(ajay㉿kali)-[~/myexpos/xsm]
└─$ ./xsm 
1
3
5
7
9
11
13
15
17
19
Machine is halting.

```

