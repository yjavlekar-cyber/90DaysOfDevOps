#Day 21 – Shell Scripting Cheat Sheet: Build Your Own Reference Guide.
  #Task 1-Basics
  1.Shebang (#!/bin/bash) — Shebang should be used on the top of shell script so that the script could identify what type of shell we are using.
  
  2.Running a script chmod +x - In order to execute the shell script we first need to modify its permission to executable before running it can be done by using chmod +x script.sh.
    e.g chmod +x backup.sh
  
  3.Comments — single line (#) and inline- In a script in order to explain or to define certain logics we can use comments which are used with # when we start the comment from the start of the line it is called full line comment and if in between
  of the line it is called in-line comment.
        e.g #This is a full line comment.
            echo "comment" # this is inline comment.
  There is also another type of comment which is called Multi-line comment which starts with delimeter followed by two redirection operators and and two same words whatever we will right in between those two words will be ignored by the script.
        e.g :>>'comment'
              this is a 
              multiline.
              comment
  4.Variables — declaring, using, and quoting ($VAR, "$VAR", '$VAR')-In a script instead of hard-codding we assign the values to certain variables so that whenever if we want to change anything we can just change the values of those variables.
              *declaring a avriable is basically assigning a value to a variable by using = operator.
              e.g name=yogesh
              *using and qouting- This means using the variable which was earlier declared inside our logic with quoting so that the output doesn't breaks.
              e.g echo "$name"
  5.Reading user input — read we can use read or read -p to take user input in simple terms we will take the user input using read and we can use that further in our logic.
              e.g read -p "Enter your name:"name
                    echo "my name is $name"

  6.Command-line arguments — $0, $1, $#, $@, Arguments can be easily defined as number of words in a command in linux in a shell script we can use arguments by assigning numbers like $1 $2 which basically will fetch or use the arguments which we will put 
              while running the script for e.g ./script.sh sample.log (In this ./script.sh is argument $0 and sample.log $1).
              Basically arguments are numbering or positioning of input given to the shell to execute.
              e.g In a shell we have the following script:
              if [ "$1" = "yogesh" ];then
                    echo "Hello yogesh"
              As in the above script we have an argument which is $1 means the input after the script name
              so if we run our script ./script.sh yogesh
            this will print Hello yogesh.

  #Task 2: Operators and Conditionals:

  1.String comparisons (=, !=, -z, -n)- String comparisons are used to verify if the string is same(=),different(!=),empty(-z) or not empty(-n).
          	#!/bin/bash
            if [ "$1" = "yogesh" ];then
                    echo "Hello yogesh"
  2.Integer comparisons (-eq, -ne, -lt, -gt, -le, -ge)- To compare the integers in our logic we can use integer comparison.
            Suppose we have logic where if the total number of arguments are zero it should print something we will use this because we are dealing with integers.
            e.g if [ $# -eq 0 ];then
              echo "No arguments."

  3.File test operators (-f, -d, -e, -r, -w, -x, -s)-This operators are used for the operations related to files or directories for eg -f denotes is it a regular file,-d is it a directory,-e represents is the file exist at all.
             e.g if [ -f "script.sh" ];then
                      echo "File exists"
                  fi
                This basically uses -f to check wether it is a regular file or not.

  4.if, elif, else syntax- If else is used to put certain conditions and if those conditions are fullfilled certain activites should be carried out.
              the synatx of if else is below
                  if [ ou logic ];then
                        echo "echo or whetever activity we want to carry out"
                  else
                  elif
                  fi

  5.Logical operators (&&, ||, !)-&&= if this is used in between two commands if the first commands succeeds then second command will run.
                                    e.g mkdir new-project && cd new-project
                                  ||= If the first command fails means there is no output then only the second command will run.
                                    e.g grep "error" file.log || echo "no error"
                                  != This basically reverted the exit status success into failure and failuer into success.
                                    e.g if [ ! -f "file.log ];then
                                                echo "File doesn't exist"
                                      usually -f searched for the regular file but ! infront of it even if the file exist it will revert the result.
  6.Case statements — case ... esac-this is basically like using if else condition multiple times in here we can use the variable against multiple patterns.
                                        e.g#!/bin
                                            echo "Enter your favourite fruit:"
                                             read fruit
                                            
                                             case "$fruit" in
                                                      "apple")
                                                    echo "Apples are great for health."
                                                    ;;
                                                    "banana" | "plantain")
                                                    echo "Bananas provide instant energy."
                                             esac
