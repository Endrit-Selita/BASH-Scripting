# Variables

They are an essential part of bash scripting as they allow you to store and manipulate data
- This makes your scripts dynamic and flexible 
- They are like containers that hold data like: texts, strings, numbers and arrays.
- They provide a way to store values that can be accessed and modified throughout the script

To create a variable you assign a value to it using the assignment operator (the = sign)
Then when referencing the variable in the script you put a dollar sign infront - $variable

E.g:
```
Vim var.sh
1 #!/bin/bash 
2
3 greeting=’Hello World’
4 count=42
5 fruits=(“apple”, “banna”, “orange”)
6 name=”Max”
7
8 echo “Hello, $name” [this will say hello to the variable name which we made max]
9 echo $greeting
10 echo $count
11 echo $fruits
:wq!
sudo chmod +x var.sh
./var.sh
“Hello, ”Max””
Hello World
42
“apple”,
```

---

# Parameters

These are input values/arguments. By allowing input in the command line you can make your script more versatile, interactive and customisable. 

You always provide parameters after the script name, separated by spaces 
Example: `./script.sh parameter1* parameter 2`
In vim they are referenced with the dollar sign and number

E.g
```
vim script.sh
1 #!/bin/bash
2
3 echo “Parameter 1: $1”
4 echo “Parameter 2: $2”
5 echo “Parameter 3: $3”
:wq!
sudo chmod +x script.sh
./script.sh word1 word2
Parameter 1: word1
Parameter 2: word2
Parameter 3:
```

As you can see, where we referenced parameter 1 and 2 after the script name, they showed up in replacement of the dollar sign $1 and $2, $3 is left blank because we didn't input a parameter for it

If you want all parameters in one signal command, it is $@

E.g 
```
vim script.sh
1 #!/bin/bash
2
3 echo “Parameter 1: $1”
4 echo “Parameter 2: $2”
5 echo “Parameter 3: $3”
6
7 echo “All Parameters: $@”
:wq!
sudo chmod +x script.sh
./script.sh word1 word2 word3
Parameter 1: word1
Parameter 2: word2
Parameter 3: word3
All Parameters: word1 word2 word3
```

---

# Arithmetic Expansion

BASH allows us to perform mathematical calculations and evaluate expressions using the dollar and double parentheses notation $(( ))
Within this we can perform arithmetic calculations which make our scripts more flexible and dynamic

E.g
```
Vim math1.sh

1 #!/bin/bash
2
3 num1=5
4 num2=10
5 
6 result=$((num1 + num2))
7
8 echo “The sum of $num1 and $num2 is: $result”
:wq!

sudo chmod +x var.sh
./math1.sh
The sum of 5 and 10 = 15
```

The $ dollar signs are really important so it knows to reference the variables

---

# Arithmetic Expansion with Parameters

This allows you to provide any input and make it more dynamic

E.g
```
Vim math2.sh
1 #!/bin/bash
2
3 num1=$1
4 num2=$2
5 
6 result=$((num1 + num2))
7
8 echo “The sum of $num1 and $num2 is: $result”
:wq!

sudo chmod +x var.sh
./math1.sh 13 36
The sum of 13 and 36 = 49
```

If you wanted something a bit more complicated, you can make it work out the area and perimeter of a rectangle

E.g
```
Vim math3.sh
1 #!/bin/bash
2
3 length=$1
4 width=$2
5 
6 area=$((length * width))
7 perimeter=$((2 *(length + width))
8 
9 echo “Rectangle area: $area”
10 echo “Rectangle perimeter: $perimeter”
:wq!
sudo chmod +x var.sh
./math2.sh 7 9
Rectangle area: 63
Rectangle perimeter: 32
```
