# Day 21 – Shell Scripting Cheat Sheet: Build Your Own Reference Guide

## Summary Table

| Command / Concept | Usage / Purpose |
| :--- | :--- |
| **#!/bin/bash** | Shebang: Identifies the shell interpreter for the script. |
| **chmod +x** | Permission: Makes a script executable. |
| **#** | Comments: Single-line or in-line notes ignored by the shell. |
| **VAR=val** | Variables: Assigning values to variables for reusability. |
| **read** | User Input: Captures input from the user during execution. |
| **$0, $1...** | Arguments: Positional parameters passed to the script. |
| **[ "$A" = "$B" ]** | String Comparison: Checks if strings are equal, different, or empty. |
| **[ $A -eq $B ]** | Integer Comparison: Compares numbers (equal, greater, less, etc.). |
| **[ -f file ]** | File Tests: Checks if a file exists, is a directory, etc. |
| **if, elif, else** | Conditionals: Executes code blocks based on logic. |
| **&&, ||, !** | Logical Ops: AND, OR, and NOT for combining conditions. |
| **case** | Pattern Matching: Cleaner alternative for multiple if-else checks. |
| **for** | Iteration: Loops through a list or a range of numbers. |
| **while** | True Loop: Runs as long as a condition is true. |
| **until** | False Loop: Runs until a condition becomes true. |
| **break / continue** | Loop Control: Stop a loop or skip an iteration. |
| **function()** | Functions: Reusable blocks of code. |
| **local** | Local Scope: Restricts variable visibility to a function. |
| **grep** | Search: Finds patterns in files (supports -i, -c, -v, etc.). |
| **awk** | Processing: Field-based text manipulation and reporting. |
| **sed** | Editing: Stream editor for find-and-replace or deletion. |
| **cut** | Extraction: Extracts columns using a delimiter. |
| **sort** | Sorting: Arranges lines alphabetically, numerically, or reversed. |
| **tr** | Translate: Swaps or deletes individual characters. |
| **wc** | Counting: Counts lines, words, and characters. |
| **head / tail** | Slice: Shows the start or end of a file. |
| **find** | Locating: Finds files based on name, time, or type. |
| **jq** | JSON Parser: Command-line tool for parsing JSON data. |
| **set -e, -u, -x** | Debugging: Controls script exit behavior and tracing. |
| **trap** | Cleanup: Executes commands automatically on script exit. |

---

## #Task 1-Basics

### 1. Shebang (`#!/bin/bash`)
Shebang should be used on the top of shell script so that the script could identify what type of shell we are using.
```bash
#!/bin/bash
```

### 2. Running a script `chmod +x`
In order to execute the shell script we first need to modify its permission to executable before running it can be done by using `chmod +x script.sh`.
```bash
chmod +x backup.sh
./backup.sh
```

### 3. Comments — single line (`#`) and inline
In a script in order to explain or to define certain logics we can use comments which are used with `#` when we start the comment from the start of the line it is called full line comment and if in between of the line it is called in-line comment.
```bash
#This is a full line comment.
echo "comment" # this is inline comment.
```
There is also another type of comment which is called Multi-line comment which starts with delimeter followed by two redirection operators and and two same words whatever we will right in between those two words will be ignored by the script.
```bash
:>>'comment'
this is a 
multiline.
comment
comment
```

### 4. Variables — declaring, using, and quoting (`$VAR`, `"$VAR"`, `'$VAR'`)
In a script instead of hard-codding we assign the values to certain variables so that whenever if we want to change anything we can just change the values of those variables.
* declaring a avriable is basically assigning a value to a variable by using `=` operator.
```bash
name=yogesh
```
* using and qouting- This means using the variable which was earlier declared inside our logic with quoting so that the output doesn't breaks.
```bash
echo "$name"
```

### 5. Reading user input — `read`
we can use read or `read -p` to take user input in simple terms we will take the user input using read and we can use that further in our logic.
```bash
read -p "Enter your name:" name
echo "my name is $name"
```

