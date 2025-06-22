# Introduction to Error Handling

Error handling in scripts is about foreseeing where things can go wrong and taking appropriate measures to handle those situations rather than letting the script crash or even worse, continue in an erroneous state. This makes your scripts more trustworthy and saves a lot of time.

e.g:

```
1 #!/bin/bash
2
3 num1=10
4 num2=0
5
6 if [ $num2 -eq 0 ]; then
7 echo "Error: Division by zero is not allowed"
8 exit 1
9 fi
10
11 result=$((num1/num2))
12
13 echo "The result is: $result"
```

Now when we run the script and we divide by 0 instead of the script crashing it will let us know that we can not divide by 0

---

## if Statements Recap for Error Handling

```
1 #!/bin/bash
2
3 FILE="/nonexistent"
5
5 if [[ -f "$FILE" ]]; then
6 	echo "File exists."
7 else 
8  	echo "File does not exist."
9 fi
```

-f checks if a file exists, so we check if the **parameter FILE** exists and if it does not instead of the script crashing the error handling tells us that the file does not exist 

---

# Exit Codes

Whenever a command or script ends, it returns an exit code to the system. This is a numerical value that represents whether the command or script completed successfully or not. In general an exit code of 0 indicates success and any non zero exit code indicates an error.


To check the exit code of the last executed command: `echo $?`


You can use them in if statements in scripts, if it is wrong then you add exit 1 under what to echo if the if statement is not correct

---

# set -e

set -e is a set command used in error handling. When included at the start of the script, the script will stop executing as soon as any command returns a non-zero exit code. 

Example:

```
1 #!/bin/bash
2
3 set -e
4
5 echo "Before the script"
6
7 non_existent_command
8
9 echo "After the script"
```

When executed, this script will run:
```
Before the script
Non_existent_command: command not found
```

It stopped executing when it found an error due to set -e

However, not all non-zero exit codes are errors that should stop your script. Sometimes you might expect a non- zero exit code and want your script to continue in those cases you wouldn't set -e.

---

# set -u

set -u is a set command used in error handling. It forces a bash script to stop if it encounters an uninitialised/undefined variable. It helps you prevent scenarios where missing data could lead to incorrect results or unexpected behavior.

Example: 

```
1 #!/bin/bash
2
3 set -u
4 X=10
5 Y=20
6 Z=$((X +Y +W))
7 echo “Z equals: $Z”
When executed, this script will run:
line 6: W: unbound variable 
```

It prevents your scripts from running into problems due to missing data

---

# set -x

set -x is a set command used in error handling/debugging. This prints out each command that will be executed to the terminal before it is actually executed.

Example:

```
vim setx.sh
1 #!/bin/bash
2
3 set -x
4 echo "starting the script"
5 x=10
6 y=20
7 z=$((x + y))
8 echo "the value of z is: $z"

./setx.sh

+ echo 'starting the script'
starting the script
+ x=10
+ y=20
+ z=30
+ echo 'the value of z is: 30'
starting the script
the value of z is: 30
```

Set -x printed out each command before it executed the script. Once you are done debugging you can disable the option by adding set +x at the end of the script, which is very useful if you just want to debug a certain part of a script.

---

# set -eux

BASH allows all 3 commands to be used at once. This will stop the script if there is an:
- Error (-e)
- Undefined variable (-u)
- Print out each command (-x)

This will work in the same way as before, stopping at the first error of uninitialised variable while listing out the commands before execution 


Though combining these options can be very helpful. It should be done thoughtfully considering the specific requirements and context of your script.

---

# More Set Commands

`set -o nounset`
- This works in the same way as set -u

`set -o errexit`
- This works in the same way as set -e

`set -o pipefail`
- This causes the pipeline to return the exit status of the last command in the pipeline that exited with a non-zero status (error code). This is really useful when you are piping commands together.

Example:

```
1 #!/bin/bash
2
3 set -o pipefail
4
5 cat non_existanat_file | grep “something”
```

When executed:
`cat: non_existanat_file: no such file or directory`

It stopped the script where the pipeline returned a non-zero exit code and didnt even allow the grep to run so we know where the problem is.

