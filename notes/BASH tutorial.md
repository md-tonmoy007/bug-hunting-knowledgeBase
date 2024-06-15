### Title: learning Bash scripting
Tags: #bash #bash-scripting
Related to: 
See also: [[Bash tutorial - 2]]
Previous:

### Body
#### **Summary:** Should be short, no prose

#### **Notes:**

##### **variables:**

- **$0** - The name of the Bash script.
- **$1 - $9** - The first 9 arguments to the Bash script. (As mentioned above.)
- **$#** - How many arguments were passed to the Bash script.
- **$@** - All the arguments supplied to the Bash script.
- **$?** - The exit status of the most recently run process.
- `**$$**` - The process ID of the current script.
- **$USER** - The username of the user running the script.
- **$HOSTNAME** - The hostname of the machine the script is running on.
- **$SECONDS** - The number of seconds since the script was started.
- **$RANDOM** - Returns a different random number each time is it referred to.
- **$LINENO** - Returns the current line number in the Bash script.

##### Command substitution
You can use `$()` this to substitute things
for example:
```bash
myvar=$( ls /etc | wc -l )
```

##### Export:
`export var1`
	make the variable var1 available  to child processes

##### Reading variable 
<mark class="hltr-grey">read.sh</mark>
```sh

#!/bin/bash
# Ask the user for their name
echo Hello, who am I talking to?
read varname

echo It\'s nice to meet you $varname
```

💡in the echo or reuse the variable <mark class="hltr-yellow">varname</mark> we used `$varname`

> 	-p : allows you to specify a prompt 
> -s : makes the input silent
> -sp: give u a prompt and make the input silent


###### Reading from standard i/0

```js
- STDIN - /dev/stdin or /proc/self/fd/0
- STDOUT - /dev/stdout or /proc/self/fd/1
- STDERR - /dev/stderr or /proc/self/fd/2
```

example:
<mark class="hltr-grey">summary.sh</mark>
```sh
1. #!/bin/bash
2. # A basic summary of my sales report

4. echo Here is a summary of the sales data:
5. echo ====================================
6. echo

8. cat /dev/stdin | cut -d' ' -f 2,3 | sort
```
command line: `cat salesdata.txt | ./summary`
see more about `cat` command [[Linux command - cut|here]].

##### Arithmetic
###### let
**let** is a builtin function of Bash that allows us to do simple arithmetic.
it stores the arithmetic operation in a variable

example:
```sh
1. #!/bin/bash
2. # Basic arithmetic using let

4. let a=5+4
5. echo $a # 9

7. let "a = 5 + 4"
8. echo $a # 9

10. let a++
11. echo $a # 10

13. let "a = 4 * 5"
14. echo $a # 20

16. let "a = $1 + 30"
17. echo $a # 30 + first command line argument
```


###### Expr
**expr** is similar to let except instead of saving the result to a variable it instead prints the answer. Unlike **let** you don't need to enclose the expression in quotes. You also must have spaces between the items of the expression. It is also common to use **expr** within command substitution to save the output to a variable.

```sh
1. #!/bin/bash
2. # Basic arithmetic using expr

4. expr 5 + 4

6. expr "5 + 4"

8. expr 5+4

10. expr 5 \* $1

12. expr 11 % 2

14. a=$( expr 10 - 3 )
15. echo $a # 7
```

######  Double Parentheses

```sh
1. #!/bin/bash
2. # Basic arithmetic using double parentheses

4. a=$(( 4 + 5 ))
5. echo $a # 9

7. a=$((3+5))
8. echo $a # 8

10. b=$(( a + 3 ))
11. echo $b # 11

13. b=$(( $a + 4 ))
14. echo $b # 12

16. (( b++ ))
17. echo $b # 13

19. (( b += 3 ))
20. echo $b # 16

22. a=$(( 4 * 5 ))
23. echo $a # 20
```


### References
- [[]]