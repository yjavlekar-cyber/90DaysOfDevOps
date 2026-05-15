#Day 21 – Shell Scripting Cheat Sheet: Build Your Own Reference Guide.
  #Task 1-Basics
  1.Shebang (#!/bin/bash) — Shebang should be used on the top of shell script so that the script could identify what type of shell we are using.
  
  2.Running a script chmod +x - In order to execute the shell script we first need to modify its permission to executable before running it can be done by using chmod +x script.sh.
  
 3. Comments — single line (#) and inline- In a script in order to explain or to define certain logics we can use comments which are used with # when we start the comment from the start of the line it is called full line comment and if in between
  of the line it is called in-line comment.
  There is also another type of comment which is called Multi-line comment which starts with delimeter followed by two redirection operators and and two same words whatever we will right in between those two words will be ignored by the script.
  
  4.Variables — declaring, using, and quoting ($VAR, "$VAR", '$VAR')-In a script instead of hard-codding we assign the values to certain variables so that whenever if we want to change anything we can just change the values of those variables.
              *declaring a avriable is basically assigning a value to a variable by using = operator.
              *using and qouting- This means using the variable which was earlier declared inside our logic with qouting so that the output doesn't breaks.
              
  5.Reading user input — read we can use read or read -p to take user input in simple terms we will take the user input using read and we can use that further in our logic.
  
  6.Command-line arguments — $0, $1, $#, $@, Arguments can be easily defined as number of words in a command in linux in a shell script we can use arguments by assigning numbers like $1 $2 which basically will fetch or use the arguments which we will put 
  while running the script for e.g ./script.sh sample.log (In this ./script.sh is argument $0 and sample.log $1).
  Basically arguments are numbering or positioning of input given to the shell to execute.

  #Task 2: Operators and Conditionals:

  1.String comparisons (=, !=, -z, -n)-
  
  Integer comparisons (-eq, -ne, -lt, -gt, -le, -ge)
  
  File test operators (-f, -d, -e, -r, -w, -x, -s)
  if, elif, else syntax
  Logical operators — &&, ||, !
  Case statements — case ... esac