### 6. Command-line arguments — `$0`, `$1`, `$#`, `$@`
Arguments can be easily defined as number of words in a command in linux in a shell script we can use arguments by assigning numbers like `$1` `$2` which basically will fetch or use the arguments which we will put while running the script for e.g `./script.sh sample.log` (In this `./script.sh` is argument `$0` and `sample.log` `$1`).
Basically arguments are numbering or positioning of input given to the shell to execute.
```bash
if [ "$1" = "yogesh" ];then
      echo "Hello yogesh"
fi
```
As in the above script we have an argument which is `$1` means the input after the script name so if we run our script `./script.sh yogesh` this will print Hello yogesh.

---

## #Task 2: Operators and Conditionals

### 1. String comparisons (`=`, `!=`, `-z`, `-n`)
String comparisons are used to verify if the string is same(`=`),different(`!=`),empty(`-z`) or not empty(`-n`).
```bash
#!/bin/bash
if [ "$1" = "yogesh" ];then
      echo "Hello yogesh"
fi
```

### 2. Integer comparisons (`-eq`, `-ne`, `-lt`, `-gt`, `-le`, `-ge`)
To compare the integers in our logic we can use integer comparison. Suppose we have logic where if the total number of arguments are zero it should print something we will use this because we are dealing with integers.
```bash
if [ $# -eq 0 ];then
  echo "No arguments."
fi
```

### 3. File test operators (`-f`, `-d`, `-e`, `-r`, `-w`, `-x`, `-s`)
This operators are used for the operations related to files or directories for eg `-f` denotes is it a regular file, `-d` is it a directory, `-e` represents is the file exist at all.
```bash
if [ -f "script.sh" ];then
      echo "File exists"
fi
```

### 4. if, elif, else syntax
If else is used to put certain conditions and if those conditions are fullfilled certain activites should be carried out.
the synatx of if else is below:
```bash
if [ ou logic ];then
      echo "echo or whetever activity we want to carry out"
else
      # activity
elif
      # activity
fi
```

### 5. Logical operators (`&&`, `||`, `!`)
* `&&` = if this is used in between two commands if the first commands succeeds then second command will run.
  `mkdir new-project && cd new-project`
* `||` = If the first command fails means there is no output then only the second command will run.
  `grep "error" file.log || echo "no error"`
* `!` = This basically reverted the exit status success into failure and failuer into success.
```bash
if [ ! -f "file.log" ];then
      echo "File doesn't exist"
fi
```

### 6. Case statements — `case ... esac`
this is basically like using if else condition multiple times in here we can use the variable against multiple patterns.
```bash
#!/bin/bash
echo "Enter your favourite fruit:"
read fruit

case "$fruit" in
      "apple")
      echo "Apples are great for health."
      ;;
      "banana" | "plantain")
      echo "Bananas provide instant energy."
      ;;
esac
```

---

## #Task 3: Loops

### 1. for loop — list-based and C-style
for loops are used to iterate or list down the date from a list.
**list-based:**
```bash
for i in {1..5}
do
      echo $i
done
```
**c-style- is used for arithmetic type logics:**
```bash
for (( num=1 ; num<=10 ; num ++ ))
do
      echo $num
done
```

### 2. while loop
this is basically a true loop if the logic is true then the command will keep iterating until we stop it.
```bash
read -p "enter your number:" number

while [ "$number" -gt 10 ]
do
      echo "Greater"
      exit 1
done
echo "less"
```

### 3. Until loop
This is opposite to the while loop it basically false loop it says until this logic is true do this and done infinetly till we stop it.
```bash
read -p "enter your number:" number

until  [ "$number" -gt 10 ]
do
      echo "less"
      exit 1
done
echo "greater"
```

