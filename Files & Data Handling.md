# User Inputs

User input allows our scripts to interact with the users and make them more dynamic and responsive

Command read = capture the users input 

```
Vim userinput.sh
1 #!/bin/bash
2 greet_user() {
3 	echo “What is your name?”
4	read name
5	echo “Hello $name”
6 }
7 greet_user
Chmod +x userinput.sh
userinput.sh
Result:
What is your name?
[you respond] Max
Hello Max
```

# Handling Bad Data

Bad data is invalid or unexpected user inputs that may cause errors or undesired behavior in our scripts.

By implementing proper error handling techniques, we ensure our function handle bad data and provide informative feedback to the user


One way we can do this is using conditional statements to check the validity of the input 

Example, the first if makes sure that the answer is a number, if it is not the echo invalid age will appear and will return back to the start:

`=~ ^[0-9]+$` command makes sure the argument is a number.

`${input//[^a-zA-Z0-9]/}` command makes sure the argument / answer is a letter or number (no special characters).

We return 1 (a non 0 exit code) suggesting we have encountered an error (made the if statement at the bottom)

```
vim validateage.sh
1 validate_age() {
2  local age=$1
3
4    if [[ ! $age =~ ^[0-9]+$ ]]; then
5        echo "Invalid age. Please provide a numeric value."
6        return 1
7    fi
8
9    if (( age < 18 )); then
10        echo "Sorry, you must be at least 18 years old."
11        return 1
12    fi
13
14    echo "Congratulations! You are eligible."
15    return 0
16 }
17
18 echo “Please enter your age: “
19 read user_age
20 validate_age “$user_age”
21 exit_code=$?
22 if (( exit_code != 0 )); then
23 echo “Input validation failed”
24 else
25 echo “Validation passed”
26 fi

./ validateage.sh
Please enter your age:
19
Congratulations! You are eligible.
Validation passed
```

# Piping

The pipe symbol is `|` 

Piping (within functions) allows us to store variables. Piping allows us to pass the output of one command as input to another. It also allows us to connect commands and pass the output of one command as input to another. 

Example:

```
1 #!/bin/bash
2 get_file_count() {
3 	Local directory=”$1”
4	  Local file_count
5 file _count=$(ls “$directory” | wc -l)
6 Echo “Number of files in $directory: $file_count”
7 }
8 get_file_count "./"     # "./" is current directory
```
Depending where we run this function we will get the number of files , the perimeter in this script is the current direcoty ./
