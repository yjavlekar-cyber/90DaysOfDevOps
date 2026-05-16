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
#Task 3: Loops
1. for loop — list-based and C-style-
   for loops are used to iterate or list down the date from a list.
   list-for i in {1..5}
   do
         echo $i
   done
  
   c-style- is used for arithmetic type logics
   for (( num=1 ; num<=10 ; num ++ ))
   do
            echo $num
   done

2. while loop- this is basically a true loop if the logic is true then the command will keep iterating until we stop it.
read -p "enter your number:" number

while [ "$number" -gt 10 ]
do

        echo "Greater"
        exit 1
done
echo "less"

3.Until loop- This is opposite to the while loop it basically false loop it says until this logic is true do this and done infinetly till we stop it.
read -p "enter your number:" number

until  [ "$number" -gt 10 ]
do

        echo "less"
        exit 1
done
echo "greater"


4.Loop control — break, continue
break- In shell scripting break acts as a stop button which gets triggered when the condition is fullfilled just like in below script if you see if the number is greater than 10 it will stop the infinty loop of greater but will also continue to run the next command which is to print less it doesnot stop overall script just the particular condition.
e.g
#!/bin/bash

read -p "enter your number:" number

        while [ "$number" -gt 10 ]
        do
                echo "greater"
                break
        done
echo "less"

continue:This basically skips whichever condition we set from to final output just like in below example we are iterating numbers from 1-5 but there is condition if i is 4 skip it so the output will only give us numbers other than 4.
e.g
#!/bin/bash
for i in {1..5}
do
        if [ $i = 4 ];then
                continue
        fi
        echo $i
done

5.Looping over files- to list down the files we can use belwo script where whetever file type we have mentioned after asteric it will iterate those files just like in below script the output was all the .log files were listed.
e.g
Script-
 for file in *.log
 do
         echo $file
 done

5.Looping over command output — while read line
while read line lets as read the data inside the file and also we can run commands using the data inside the file.
for eg we have a file with usernames and departments we want to make directories of those usernames we will use whil read line which we read the data each line at time and will do mkdir on those line.
e.g
Script-
while IFS=":" read -r username department
do
        echo "processing $username"
        sudo mkdir -p "/home/yogesh_jawlekar/script/day21/company/$department/$username"
done < users.txt

#Task 4: Functions
1.Defining a function — function_name() { ... }
Function can be defined with a parenthesis infront which carries the code or logic in curly brackets.
e.g script
function() {
        echo "hello yogesh"
}
2.Calling a function-
Once we have a function inorder to make it functional we need to call it calling is basically writing the function name just like in below example.
new_function() {
         echo "hello yogesh"
}
new_function
3.Passing arguments to functions — $1, $2 inside functions
In the below script we have called first argument if that first argument is the same as mentioned then this will perform the action
In below script.
e.g script
new_function() {
        if [ "$1"= "hi" ];then
                echo "hello yogesh"
        fi
}
new_function $1
4.Return values — return vs echo
return- return is basically use only inside a function where return 0 means sucess and return 1 means error return basically tells that if this is true or false then skip the function and operate if their are any operations other than that function 
like in below script we have set a logic where if first argument is hi return 0 else echo new and their is another activity outside the function which is echo new world.
so in here if we run the script with hi which is our first argument the return will stop the function there only and it will echo new world but if the first argument is not hi or other that hi it will perform else and also the outside operation.
new_function() {
        if [ "$1" = "hi" ];then
                return 0
        else
                echo "new"
        fi
}
new_function $1
echo "new world"
*note*
exit1/0-can be used in whole of script.
return1/0-can only be used inside of function.

5.Local variables — local
local variables are simply the variables which can only be used inside the function but for that before the variable name we need to assign keywork local then variable and its value.
In below script if first argument is other than hi the logic will echo hello yogesh but outside the function there is also echo "$new" which will not work because there is no value assigned to it.
e.g script
new_function() {
        local new="hello yogesh"
        if [ "$1" = "hi" ];then
                return 1
        else
                echo "$new"
        fi
}
new_function $1
echo "$new"

#Task 5: Text Processing Commands
1.grep — search patterns, -i, -r, -c, -n, -v, -E
    -i = yogesh_jawlekar@Profound:~/script/day21$ grep -i "GREP" 1.log
    This is a file which informs how to use grep with -i
    grep -i is used to find the word by being insensitice to case.
    -c = yogesh_jawlekar@Profound:~/script/day21$ grep -c "grep" 1.log
      2
      grep -c is used to count the number of that word like how many times that word has comeup in that file.
2.awk
In awk i feel the most usefull is the -F(capital F) which is a field seperator awk by default assumes that file is seprated by space but if suppose we have csv file we can assign this to let awk know that this file is sperated by comma.
e.g awk -F "," '{print $1}' filename
Patterns in awk:
  searchin words 
  awk -F "," '/erro/ {print $1}' filename
  condition
  awk -F "," '$2 == "HR" {print $1}
  here it will only print coloumn $1 where in column $2 HR is their
BEGIN and END
Through this basically print at the start and at the end and in between we will print our data as per the belwo script.
e.g
awk -F ":" 'BEGIN {print "START"}
        {print $1}
     END {print "End of the report"}' names.txt
3.sed — substitution, delete lines, in-place edit -sed is find and replace tool which works line-by-line
  Substitution-is bascially denoted by s at the start 
  sed 's/Pune/Mumbai/g' names.txt
  In here sed asks to change pune with mumbai with s being seprator and g to check whole line to replace not just the first pune in that line.

  delete lines:
  In sed we can delete lines with their numbering or there patterns
  sed '2d' names.txt
  this will delete the second line.
  sed '/error/' names.txt
  this will delete those lines which have the word error in them.

  In-place edit:
  By default sed only changes the output keeping the actually file still the same if we use in-place edit which is denoted by -i that will change the file aswell.
  e.g
  sed -i 's/old/new/g' names.txt
  this will change the whole file names.txt wherever in the file old is mentioned it will be replaced by new.


4.cut — extract columns by delimiter we can use cut to extract speicific coloumns or specific range of coloumns from  a file
cut -d ":" -f 2-4 names.txt
In here -d is a delimitor which tells how to file is divided
-f 2-4 or 1 or 1,2- This basically tell to cut that from range 2-4 we have to extract data or only one or one and two basically through this we can select which coloumns we have to extract.

