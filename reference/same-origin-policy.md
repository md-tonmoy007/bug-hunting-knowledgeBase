---
tags:
  - cors
  - cors-misconfigurations
  - sop
---


The same-origin policy is a web browser security mechanism that aims to prevent websites from attacking each other.


### ✅ What is Allowed?

Some **resources can be loaded from other websites**, even if JavaScript can’t read them:

- `<img src="other.com/image.jpg">` – ✅ allowed
- `<script src="other.com/script.js">` – ✅ allowed    
- `<video src="other.com/video.mp4">` – ✅ allowed

BUT: JavaScript **cannot look inside** the image, script, or video loaded from another site.


### ⚠️ Exceptions to the Rule

Some things are **partially allowed** cross-domain:

| Object/Action                                       | Readable? | Writable? | Notes                                             |
| --------------------------------------------------- | --------- | --------- | ------------------------------------------------- |
| `location.href` (URL of iframe or window)           | ❌         | ✅         | You can set the URL but not read it               |
| `window.length` (number of frames)                  | ✅         | ❌         | Can read but not change                           |
| `window.closed` (is the window closed?)             | ✅         | ❌         | Can check but not set                             |
| `window.focus()`, `window.blur()`, `window.close()` | ✅         | ✅         | Can be used on other windows                      |
| `postMessage()`                                     | ✅         | ✅         | A safe way to send data between different domains |


### 🍪 Cookies Exception

- Cookies are shared **between subdomains** (e.g., `shop.example.com` and `blog.example.com`) by default.
- This is **less strict**, but **you can reduce risk** by using the `HttpOnly` flag, which hides cookies from JavaScript.



### 🛠️ Relaxing SOP with `document.domain`

If two subdomains want to share data (like `marketing.example.com` and `example.com`), they can:

1. **Both set** `document.domain = "example.com"` in JavaScript.
2. Then, **JavaScript access is allowed** between them.

⚠️ You **cannot** set `document.domain = "com"` – modern browsers block this for safety.