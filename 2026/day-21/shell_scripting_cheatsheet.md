# Day 21 – Shell Scripting Cheat Sheet

## Summary Table

| Category | Commands / Concepts |
| :--- | :--- |
| **Basics** | Shebang, Permissions, Comments, Variables, Input, Arguments |
| **Conditionals** | String/Integer comparisons, File tests, If/Else, Logical ops, Case |
| **Loops** | For, While, Until, Break, Continue, Iterating files/output |
| **Functions** | Defining, Calling, Passing arguments, Return vs Echo, Local variables |
| **Text Processing** | grep, awk, sed, cut, sort, tr, wc, head/tail |
| **Patterns** | File deletion, Error counting, String replace, Disk alerts, JSON/CSV parsing |
| **Error Handling** | set -e, set -u, set -o pipefail, set -x, Exit codes, Trap |

---

## Task 1: Basics

### 1. Shebang (`#!/bin/bash`)
Used on the top of the script so the script can identify what type of shell we are using.
#!/bin/bash


### 2. Running a script (`chmod +x`)
Modify permission to executable before running.
  chmod +x script.sh
  ./script.sh


### 3. Comments (Single-line and Multi-line)
Single-line uses `#`. Multi-line uses a delimiter where everything between the two words is ignored.
  This is a full-line comment
  echo "comment" # This is an inline comment

  : << 'COMMENT'
  this is a
  multiline.
  comment
  COMMENT


### 4. Variables (Declaring, Using, and Quoting)
Instead of hard-coding, we assign values to variables using the `=` operator. Use `$VAR` or `"$VAR"` to use them.
  name=yogesh
  echo "$name"


### 5. Reading user input (`read`)
We take user input using `read` or `read -p` and use that further in our logic.
  read -p "Enter your name: " name
  echo "my name is $name"


### 6. Command-line arguments (`$0`, `$1`, `$#`, `$@`)
Fetching or using inputs provided while running the script. `$0` is the script, `$1` is the first input.
  Example: ./script.sh yogesh
  if [ "$1" = "yogesh" ]; then
      echo "Hello yogesh"
  fi


 ---

## Task 2: Operators and Conditionals
   
### 1. String comparisons (`=`, `!=`, `-z`, `-n`)
Used to verify if the string is same (`=`), different (`!=`), empty (`-z`), or not empty (`-n`).
  if [ "$1" = "yogesh" ]; then
      echo "Hello yogesh"
  fi


