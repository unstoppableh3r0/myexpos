# Understanding the systems

Load/retrieve data and executable files from/to your host (Unix) system into the XSM disk.
Explain the disk data structures of the XFS file system - INODE table, disk free list and root file.
Find out the data blocks into which a data/executable file is stored in the XSM disk by examining the INODE table and root file.



```
┌──(ajay㉿kali)-[~/myexpos/xfs-interface]
└─$ ./xfs-interface 
Unix-XFS Interace Version 2.0. 
Type "help" for getting a list of commands.
# fdisk 
Formatting Complete. "disk.xfs" created.
# exit

```


```
0 	 - 	 1  
1 	 - 	 1  
2 	 - 	 1  
3 	 - 	 1  
4 	 - 	 1  
5 	 - 	 1  
6 	 - 	 1  
7 	 - 	 1  
8 	 - 	 1  
9 	 - 	 1  
10 	 - 	 1  
11 	 - 	 1  
12 	 - 	 1  
13 	 - 	 1  
14 	 - 	 1  
15 	 - 	 1  
16 	 - 	 1  
17 	 - 	 1  
18 	 - 	 1  
19 	 - 	 1  
20 	 - 	 1  
21 	 - 	 1  
22 	 - 	 1  
23 	 - 	 1  
24 	 - 	 1  
25 	 - 	 1  
.
.
.
No of Free Blocks = 443
Total no of Blocks = 512

```

Creating a file in your UNIX machine with sample data

```
┌──(ajay㉿kali)-[~/myexpos]
└─$ cat sample.dat 
There is a place where the sidewalk ends
And before the street begins,
And there the grass grows soft and white,
And there the sun burns crimson bright,
And there the moon-bird rests from his flight
To cool in the peppermint wind.

```

Now check the Inode table entry for the file sample.dat in the UNIX file inode_table.txt and find the block numbers of its data blocks. The contents of the file inode_table.txt will be as follows:

```
# copy 3 4 $HOME/myexpos/inode_table.txt
```


```
┌──(ajay㉿kali)-[~/myexpos]
└─$ cat inode_table.txt   
1
root
512
0
0
-1
-1
-1
5
-1
-1
-1
-1
-1
-1
-1
2
sample.dat

```

Copy the data blocks from the XFS disk and display it as a UNIX file $HOME/myexpos/data.txt

```
# copy 69 69 $HOME/myexpos/data.txt
```

```
┌──(ajay㉿kali)-[~/myexpos]
└─$ cat data.txt       
There is a plac
e where the sid
ewalk ends
And before the 
street begins,
And there the g
rass grows soft
 and white,
And there the s
un burns crimso
n bright,
And there the m
oon-bird rests 
from his flight


To cool in the 
peppermint wind

```
