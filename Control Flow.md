# if Statements

If statements allow you to introduce decision making logic into your scripts, execute different code blocks based on specific conditions.They allow you to control the flow of your scripts based on the results.

An if statement starts with if and ends in fi and the code block that needs to be executed will be between the then and fi so if the condition is true the code block will be executed

If statements are used using comparison operators: eq = equals, ne = not equal to, lt = less than, gt = greater than, le = less than or equal to, ge = greater than or equal to, && = and, || = or, == = equals to, != = does not equal to

Structure of if statement in BASH:
```
Vim if.sh
1 #!/bin/bash
2
3 if [ condition 1 ] && [ condition 2 ] # (use square brackets with space at start and end)
4 then
5 # code block to be executed if both conditions met
6 fi
```

Example of if statement:
```
Vim if.sh
1 #!/bin/bash
2
3 age=25
4 
5 if [ $age -gt 18 ]
6 then
7 echo “You are an adult”
8 fi
```
---

# else and elif

## else

The else clause allows an alternative code block to be executed when the if condition evaluates to false. It provides an alternative path to your scripts flow offering flexibility and versatility.

```
Vim if.sh
1 #!/bin/bash
2
3 if [ condition 1 ] && [ condition 2 ]
4 then
5 code block to be executed if condition is true
6 else
7 code block to be executed if condition is false
8 fi
```

Example of if statement with else:
```
Vim if.sh
1 #!/bin/bash
2
3 age=15
4 
5 if [ $age -gt 18 ]
6 then
7 echo “You are an adult”
8 else
9 echo “You are not an adult”
10 fi
:wq!
sudo chmod +x if.sh
./if.sh
You are not an adult
```

## elif
You can add multiple if statements with elif

Example of if statement with elif:
```
Vim if.sh
1 #!/bin/bash
2
3 score=85
4 
5 if [ $score -ge 90]
6 then
7 echo “Excellent”
8 elif [ $score -ge 80 ]
9 then
10 echo “Good”
11 else
12 echo “You need to try again”
13 fi
:wq!
sudo chmod +x if.sh
./if.sh
Good
```

---

# Nested if Statements

Nested if statements allow us to create more complex decision making structures by imbedding if statements within other if statements 

Also, after the condition, instead of entering then on a new line, you can add a semicolon and add then

Example, if you qualify to get into 6th form based on age and grade:

```
Vim if.sh
1 #!/bin/bash
2 age=$1
3 grade=$2
4 if [ $age -gt 18 ]; then
5 echo “You are eligible based on age”
6	if [ $grade -ge 80 ]; then
7	echo “You are eligible based on your grade”
8	echo “Congrats! You are eligible”
9	else
10	echo “ Sorry your grade is not high enough”
11	fi
12 else
13 echo “Sorry you are not eligible”
14 fi
If age is 18 or under you will get “Sorry you are not eligible”
if your grades are under 80 “You are eligible based on age, Sorry your grade is not high enough”
if age and grades are 19 and 80 then “You are eligible based on age, You are eligible based on your grade, Congrats! You are eligible”
If age and grades are 18 and 79 you will get “Sorry you are not eligible”
```

---

# while Loops

While loops allow you to repeatedly execute a block of codes as long as a certain condition remains true. They provide a powerful tool for automating tasks and iterating over data.
++ = it adds 1 for each iteration of this while loop

The structure of a while looping bash
```
1 #!/bin/bash
2 while [ condition ]
3 do 
4 code to be executed
5 done
```

Example, increase count by 1 until it becomes less then or equal to 5:

```
Vim count.sh
1 #!/bin/bash
2 count=1
3 while [ $count -le 5 ]
4 do
5 echo  “Count: $count”
6 ((count++))
7 done
:wq!, chmod +x count.sh, ./count.sh
“Count: 1”
“Count: 2”
“Count: 3”
“Count: 4”
“Count: 5”
```