### 4. Loop control — break, continue
**break-** In shell scripting break acts as a stop button which gets triggered when the condition is fullfilled just like in below script if you see if the number is greater than 10 it will stop the infinty loop of greater but will also continue to run the next command which is to print less it doesnot stop overall script just the particular condition.
**continue:** This basically skips whichever condition we set from to final output just like in below example we are iterating numbers from 1-5 but there is condition if i is 4 skip it so the output will only give us numbers other than 4.
```bash
#!/bin/bash
for i in {1..5}
do
      if [ $i = 4 ];then
            continue
      fi
      echo $i
done
```

### 5. Looping over files
to list down the files we can use belwo script where whetever file type we have mentioned after asteric it will iterate those files just like in below script the output was all the .log files were listed.
```bash
for file in *.log
do
      echo $file
done
```

### 6. Looping over command output — while read line
while read line lets as read the data inside the file and also we can run commands using the data inside the file.
for eg we have a file with usernames and departments we want to make directories of those usernames we will use whil read line which we read the data each line at time and will do mkdir on those line.
```bash
while IFS=":" read -r username department
do
      echo "processing $username"
      sudo mkdir -p "/home/yogesh_jawlekar/script/day21/company/$department/$username"
done < users.txt
```

---

## #Task 4: Functions

### 1. Defining a function — `function_name() { ... }`
Function can be defined with a parenthesis infront which carries the code or logic in curly brackets.
```bash
function() {
      echo "hello yogesh"
}
```

### 2. Calling a function
Once we have a function inorder to make it functional we need to call it calling is basically writing the function name just like in below example.
```bash
new_function() {
      echo "hello yogesh"
}
new_function
```

### 3. Passing arguments to functions — `$1`, `$2` inside functions
In the below script we have called first argument if that first argument is the same as mentioned then this will perform the action.
```bash
new_function() {
      if [ "$1"= "hi" ];then
            echo "hello yogesh"
      fi
}
new_function $1
```

### 4. Return values — return vs echo
**return-** return is basically use only inside a function where return 0 means sucess and return 1 means error return basically tells that if this is true or false then skip the function and operate if their are any operations other than that function like in below script we have set a logic where if first argument is hi return 0 else echo new and their is another activity outside the function which is echo new world.
```bash
new_function() {
      if [ "$1" = "hi" ];then
            return 0
      else
            echo "new"
      fi
}
new_function $1
echo "new world"
```
**\*note\***
* exit1/0-can be used in whole of script.
* return1/0-can only be used inside of function.

### 5. Local variables — `local`
local variables are simply the variables which can only be used inside the function but for that before the variable name we need to assign keywork local then variable and its value.
In below script if first argument is other than hi the logic will echo hello yogesh but outside the function there is also `echo "$new"` which will not work because there is no value assigned to it.
```bash
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
```

---

## #Task 5: Text Processing Commands

### 1. grep — search patterns, -i, -r, -c, -n, -v, -E
* `-i` = `grep -i "GREP" 1.log` (insensitice to case)
* `-c` = `grep -c "grep" 1.log` (count number of word)

### 2. awk
In awk i feel the most usefull is the -F(capital F) which is a field seperator awk by default assumes that file is seprated by space but if suppose we have csv file we can assign this to let awk know that this file is sperated by comma.
`e.g awk -F "," '{print $1}' filename`

**BEGIN and END**
Through this basically print at the start and at the end and in between we will print our data as per the belwo script.
```bash
awk -F ":" 'BEGIN {print "START"}
      {print $1}
      END {print "End of the report"}' names.txt
```

### 3. sed — substitution, delete lines, in-place edit
sed is find and replace tool which works line-by-line.
* **Substitution-** is bascially denoted by `s` at the start: `sed 's/Pune/Mumbai/g' names.txt`
* **delete lines:** `sed '2d' names.txt` (delete second line) or `sed '/error/' names.txt`
* **In-place edit:** By default sed only changes the output keeping the actually file still the same if we use in-place edit which is denoted by `-i` that will change the file aswell.
  `sed -i 's/old/new/g' names.txt`

