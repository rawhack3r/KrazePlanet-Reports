## Title

Reflected XSS to Account Takeover

**Affected URL:** https://portal.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Severity:** Critical

## Description
A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.


## Steps to Reproduce

1. Visit the Affected URL :- https://portal.pwnedbox.site/?cat=%27%22%3EKaran%3C%3E%22%271%27)%22--%3E%3CK%2FAutofocus%2FContentEditable%2FOnFocusIn%3D%26%2397%26%23108%26%23101%26%23114%26%23116%26%2396%26%2375%26%2396%3C!--

2. Observe that JavaScript executes in the browser.

**Affected Parameter:** https://portal.pwnedbox.site/?cat=

XSS payload used in the vulnerable parameter:

   ```html
       1')"--><K%2FAutofocus%2FContentEditable%2FOnFocusIn%3D%26%2397%26%23108%26%23101%26%23114%26%23116%26%2396%26%2375%26%2396<!--
   ```


## Proof of Concept (POC)

### Screenshot

<img width="1917" height="480" alt="Screenshot 2026-11-17 072916" src="https://github.com/user-attachments/assets/2424a364-6ac5-4503-9a12-7eaa37e03574" />
<img width="1917" height="367" alt="Screenshot 2026-11-17 072841" src="https://github.com/user-attachments/assets/36f493aa-b2de-43f4-9c5d-7988ce5a3058" />



### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1WfbaRPUokpTtNMT2fj7Pg7dfcq67MNmK/view?usp=sharing]


## Impact

- **Account Takeover:** Stealing session cookies through `document.cookie` , potentially allowing attackers to hijack user accounts, and can lead to Account Takeover.
- **Sensitive Data Theft:** Accessing personal information, API responses, and other sensitive data available to the victim's browser by using payloads.
- **Credential Theft:** Injecting fake login forms to capture users' login credentials.



## Remediation

- Context-Aware Output Encoding: Properly encode user-controlled input before rendering it in HTML, attributes, JavaScript, or other contexts.
- HTML Sanitization: Use a maintained HTML sanitization library, such as DOMPurify, when user-submitted HTML is required.
- Session Cookie Protection: Configure session cookies with HttpOnly, Secure, and appropriate SameSite attributes to reduce session-related risks.
- Web Application Firewall (WAF): If available, deploy or configure a WAF with appropriate XSS detection and filtering rules to help detect and block common malicious payloads.


### References

These are useful technical references for understanding and documenting XSS impact:

1. [PortSwigger – Cross-Site Scripting and Impact](https://portswigger.net/web-security/cross-site-scripting)
2. [PortSwigger – Exploiting XSS Vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/exploiting)
3. [OWASP – Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
4. [OWASP – XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
5. [Microsoft – Weaponizing Cross-Site Scripting](https://www.microsoft.com/en-us/msrc/blog/2025/11/weaponizing-cross-site-scripting-when-one-bug-isnt-enough)
