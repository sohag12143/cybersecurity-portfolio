# 🔐 Sensitive Data Exposure via Public .env File (Full Recon to Report)

## 🧾 Executive Summary

During reconnaissance, I identified an exposed `.env` file in a publicly accessible repository. The file contained sensitive credentials including API keys and database secrets. These credentials were actively valid and allowed unauthorized API interaction.

---

## 🎯 Scope & Methodology

* Passive reconnaissance (OSINT)
* GitHub code exposure analysis
* API validation testing
* Safe verification (no destructive action)

---

## 🔍 Step 1: Reconnaissance (OSINT)

Started with advanced search dorking on GitHub:

```bash
site:github.com "DB_PASSWORD" OR "API_KEY" OR "SECRET_KEY" OR ".env"
```

Refined search:

```bash
site:github.com "API_KEY" "targetname"
```

Then manually reviewed repositories.

---

## 🔍 Step 2: Repository Enumeration

Cloned repository:

```bash
git clone https://github.com/target/repo.git
cd repo
```

Searched for sensitive files:

```bash
find . -name ".env"
```

---

## 🚨 Step 3: Vulnerability Discovery

Located `.env` file:

```env
API_KEY=sk_test_xxxxxx
DB_PASSWORD=pass_xxxxxx
JWT_SECRET=secret_xxxxxx
```

This file should NEVER be public.

---

## 🧪 Step 4: Validation

Tested API key safely:

```bash
curl -H "Authorization: Bearer sk_test_xxxxxx" https://api.target.com/profile
```

Response:

```json
{
  "user": "test",
  "status": "active"
}
```

→ Confirmed valid access.

---

## ⚠️ Step 5: Impact Analysis

An attacker could:

* Access private APIs
* Extract user data
* Modify backend resources
* Abuse billing systems

---

## 🧠 Step 6: Real-world Attack Scenario

1. Attacker finds `.env`
2. Extracts API key
3. Uses automated script:

```bash
for i in {1..1000}; do
 curl -H "Authorization: Bearer API_KEY" https://api.target.com/data
done
```

→ Mass data exfiltration

---

## 🛠 Tools Used

* GitHub (OSINT)
* Terminal (Kali Linux)
* Curl
* Grep / Find

---

## 🛡️ Mitigation

* Remove `.env` immediately
* Rotate all secrets
* Add `.env` to `.gitignore`
* Use secret managers (Vault, AWS Secrets)
* Monitor logs for abuse

---

## 📨 Responsible Disclosure

* Reported via bug bounty platform
* Provided PoC (sanitized)
* Suggested mitigation steps

---

## ✅ Final Result

* Vulnerability acknowledged
* Severity: High
* Demonstrates risk of improper secret handling

---

## 📌 Key Learning

Never store secrets in public repositories — always use environment isolation.

