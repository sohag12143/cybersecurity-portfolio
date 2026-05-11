# 🍪 Sensitive Email Disclosure via Client-side Cookies

## 🧾 Executive Summary

Sensitive user email information was stored in plaintext within client-side cookies, exposing privacy risks.

---

## 🔍 Step 1: Recon

Logged into application

Opened DevTools:

* Application → Cookies

---

## 🚨 Step 2: Discovery

Found:

```bash
user_email=testuser@gmail.com
```

---

## 🧪 Step 3: Cookie Analysis

Attributes:

* HttpOnly ❌
* Secure ❌
* SameSite: None ❌

---

## 🔬 Step 4: Network Analysis

Captured traffic using Wireshark

Observed cookie transmitted in plaintext over HTTP.

---

## 🧠 Step 5: Exploitation Scenario

1. Attacker on public WiFi
2. Sniffs traffic
3. Extracts cookie:

```bash
tcpdump -i wlan0 port 80
```

4. Gets email data

---

## ⚠️ Impact

* Privacy leak
* User profiling
* Targeted phishing

---

## 🛠 Tools Used

* Browser DevTools
* Wireshark
* tcpdump

---

## 🛡️ Mitigation

* Avoid storing sensitive data in cookies
* Use HttpOnly & Secure flags
* Encrypt sensitive values
* Enforce HTTPS

---

## 📨 Responsible Disclosure

* Reported issue with proof
* Suggested best practices

---

## ✅ Final Result

* Severity: Medium
* Privacy impact confirmed

---

## 📌 Key Learning

Client-side storage must never contain sensitive user data.
