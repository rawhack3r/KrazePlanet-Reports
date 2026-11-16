## Title

Reflected XSS on Form Function

## Description

**Affected URL:** https://account.pwnedbox.site

**Vulnerability Type:** Reflected Cross-Site Scripting (XSS)

**Parameter:** https://account.pwnedbox.site/?lname=

**Severity:** [High]

**Description:**

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the application. User-supplied input is reflected in the HTTP response without proper sanitization or output encoding, allowing JavaScript execution in the victim's browser.

## Steps to Reproduce

1. Visit the affected URL :- https://account.pwnedbox.site
2. Navigate to the vulnerable functionality.
3. Insert the following XSS payload into the vulnerable parameter:

   ```html
   "><svg onload="&#99;&#111;&#110;&#102;&#105;&#114;&#109;&#40;&#49;&#41;">
   ```

4. Submit the input.
5. Observe that JavaScript executes in the browser.

## Proof of Concept (POC)

### Screenshot


[Insert Screenshot Here]

### Video Demonstration


**Video Link:** [https://drive.google.com/file/d/1uD5Q6fph2x5Ti3ccMC3i1IAjjyLU1vZO/view?usp=sharing]

### HTTP Request / Response


```http
https://account.pwnedbox.site/?lname=%22%3E%3Csvg+onload%3D%22%26%2399%3B%26%23111%3B%26%23110%3B%26%23102%3B%26%23105%3B%26%23114%3B%26%23109%3B%26%2340%3B%26%2349%3B%26%2341%3B%22%3E
```

### Payload

```html
   "><svg onload="&#99;&#111;&#110;&#102;&#105;&#114;&#109;&#40;&#49;&#41;">
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
