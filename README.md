
# 🔐 Insecure Direct Object Reference (IDOR) in Invoice Download – Smart Dukaan

> 🚨 Critical vulnerability allowing unauthorized access to private user invoices via insecure ID-based access.

## 📌 Summary

During a security assessment of **[store.smartdukaan.com](https://store.smartdukaan.com)**, a critical **Insecure Direct Object Reference (IDOR)** vulnerability was identified in the invoice download functionality. By manipulating the `id` parameter in the download URL, an attacker could access invoices belonging to other users without proper authorization.

---

## 🎯 Vulnerability Details

- **Type:** Insecure Direct Object Reference (IDOR)
- **Risk Level:** 🔴 Critical
- **Affected Endpoint:** `GET /user/invoice/download?id=12345`
- **Authentication Required:** ✅ Yes (but no authorization enforced)

### 🔥 Impact
- Unauthorized access to other users' **invoices**
- Exposure of **personal data**, **order details**, and **billing information**
- Potential for **mass scraping** of user data
- **Violation of data privacy laws** and regulatory compliance

---

## 🧪 Steps to Reproduce

1. **Login to your account** at [Smart Dukaan](https://store.smartdukaan.com).
2. Navigate to **My Orders / Invoices**.
3. Use **Burp Suite** to intercept the invoice download request:
    ```
    GET /user/invoice/download?id=12345 HTTP/1.1
    Host: store.smartdukaan.com
    Authorization: Bearer <your-token>
    ```
4. Modify the `id` parameter to another invoice number (e.g., `id=12346`).
5. Forward the request and observe the server response.
6. ✅ Invoice from another user is downloaded successfully — **no ownership checks performed**.

---

## 📷 Proof of Concept (PoC)

| Screenshot | Description |
|-----------|-------------|
| ![PoC 1](https://shorturl.at/ESi5v) | Accessing invoices by manipulating ID |
| ![PoC 2](https://shorturl.at/NnzcG) | Multiple invoices retrieved without authorization |

🎥 **Video PoC:** [Watch the Exploitation](https://shorturl.at/NnzcG)

---

## 🛡️ Recommended Fixes

1. **Server-Side Authorization**
   - Ensure that the invoice ID belongs to the authenticated user.
2. **Avoid Direct IDs**
   - Use UUIDs or secure mappings to avoid exposing internal references.
3. **Logging & Monitoring**
   - Track invoice download activity and flag unusual patterns.
4. **Rate Limiting**
   - Prevent brute-force or sequential ID access.
5. **Regular Security Testing**
   - Include IDOR scenarios in automated and manual security assessments.

---

## 📚 References

- [OWASP Top 10 – A01:2021 – Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
- [OWASP Testing Guide – IDOR](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/03-Testing_for_Insecure_Direct_Object_References)
- [ISO/IEC 27001 – Access Control](https://www.iso.org/standard/54534.html)

---

## ✍️ Author

👤 **Prince Patel**  
💼 Security Researcher | Red Team | Exploit Dev  
📧 your.email@domain.com  
🐦 Twitter: [@YourHandle](https://twitter.com/yourhandle)  
🔗 LinkedIn: [linkedin.com/in/yourname](https://linkedin.com/in/yourname)

---

## 📢 Disclaimer

> This report is shared for educational and responsible disclosure purposes only. The author is not responsible for any misuse of this information.
