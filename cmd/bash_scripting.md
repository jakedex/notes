# Bash Scripting

### Basics 
* Shebang line `\#!/bin/bash` indicates that the bash interpreter should be used to run the scipt. Must be first line of file.
* Follow the shebang with any command you'd like. 
* Use `-x` to debug the scripts
* Add additional commands on the next line or separate them with `;`

### Variables
* Different types of variables: e.g. Local, global, stirng, integer constant, array. 
* Global (ie Environment) variables are available everywhere, whereas local are only the in current script
* Use `echo $HOME` to view values of specific env variables, and 'env' to view all global vars
* Variables are case sensitive and capitalized by default, local vars usually lowercase
* Use double quotes around variable to avoid throwing expcetion when file name has a space

### Conditionals
* e.g. 
`if condition
then
 do something
else 
 do something else
fi`

* `test` is a bash command which tests our expression and returns true or false
* `$?` var stores the exit status of the command - successful will return 0
* e.g. `test "$?" -eq 0`

### Comparison
* numeric
	* eq 
	* ne (not equal to)
	* gt (is greater than)
	* ge (is greater than or equal to)
	* lt (is less than)
	* le (less than or equal to)
* string
	* ==
	* !=
	* <
	* <=
	* \>
	* \>=

### Misc
use \`\` or $() to include output of command in echo statement

* e.g. ``echo "This is my `wc -l < /etc/group`th beer"``

