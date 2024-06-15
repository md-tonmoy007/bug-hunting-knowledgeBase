---
id: ca8c4414-716a-4b93-b666-72593c457ca9
title: Sqli Union based
tags:
  - sql
  - sqli
source: web pentester handbook 2 (p-306)
source_title: 
source_description: ""
source_image_url: ""
created_date: 2024-06-04
modified_date: 2024-06-04
Status: 0
---
Three important
points mean that your task usually is easy:

- For the injected query to be capable of being combined with the first, it is
not strictly necessary that it contain the same data types. Rather, they must
be compatible. In other words, each data type in the second query must
either be identical to the corresponding type in the first or be implicitly
convertible to it. You have already seen that databases implicitly convert
a numeric value to a string value. In fact, the value NULL can be converted
to any data type. Hence, if you do not know the data type of a particular
field, you can simply SELECT NULL for that field.

- In cases where the application traps database error messages, you can
easily determine whether your injected query was executed. If it was,
additional results are added to those returned by the application from its
original query. This enables you to work systematically until you discover
the structure of the query you need to inject.

- In most cases, you can achieve your objectives simply by identifying a
single field within the original query that has a string data type. This is
sufficient for you to inject arbitrary queries that return string-based data
and retrieve the results, enabling you to systematically extract any desired
data from the database.