Example that uses array, we have an array called fruits with 3 elements: apple, banana and orange. Then it starts a while loop that iterates over the arrays elements, within each iteration it prints the current fruit and increments the index variable by 1. The loop continues until all the elements in the array have been processed.

```
Vim arraywhile.sh
1 #!/bin/bash
2 fruits=(“apple” “banana” “orange”) #make sure there is a space between the elements
3 index=0
4 while [ $index -lt ${#fruits[@]} ] #@ means to display all of them
5 do
6 echo “Fruits: ${fruits[$index]}”
7 ((index++))
8 done
:wq!, chmod +x arraywhile.sh, ./arraywhile.sh
“Fruits: “apple””
“Fruits: “banana””
“Fruits: “orange””
```

---

# for Loops

for loops allows you to iterate over a sequence of values and perform repetitive tasks. 
They enable you to repeat a block of code for a specified number of iterations over a sequence of values.

They start with the keyword for then followed by: a variable in sequence, then do, the code block to be executed and then finish with done. 
; semicolon is used to separate commands
The structure of a for loop:

```
1 #!/bin/bash
2 for variable in sequence
3 do
4 code block to be executed
5 done
```

Example: 
```
Vim forloop.sh
1 #!/bin/bash
2 for (( i=1; i<=5; i++ )) #this means for i equals one, less or equal to 5 then add 1 to i
3 do
4 echo “Number: $i”
5 done
:wq!, chmod +x forloop.sh, ./forloop.sh
“Number: 1”
“Number: 2”
“Number: 3”
“Number: 4”
“Number: 5”
```

## Example with array:

```
Vim forlooparray.sh
1 #!/bin/bash
2 fruits=(“apple” “banana” “orange”)
3 for fruits in “${fruits[@]}”
4 do
5 echo “Fruits: $fruit”
6 done
“Fruits: ““apple””
“Fruits: “banana””
“Fruits: “orange”””
```

## Example of sequence:

```
1 #!/bin/bash
2 for number in $(seq 1 5) #sequence command will generate number from 1 to 5
3 do
4 echo “Number: $number”
5 done
“Number: 1”
“Number: 2”
“Number: 3”
“Number: 4”
“Number: 5”
```
---

# Break and Continue

Break and continue are control statements provide additional control within for and while loops allowing you the flexibility to interrupt a loop or skip iterations based on specific conditions

The break statement immediately exits the innermost loop it's displaced regardless of the loop's condition.

Example, this would go up to number 5, but the break statement means it stops when i is equal to 3:

```
1 #!/bin/bash
2 for (( i=1; i<=5; i++ ))
3 do
4 if [ $i -eq 3 ]
5 then
6 break
7 fi
8 echo "number: $i"
9 done
Result:
Number: 1
Number: 2
```

The continue statement skips the innermost loop

Example, this would go from 1 to 5, but the continue statement means it skips when i is equal to 3:

```
1 #!/bin/bash
2 for (( i=1; i<=5; i++ ))
3 do
4 if [ $i -eq 3 ]
5 then
6 continue
7 fi
8 echo "number: $i"
9 done
Result:
Number: 1
Number: 2
Number: 4
Number: 5
```

Break and continue can be used in while loops as well

This is saying do echo count: 1 ++ but with an if statement  inside which says when count i sequel to 4 break

```
1 #!/bin/bash
2 count=1
3 while true
4 do
5 echo “Count: $count”
6 ((count++))
7 if [ $count -eq 4 ]
8 then
9 break
10 fi
11 done
Result:
Count: 1
Count: 2
Count: 3
```

In this script, when the count is equal to 3 we just increment it by 1 without actually printing it out

```
1 #!/bin/bash
2 count=1
3 while [ $count -le 5 ]
4 do 
5 	if [ $count -eq 3 ]
6 	then
7 	((count++))
8 	continue
9 	fi
10 echo “count: $count”
11 ((count++))
12 done
Result:
Count: 1
Count: 2
Count: 4
Count: 5
```
