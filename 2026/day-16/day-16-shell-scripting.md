#Task 1:  First Script
==>vim hello.sh
script:
  #!/bin/bash
echo "hello, Devops!"

Output= hello, Devops!

What happens if you remove the shebang line?
==> As I using the bash shell even If I remove the shebang It is not affecting the output.

#Task 2: Variables
==>Variables.sh

Script:
  #!/bin/bash
Name=Yogesh
Role=Devops
echo "Hello, I am $Name and I have started learning $Role"

Output= Hello, I am Yogesh and I have started learning Devops

Summary- Created a script in which i tried to assign values to variables Name and Role, and also I have used them in sentence.

#Task 3: User Input with read
==> 
*vim greet.sh*
Script-#!/bin/bash
read -p "Enter your name:" Name
echo "My name is $Name"

Output-Enter your name:yogesh
        My name is yogesh
        
Permisions- sudo chmod +x greet.sh

Summary- In here we have structered the script in such a manner where first will take input from the user and that input we will print in the output.


Task 4: If-Else Conditions
==>
Script:
#!/bin/bash
for i in {1..5}
do
        read -p "Enter the number of your choice:" Number
        if [ "$Number" -gt 0 ];then
                echo "Positive"
        elif [ "$Number" -lt 0 ];then
                echo "Negative"
        else
                echo "Zero"
        fi
done

Output-yogesh_jawlekar@Profound:~/script/newscripts$ ./check_number.sh
Enter the number of your choice:5
Positive
Enter the number of your choice:5
Positive
Enter the number of your choice:2
Positive
Enter the number of your choice:0
Zero
Enter the number of your choice:-6
Negative

Summary-In this task I created a script where I created a loop which will run 5 times and in that loop first we took input of the number and by putting IF conditions we have taken the output where if the input number is positive the output will print positive like that 
negative and zero as well.

ask 5: Combine It All
Script-
#!/bin/bash



read -p "Enter the service name:" package

read -p "Do you want to check the status of $package? (y/n)" input

if [ "$input" == "y" ];then
        sudo systemctl status $package

else
        echo "Skipped"


fi

Output-Enter the service name:nginx
Do you want to check the status of nginx? (y/n)n
Skipped

Summary-In this script we have checked the package status if input is y then it will check the status and if input is n it will skip.
