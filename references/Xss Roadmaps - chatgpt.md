---
tags:
  - xss
  - roadmap
---
Here’s a **deep, vertical XSS-mastery roadmap**, broken into progressive modules. Each module lists key concepts, hands-on labs, and further reading/research topics so you can dive as deep as you like.

---

## 📚 Module 1: Foundations of XSS and Web Security

**Goal:** Understand the web platform and how XSS fits into the security landscape.

1. **Core Web Concepts**
    
    - HTTP request/response model & headers.
        
    - HTML parsing rules and DOM tree construction.
        
    - JavaScript execution context and Same-Origin Policy.
        
2. **XSS Overview (OWASP)**
    
    - Reflected, Stored, DOM-based XSS definitions.
        
    - Why XSS remains Top-10.
        
3. **Hands-On Labs**
    
    - PortSwigger “Cross-site scripting (reflected)” lab series.
        
    - Google XSS Game (levels 1–5).
        
4. **Deep Research Topics**
    
    - HTML tokenizer quirks (e.g., how browsers handle broken tags).
        
    - Character encoding traps (Unicode normalization).
        

---

## 🔎 Module 2: Reflected XSS Deep Dive

**Goal:** Master every injection context in a reflected flow.

1. **Injection Contexts**
    
    - HTML body/text, attributes, tag names.
        
    - JavaScript contexts: string, numeric, URI, CSS.
        
    - Event handler attributes (e.g., `onload`, `onclick`).
        
2. **Context-Aware Payload Crafting**
    
    - Bypassing simple filters: quote-balancing, comment insertion.
        
    - Contextual encoding vs. sanitization failures.
        
3. **Labs & Exercises**
    
    - PortSwigger “Context-based injection” challenges.
        
    - Build your own micro-app and experiment with payloads.
        
4. **Research & Write-Ups**
    
    - Study real-world bounty reports on complex reflected XSS.
        
    - Track filtering libraries (e.g., ESAPI, AntiSamy) failures.
        

---

## 💾 Module 3: Stored and **DOM-Based** XSS

**Goal:** Dissect how data flows lead to persistent and client-side DOM XSS.

1. **Stored XSS Mechanics**
    
    - Data storage points (DB, log files, feeds).
        
    - Impact analysis: CSRF token theft, user pivot.
        
2. **DOM XSS Anatomy**
    
    - Sources (`location`, `document.cookie`, `postMessage`).
        
    - Sinks (`innerHTML`, `document.write`, `eval`).
        
    - DOMPurify bypass case studies.
        
3. **Hands-On**
    
    - DOM XSS labs on PortSwigger.
        
    - Build tiny page using `window.location.hash` → inject payload.
        
4. **Advanced Research**
    
    - Evaluate sanitizers (DOMPurify, xss-filters) under mutation attacks.
        
    - Write a tiny fuzzer for DOMPurify edge cases.
        

---

## 🛡️ Module 4: WAF Evasion Techniques for XSS

**Goal:** Learn how to bypass common web-application firewalls.

1. **WAF Fundamentals**
    
    - Signature vs. anomaly detection.
        
    - Popular WAFs: ModSecurity, AWS WAF, Cloudflare.
        
2. **Evasion Tactics**
    
    - Encoding chains (double-encode, UTF-7).
        
    - Payload mutation (case changes, comment injections).
        
    - Polyglot payloads (work in multiple contexts).
        
3. **Tools & Practice**
    
    - WAFW00F to fingerprint WAF.
        
    - Test payloads through Burp’s Intruder with payload filters.
        
4. **Research Directions**
    
    - Study recent vulnerabilities in major WAF rulesets.
        
    - Contribute to waf-bypass GitHub repos.
        

---

## 📝 Module 5: Advanced HTML Sinks & Polyglots

**Goal:** Catalog every “sink” and craft universal payloads.

1. **HTML/JS Sinks Inventory**
    
    - `innerHTML` vs. `outerHTML` vs. `insertAdjacentHTML`.
        
    - JS APIs: `setAttribute`, `execScript`, `postMessage`.
        
2. **Polyglot Mastery**
    
    - Build minimal payloads that survive multiple contexts.
        
    - Understand browser parsing differences (Chrome vs. IE/Edge).
        
3. **Labs**
    
    - Create a table of sinks + required payload prefix/suffix.
        
    - Test polyglots on various browser dev tools.
        
4. **Deep Dive**
    
    - Analyze the HTML5 spec for new parsing rules.
        
    - Research “script gadget” discovery (JS libs offering XSS gadgets).
        

---

## 🔐 Module 6: Content Security Policy (CSP) & Bypasses

**Goal:** Understand and defeat client-side defenses.

1. **CSP Basics**
    
    - Directives: `script-src`, `unsafe-inline`, `nonce`, `hash`.
        
    - Reporting mode vs. enforcement.
        
2. **Bypass Vectors**
    
    - Whitelisted hosts & trusting external scripts.
        
    - DOM-based bypass via `importScripts` in workers.
        
    - CSP header misconfigurations (missing `default-src`).
        
3. **Hands-On**
    
    - Spin up test pages with strict CSP, try inline/external bypasses.
        
    - Use Burp to modify CSP on-the-fly.
        
4. **Research**
    
    - Recent CVEs showing CSP escape.
        
    - Write a blog post on CSP edge cases (e.g., old browsers).
        

---

## 🤖 Module 7: Automation, Tooling & Bug-Bounty Workflow

**Goal:** Integrate XSS hunting into your daily bug-bounty toolkit.

1. **Proxy & Scanner Plugins**
    
    - Burp Suite recipes: custom scanner checks, Burp Extender.
        
    - Turbo Intruder for mass-XSS fuzzing.
        
2. **Recon & Detection**
    
    - Use subdomain enumeration to find hidden XSS targets.
        
    - Integrate XSSHunter to catch blind/stored XSS.
        
3. **Reporting & Triage**
    
    - Craft PoC with clear reproduction steps.
        
    - Severity assessment (OWASP risk rating).
        
4. **Continuous Learning**
    
    - Subscribe to PortSwigger blog, OWASP AppSec events.
        
    - Follow researchers on Twitter/GitHub (e.g., @defparam, @0xInfection).
        

---

## 📈 Module 8: Research & Contribution

**Goal:** Become recognized in the community and push the field forward.

1. **Original Research**
    
    - Publish new WAF bypass techniques or sanitizer flaws.
        
    - Present at local meetups or write whitepapers.
        
2. **Open-Source**
    
    - Contribute XSS tests to SecLists or PayloadsAllTheThings.
        
    - Build your own XSS-challenge platform.
        
3. **Mentorship & Collaboration**
    
    - Pair up with other hunters; review each other’s reports.
        
    - Participate in CTFs focusing on web challenges.
        

---

### Suggested Timeline

- **Months 1–2:** Modules 1–2 fundamentals + labs.
    
- **Months 3–4:** Modules 3–4 (stored/DOM + WAF evasion).
    
- **Months 5–6:** Modules 5–6 (advanced sinks + CSP).
    
- **Ongoing:** Modules 7–8—automate, hunt live scopes, contribute research.
    

---

> **Tip:** Keep a “research lab” VM/containers with multiple browser versions, proxy tools, and scripted testbeds. Track every new finding in a personal wiki or GitHub repo so you build a reusable XSS knowledge base.

Feel free to adapt pacing and depth to your schedule—but follow each module’s mix of **theory → labs → research** to truly master XSS end-to-end. Good hunting!



## They didn't mentioned COR misconfigurations