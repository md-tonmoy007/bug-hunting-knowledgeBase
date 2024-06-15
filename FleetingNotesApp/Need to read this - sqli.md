---
id: ca8c4414-716a-4b93-b666-72593c457ca9
title: START HERE
tags:
  - "#sql"
  - sqli
source: web pentester handbook 2 (p-303)
source_title: ""
source_description: ""
source_image_url: ""
created_date: 2024-06-04
modified_date: 2024-06-04
Status: 0
---
A further point of interest when fi ngerprinting databases is how MySQL
handles certain types of inline comments. If a comment begins with an exclama-
tion point followed by a database version string, the contents of the comment
are interpreted as actual SQL, provided that the version of the actual database
is equal to or later than that string. Otherwise, the contents are ignored and
treated as a comment. Programmers can use this facility much like preproces-
sor directives in C, enabling them to write different code that will be processed

conditionally upon the database version being used. An attacker also can use this
facility to fi ngerprint the exact version of the database. For example, injecting
the following string causes the WHERE clause of a SELECT statement to be false if
the MySQL version in use is greater than or equal to 3.23.02:
```
/*!32302 and 1=0*/
```