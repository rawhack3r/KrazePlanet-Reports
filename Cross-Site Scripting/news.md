## Title

Reflected XSS to Account Takeover

**Affected URL:** https://news.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Severity:** Critical

## Description
A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.


## Steps to Reproduce

1. Visit the Affected URL :- https://news.pwnedbox.site/?title=%22%3E1--%3E%3C/Title/%3C/Style/%3C/Textarea/%3C/Iframe/%3E%3CImg/Src/OnError=(confirm)(1)//

2. Visit the affected.

3. Observe that JavaScript executes in the browser.

**Affected Parameter:** https://news.pwnedbox.site/?title=

XSS payload used in the vulnerable parameter:

   ```html
   ">1--></Title/</Style/</Textarea/</Iframe/><Img/Src/OnError=(confirm)(1)//
   ```


## Proof of Concept (POC)

### Screenshot


<img width="1917" height="507" alt="Screenshot 2026-11-17 053400" src="https://github.com/user-attachments/assets/87ae909a-d5b0-466e-aac2-69bb84b29570" />
<img width="1917" height="842" alt="Screenshot 2026-11-17 053348" src="https://github.com/user-attachments/assets/5676dbe5-0a62-4289-9066-e426bef88bcf" />




### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1O1YSB7RQ8xWs8Nv1braF2mVk1QHMUBRr/view?usp=sharing]


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
