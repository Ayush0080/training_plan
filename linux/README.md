# We will learn about linux basic and master command

# command structure - commandName -options inputs
```bash
cal 12 2025 - command=cal inputs= 12, 2025 
```
# cal command use to show calender 
```bash 
cal 12 2025 - command=cal inputs= 12, 2025 
date -u - command=date options= -u
use for short options and -- use for longForm
```
# Short-form Options
 
### Short-form options are where a letter defines an option. Each option is prepended by a dash 
```bash 
commandName –a –b –c args 
```
### To save typing, you could join together the options:
```bash 
commandName –abc args 
```
### Both of these formats are equivalent.

# Command Line Arguments
  
### Command line arguments are a type of input that commands operate on.Some commands can take an unlimited amount of inputs, some take a specific amount, and some take none at all. Consult the manual page for the specific command for more information.
```bash 
cal 12 2017 
```
### Here the cal command has 2 command line arguments. The number 12 and the number 2017.

#  Using the Manual
```bash
man –k <search term> Search the manual for pages 
matching <search term>.
man 5 <page name> Open the man page called <page 
name> in section 5 of the manual. 
(replace <page name> and 5 as 
required)
man <page name> Open the man page called <page 
name> in section 1 of the manual 
```
# redirection 
```bash 
Standard input is stream number o
Standard output is stream number 1
Standard error is stream number 2
cat 1>> output.txt = use to append the content to the file (>>)
cat 1> output.txt = where > will overwrite a file
cat 0>input.txt 1>output.txt - redirect  Standard input to Standard output
```

# Piping
 ### is the connection of the standard output of one command to the standard input ofanother command. Piping using the pipe character (|)
```bash
commandOne –options arguments | commandTwo –options arguments
``` 
#  tee
### The tee command allows us to take a “snapshot” of the data in the pipeline without breaking the pipeline.
```bash
commandOne –options arguments | tee snapshot.txt |commandTwo –options arguments
```
# xargs

### xargs is use to convert standard input to the commnad line argumnet , Piping connects the standard output of one command to the standard input of another command. But what if the second command doesn’t accept standard input? e.g. the echo command.The key is to transform the data coming in, into command line arguments. This is possible using the xargs command
```bash
commandOne –options arguments | xargs echo

 date | xargs echo "hello"
 hello Tue Aug 19 06:31:33 UTC 2025

 date | cut --delimiter=" " --fields=1 | xargs echo
 Tue

 cat filestodelete.txt | rm
 rm: missing operand
 Try 'rm --help' for more information.

 cat filestodelete.txt | xargs rm
```
# Aliases

### Aliases allow you to save your pipelines and commands with easy to remember nicknames so that they can be used later much easier

You define aliases in your .bash_aliases file in your home directory
```bash
cat .bash_aliases
alias getdates='date | tee /home/ubuntu/fulldate.txt | cut --delimiter=" " --fields=1 | tee /home/ubuntu/shortdate.txt | xargs echo hello'

getdates
hello Tue

cat shortdate.txt
Tue

 cat fulldate.txt
Tue Aug 19 07:54:58 UTC 2025

cat .bash_aliases
alias getdates='date | tee /home/ubuntu/fulldate.txt | cut --delimiter=" " --fields=1 | tee /home/ubuntu/shortdate.txt | xargs echo hello'
alias getcal="xargs cal -A 1 -B 1 > /home/ubuntu/calen.txt"
ubuntu@ip-172-31-44-69:~$ alias getcal="xargs cal -A 1 -B 1 > /home/ubuntu/calen.txt"

echo "08 2025" | getcal

 cat calen.txt
                            2025
        July                 August              September
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
       1  2  3  4  5                  1  2      1  2  3  4  5  6
 6  7  8  9 10 11 12   3  4  5  6  7  8  9   7  8  9 10 11 12 13
13 14 15 16 17 18 19  10 11 12 13 14 15 16  14 15 16 17 18 19 20
20 21 22 23 24 25 26  17 18 19 20 21 22 23  21 22 23 24 25 26 27
27 28 29 30 31        24 25 26 27 28 29 30  28 29 30
                      31
```

# Linux File System
 ### File System Navigation
 The Linux File System follows a tree-like structure starting at a base (or root) directory, indicated by the slash (/). 
 Paths that start at the base directory (/) are known as absolute paths.
  ~ its means path of current users home directory

 find full path of current working directory
```bash 
pwd
/home/ubuntu
```

find files and directories and with use of -F differentiate  of the file and directories 

```bash
ls -F
calen.txt  date.txtx  file1.txt          fulldate.txt   input.txt   shortdate.txt  today.txtx
date.txt   error.txt  filestodelete.txt  fulldate.txtx  output.txt  today.txt      training_plan/

 ls
calen.txt  date.txtx  file1.txt          fulldate.txt   input.txt   shortdate.txt  today.txtx
date.txt   error.txt  filestodelete.txt  fulldate.txtx  output.txt  today.txt      training_plan

```

 list file and directories in long format

 ```bash
 ls -l
total 48
-rw-rw-r-- 1 ubuntu ubuntu  569 Aug 19 08:02 calen.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 04:31 date.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 04:29 date.txtx
-rw-rw-r-- 1 ubuntu ubuntu  264 Aug 18 16:49 error.txt
-rw-rw-r-- 1 ubuntu ubuntu  164 Aug 19 09:24 file1.txt
-rw-rw-r-- 1 ubuntu ubuntu    0 Aug 19 07:04 filestodelete.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 07:54 fulldate.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 05:12 fulldate.txtx
-rw-rw-r-- 1 ubuntu ubuntu    7 Aug 18 16:57 input.txt
-rw-rw-r-- 1 ubuntu ubuntu    7 Aug 18 16:57 output.txt
-rw-rw-r-- 1 ubuntu ubuntu    4 Aug 19 07:54 shortdate.txt
-rw-rw-r-- 1 ubuntu ubuntu    4 Aug 19 05:14 today.txt
-rw-rw-r-- 1 ubuntu ubuntu    0 Aug 19 04:57 today.txtx
drwxrwxr-x 4 ubuntu ubuntu 4096 Aug 18 15:09 training_plan
```

 list file and directories in long format with human readable

