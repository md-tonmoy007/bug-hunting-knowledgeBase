### Title testing union based sqli
Tags: #sqli 
Author:
Reference: web pentester handbook 2 (p-307)

#### Notes
**Summary**: 1-2 sentence overview
**Notes**:
Your first task is to discover the number of columns returned by the original
query being executed by the application. You can do this in two ways:
1. You can exploit the fact that NULL can be converted to any data type to
systematically inject queries with different numbers of columns until your
injected query is executed. For example:
```
‘ UNION SELECT NULL--
‘ UNION SELECT NULL, NULL--
‘ UNION SELECT NULL, NULL, NULL--
```
When your query is executed, you have determined the number of col-
umns required. If the application doesn’t return database error messages,
you can still tell when your injected query was successful. An additional
row of data will be returned, containing either the word NULL or an empty
string. Note that the injected row may contain only empty table cells and so
may be hard to see when rendered as HTML. For this reason it is preferable
to look at the raw response when performing this attack.

2. Having identified the required number of columns, your next task is to
discover a column that has a string data type so that you can use this to
extract arbitrary data from the database. You can do this by injecting a
query containing NULLs, as you did previously, and systematically replac-
ing each NULL with a. For example, if you know that the query must return
three columns, you can inject the following:
```
‘ UNION SELECT ‘a’, NULL, NULL--
‘ UNION SELECT NULL, ‘a’, NULL--
‘ UNION SELECT NULL, NULL, ‘a’--
```
When your query is executed, you see an additional row of data containing the
value a. You can then use the relevant column to extract data from the database.
#### NOTE
In Oracle databases, every SELECT statement must include a FROM
attribute, so injecting UNION SELECT NULL produces an error regardless of
the number of columns. You can satisfy this requirement by selecting from the
globally accessible table DUAL. For example:
```
‘ UNION SELECT NULL FROM DUAL--
```


#### POC
When you have identified the number of columns required in your injected
query, and have found a column that has a string data type, you are in a position
to extract arbitrary data. A simple proof-of-concept test is to extract the version
string of the database, which can be done on any DBMS. For example, if there
are three columns, and the fi rst column can take string data, you can extract
the database version by injecting the following query on MS-SQL and MySQL:
```
‘ UNION SELECT @@version,NULL,NULL--
```
Injecting the following query achieves the same result on Oracle:
```
‘ UNION SELECT banner,NULL,NULL FROM v$version--
```
In the example of the vulnerable book search application, we can use this
string as a search term to retrieve the version of the Oracle database:


# Extracting data
[[SQL injection - Extracting data|Learn how to extract data from a union based sqli]].