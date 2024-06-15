### Title: Union clause
Tags: #sqli #sql
Author:
Reference:https://www.youtube.com/watch?v=su-fxrvKTCk

#### Notes
**Summary**:
Union combines the results of two or more SELECT statements
**Notes**:
```sql?
SELECT * From income;
UNION
SELECT * FROM expenses;

```

For it to to work both table have to same number of column. All we can select distinct column like this - SELECT col1, col2 from income ....
Also the data type in same column should be maintained and interchangeable.