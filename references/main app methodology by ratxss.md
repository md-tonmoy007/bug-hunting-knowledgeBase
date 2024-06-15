### Title: main app methodology by ratxss
Tags: #methodology
Author:uncle-rat
Reference:https://freedium.cfd/https://medium.com/geekculture/main-app-bug-bounty-methodology-v3-e6310e21b88e

#### Notes
**Summary**: 1-2 sentence overview
**Notes**:
1. Look for authorization vuln. See what things can do as a authenticated, non-authenticated and if possible admin. And don't forget to note them.
   ![[Pasted image 20240609131627.png]]
2. Then he uses an attack vector to test xss, html injection and html tag attribution injection. He does this for every forms.
```html
'"><u>THE XSS RAT WAS HERE
```
3. In file upload (profile pic upload) he tries basic xxe svg.
4. in links he tries ssrf attacks
5. He also do a SSTI attack if he thinks server side template engine is used.
	    SSTI (SERVER SIDE TEMPLATE INJECTION) 
	    CSTI (CROSS SITE TEMPLATE INJECTION)

6. Then he test for SQLi attacks
7. then he goes for IDOR attacks
8. Work with the sign in/ sign up part
   watch the request portal
   test for password reset.
   play with http of these portions.
9. Then he tries with csrf.
10. Look for parameters play with them.
11. LFI/RFI and path traversal
12. Command injection