### 2. Integer comparisons (`-eq`, `-ne`, `-lt`, `-gt`, `-le`, `-ge`)
Used to compare integers in our logic, such as checking if total arguments are zero.
  if [ $# -eq 0 ]; then
      echo "No arguments."
  fi


### 3. File test operators (`-f`, `-d`, `-e`, `-r`, `-w`, `-x`, `-s`)
Used for operations related to files or directories (e.g., `-f` for regular file, `-d` for directory).
  if [ -f "script.sh" ]; then
      echo "File exists"
  fi


### 4. `if`, `elif`, `else` syntax
Used to put certain conditions; if fulfilled, certain activities are carried out.
  if [ condition ]; then
      echo "activity"
  else
      echo "other activity"
  fi

   1
### 5. Logical operators (`&&`, `||`, `!`)
`&&`: second command runs if first succeeds. `||`: second runs if first fails. `!`: Reverts the exit status.
  mkdir new-project && cd new-project
  grep "error" file.log || echo "no error"
  if [ ! -f "file.log" ]; then echo "File doesn't exist"; fi

   1
   2 ### 6. Case statements (`case ... esac`)
   3 Used against multiple patterns instead of multiple if-else conditions.
  case "$fruit" in
      "apple") echo "Apples are great for health." ;;
      "banana" | "plantain") echo "Bananas provide instant energy." ;;
  esac

   1
   2 ---
   3
   4 ## Task 3: Loops
   5
   6 ### 1. `for` loop (List-based and C-style)
   7 Used to iterate or list down data from a list or perform arithmetic logic.
  List-based
  for i in {1..5}; do echo $i; done

  C-style
  for (( num=1 ; num<=10 ; num++ )); do echo $num; done

   1
   2 ### 2. `while` loop
   3 A "true" loop; if the logic is true, it keeps iterating until stopped.
  while [ "$number" -gt 10 ]; do
      echo "Greater"
      exit 1
  done

   1
   2 ### 3. `until` loop
   3 Opposite to while; a "false" loop that runs until the logic becomes true.
  until [ "$number" -gt 10 ]; do
      echo "less"
      exit 1
  done

   1
   2 ### 4. Loop control (`break`, `continue`)
   3 `break` stops the loop once triggered. `continue` skips the specific condition but finishes the loop.
  for i in {1..5}; do
      if [ $i = 4 ]; then continue; fi # Skips 4
      echo $i
  done
   1
   2 ### 5. Looping over files
   3 Iterates over whatever file type is mentioned after the asterisk.
  for file in *.log; do
      echo $file
  done

   1
   2 ### 6. Looping over command output (`while read line`)
   3 Lets us read data inside a file one line at a time to run commands.
  while IFS=":" read -r username department; do
      echo "processing $username"
      sudo mkdir -p "./company/$department/$username"
  done < users.txt

   1
   2 ---
   3
   4 ## Task 4: Functions
   5
   6 ### 1. Defining and Calling a function
   7 Groups logic in curly brackets. Call it simply by writing its name.
  new_function() {
      echo "hello yogesh"
  }
  new_function # Calling the function

   1
   2 ### 2. Passing arguments and Return values
   3 Functions use `$1`, `$2` internally. `return` is for success/error codes inside functions.
  new_function() {
      if [ "$1" = "hi" ]; then
          return 0 # Success status
      else
          echo "new"
      fi
  }

   1
   2 ### 3. Local variables (`local`)
   3 Variables that can only be used inside the function they are defined in.
  new_function() {
      local new="hello yogesh"
      echo "$new"
  }

   1
   2 ---
   3
   4 ## Task 5: Text Processing
   5
   6 ### 1. `grep`
   7 Search patterns with `-i` (case insensitive), `-c` (count), `-v` (invert), etc.
  grep -i "GREP" 1.log
  grep -c "grep" 1.log

   1
   2 ### 2. `awk`
   3 Useful for column separation using `-F`. Supports `BEGIN` and `END` patterns.
  awk -F ":" 'BEGIN {print "START"} {print $1} END {print "End"}' names.txt

   1
   2 ### 3. `sed`
   3 Find and replace tool that works line-by-line. Use `-i` for in-place edits.
  sed 's/Pune/Mumbai/g' names.txt
  sed -i 's/old/new/g' names.txt

   1
   2 ### 4. `cut`
   3 Extracts specific columns using a delimiter (`-d`) and field (`-f`).
  cut -d ":" -f 2-4 names.txt

   1
   2 ### 5. `sort`
   3 Sorts data alphabetically (`-d`), numerically (`-n`), or reverse (`-r`). `-u` gives unique lines.
  sort -r names.txt # Reverse alphabetical (Z-A)
  sort -u fruits.txt # Unique items only

   1
   2 ### 6. `tr` (Translate)
   3 Used to translate or delete characters. It maps characters in set1 to set2.
   4 **Your Mapping Example:** `tr 'yogesh' 'sourav'`
   5 *   `y` → `s`, `o` → `o`, `g` → `u`, `e` → `r`, `s` → `a`, `h` → `v`
  cat names.txt | tr 'yogesh' 'sourav'
  cat names.txt | tr -d ':' # Deletes all colons

   1
   2 ### 7. `wc` (Word Count)
   3 Counts lines (`-l`), words (`-w`), and characters.
  wc -l names.txt
  cat names.txt | tr ":" " " | wc -w # Use tr to help wc see words

   1
   2 ---
   3
   4 ## Task 6: Patterns and One-Liners
   5
   6 ### 1. Find and delete files older than 30 days
  find "$source" -name "*.gz" -type f -mtime +30 -exec rm -f {} +

   1
   2 ### 2. Count lines in all `.log` files
  total_errors=$(grep -oh "ERROR" *.log | wc -l)
   1
   2 ### 3. Replace a string across multiple files
  sed -i 's/old/new/g' *.{log,txt,conf}

   1
   2 ### 4. Monitor disk usage with alerts
  THRESHOLD=90
  usage=$(df -h / | grep / | awk '{ print $5 }' | sed 's/%//')
  if [ "$usage" -gt "$THRESHOLD" ]; then
      echo "ALERT: Disk at ${usage}%"
  fi

   1
   2 ### 5. JSON parsing with `jq`
  cat user.json | jq '.user'
  cat user.json | jq -r '.info.city'
### 6. Tail a log in real-time
tail -f app.log | grep -i "error"

---
 ## Task 7: Error Handling and Debugging

### 1. `set -e`, `-u`, `-o pipefail`
*   `-e`: Exit on any command failure.
*   `-u`: Error on unassigned variables.
*   `-o pipefail`: Catch errors inside pipes.
### 2. `set -x` (Debug mode)
Prints every command with its variables expanded to the terminal.
   + NAME=Yogesh
   + echo 'Hello Yogesh'


### 3. Exit codes and Trap
*   `$?`: Status of last command (0=success).
*   `trap`: Automatically runs a cleanup function on exit.
  trap cleanup EXIT
