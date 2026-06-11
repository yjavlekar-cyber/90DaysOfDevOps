#  YAML Basics
## Task 1: Key-Value Pairs
  name: yogesh
  role: DevOps Engineer
  Experience: fresher
  Learning: true
  
  Created a person.yaml file where entered above data in key:value pairs.
  yaml full fomr is yet another mark-up language.
  
## Task 2: Lists
If for any key the values are more than one we can use lists to connect them.
1) tools:
    - linux
    - git
    - github
    - docker
    - github actions
In above example we can create a iteration list below our key to list down the values.

2) hobbies: [Music,Devops,Travel]
In this we can just mention the values in square bracket seprated by comas and double qoutes are not compulsory but no issue w=if we use them.


## Task 3: Nested Objects
Basically we can create a list but what if we also want to bifurcate further we can create nested objects example can be found below:
databases:
  - host: yogesh
    name: yogesh_db
    credentials:
      - user: yogesh_new
        password: yogesh123

where if we see under database we have listed host, name and credentials but also under credentials we have nested user and their password.

## Task 4: Multi-line Strings
Suppose we have a description in yaml file which can be represented below two methods:
### The | block style (preserves newlines)
    If we are using block style method and suppose the description is of around 2-3 lines.
    This style will print/keep the description as it is our will divide it line by line.
    
    Description: |
      This is a multiline string
      It preservers all newlines
      Each line is on a new line
    
    Output:
      This is a multiline string
      It preservers all newlines
      Each line is on a new line

### The > fold style (folds into one line)
In this style the all the three lines will be combined and represented in one single line like below.
Output-
his is a multiline string,It preservers all newlines,Each line is on a new line


## Task 5: Validate Your YAML
To validate our yaml files first we need to have yamllint in our system which can be easily installed by doing.
sudo apt install yamllint

we used below command to validate our yaml files.
yamllint sever.yaml

This is basically A linter for YAML files. yamllint does not only check for syntax validity, but for weirdnesses like key
repetition and cosmetic problems such as lines length, trailing spaces, indentation, etc.

- Findings
1) At the start document start which is represented by
---(three dashes) was missing.

2)Another issue was thier was some trailing white spaces which can be identified by yammlinter.com or we can open our code in VS code and ctrl + shift + p and search for trailing white spaces
this will show us in this case at the end there was an extra space which vim was not detecting.

And now finnaly when i run yamllint server.yaml there is no output it means the yaml file is perfect with no errors.
3) too few spaces after comma this issue is faced when we use brackets for list where after comma we have not given any space then this issue arises.


