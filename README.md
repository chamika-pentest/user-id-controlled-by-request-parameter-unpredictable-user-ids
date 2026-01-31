# user-id-controlled-by-request-parameter-unpredictable-user-ids
PortSwigger Web Security Academy lab write-up: User ID controlled by request parameter, with unpredictable user IDs – demonstrating horizontal privilege escalation due to broken access control.

# User ID Controlled by Request Parameter (Unpredictable User IDs)

**Platform:** PortSwigger Web Security Academy  
**Lab Level:** Apprentice  
**Lab Name:** User ID controlled by request parameter, with unpredictable user IDs  
**Category:** Access Control / Horizontal Privilege Escalation  
**Author:** Chamika Jayasooriya  
**Field:** Cybersecurity / Penetration Testing  

---

## 📌 Introduction

This repository contains a professional security lab write-up for the **“User ID controlled by request parameter, with unpredictable user IDs”** lab from the PortSwigger Web Security Academy.

The lab demonstrates a **horizontal privilege escalation** vulnerability caused by improper access control enforcement. Although the application uses **GUIDs (Globally Unique Identifiers)** instead of sequential user IDs, it fails to perform proper **server-side authorization checks**, allowing unauthorized access to other users’ sensitive data.

---

## 🎯 Lab Objective

The objectives of this lab are:

- Log in as a normal user
- Identify another user’s GUID (Carlos)
- Manipulate the request parameter to access another user’s account
- Retrieve and submit Carlos’s API key

---

## 🔍 Vulnerability Overview

### Vulnerability Type
- Broken Access Control  
- Horizontal Privilege Escalation  

### Description
The application identifies users using GUIDs in the account page URL. While GUIDs are difficult to guess, they do not provide security by themselves. If an attacker obtains another user’s GUID through publicly accessible content, they can manipulate request parameters to access unauthorized resources.

---

## 🛠 Tools & Environment

- Web Browser (Chrome / Firefox)
- PortSwigger Web Security Academy Lab Environment
- Optional: Burp Suite (for request inspection)

---

## 👤 Test Accounts Used

| Username | Password | Role |
|--------|----------|------|
| wiener | peter | Normal User |
| carlos | Unknown | Normal User |

---

## 🚀 Step-by-Step Exploitation

### Step 1: Identify a Blog Post by Carlos
Browse the application and locate a blog post authored by **Carlos**.

📸 *Screenshot: Blog post authored by Carlos*

---

### Step 2: Extract Carlos’s User ID (GUID)
Click on Carlos’s username and observe the URL containing a **GUID** identifying his account. Save this GUID for later use.

---

### Step 3: Log in as Normal User
Log in using the supplied credentials:

- **Username:** wiener  
- **Password:** peter  

Navigate to the **My Account** page.

---

### Step 4: Modify the Request Parameter
Replace Wiener’s `id` parameter with Carlos’s GUID in the account page URL.

**Example:**

---

### Step 5: Access Unauthorized Data
The application displays **Carlos’s account details**, including his API key, without performing proper authorization checks.

---

### Step 6: Submit the API Key
Copy Carlos’s API key and submit it to complete the lab.

---

## ⚠️ Impact Analysis

- Exposure of sensitive user data (API keys)
- Unauthorized access to other user accounts
- Potential API abuse or account takeover

---

## 🧠 Root Cause

The application relies solely on the `id` request parameter to identify user accounts without verifying whether the authenticated user is authorized to access the requested resource.

---

## 🛡 Mitigation & Recommendations

- Enforce strict **server-side authorization checks**
- Ensure users can only access resources linked to their own session
- Avoid relying on **obscurity (GUIDs)** as a security control
- Implement access control based on authenticated user identity

---

## ✅ Conclusion

This lab demonstrates that **unpredictable identifiers do not prevent access control vulnerabilities**. Proper authorization must always be enforced on the server side to prevent horizontal privilege escalation attacks.

---

## 📚 References

- PortSwigger Web Security Academy – Access Control Labs  
- OWASP Top 10 – Broken Access Control  

---

## 👨‍💻 Author

**Chamika Jayasooriya**  
Cybersecurity / Penetration Testing  

---

## 📂 Repository Usage

This repository is suitable for:
- GitHub cybersecurity portfolios
- Academic submissions
- Internship and entry-level security role showcases