```bash
 ls -lh
total 48K
-rw-rw-r-- 1 ubuntu ubuntu  569 Aug 19 08:02 calen.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 04:31 date.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 04:29 date.txtx
-rw-rw-r-- 1 ubuntu ubuntu  264 Aug 18 16:49 error.txt
-rw-rw-r-- 1 ubuntu ubuntu  164 Aug 19 09:24 file1.txt
-rw-rw-r-- 1 ubuntu ubuntu    0 Aug 19 07:04 filestodelete.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 07:54 fulldate.txt
-rw-rw-r-- 1 ubuntu ubuntu   29 Aug 19 05:12 fulldate.txtx
-rw-rw-r-- 1 ubuntu ubuntu    7 Aug 18 16:57 input.txt
-rw-rw-r-- 1 ubuntu ubuntu    7 Aug 18 16:57 output.txt
-rw-rw-r-- 1 ubuntu ubuntu    4 Aug 19 07:54 shortdate.txt
-rw-rw-r-- 1 ubuntu ubuntu    4 Aug 19 05:14 today.txt
-rw-rw-r-- 1 ubuntu ubuntu    0 Aug 19 04:57 today.txtx
drwxrwxr-x 4 ubuntu ubuntu 4.0K Aug 18 15:09 training_plan
 ```

 cd (change directorie) 
  ~ = The current user’s home directory
.  = The current folder.
.. = The parent directory of the current 
folder

```bash
cd training_plan/
```
change back to home directory


```bash
~/training_plan$ cd
# go to the base directory
 cd /
```
list out hidden files and directores  

 ```bash
ls -a
.              .bash_history  .cache    .ssh                       calen.txt  error.txt          fulldate.txt   output.txt     today.txtx
..             .bash_logout   .lesshst  .sudo_as_admin_successful  date.txt   file1.txt          fulldate.txtx  shortdate.txt  training_plan
.bash_aliases  .bashrc        .profile  .viminfo                   date.txtx  filestodelete.txt  input.txt      today.txt
 ```



  ### File Extensions

  get file type
```bash
file shortdate.txt
shortdate.txt: ASCII text
```

 ### Wildcard
 Regular expressions are patterns that can be used to match text.

 In Linux, they are used to 
allow a user to make rather generic expressions about what files they want a command to 
operate on. 

Creating regular expressions to match filenames is known as globbing.

The regular expression patterns can be made using special building blocks known as wildcards. 
Wildcards are symbols with specific meanings to the shell.

wildcard and regular expressions are case sensitve.

* = Matches anything, regardless of 
length. 

? =  Matches anything, but for one place 
only.

[options] = Matches any of the options inside 
for 1 place only

```bash
ls *
calen.txt  date.txtx  file1.txt          fulldate.txt   input.txt   shortdate.txt  today.txtx
date.txt   error.txt  filestodelete.txt  fulldate.txtx  output.txt  today.txt

training_plan:
practice

ls f*
file1.txt  filestodelete.txt  fulldate.txt  fulldate.txtx


ls file[123456].txt
file1.txt

ls file[0-9][A-Z][a-z].txt
```

### Creating Files and Directories

creat a new empty file
```bash
touch fileA.txt
```
creat a directory 
```bash
 mkdir folder
```

creat a directory  with path
```bash
  mkdir -p new/folder
```

creat a  multiple directory using single line command with using braces
```bash
mkdir {jan,feb,mar,apr,may}_{20,21,22,23,24}
```

### Deleting Files and Directories
 delete file
 ```bash
  rm fileA.txt
  rm date.txt shortdate.txt
```

delte file using wild card
```bash
 rm file*
 rm *.txt
 rm *2*
 rm *.jpg
 rm *[2,3]*
```

delete directory
```bash
rm -r feb_21/
```
delete directory --interactive(-i) 
```bash
rm -ri defolder/
```
delete empty directory
```bash
 rmdir defolder/*
rmdir: failed to remove 'defolder/folder1': Directory not empty
rmdir: failed to remove 'defolder/folder2': Directory not empty
```

### Copying Files and Directories

copy file

```bash
cp file1.txt file2.txt
```

copy file in to another directory 

```bash
cp file1.txt file2.txt training_plan/
```

copy directory
```bash
cp -r training_plan/practice/  /home/ubuntu/
```

### moving and renaming files and directories

rename the file name 
```bash
mv file1.txt fileA.txt
```
rename the directory name 
```bash
mv new/ new1
```
move file one folder to another folder 
```bash
mv new1/* /home/ubuntu
```

move folder to another folder 
```bash
mv new1/ /home/ubuntu
```

move folder to another folder with chnage of new folder name 
```bash
mv training_plan/new1/ /home/ubuntu/new2
```

### Editing files with Nano

nano configuring file is /etc/nanorc


```bash
nano file1.txt

save file with ctr+o

insert another filr content to current file ctr+r

search word ctr+w

replace using ctr+\
```

