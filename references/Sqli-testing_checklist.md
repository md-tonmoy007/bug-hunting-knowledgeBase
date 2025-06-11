---
tags:
  - sql
  - sqli
---


## Check if the sqli exists

1. submit a single string - '
2. if the is a error or anomaly when ' is given, then give '', if the  anomaly gone 
3. sqli exists for different databases
	1. Oracle: ‘||’FOO
	2. MS-SQL: ‘+’FOO
	3. MySQL: ‘ ‘FOO (note the space between the two quotes)

[[references/SQL payload|SQL payload]]
