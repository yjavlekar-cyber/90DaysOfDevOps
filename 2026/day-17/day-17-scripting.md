#Task 1: For Loop
 1) Create for_loop.sh that:
    Loops through a list of 5 fruits and prints each one.
    -script:
          #!/bin/bash
          for i in {Apple,Banana,Pineapple,Jackfruit,Orange};
          do
            echo "$i"
          done
    -Output=
    yogesh_jawlekar@Profound:~/script$ ./for_loop.sh
                                        Apple
                                        Banana
                                        Pineapple
                                        Jackfruit
                                        Orange

2)Create count.sh that:
  Prints numbers 1 to 10 using a for loop.
  -Script=
              #!/bin/bash
              for i in {1..10}
              do
                      echo "$i"
              done
  -Output-
          yogesh_jawlekar@Profound:~/script$ ./count.sh
                      1
                      2
                      3
                      4
                      5
                      6
                      7
                      8
                      9
                      10



#Task 2: While Loop
1)Create countdown.sh that:
  Takes a number from the user
  Counts down to 0 using a while loop
  Prints "Done!" at the end
Script-
    #!/bin/bash
    read -p "Enter the number:" number
    while [ $number -ge  1 ];
    do
            ((number--))
            echo "$number"
    done
            echo "done!"
Output-
  Enter the number:5
            4
            3
            2
            1
            0
            done!

#Task 3: Command-Line Arguments
1.Create greet.sh that:
Accepts a name as $1
Prints Hello, <name>!
If no argument is passed, prints "Usage: ./greet.sh "

Script-#!/bin/bash
     if [ $# -eq 0 ];then
            echo "usage:./greet.sh"
     else
            echo "Hello,$1"
    fi
Output-yogesh_jawlekar@Profound:~/script$ ./greet.sh
        usage:./greet.sh
        yogesh_jawlekar@Profound:~/script$ ./greet.sh yogesh
        Hello,yogesh

  2.Create args_demo.sh that:
    Prints total number of arguments ($#)
    Prints all arguments ($@)
    Prints the script name ($0)
      Script-
        #!/bin/bash
        echo "Total number of arguments="$#
        echo "All arguments="$@
        echo "Script name="$0
      Output-
        yogesh_jawlekar@Profound:~/script$ ./args_demo.sh Hello, how are you?
        Total number of arguments=4
        All arguments=Hello, how are you?
        Script name=./args_demo.sh

#Task 4: Install Packages via Script
  Script-
    #!/bin/bash
    package=$1
    if dpkg -s $package >/dev/null 2>&1;then
            echo "$package already installed."
            exit 1
    else
            echo "Continuing Installation" && sudo apt update && sudo apt install $package
    fi
  Output-
    yogesh_jawlekar@Profound:~/script$ ./install_packages.sh nginx
    nginx already installed.

#Task 5: Error Handling
  Script-#!/bin/bash
    set -e
    mkdir /tmp/devops-test
    echo "Directory already exists"
Output-
  yogesh_jawlekar@Profound:~/script$ ./safe_script.sh
  mkdir: cannot create directory ‘/tmp/devops-test’: File exists
  Summary- As the file already exist set -e stopped the script at the error of mkdir only.

  
What I learned:
  In todays assignment I did try some basic scripts where i learned some new techniques which are:
  1)how to use for and while loop in a script.
  2)How to use arguments to execute the script?
  3)Also tried basic automation for package installation where if the package already exist the script will tell us if not it will install the package using arguments.
  4)Then also used set -e which we can use at the top of the script below shebang so that if will running script if there is an error the script will stop at that point only it will not run further commands.

  
