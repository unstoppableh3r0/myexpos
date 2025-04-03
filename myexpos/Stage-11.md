
# Introduction to Expl

```
┌──(arjun㉿arjun)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface  
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# load --init ../expl/expl_progs/numbers.xsm
File ../expl/expl_progs/numbers.xsm not found.
# ^[[200~load --init ../expl/samples/numbers.xsm
Unknown command "load". See "help" for more information.
# ~load --init ../expl/samples/numbers.xsm
Unknown command "~load". See "help" for more information.
# load --init ../expl/samples/numbers.xsm
# ^[[200~load --int=10 ../spl/spl_progs/haltprog.xsm
Unknown command "load". See "help" for more information.
# load --int=10 ../spl/spl_progs/haltprog.xsm
# load --exhandler ../spl/spl_progs/haltprog.xsm
# load --os ../spl/spl_progs/os_startup.xsm
# load --library ../expl/library.lib
# ^[[200~load --int=timer ../spl/spl_progs/timer.xsm
Unknown command "load". See "help" for more information.
# load --int=timer ../spl/spl_progs/timer.xsm
# load --int=7 ../spl/spl_progs/print.xsm
# exit
```

```
┌──(arjun㉿arjun)-[~/myexpos/xsm]
└─$ ./xsm --timer 0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
Machine is halting.
```