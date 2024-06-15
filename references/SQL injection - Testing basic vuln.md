- [[#Title: SQL injection - Injecting into String Data|Title: SQL injection - Injecting into String Data]]
- [[#tips|tips]]
- [[#tips#Title: Injecting into String Data|Title: Injecting into String Data]]


### Title: SQL injection - Injecting into String Data
Tags: #sqli 
Author:
Reference: web pentester handbook 2

#### Notes
Summary: 1-2 sentence overview
Notes:
1. Submit a single quotation mark as the item of data you are targeting.
Observe whether an error occurs, or whether the result differs from the
original in any other way. If a detailed database error message is received,
consult the “SQL Syntax and Error Reference” section of this chapter to
understand its meaning.

2. If an error or other divergent behavior was observed, submit two single
quotation marks together. Databases use two single quotation marks as
an escape sequence to represent a literal single quote, so the sequence is
interpreted as data within the quoted string rather than the closing string
terminator. If this input causes the error or anomalous behavior to disap-
pear, the application is probably vulnerable to SQL injection.

3. As a further verification that a bug is present, you can use SQL concat-
enator characters to construct a string that is equivalent to some benign
input. If the application handles your crafted input in the same way as it
does the corresponding benign input, it is likely to be vulnerable. Each
type of database uses different methods for string concatenation. The
following examples can be injected to construct input that is equivalent to
FOO in a vulnerable application:

 - Oracle: ‘||’FOO
 - MS-SQL: ‘+’FOO
 - MySQL: ‘ ‘FOO (note the space between the two quotes)


### tips-1
One way of confi rming that the application is interacting with a back-
end database is to submit the SQL wildcard character % in a given parameter.
For example, submitting this in a search field often returns a large number of
results, indicating that the input is being passed into a SQL query. Of course,
this does not necessarily indicate that the application is vulnerable — only that
you should probe further to identify any actual flaws.


### Title: Injecting into numerical Data

Tags: #sqli 
Author:
Reference: web pentester handbook 2

#### Notes
Summary: 1-2 sentence overview
Notes:
1. Try supplying a simple mathematical expression that is equivalent to the
original numeric value. For example, if the original value is 2, try submit-
ting 1+1 or 3-1. If the application responds in the same way, it may be
vulnerable.

2. The preceding test is most reliable in cases where you have confirmed
that the item being modified has a noticeable effect on the applica-
tion’s behavior. For example, if the application uses a numeric PageID
parameter to specify which content should be returned, substituting 1+1
for 2 with equivalent results is a good sign that SQL injection is present.
However, if you can place arbitrary input into a numeric parameter with-
out changing the application’s behavior, the preceding test provides no
evidence of a vulnerability.

3. If the first test is successful, you can obtain further evidence of the vulnera-
bility by using more complicated expressions that use SQL-specific keywords
and syntax. A good example of this is the ASCII command, which returns
the numeric ASCII code of the supplied character. For example, because the
ASCII value of A is 65, the following expression is equivalent to 2 in SQL:
67-ASCII(‘A’)

4. The preceding test will not work if single quotes are being filtered.
However, in this situation you can exploit the fact that databases implic-
itly convert numeric data to string data where required. Hence, because
the ASCII value of the character 1 is 49, the following expression is equiv-
alent to 2 in SQL:
51-ASCII(1)





### tips-2
 A common mistake when probing an application for defects such as SQL
injection is to forget that certain characters have special meaning within HTTP
requests. If you want to include these characters within your attack payloads,
you must be careful to URL-encode them to ensure that they are interpreted in
the way you intend. In particular:
-  & and = are used to join name/value pairs to create the query string and
the block of POST data. You should encode them using %26 and %3d,
respectively.
-  Literal spaces are not allowed in the query string. If they are submitted,
they will effectively terminate the entire string. You should encode them
using + or %20.
- Because + is used to encode spaces, if you want to include an actual +
in your string, you must encode it using %2b. In the previous numeric
example, therefore, 1+1 should be submitted as 1%2b1.
-  The semicolon is used to separate cookie fi elds and should be encoded
using %3b.
These encodings are necessary whether you are editing the parameter’s
value directly from your browser, with an intercepting proxy, or through any
other means. If you fail to encode problem characters correctly, you may inval-
idate the entire request or submit data you did not intend to.

### Title: Injecting into the Query Structure
Tags:
Author:
Reference:

#### Notes
Summary: 1-2 sentence overview
Notes:
```
SELECT author, title, year FROM books WHERE publisher = ‘Wiley’ ORDER BY
title ASC
```

1. Make a note of any parameters that appear to control the order or field
types within the results that the application returns.
2. Make a series of requests supplying a numeric value in the parameter
value, starting with the number 1 and incrementing it with each subse-
quent request:

	- If changing the number in the input affects the ordering of the results,
	the input is probably being inserted into an ORDER BY clause. In SQL,
	ORDER BY 1 orders by the first column. Increasing this number to 2
	should then change the display order of data to order by the second
	column. If the number supplied is greater than the number of columns
	in the result set, the query should fail. In this situation, you can confirm
	that further SQL can be injected by checking whether the results order
	can be reversed, using the following:
	1 ASC --
	1 DESC --

	- If supplying the number 1 causes a set of results with a column contain-
	ing a 1 in every row, the input is probably being inserted into the name
	of a column being returned by the query. For example:
	SELECT 1,title,year FROM books WHERE publisher=’Wiley’


- [[Bypass filters | here are some bypass methods]]
- 