### 4. cut — extract columns by delimiter
we can use cut to extract speicific coloumns or specific range of coloumns from a file.
`cut -d ":" -f 2-4 names.txt`

### 5. sort
Sort is basically used to sort the data available as per our needs.
* alphabetical: `sort -d file`
* numerical: `-n` (mostly used) or `-g` (mathematical equations)
* reverse: `sort -r names.txt`
* unique: `sort -u fruits.txt`

### 6. tr
This basically use to translate or delete specific characters not words even if we put two string to replace it will break them down into charachters and replace each charachter.
**Example Mapping for `tr 'yogesh' 'sourav'`:**
1. Yogesh:
   * Y (Capital Y stays Y)
   * o → o
   * g → u
   * e → r
   * s → a
   * h → v
   * Result: Yourav

```bash
cat names.txt | tr 'yogesh' 'sourav'
cat names.txt | tr -d ':'
```

### 7. wc
we can use wc command to count lines words and charactes.
* lines: `wc -l`
* words: `wc -w`
```bash
cat names.txt | tr ":" " " | wc -w
```

### 8. head/tail
* head: `cat names.txt | head -1`
* tail: `cat names.txt | tail -1`

---

## #Task 6: Useful Patterns and One-Liners

### 1. Find and delete files older than N days
```bash
del_list=$(find "$source" -name "*.gz" -type f -mtime +30 -print)
if [ -n "$del_list" ];then
      echo "$del_list" | xargs rm -f
      del_count=$(echo "$del_list" | wc -l)
fi
```

### 2. Count lines in all .log files
```bash
total_errors=$(grep -oh "ERROR" *.log | wc -l)
```

### 3. Replace a string across multiple files
```bash
sed -i 's/old/new/g' *.{log,txt,conf}
```

### 4. Check if a service is running
```bash
systemctl status service
```

### 5. Monitor disk usage with alerts
```bash
THRESHOLD=90
usage=$(df -h / | grep / | awk '{ print $5 }' | sed 's/%//')
if [ "$usage" -gt "$THRESHOLD" ]; then
      echo "ALERT: Disk usage is at ${usage}%! Cleaning up logs..."
else
      echo "Disk usage is fine: ${usage}%"
fi
```

### 6. Parse CSV or JSON from command line
**CSV:**
```bash
cut -d',' -f2 data.csv
awk -F',' '$4 > 2200 {print $2 " earns " $4}' data.csv
```
**Json:**
```bash
cat user.json | jq '.user'
cat user.json | jq '.info.city'
cat user.json | jq '.skills[0]'
```

### 6. Tail a log and filter for errors in real time
```bash
tail -f your_log_file.log | grep -i "error"
```

---

## #Task 7: Error Handling and Debugging

### 1. `set -e` — exit on error
If on top of the script below shebang we put `set -e` it works as a signal for script to stop executing whenever there is an error.

### 2. `set -u` — treat unset variables as error
This basically informs us that if we use any variable for which we have not assigned any value that will give us an output which says unbound variables.

### 3. `set -o pipefail` — catch errors in pipes
In `set -o pipefail` if command like this fails the script immediately stops.

### 4. `set -x` — debug mode (trace execution)
This will show us the command and its exccution we will now where are script is failing.
```bash
+ NAME=Yogesh
+ echo 'Hello Yogesh'
Hello Yogesh
```

### 5. Exit codes — `$?`, `exit 0`, `exit 1`
* `$?`: status of last command.
* `exit 0`: success.
* `exit 1`: error.

### 6. Trap — `trap 'cleanup' EXIT`
trap ensures a specific command or function (like cleanup) runs automatically when a script finishes or is interrupted, no matter what happens.
```bash
cleanup() {
      echo "Done! Cleaning up temporary files..."
}
trap cleanup EXIT
```