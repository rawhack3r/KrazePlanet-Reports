## Title

Reflected XSS to account Takeover

## Description

**Affected URL:** https://news.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Parameter:** https://news.pwnedbox.site/?title=

**Severity:** Critical

**Description:**

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.

## Steps to Reproduce

1. Visit the affected URL :- https://news.pwnedbox.site/?title=%22%3E1--%3E%3C/Title/%3C/Style/%3C/Textarea/%3C/Iframe/%3E%3CImg/Src/OnError=(confirm)(1)//
2. Navigate to the vulnerable functionality.
3. Insert the following XSS payload into the vulnerable parameter:

   ```html
   ">1--></Title/</Style/</Textarea/</Iframe/><Img/Src/OnError=(confirm)(1)//
   ```

4. Submit the input.
5. Observe that JavaScript executes in the browser.

## Proof of Concept (POC)

### Screenshot


<img width="1917" height="507" alt="Screenshot 2026-11-17 053400" src="https://github.com/user-attachments/assets/e7d901c2-ac3d-4301-adde-f6c9c622d66d" />
<img width="1917" height="842" alt="Screenshot 2026-11-17 053348" src="https://github.com/user-attachments/assets/d114a9d6-aa34-40e6-9ebb-46e8c7d92ab1" />


### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1O1YSB7RQ8xWs8Nv1braF2mVk1QHMUBRr/view?usp=sharing]


## Impact

Depending on the application's functionality, this vulnerability could lead to:

- **Account Takeover:** Stealing session cookies through `document.cookie` , potentially allowing attackers to hijack user accounts, and can lead to Account Takeover.
- **Sensitive Data Theft:** Accessing personal information, API responses, and other sensitive data available to the victim's browser by using payloads.
- **Credential Theft:** Injecting fake login forms to capture users' login credentials.

### References

These are useful technical references for understanding and documenting XSS impact:

1. [PortSwigger – Cross-Site Scripting and Impact](https://portswigger.net/web-security/cross-site-scripting)
2. [PortSwigger – Exploiting XSS Vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/exploiting)
3. [OWASP – Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
4. [OWASP – XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
5. [Microsoft – Weaponizing Cross-Site Scripting](https://www.microsoft.com/en-us/msrc/blog/2025/11/weaponizing-cross-site-scripting-when-one-bug-isnt-enough)


## Remediation

- For HTML text and quoted attribute contexts, use appropriate encoding to prevent special characters from being interpreted as HTML syntax.
- Properly encode user-controlled output based on its HTML context.
- Sanitize untrusted input where appropriate.
- Avoid unsafe DOM manipulation methods such as `innerHTML`.
- Implement a restrictive Content Security Policy (CSP) as an additional security layer.

## References

- https://owasp.org/www-community/attacks/xss/
- https://portswigger.net/web-security/cross-site-scripting
