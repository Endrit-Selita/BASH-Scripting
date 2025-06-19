# **Introduction to bash scripting**

**Bash**: A command-line tool to interact with your computer.

**Bash Script**: A file containing a series of commands you want the computer to execute automatically.

## Why Learn It?

- **Automate tasks**: Save time on repetitive actions.
- **Manage systems**: Handle files, software installs, and system configurations.
- **Boost efficiency**: Get more done with less typing!

**Run Your Script**:

- - Make it executable: `chmod +x your_script.sh` (You learn this in the Linux Module)
    - Run it: `your_script.sh`

## Basic Concepts

- **Variables**:
  - Store values: name="Ahmed"
  - Use them: echo "Hello, $name"
- **Comments**:
  - Add explanations with #.  
        Example: # This line says hello
- **Conditionals**:
  - Make decisions with if statements.  
        Example:  
        if \[ $name == "Alice" \]; then echo "Hi Alice!" fi
- **Loops**:
  - Repeat actions with for or while.  
        Example:  
        for i in 1 2 3; do echo "Number $i" done
- **Functions**:
  - Group commands for reuse.  
        Example:  
        greet() { echo "Hello, $1!" } greet "Alice"
- **User Input**:
  - Get input from users.  
        Example:  
        read -p "Enter your name: " name echo "Hello, $name!"

# Bash Scripting

Command `touch _xyz_.sh` \= make a script, remember it is .sh at the end, not .txt

Then open your script with `vim _xyz_.sh`

Save and exit with `:wq!`

Scripts need to be executable so change the permission with `chmod +x scriptname`

To execute type `./filename.sh` or `sh filename.sh` or `bash filename.sh` (if you didn't specify bash in the script)

The 1st line is ALWAYS `#!/bin/bash` **(The shebang)**

A basic example is:

```
touch script1.sh

vim script1.sh

1 #!/bin/bash

2

3 echo “hello world”

:wq!

chmod +x script1.sh
# Command: **chmod +x script1.sh** (change so the script is executable - can check ls -l to check it has x for all 3 users)

./script1.sh
# Command: **./script1.sh** (./ allows us to execute the script)

hello world

```

The shebang **(#!/**bin/bash) is basically telling the script to interpret all lines after with binary bash. The path after the exclamation mark is essentially pointing to the specific interpreter or SHELL that should handle the script. This allows consistency when running scripts, even if you are on a different shell, e.g using zsh, because of the shebang. If you didn't have it you can use bash instead of ./ to make it interpret it in bash.

- E.g If you are writing a python 3 script it would be #!/usr/bin/python3

# **Comments**

Comments are lines in the script that are not executed part of the code, but as informative text for us reading the script. This is considered a best practice because it helps you and others understand the purpose, functionality, and logic of the script.

There are single line and multi line comments

Single line comments: start with **#** - space - then whatever is written after will be treated as a comment

Multi line comments are between **single quote marks**:

Start with: ’ *space* **comment** and end with **‘ single quote marks**

- When you execute the script it doesn't bring up the comments, you must use **cat script1.sh**

# **Running Scripts from ANYWHERE!**

We run the scripts from its current directory using the ./. However, what if we wanted to run it from anywhere without specifying its path? The trick here to:

Place the script in one of the PATH environment variables

- They tell the shell which directories to search in for executable files in response to commands

Type **echo $PATH** to bring up directories that can be run and executed from anywhere in the terminal, they are between TWO COLONS

- To move this to the directory (e.g /usr/local/bin) **sudo mv script1.sh /usr/local/bin/script1** it will then ask you for your password
- Then change the permission to executable by **chmod +x /usr/local/bin/greet**
- The **script1** at the end changes the name so it is easier for people to execute
- Now when you run the command **script1** it will say Hello World no matter where you are in the terminal
