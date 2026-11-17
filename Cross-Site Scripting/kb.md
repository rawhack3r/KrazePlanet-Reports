## Title

Reflected XSS to Account Takeover

**Affected URL:** https://kb.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Severity:** Critical

## Description
A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.


## Steps to Reproduce

1. Visit the Affected URL :- https://kb.pwnedbox.site/?search=1%3C!--%3E%3CSvg/OnLoad=(confirm)(1)--%3E

2. Observe that JavaScript executes in the browser.

**Affected Parameter:** https://kb.pwnedbox.site/?search=

XSS payload used in the vulnerable parameter:

   ```html
       1<!--><Svg/OnLoad=(confirm)(1)-->
   ```


## Proof of Concept (POC)

### Screenshot

<img width="1906" height="633" alt="Screenshot 2026-11-17 074147" src="https://github.com/user-attachments/assets/124bcc03-72ac-4125-ba8a-8d7b0c52d202" />
<img width="1917" height="407" alt="Screenshot 2026-11-17 074135" src="https://github.com/user-attachments/assets/36dbf887-b12a-464b-b380-9aeb6a8fc83d" />



### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1K1LCBqJe9sh34REnD9bd5TktC6HUw2e9/view?usp=sharing]


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
