# Practice file
## Usage of touch
      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ touch notes.txt
      Above first by using touch command i created a file named notes.txt

## cat to write in file.
      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ cat>notes.txt
      This day 06 of my 90days of devops journey.
      Been great so far.
      Really learning lot of new things
      
      =>> By using cat>file name on the terminal it self i wrotes the lines.

## cat to append in file
      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ cat>>notes.txt
      I forgot to mention that I have started posting on linked in.
      
      ==>then agian with the help of cat but this time >> which will help to append new lines in the file notes.txt

## cat to read files
      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ cat notes.txt
      This day 06 of my 90days of devops journey.
      Been great so far.
      Really learning lot of new things
      I forgot to mention that I have started posting on linked in.
      
      ==> and you can see when we did cat we can read the file.

*note*
>-overwrites
>>-Appends

## Usage of head
      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ head -2 notes.txt
      This day 06 of my 90days of devops journey.
      Been great so far.
      
      ==> By using head -2 we printed first two lines of the file.

## Usage of tail
      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ tail -2 notes.txt
      
      Really learning lot of new things
      I forgot to mention that I have started posting on linked in.
      ==>By using tail we printed last two lines of the file notes.txt
   
## Usage of tee

      yogesh_jawlekar@Profound:/mnt/c/Users/yogesh jawlekar/projects$ tee notes.txt
      This is 5th line.
      This is 5th line.
      
      ==> When we use command tee it allows us to type or feed whatever lines or 
      data in the file and once done it prints back the same lines as if it is showing back us our data.
