### Title: More on bash(if/else, loops, ...)
Tags:  #bash  #bash-scripting 
Related to: [[BASH tutorial]]
See also: 
Previous:[[BASH tutorial]]

### Body
#### **Summary**: 
will write about some more advance bash topics.

#### **Notes**:
##### if statements:

```sh
if [ <some test> ]  
then  
<commands>  
fi
```

![[Pasted image 20240606121447.png]]

<mark class="hltr-red">some key points</mark>:
- **=** is slightly different to **-eq**. [ 001 = 1 ] will return false as = does a string comparison (ie. character for character the same) whereas -eq does a numerical comparison meaning [ 001 -eq 1 ] will return true.
- When we refer to FILE above we are actually meaning a [path](https://ryanstutorials.net/linuxtutorial/navigation.php). Remember that a path may be absolute or relative and may refer to a file or a directory.
- Because [ ] is just a reference to the command **test** we may experiment and trouble shoot with test on the command line to make sure our understanding of its behaviour is correct.


example:
```sh
1. #!/bin/bash
2. # Basic if statement

4. if [ $1 -gt 100 ]
5. then
6. echo Hey that\'s a large number.
7. pwd
8. fi

10. date
```

###### If Elif Else

```sh
if [ <some test> ]  
then  
<commands>  
elif [ <some test> ]  
then  
<different commands>  
else  
<other commands>  
fi
```



###### boolean operations
we can use `&&` and `||` operation boolean opeartions.

###### case statements:

```sh
case <variable> in  
<pattern 1>)  
<commands>  
;;  
<pattern 2>)  
<other commands>  
;;  
esac
```



##### while loop

```sh
while [ <some test> ]  
do  
<commands>  
done
```

```sh
1. #!/bin/bash
2. # Basic while loop

4. counter=1
5. while [ $counter -le 10 ]
6. do
7. echo $counter
8. ((counter++))
9. done

11. echo All done
```

##### until loops

```sh
until [ <some test> ]  
do  
<commands>  
done
```

```sh
1. #!/bin/bash
2. # Basic until loop

4. counter=1
5. until [ $counter -gt 10 ]
6. do
7. echo $counter
8. ((counter++))
9. done

11. echo All done
```

<mark class="hltr-red">diff between until and while loop:</mark>

Leave the towel on the line `until` it's dry
We could have said:
Leave the towel on the line `while` it is not dry.
Or:
Leave the towel on the line `while` it is wet.

##### For loops
```sh
for var in <list>  
do  
<commands>  
done
```

```sh
1. #!/bin/bash
2. # Basic for loop

4. names='Stan Kyle Cartman'

6. for name in $names
7. do
8. echo $name
9. done

11. echo All done
```

###### range in for loop
- {1..5} -> 1 to 5.
- {10..0..2} -> 10 to 0 with 2 interval.


💡 you can use `break` and `continue` to control the loops

for function plz review this : https://ryanstutorials.net/bash-scripting-tutorial/bash-functions.php
### References
- [[]]