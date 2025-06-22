# Basics of Functions

Functions allow us to turn our code into modules, improve script organisation and enhance readability.

Structure of a function

```
1 #!/bin/bash
2 function_name () { 
3  # code block to be executed is between the curly bracket
4 }
5 function_name [here you have to call the function]
```

Example:

```
Vim function.sh
1 #!/bin/bash
2 hello_world () {
3 echo “hello world”
4 }
5 hello_world
Result: hello world
```

We are going to use Parameters with local variable called name in this functions 

```
Vim function1.sh
1 #!/bin/bash
2 greet_person() {
3  local name=”$1” #make sure to have the parameter in speech marks
4 echo “Hello, $name”
5 }
6 greet_person “$1”
./function1.sh endrit
Hello, endrit
```

---

# Parameters (positional and special)

There are 2 types of parameters 
- Positional 
- Special

Positional parameters are parameters in a position, eg - $0 prints the name of the scripts, $1 is the first amendment (the 1st parameter) and so on

Special parameters are ones without a position but give you information about the parameters

- `$@` lists all the parameters / arguments
- `$#` states the number of parameters / arguments

E.g

```
vim arguments.sh
1 #!/bin/bash
2 print_arguments() {
3      echo "Number of arguments: $#"
4       echo "Script name: $0"
5       echo "First argument: $1"
6       echo "Second argument: $2"
7      echo "All arguments: $@"
8  }
9 # Call the function and pass all script arguments to it
10 print_arguments "$@"
Chmod +x arguments.sh
./arguments.sh "Alice" "Bob"
Result is:
Number of arguments: 2
Script name: ./2arguments.sh
First argument: Alice
Second argument: Bob
All arguments: Alice Bob
```
