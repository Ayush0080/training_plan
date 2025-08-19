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

## 

 





