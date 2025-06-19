To test for Reflected XSS in a bug bounty program, follow this checklist:

### **Reflected XSS (RXSS) Testing Checklist**  

#### **1. Identify Entry Points**  
- [ ] URL query parameters  
- [ ] POST body parameters  
- [ ] URL path segments  
- [ ] HTTP headers (e.g., `User-Agent`, `Referer`, `Cookie`)  

#### **2. Submit Test Values**  
- [ ] Inject a unique **8-character random alphanumeric string** (e.g., `r4nd0m12`)  
- [ ] Check if the value is reflected in the response  
- [ ] Use Burp Intruder with **grep payloads** to automate reflection detection  

#### **3. Determine Reflection Context**  
- [ ] **HTML Body** (between tags, e.g., `<div>INJECTION</div>`)  
- [ ] **HTML Attribute** (e.g., `<input value="INJECTION">`)  
- [ ] **JavaScript String** (e.g., `var x = 'INJECTION';`)  
- [ ] **URL Context** (e.g., `<a href="INJECTION">`)  

#### **4. Test Initial XSS Payloads**  
- **Basic XSS Payload:**  
  ```html
  <script>alert(document.domain)</script>
  ```  
- **If blocked, try variations:**  
  ```html
  "><script>alert(1)</script>
  ' onmouseover=alert(1) x='
  javascript:alert(1)
  ```  
- [ ] Test in **Burp Repeater** and check if payload executes  

#### **5. Bypass Input Filters**  
- [ ] **Case switching** (e.g., `<ScRiPt>alert(1)</ScRiPt>`)  
- [ ] **Encoding** (e.g., `%3Cscript%3Ealert(1)%3C/script%3E`)  
- [ ] **Double encoding** (e.g., `%253Cscript%253E`)  
- [ ] **Alternative tags/events** (e.g., `<img src=x onerror=alert(1)>`)  
- [ ] **Breaking out of strings** (e.g., `'; alert(1); //`)  

#### **6. Verify Exploit in Browser**  
- [ ] Paste URL with payload into browser  
- [ ] Confirm JavaScript execution (e.g., `alert(document.domain)`)  
- [ ] Check if payload is **URL-encoded/decoded** correctly  

#### **7. Document Findings**  
- [ ] Record vulnerable parameters  
- [ ] Note input validation bypass techniques  
- [ ] Save proof-of-concept (PoC) request/response  

### **Optional Advanced Checks**  
- [ ] Test for **DOM-based XSS** if reflection is in JavaScript  
- [ ] Check for **CSP bypasses** if payloads are blocked  
- [ ] Test for **XSS via HTTP headers** (if applicable)  

This checklist ensures a structured approach to finding and validating reflected XSS vulnerabilities. 🚀