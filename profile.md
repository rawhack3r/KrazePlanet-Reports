## Title

Reflected XSS Form Function


## Description

**Affected URL:** https://profile.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Parameter:** https://profile.pwnedbox.site/?lname=

**Severity:** [High]

**Description:**

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.

## Steps to Reproduce

1. Visit the affected URL :- https://tutorialrepublic.pwnedbox.site/ .
2. Navigate to the vulnerable functionality.
3. Insert the following XSS payload into the vulnerable parameter:

   ```html
   "><img src=x onerror="&#97;&#108;&#101;&#114;&#116;&#40;&#49;&#41;">
   ```

4. Submit the input.
5. Observe that JavaScript executes in the browser.

## Proof of Concept (POC)

### Screenshot


<img width="1917" height="467" alt="Screenshot 2026-11-16 092950" src="https://github.com/user-attachments/assets/3f4d6921-2ec1-4629-95d3-b3323558b228" />
<img width="1915" height="852" alt="Screenshot 2026-11-16 092945" src="https://github.com/user-attachments/assets/e90201dd-ac09-4494-a631-f80932ae21a1" />


### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1IBN8RYy7sk-vfs6ZqqCVDFbvgqb8MH28/view?usp=sharing]

### HTTP Request / Response


```http
https://profile.pwnedbox.site/?lname=%22%3E%3Cimg+src%3Dx+onerror%3D%22%26%2397%3B%26%23108%3B%26%23101%3B%26%23114%3B%26%23116%3B%26%2340%3B%26%2349%3B%26%2341%3B%22%3E
```

### Payload

```html
   "><img src=x onerror="&#97;&#108;&#101;&#114;&#116;&#40;&#49;&#41;">
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
